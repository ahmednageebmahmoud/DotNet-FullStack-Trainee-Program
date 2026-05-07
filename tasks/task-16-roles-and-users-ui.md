# Task 16 — Roles & Users UI

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Frontend Only |
| **Depends On** | Task 10 — Login Page & Auth State, Task 11 — HTTP Interceptor & API Error Handling, Backend Task 06 — Add Roles, Claims & Users API |
| **Deliverable** | Users, roles, permissions lists, and add user screen |

---

## Goal

Build the Angular admin screens for users, roles, and permissions. Let the trainee browse users, roles, and permissions, create a new user, load roles from the backend, and assign the new user to exactly one role.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Reactive Forms** | Build the add user form |
| **Dropdown** | Choose a role |
| **Password Strength Indicator** | Show password strength |
| **HttpClient** | Load users, roles, and permissions from the API |
| **Tailwind CSS** | Style the page |

---

## API Dependencies

- `GET /api/roles`
- `GET /api/roles/{id}/claims`
- `POST /api/users`
- `GET /api/users`
- `GET /api/users/{id}`
- `GET /api/permissions`

---

## Deliverables

- [ ] Create a `users-list` page
- [ ] Create a `roles-list` page
- [ ] Create a `permissions-list` page
- [ ] Create an `add-user` page with a Reactive Form
- [ ] Load roles into a dropdown from the API on the add user page
- [ ] Require the user to be assigned to exactly one role when submitting the add user form
- [ ] Show role claims when a role is selected
- [ ] Show a password strength indicator
- [ ] Add confirm password validation
- [ ] Create a user details page or side panel
- [ ] Connect the forms and lists to the API

---

## Validation Requirements

| Field | Rules |
|---|---|
| **FullName** | Required, min 3, max 100 |
| **Email** | Required, valid email |
| **Password** | Required, min 8, upper + lower + number + symbol |
| **ConfirmPassword** | Must match password |
| **Role** | Required, exactly one role must be selected |

---

## Tips

### Angular
1. Put the password match validator on the whole form group.
2. Load roles from the API instead of hard-coded values.
3. Keep role and claim response models aligned with the backend contracts.
4. The add user request should send one selected role id or role name, based on the backend contract.
