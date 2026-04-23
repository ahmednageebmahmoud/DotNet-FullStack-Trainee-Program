# Task 08 — Apply Authorization

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🔴 Advanced |
| **Estimated Duration** | 5 Days |
| **Type** | Full Stack |
| **Depends On** | Task 07 — Login with JWT and Cookie |
| **Deliverable** | Full authorization in frontend and backend |

---

## Goal

Apply permissions to pages, buttons, routes, and API endpoints. Each user should only see and use what is allowed for that user.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Route Guards** | Protect routes |
| **Custom Directive** | Show or hide elements by permission |
| **Auth Service** | Read user claims |
| **Navigation Menu** | Show menu items by permission |
| **Role-based UI** | Show the right buttons for each user |

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **Claims-based Authorization** | Use `[Authorize(Policy = "...")]` |
| **Authorization Policies** | Create one policy per claim |
| **Policy Registration** | Register policies in `Program.cs` |
| **403 Response** | Return forbidden when user has no permission |

---

## Deliverables

### Frontend — Angular
- [ ] Create a dynamic `NavMenuComponent`
- [ ] Show product pages only for `products:view`
- [ ] Show add product page only for `products:create`
- [ ] Show users page only for `users:view`
- [ ] Create a route guard that checks the required claim
- [ ] Redirect to `/forbidden` when access is denied
- [ ] Create a simple `forbidden` page
- [ ] Create `*appHasPermission="'products:create'"`
- [ ] Hide DOM elements when the user has no permission

### Permission Map
| Button or Link | Required Permission |
|---|---|
| Add Product | `products:create` |
| Delete Product | `products:delete` |
| Change Status | `products:change-status` |
| Add User | `users:create` |
| Statistics | `statistics:view` |

### Backend — ASP.NET Core
- [ ] Create authorization policies in `Program.cs`
- [ ] Protect `GET /api/products`
- [ ] Protect `POST /api/products`
- [ ] Protect `DELETE /api/products/{id}`
- [ ] Protect `PATCH /api/products/{id}/status`
- [ ] Protect `GET /api/users`
- [ ] Protect `POST /api/users`
- [ ] Return `403 Forbidden` with a clear message when needed

---

## Hints

- Create a structural directive (using `*` syntax) that reads the current user's claims from `AuthService` and either renders or removes the element from the DOM entirely.
- Build the navigation menu from a list of items where each item has a required permission — filter the list at render time.
- Register one authorization policy per claim string in `Program.cs`.
- Claims from the JWT are available via `HttpContext.User` in backend handlers and controllers.

---

## Validation Requirements

### Frontend
| Case | Rule |
|---|---|
| User without `products:delete` | Delete button should not be in the DOM |
| Route without permission | Redirect to `/forbidden` |
| Expired token | Redirect to `/login` |

### Backend
| Case | Rule |
|---|---|
| Token exists but claim is missing | Return `403 Forbidden` |
| Token is missing or expired | Return `401 Unauthorized` |

Security note: hiding a button in Angular is only for UI. Real protection must be in the backend.

---

## Tips

### Angular
1. Use a structural directive, not only `[hidden]`.
2. Keep claims in the auth service after login.
3. Build the menu from a list of items with permissions.

### Backend
1. Claims from JWT are available in `HttpContext.User`.
2. Use custom authorization handlers only when the rules are more complex.
3. Add JWT support in Swagger for testing.
