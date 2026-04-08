# Task 03 — Soft Delete & SaveChanges Interceptor

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Beginner to Intermediate |
| **Estimated Duration** | 1–2 Days |
| **Type** | Full Stack |
| **Depends On** | Task 01 — Add Product, Task 02 — Display Products |
| **Deliverable** | Reusable soft delete infrastructure + audit auto-fill via interceptor + delete endpoint |

---

## Goal

Build the shared infrastructure for soft delete and auditing so all future entities can inherit from it. Use a `SaveChanges` interceptor to automatically fill audit fields (`CreatedAt`, `UpdatedAt`, `IsDeleted`, `DeletedAt`) without repeating that logic in every service or handler.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **HttpClient** | Call the DELETE endpoint |
| **Confirm Dialog** | Ask user to confirm before deleting |

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **EF Core Base Entities** | `AuditableEntity` and `SoftDeleteEntity` base classes |
| **EF Core Global Query Filter** | Automatically exclude soft-deleted rows from all queries |
| **SaveChanges Interceptor** | Auto-fill audit and soft-delete fields on every save |
| **DbContext** | Register the interceptor and global filters |

---

## Deliverables

### Frontend — Angular
- [ ] Add a delete button on the product list and/or detail page
- [ ] Show a confirm dialog before sending the delete request
- [ ] Remove the product from the list after a successful delete

### Backend — ASP.NET Core
- [ ] Create `SoftDeleteEntity` base class that extends `AuditableEntity` (from Task 01) and adds `IsDeleted`, `DeletedAt`
- [ ] Update the `Product` entity to inherit from `SoftDeleteEntity`
- [ ] Create a `SaveChangesInterceptor` that:
  - Sets `CreatedAt` on `Added` entities
  - Sets `UpdatedAt` on `Modified` entities
  - Sets `IsDeleted = true` and `DeletedAt` on `Deleted` entities (converts hard delete to soft delete)
- [ ] Register the interceptor in `DbContext` or via DI
- [ ] Add a global query filter in `DbContext` to automatically exclude rows where `IsDeleted = true`
- [ ] Create `DELETE /api/products/{id}` endpoint that triggers the soft delete via EF Core

---

## Database Schema

### Updates to `Products`
```sql
Products
├── Id            (int, PK, Identity)
├── Name          (nvarchar(200), NOT NULL)
├── Description   (nvarchar(1000), NULL)
├── Price         (decimal(18,2), NOT NULL)
├── Quantity      (int, NOT NULL)
├── IsDeleted     (bit, NOT NULL, Default: 0)
├── DeletedAt     (datetime2, NULL)
├── CreatedAt     (datetime2, NOT NULL)
├── CreatedBy     (nvarchar(100), NOT NULL)
├── UpdatedAt     (datetime2, NULL)
└── UpdatedBy     (nvarchar(100), NULL)
```

---

## Hints

### Interceptor
- Create a class that extends `SaveChangesInterceptor` and override both the sync and async `SavingChanges` methods.
- Inside the interceptor, loop through `context.ChangeTracker.Entries()` to inspect each tracked entity.
- For `Added` entities, set `CreatedAt`. For `Added` or `Modified` entities, set `UpdatedAt`.
- For `Deleted` entities that implement `SoftDeleteEntity`, change the state back to `Modified`, then set `IsDeleted = true` and `DeletedAt`.
- Register the interceptor via DI and pass it to `AddInterceptors()` on your `DbContextOptionsBuilder`.

### Global Query Filter
- In `OnModelCreating`, loop through all entity types and apply a query filter only on types that inherit from `SoftDeleteEntity`.
- The filter should exclude rows where `IsDeleted` is `true`.
- After the filter is set, you never need to add `.Where(x => !x.IsDeleted)` in any query.

---

## Validation Requirements

| Case | Rule |
|---|---|
| `CreatedAt` | Must be set automatically — never by the caller |
| `UpdatedAt` | Must be updated automatically on every modify |
| `IsDeleted` | Must be set by the interceptor, not by service code |
| Global filter | All queries must exclude soft-deleted rows by default |
| Delete | Return 404 if product does not exist |
| Delete | Return 404 if product is already deleted |
| Before delete | Frontend must show a confirm dialog |

---

## Tips

### Frontend
1. Use a modal or dialog for the delete confirmation.
2. After a successful delete, reload the product list or navigate back.

### Backend
1. Use `SaveChangesInterceptor` (not override `SaveChanges`) so the logic works with DI and async.
2. Keep `CreatedBy` / `UpdatedBy` as a separate concern — fill them from `ICurrentUserService` or `IHttpContextAccessor` in the interceptor.
3. The global query filter runs automatically — no need to add `.Where(x => !x.IsDeleted)` everywhere.
4. Add a migration after updating the `Product` entity.
5. Test that a soft-deleted product does not appear in any GET query.
