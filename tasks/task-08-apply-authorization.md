# Task 08 — Apply Authorization

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🔴 Advanced |
| **Estimated Duration** | 5 Days |
| **Type** | Backend Only |
| **Depends On** | Task 07 — Login with JWT |
| **Deliverable** | Claims-based API authorization |
| **Frontend Follow-Up** | Task 17 — Frontend Authorization |

---

## Goal

Apply permissions to API endpoints. Each user should only access backend resources that are allowed for that user.

---

## Required Technologies

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **Claims-based Authorization** | Use `[Authorize(Policy = "...")]` |
| **Authorization Policies** | Create one policy per claim |
| **Policy Registration** | Register policies in `Program.cs` |
| **403 Response** | Return forbidden when user has no permission |

---

## Deliverables

### Backend — ASP.NET Core
- [ ] Create authorization policies in `Program.cs`
- [ ] Protect `GET /api/products`
- [ ] Protect `POST /api/products`
- [ ] Protect `DELETE /api/products/{id}`
- [ ] Protect `PATCH /api/products/{id}/status`
- [ ] Protect `GET /api/users`
- [ ] Protect `POST /api/users`
- [ ] Protect `GET /api/statistics`
- [ ] Return `403 Forbidden` with a clear message when needed

### Endpoint Permission Map
| Endpoint | Required Permission |
|---|---|
| `GET /api/products` | `products:view` |
| `POST /api/products` | `products:create` |
| `DELETE /api/products/{id}` | `products:delete` |
| `PATCH /api/products/{id}/status` | `products:change-status` |
| `GET /api/users` | `users:view` |
| `POST /api/users` | `users:create` |
| `GET /api/statistics` | `statistics:view` |

---

## Hints

- Register one authorization policy per claim string in `Program.cs`.
- Claims from the JWT are available via `HttpContext.User` in handlers and controllers.
- Keep authorization rules close to the endpoint or handler that requires them.

---

## Validation Requirements

| Case | Rule |
|---|---|
| Token exists but claim is missing | Return `403 Forbidden` |
| Token is missing or expired | Return `401 Unauthorized` |

Security note: UI visibility is not real protection. The backend must enforce all permissions.

---

## Tips

### Backend
1. Claims from JWT are available in `HttpContext.User`.
2. Use custom authorization handlers only when the rules are more complex.
3. Add JWT support in Swagger for testing.
