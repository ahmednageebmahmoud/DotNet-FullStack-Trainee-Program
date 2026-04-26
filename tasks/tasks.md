# Training Plan — Angular & .NET

## Overview

This is a training plan for interns. They will first build the backend with ASP.NET Core and SQL Server, then build the frontend with Angular and Tailwind CSS on top of the completed APIs.

---

## Core Technologies

| Layer | Technologies |
|---|---|
| **Frontend** | Angular 17+, Tailwind CSS, Reactive Forms, RxJS |
| **Backend** | ASP.NET Core Web API, Entity Framework Core, MediatR (CQRS) |
| **Auth** | ASP.NET Core Identity, JWT, HttpOnly Cookie |
| **Database** | SQL Server |
| **Tools** | Swagger, Postman |

---

## Execution Order

1. Complete backend tasks from Task 01 to Task 09.
2. Review and approve the backend implementation.
3. Start frontend tasks from Task 10 to Task 18.

## Phase 1 — Backend Tasks

| # | Task | Level | Days | Depends On |
|---|---|---|---|---|
| 01 | [Add Product API & Persistence](task-01-add-product.md) | 🟢 Beginner | 4 Days | — |
| 02 | [Display Products API + Pagination](task-02-display-products.md) | 🟡 Beginner to Intermediate | 3 Days | Task 01 |
| 03 | [Soft Delete Interceptor & Delete Endpoint](task-03-soft-delete-interceptor.md) | 🟡 Beginner to Intermediate | 1–2 Days | Task 01 + Task 02 |
| 04 | [Change Product Status + Audit History](task-04-change-product-status.md) | 🟡 Intermediate | 3 Days | Task 01 + Task 02 + Task 03 |
| 05 | [Refactor and Apply CQRS](task-05-cqrs-refactor.md) | 🔴 Advanced | 4 Days | Task 01 + Task 02 + Task 03 + Task 04 |
| 06 | [Add Roles, Claims & Users API](task-06-roles-and-users.md) | 🟡 Intermediate | 5 Days | Task 05 |
| 07 | [Login with JWT](task-07-login-jwt.md) | 🟡 Intermediate | 3 Days | Task 06 |
| 08 | [Apply Authorization](task-08-apply-authorization.md) | 🔴 Advanced | 5 Days | Task 07 |
| 09 | [Statistics API](task-09-statistics-dashboard.md) | 🟡 Intermediate | 3 Days | Task 08 |

## Phase 2 — Frontend Tasks

| # | Task | Level | Days | Depends On |
|---|---|---|---|---|
| 10 | [Login Page & Auth State](task-10-login-authentication.md) | 🟢 Beginner to Intermediate | 2 Days | Backend Tasks 01–09 |
| 11 | [HTTP Interceptor & API Error Handling](task-11-http-interceptor-and-error-handling.md) | 🟡 Intermediate | 2 Days | Task 10 |
| 12 | [Add Product Page](task-12-add-product-ui.md) | 🟢 Beginner | 2 Days | Task 11 |
| 13 | [Display Products + Pagination UI](task-13-display-products-and-pagination-ui.md) | 🟡 Beginner to Intermediate | 3 Days | Task 11 + Task 12 |
| 14 | [Soft Delete UX](task-14-soft-delete-ui.md) | 🟡 Beginner to Intermediate | 1 Day | Task 13 |
| 15 | [Change Product Status UI](task-15-change-product-status-ui.md) | 🟡 Intermediate | 2 Days | Task 13 + Task 14 |
| 16 | [Roles & Users UI](task-16-roles-and-users-ui.md) | 🟡 Intermediate | 3 Days | Task 10 + Task 11 |
| 17 | [Frontend Authorization](task-17-apply-frontend-authorization.md) | 🔴 Advanced | 3 Days | Task 16 |
| 18 | [Statistics Dashboard UI](task-18-statistics-dashboard-ui.md) | 🟡 Intermediate | 2 Days | Task 17 |

---

## Rough Timeline

```text
Phase 1:   Task 01 -> Task 09            -> Backend foundation first
Phase 2:   Task 10 -> Task 18            -> Frontend implementation second
```

---

## General Rules

- Every backend task should be done from start to finish before the frontend phase starts.
- Validation is required in the current layer of the task.
- Backend submissions must include Swagger and a Postman collection.
- Keep the code in clear feature folders.
- Do not use magic strings. Use constants.
- Do not put business logic in controllers.

