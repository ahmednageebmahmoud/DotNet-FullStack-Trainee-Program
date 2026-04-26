# Training Tasks — Angular & .NET

A structured training path for interns learning Angular and ASP.NET Core. The work is now split into two phases: backend first, then frontend.

---

## Tech Stack

| Layer | Technologies |
|---|---|
| **Frontend** | Angular 17+, Tailwind CSS, Reactive Forms, RxJS |
| **Backend** | ASP.NET Core Web API, Entity Framework Core, MediatR (CQRS) |
| **Auth** | ASP.NET Core Identity, JWT, HttpOnly Cookie |
| **Database** | SQL Server |
| **Tools** | Swagger, Postman |

---

## Prerequisites — Suggested Learning Resources

Before starting the tasks, watch the following videos to get familiar with the required technologies:

| Topic | Resource |
|---|---|
| TypeScript | [TypeScript Full Course](https://www.youtube.com/watch?v=mo409tfQSSM) |
| Angular | [Angular Full Course](https://www.youtube.com/watch?v=bW5h7gsufbk) |
| Angular Reactive Forms | [Angular Reactive Forms](https://www.youtube.com/watch?v=U9Xo0wXZIAg&pp=ygUWYW5ndWxhciByZWFjdGl2ZSBmb3Jtcw%3D%3D) |
| Install npm | [How to Install npm](https://www.youtube.com/watch?v=w4Xm46_UmJM&pp=ygUMaW5zdGFsbCBucG0g) |

---

## Workflow

Trainees must complete all backend tasks first, in order from Task 01 to Task 09. After the backend is finished and reviewed, they move to the frontend track from Task 10 to Task 18.

## Phase 1 — Backend Tasks

| # | Task | Level | Days | Status |
|---|---|---|---|---|
| 01 | [Add Product API & Persistence](tasks/task-01-add-product.md) | 🟢 Beginner | 4 Days | ✅ Available |
| 02 | [Display Products API + Pagination](tasks/task-02-display-products.md) | 🟡 Beginner to Intermediate | 3 Days | ✅ Available |
| 03 | [Soft Delete Interceptor & Delete Endpoint](tasks/task-03-soft-delete-interceptor.md) | 🟡 Beginner to Intermediate | 1–2 Days | ✅ Available |
| 04 | [Change Product Status + Audit History](tasks/task-04-change-product-status.md) | 🟡 Intermediate | 3 Days | ✅ Available |
| 05 | [Refactor and Apply CQRS](tasks/task-05-cqrs-refactor.md) | 🔴 Advanced | 4 Days | ✅ Locked |
| 06 | [Add Roles, Claims & Users API](tasks/task-06-roles-and-users.md) | 🟡 Intermediate | 5 Days | ✅ Available |
| 07 | [Login with JWT](tasks/task-07-login-jwt.md) | 🟡 Intermediate | 3 Days | ✅ Available |
| 08 | [Apply Authorization](tasks/task-08-apply-authorization.md) | 🔴 Advanced | 5 Days | ✅ Available |
| 09 | [Statistics API](tasks/task-09-statistics-dashboard.md) | 🟡 Intermediate | 3 Days | ✅ Available |

## Phase 2 — Frontend Tasks

| # | Task | Level | Days | Status |
|---|---|---|---|---|
| 10 | [Login Page & Auth State](tasks/task-10-login-authentication.md) | 🟢 Beginner to Intermediate | 2 Days | ✅ Available |
| 11 | [HTTP Interceptor & API Error Handling](tasks/task-11-http-interceptor-and-error-handling.md) | 🟡 Intermediate | 2 Days | 🔒 Locked |
| 12 | [Add Product Page](tasks/task-12-add-product-ui.md) | 🟢 Beginner | 2 Days | 🔒 Locked |
| 13 | [Display Products + Pagination UI](tasks/task-13-display-products-and-pagination-ui.md) | 🟡 Beginner to Intermediate | 3 Days | 🔒 Locked |
| 14 | [Soft Delete UX](tasks/task-14-soft-delete-ui.md) | 🟡 Beginner to Intermediate | 1 Day | 🔒 Locked |
| 15 | [Change Product Status UI](tasks/task-15-change-product-status-ui.md) | 🟡 Intermediate | 2 Days | 🔒 Locked |
| 16 | [Roles & Users UI](tasks/task-16-roles-and-users-ui.md) | 🟡 Intermediate | 3 Days | 🔒 Locked |
| 17 | [Frontend Authorization](tasks/task-17-apply-frontend-authorization.md) | 🔴 Advanced | 3 Days | 🔒 Locked |
| 18 | [Statistics Dashboard UI](tasks/task-18-statistics-dashboard-ui.md) | 🟡 Intermediate | 2 Days | 🔒 Locked |

> Backend tasks are completed and reviewed first. Frontend tasks start only after Task 09 is finished.

> Tasks 11–18 are currently ignored and locked in this README. Release them only when you want to continue beyond Task 10.

---

## General Rules

- Complete the backend phase in order before starting the frontend phase.
- Complete each task from start to finish before moving on.
- Backend submissions must include Swagger and a Postman collection.
- Frontend submissions must include proper form, route, and state validation.
- Keep the code in clear feature folders.
- Do not use magic strings — use constants.
- Do not put business logic in controllers.

---

## Rough Timeline

| Phase | Tasks |
|---|---|
| Phase 1 | Task 01 → Task 09 — Backend foundation: products, persistence, CQRS, identity, auth, and statistics API |
| Phase 2 | Task 10 → Task 18 — Frontend implementation: login, interceptors, product screens, users, authorization, and dashboard |
