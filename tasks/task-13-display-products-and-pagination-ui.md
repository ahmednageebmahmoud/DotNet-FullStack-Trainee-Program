# Task 13 — Display Products + Pagination UI

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Beginner to Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Frontend Only |
| **Depends On** | Task 11 — HTTP Interceptor & API Error Handling, Task 12 — Add Product Page, Backend Task 02 — Display Products API + Pagination |
| **Deliverable** | Product list, details view, and pagination UI |

---

## Goal

Show products in Angular using the paginated backend endpoints. Add search, pagination, loading states, and product details.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Angular Router** | Move between list and details pages |
| **HttpClient** | Get data from the API |
| **Pagination Component** | Show page numbers |
| **Search Input** | Filter products by name |
| **Query Params** | Keep page and search state in the URL |
| **Loading Spinner** | Show loading state |
| **Tailwind CSS** | Style the table or cards |

---

## API Dependencies

- `GET /api/products?pageNumber=1&pageSize=10&name=`
- `GET /api/products/{id}`

---

## Deliverables

- [ ] Create a `product-list` page
- [ ] Create a reusable pagination component
- [ ] Add a search input to filter products by name
- [ ] Reset to page 1 when the search term changes
- [ ] Keep the search term in the URL query params
- [ ] Keep the page number in the URL query params
- [ ] Show a loading spinner while data loads
- [ ] Show an empty message when there are no products
- [ ] Create a product details page or details drawer

---

## Validation Requirements

| Case | Rule |
|---|---|
| Page number in URL | If it is not a number or less than 1, go to page 1 |
| Search term in URL | Keep it in query params so refresh preserves the filter |
| Product not found | Show a clear message |
| Empty result | Show a clear empty state |

---

## Tips

### Angular
1. Use query params so refresh keeps the same page and search term.
2. Debounce the search input so the API is not called on every keystroke.
3. Make the pagination component reusable.
4. Use `trackBy` in lists for better rendering performance.