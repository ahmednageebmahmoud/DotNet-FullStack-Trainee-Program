# Task 15 — Change Product Status UI

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 2 Days |
| **Type** | Frontend Only |
| **Depends On** | Task 13 — Display Products + Pagination UI, Task 14 — Soft Delete UX, Backend Task 04 — Change Product Status + Audit History |
| **Deliverable** | Product status controls and history UI |

---

## Goal

Build the Angular UI for viewing and changing product status. Let the user update the status, show readable labels and badges, and surface status history from the backend.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Toggle or Dropdown** | Change the product status |
| **Status Badge** | Show the status with color |
| **Angular Pipe** | Convert enum values into readable text |
| **HttpClient** | Call status and history endpoints |

---

## API Dependencies

- `PATCH /api/products/{id}/status`
- `GET /api/products/{id}`
- `GET /api/product-status-histories`

---

## Deliverables

- [ ] Show the product status in the product list
- [ ] Show the product status in the product details page
- [ ] Add a button, toggle, or dropdown to change status
- [ ] Create `productStatusPipe` or an equivalent status mapping helper
- [ ] Show a confirmation message before changing the status
- [ ] Prevent sending a request when the selected status is the same as the current status
- [ ] Show recent status history on the details page or in a separate history view

---

## Validation Requirements

| Case | Rule |
|---|---|
| Change status | Show a confirm message |
| Same status | Do not allow the same value |
| Product not found | Show a clear error message |

---

## Tips

### Angular
1. Keep the status color mapping and display text in one place.
2. Reuse the shared error flow for failed status updates.
3. Build the UI so new enum values can be added later without rewriting every template.