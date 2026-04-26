# Task 07 — Login with JWT

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Backend Only |
| **Depends On** | Task 06 — Add Roles, Claims & Users API |
| **Deliverable** | JWT issuing endpoint for authenticated users |
| **Frontend Follow-Up** | Task 10 — Login Page & Auth State, Task 11 — HTTP Interceptor & API Error Handling |

---

## Goal

Build backend login for the system. The API should validate credentials, create a JWT token, and return it in the response body for the frontend to use later.

---

## Required Technologies

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **JWT** | Authentication token |
| **JwtBearer Middleware** | Validate the token |
| **Claims in Token** | Save role and permissions |
| **Refresh Token** | Optional |

---

## Deliverables

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

| Case | Rule |
|---|---|
| Wrong email | Return `401 Unauthorized` with a general message |
| Wrong password | Return `401 Unauthorized` with the same general message |
| Inactive account | Return `403 Forbidden` |

Security note: do not return different messages for wrong email and wrong password.

---

## Tips

### Backend
1. Use a strong secret key.
2. Return the token only over HTTPS in production.
3. Configure CORS correctly if frontend and backend use different ports.
4. Put claims in the token so authorization can use them later.
