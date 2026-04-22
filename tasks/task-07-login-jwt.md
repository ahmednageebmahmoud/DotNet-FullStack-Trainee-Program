# Task 07 — Login with JWT and Authorization Header

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Full Stack |
| **Depends On** | Task 06 — Add Roles, Claims & Users |
| **Deliverable** | Login page + JWT + header auth |

---

## Goal

Build login for the system. The backend should create a JWT token and return it in the response body. The frontend should attach it via the `Authorization: Bearer` header on subsequent requests and work with the login state and protected routes.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Reactive Forms** | Build the login form |
| **HTTP Interceptor** | Send auth data with requests |
| **Auth Guard** | Protect routes |
| **localStorage / sessionStorage** | Store the token client-side |
| **Auth Service** | Manage login state |
| **BehaviorSubject** | Track current user state |

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **JWT** | Authentication token |
| **JwtBearer Middleware** | Validate the token |
| **Claims in Token** | Save role and permissions |
| **Authorization Header** | Send `Bearer <token>` with each request |
| **Refresh Token** | Optional |

---

## Deliverables

### Frontend — Angular
- [ ] Create a `login` page with email and password
- [ ] Create `AuthService` with `login()`, `logout()`, `isLoggedIn()`, and `getCurrentUser()`
- [ ] Update the interceptor to send auth requests correctly
- [ ] Create an `AuthGuard` for protected pages
- [ ] Redirect to login when token is missing or expired
- [ ] Add a logout button

### Backend — ASP.NET Core
- [ ] Create `POST /api/auth/login`
- [ ] Put user id, email, full name, role, and claims in the token
- [ ] Return the token in the response body (JSON)
- [ ] Add `[Authorize]` to protected endpoints
- [ ] Add JWT settings in `appsettings.json`

---

## Data Models

### Login Request Fields

`email` and `password`.

### Login Response Fields

`id`, `fullName`, `email`, `role`, `claims` (list of claim strings), `token`, and `expiresAt`. The token must be returned in the response body as a plain string.

### JWT Payload

The token must include: `sub` (user id), `email`, `fullName`, `role`, all user claims as individual claims, `exp`, `iss`, and `aud`.

---

## Validation Requirements

### Frontend
| Field | Rules |
|---|---|
| **Email** | Required, valid email |
| **Password** | Required, min 8 |

### Backend
| Case | Rule |
|---|---|
| Wrong email | Return `401 Unauthorized` with a general message |
| Wrong password | Return `401 Unauthorized` with the same general message |
| Inactive account | Return `403 Forbidden` |

Security note: do not return different messages for wrong email and wrong password.

---

## Tips

### Angular
1. Store the token in `localStorage` or `sessionStorage` after login.
2. Use an HTTP interceptor to attach `Authorization: Bearer <token>` to every outgoing request.
3. Redirect to login on `401` responses.
4. Use an auth guard for protected pages.

### Backend
1. Use a strong secret key.
2. Return the token only over HTTPS in production.
3. Configure CORS correctly if frontend and backend use different ports.
4. Put claims in the token so authorization can use them later.
