# Task 11 — HTTP Interceptor & API Error Handling

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 2 Days |
| **Type** | Frontend Only |
| **Depends On** | Task 10 — Login Page & Auth State |
| **Deliverable** | Shared HTTP interceptor pipeline |

---

## Goal

Create the shared HTTP infrastructure for the Angular app. Attach the JWT token to protected requests, handle common API errors centrally, and keep request behavior consistent before building feature pages.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **HttpClient** | Call the backend APIs |
| **HTTP Interceptor** | Attach auth headers and handle common responses |
| **Angular Router** | Redirect on auth failures |
| **RxJS** | Catch and transform HTTP errors |
| **Alert Service** | Show reusable success and error messages |
| **Environment Files** | Store the API base URL |

---

## API Dependencies

- All protected endpoints from backend Tasks 01–09

---

## Deliverables

- [ ] Create an auth interceptor that adds `Authorization: Bearer <token>` when a token exists
- [ ] Skip the auth header for `POST /api/auth/login`
- [ ] Redirect to `/login` on `401 Unauthorized`
- [ ] Redirect to `/forbidden` or show a clear message on `403 Forbidden`
- [ ] Show a reusable error message for `500` and network failures
- [ ] Keep the API base URL in Angular environment files
- [ ] Centralize common request headers in one place

---

## Validation Requirements

| Case | Rule |
|---|---|
| Login request | Do not attach a stale auth header |
| Missing or expired token | Clear the session and redirect to `/login` |
| Forbidden response | Show a clear access denied message |
| Server or network failure | Show a generic fallback error |

---

## Tips

### Angular
1. Keep interceptors focused: auth, errors, and optional loading can be separate.
2. Do not duplicate error handling inside every service method.
3. Make sure logout logic is reusable so the interceptor and logout button use the same path.