# Task 04 — Change Product Status

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Full Stack |
| **Depends On** | Task 01 + Task 02 + Task 03 |
| **Deliverable** | Product status feature + migration + history table |

---

## Goal

Add a status field to the product. A product can be available, out of stock, or discontinued. Save every status change in a history table with date and user.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Toggle or Dropdown** | Change the product status |
| **Status Badge** | Show the status with color |
| **Reactive Forms** | Use a form if needed |
| **Angular Pipe** | Show a clear status text |

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **EF Core Migration** | Add new fields safely |
| **Enum** | Define the product status values |
| **Audit History Table** | Save status changes |
| **PATCH Endpoint** | Update one field only |

---

## Deliverables

### Frontend — Angular
- [ ] Show the product status in the product list
- [ ] Add a button, toggle, or dropdown to change status
- [ ] Create `productStatusPipe` to show a clear text
- [ ] Show the status in the product details page

### Backend — ASP.NET Core
- [ ] Add `Status` to the `Products` table
- [ ] Create the `ProductStatusHistory` table
- [ ] Run a migration without losing old data
- [ ] Create `PATCH /api/products/{id}/status`
- [ ] Save each change in `ProductStatusHistory`
- [ ] Return the status history in product details
- [ ] Create `ProductStatusHistoriesController`
- [ ] Create `GET /api/product-status-histories` with pagination and filtering

---

## Database Schema

### Update to `Products`
```sql
Products
├── ... existing columns
└── Status  (int, NOT NULL, Default: 0)
```

### New Table `ProductStatusHistory` (inherits from Audit Entity)
```sql
ProductStatusHistory : AuditEntity
├── Id            (int, PK, Identity)
├── ProductId     (int, FK -> Products.Id)
├── OldStatus     (int, NOT NULL)
└── NewStatus     (int, NOT NULL)
```

### Enum `ProductStatus`

Create an enum with the following values:

| Value | Name | Description |
|---|---|---|
| 0 | `Available` | Product is available for purchase |
| 1 | `OutOfStock` | Product is temporarily out of stock |
| 2 | `Discontinued` | Product is permanently discontinued |
| 3 | `PreOrder` | Product is available for pre-order |
| 4 | `BackOrder` | Product is on back order |
| 5 | `Draft` | Product is not yet published |

---

## API Endpoints

### `PATCH /api/products/{id}/status`
Update the status of a product and record the change in history.

### `GET /api/product-status-histories`
Return a paginated list of status history records with optional filters.

| Parameter | Type | Description |
|---|---|---|
| `ProductId` | `int?` | Filter by product ID |
| `OldStatus` | `ProductStatus?` | Filter by old status value |
| `NewStatus` | `ProductStatus?` | Filter by new status value |
| `FromDate` | `datetime?` | Filter changes from this date |
| `ToDate` | `datetime?` | Filter changes up to this date |
| `PageNumber` | `int` | Page number (default: 1) |
| `PageSize` | `int` | Items per page (default: 10) |

**Response:**
```json
{
  "items": [
    {
      "id": 1,
      "productId": 5,
      "productName": "Widget A",
      "oldStatus": 0,
      "newStatus": 1,
      "createdAt": "2026-04-10T14:30:00Z",
      "createdBy": "admin"
    }
  ],
  "pageNumber": 1,
  "pageSize": 10,
  "totalCount": 50,
  "totalPages": 5
}
```

---

## Validation Requirements

### Frontend
| Case | Rule |
|---|---|
| Change status | Show a confirm message |
| Same status | Do not allow the same value |

### Backend
| Case | Rule |
|---|---|
| Status value | Must be a valid enum value |
| Product | Return 404 if not found |
| Same status | Return 400 Bad Request |

---

## Tips

### Angular
1. Use `ngClass` to change badge colors.
2. A custom pipe makes the status easy to read.

### Backend
1. Give the new `Status` column a default value in the migration.
2. Use `PATCH` because only one field changes.
3. Save the status update and the history record in one transaction.
