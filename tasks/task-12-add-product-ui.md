# Task 12 — Add Product Page

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟢 Beginner |
| **Estimated Duration** | 2 Days |
| **Type** | Frontend Only |
| **Depends On** | Task 11 — HTTP Interceptor & API Error Handling, Backend Task 01 — Add Product API & Persistence |
| **Deliverable** | Add product page connected to the API |

---

## Goal

Build the first product management page in Angular. Create a reusable form for adding a product and connect it to the backend endpoint from Task 01.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Reactive Forms** | Build and validate the form |
| **HttpClient** | Send requests to the API |
| **Tailwind CSS** | Style the page |
| **Alert Service** | Show success and error messages |
| **Angular Router** | Redirect after a successful create |

---

## API Dependencies

- `POST /api/products`

---

## Deliverables

- [ ] Create an `add-product` page or standalone component
- [ ] Create a product form with `name`, `description`, `price`, and `quantity`
- [ ] Create a `ProductService` method for adding a product
- [ ] Show success and error messages using the shared alert flow
- [ ] Disable the submit button while saving
- [ ] Redirect to the product list or clear the form after a successful create

---

## Validation Requirements

| Field | Rules |
|---|---|
| **Name** | Required, min 3, max 200 |
| **Description** | Optional, max 1000 |
| **Price** | Required, more than 0 |
| **Quantity** | Required, 0 or more |

- Show an error message under each field when needed.
- Show a loading state while waiting for the API.

---

## Tips

### Angular
1. Use a `FormGroup` and keep the validation messages close to the controls.
2. Reuse the shared interceptor and alert flow instead of handling headers or global errors inside the component.
3. Keep the request model aligned with the backend contract from Task 01.