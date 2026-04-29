# Task 14 — Soft Delete UX

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Beginner to Intermediate |
| **Estimated Duration** | 1 Day |
| **Type** | Frontend Only |
| **Depends On** | Task 13 — Display Products + Pagination UI, Backend Task 03 — Soft Delete & SaveChanges Interceptor |
| **Deliverable** | Product deletion flow in the UI |

---

## Goal

Add the user-facing delete flow for products. Confirm the action, call the soft delete endpoint, and update the UI after a successful delete.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **HttpClient** | Call the delete endpoint |
| **Confirm Dialog** | Ask the user to confirm before deleting |
| **Alert Service** | Show success and error messages |

---

## API Dependencies

- `DELETE /api/products/{id}`

---

## Deliverables

- [ ] Add a delete action to the product list and/or details page
- [ ] Show a confirmation dialog before sending the request
- [ ] Remove the product from the current UI after a successful delete
- [ ] Show a clear error message when the product no longer exists

---

## Validation Requirements

| Case | Rule |
|---|---|
| Before delete | Show a confirm dialog |
| Delete success | Refresh or update the list immediately |
| Already deleted or not found | Show a clear error message |

---

## Tips

### Angular
1. Keep the confirmation flow reusable so it can be used in other delete actions later.
2. Reuse the shared alert pattern instead of showing raw HTTP errors.