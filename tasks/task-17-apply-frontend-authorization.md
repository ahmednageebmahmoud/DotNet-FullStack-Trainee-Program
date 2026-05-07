# Task 17 — Frontend Authorization

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🔴 Advanced |
| **Estimated Duration** | 3 Days |
| **Type** | Frontend Only |
| **Depends On** | Task 16 — Roles & Users UI, Backend Task 08 — Apply Authorization |
| **Deliverable** | Permission-aware routes, menu, and UI actions |

---

## Goal

Apply permissions in the Angular app. Show only the routes, menu items, and actions that match the current user's claims.

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

---

## API Dependencies

- Claims from the login response and JWT created in backend Tasks 07 and 08

---

## Deliverables

- [ ] Create a dynamic `NavMenuComponent`
- [ ] Show product pages only for `products:view`
- [ ] Show add product page only for `products:create`
- [ ] Show users page only for `users:view`
- [ ] Create a route guard that checks the required claim
- [ ] Redirect to `/forbidden` when access is denied
- [ ] Create a simple `forbidden` page
- [ ] Create `*appHasPermission="'products:create'"`
- [ ] Hide DOM elements when the user has no permission

---

## Permission Map

| Button or Link | Required Permission |
|---|---|
| Add Product | `products:create` |
| Delete Product | `products:delete` |
| Change Status | `products:change-status` |
| Add User | `users:create` |
| Statistics | `statistics:view` |

---

## Validation Requirements

| Case | Rule |
|---|---|
| User without `products:delete` | Delete button should not be in the DOM |
| Route without permission | Redirect to `/forbidden` |
| Expired token | Redirect to `/login` |

Security note: hiding a button in Angular is only for UI. Real protection is still enforced by the backend.

---

## Tips

### Angular
1. Use a structural directive, not only `[hidden]`.
2. Keep claims in the auth service after login.
3. Build the menu from a list of items with permissions.