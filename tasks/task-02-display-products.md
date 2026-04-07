# Task 02 — Display Products

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Beginner to Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Full Stack |
| **Depends On** | Task 01 — Add Product |
| **Deliverable** | Product list + product details |

---

## Goal

Show products in a list. Add pagination. Let the user open product details.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Angular Router** | Move between list and details pages |
| **Tailwind CSS** | Style the table or cards |
| **HttpClient** | Get data from the API |
| **Pagination Component** | Show page numbers |
| **Search Input** | Filter products by name |
| **Loading Spinner** | Show loading state |
| **Query Params** | Save page number in the URL |

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **Pagination** | Return data page by page |
| **PaginatedResult<T>** | Response model for list data |
| **Search / Filter** | Filter results by name on the backend |

---

## Deliverables

### Frontend — Angular
- [ ] Create a `product-list` page
- [ ] Create a reusable pagination component
- [ ] Add a search input to filter products by name
- [ ] Reset to page 1 when the search term changes
- [ ] Keep the search term in the URL query params
- [ ] Show a loading spinner while data loads
- [ ] Show an empty message when there are no products
- [ ] Keep the page number in the URL query params

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

### Frontend
| Case | Rule |
|---|---|
| Page number in URL | If it is not a number or less than 1, go to page 1 |
| Search term in URL | Keep it in query params so refresh preserves the filter |
| Product not found | Show a clear message |

### Backend
| Case | Rule |
|---|---|
| `pageSize` | Min 1, max 100 |
| `pageNumber` | Min 1 |
| `name` filter | Optional; if provided, apply a case-insensitive `Contains` match |

---

## Tips

### Angular
1. Use query params so refresh keeps the same page and search term.
2. Debounce the search input so the API is not called on every keystroke.
2. Make the pagination component reusable.
3. Use `trackBy` in lists for better performance.

### Backend
1. Create a generic `PaginatedResult<T>`.
2. Use `Skip` and `Take` in EF Core.

