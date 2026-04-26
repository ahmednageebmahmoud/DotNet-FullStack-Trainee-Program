# Task 02 — Display Products API + Pagination

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Beginner to Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Backend Only |
| **Depends On** | Task 01 — Add Product API & Persistence |
| **Deliverable** | Products list API + product details API |
| **Frontend Follow-Up** | Task 13 — Display Products + Pagination UI |

---

## Goal

Expose products through read endpoints. Add pagination, product details, and filtering by product name.

---

## Required Technologies

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **Pagination** | Return data page by page |
| **PaginatedResult<T>** | Response model for list data |
| **Search / Filter** | Filter results by name on the backend |

---

## Deliverables

### Backend — ASP.NET Core
- [ ] Create `GET /api/products?pageNumber=1&pageSize=10&name=`
- [ ] Filter products by name using a case-insensitive partial match when `name` is provided
- [ ] Create `GET /api/products/{id}`
- [ ] Return `TotalCount`, `PageNumber`, `PageSize`, and `Data`

---

## Response Model

The paginated response must include: `data` (the list of products for the current page), `totalCount` (total number of products), `pageNumber`, `pageSize`, and `totalPages`.

---

## Validation Requirements

| Case | Rule |
|---|---|
| `pageSize` | Min 1, max 100 |
| `pageNumber` | Min 1 |
| `name` filter | Optional; if provided, apply a case-insensitive `Contains` match |
| Product not found | Return `404 Not Found` |

---

## Tips

### Backend
1. Create a generic `PaginatedResult<T>`.
2. Use `Skip` and `Take` in EF Core.
3. Keep the response contract stable because the frontend tasks will depend on it.

