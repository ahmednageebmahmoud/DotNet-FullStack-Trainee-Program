# Training Plan — Angular & .NET

## Overview

This is a training plan for interns. They will build apps with Angular and Tailwind CSS on the frontend, and ASP.NET Core with SQL Server on the backend. Most tasks are full stack from start to finish.

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

## Tasks Summary

| # | Task | Level | Days | Depends On |
|---|---|---|---|---|
| 01 | [Add Product](task-01-add-product.md) | 🟢 Beginner | 4 Days | — |
| 02 | [Display Products + Pagination](task-02-display-products.md) | 🟡 Beginner to Intermediate | 3 Days | Task 01 |
| 03 | [Soft Delete, Interceptor & Delete Endpoint](task-03-soft-delete-interceptor.md) | 🟡 Beginner to Intermediate | 1–2 Days | Task 01 + Task 02 |
| 04 | [Change Product Status + Audit History](task-04-change-product-status.md) | 🟡 Intermediate | 3 Days | Task 01 + Task 02 + Task 03 |
| 05 | [Refactor and Apply CQRS](task-05-cqrs-refactor.md) | 🔴 Advanced | 4 Days | Task 01 + Task 02 + Task 03 + Task 04 |
| 06 | [Add Roles, Claims & Users](task-06-roles-and-users.md) | 🟡 Intermediate | 5 Days | Task 05 |
| 07 | [Login with JWT and Cookie](task-07-login-jwt.md) | 🟡 Intermediate | 3 Days | Task 06 |
| 08 | [Apply Authorization](task-08-apply-authorization.md) | 🔴 Advanced | 5 Days | Task 07 |
| 09 | [Statistics Dashboard](task-09-statistics-dashboard.md) | 🟡 Intermediate | 3 Days | Task 08 |

**Total time: about 31–32 work days (about 6–7 weeks)**

---

## Rough Timeline

```text
Week 1-2:  Task 01 + Task 02 + Task 03  -> Basics (CRUD + Soft Delete + Pagination)
Week 3:    Task 04                       -> Enums + Audit History
Week 4:    Task 05                       -> CQRS + MediatR
Week 5:    Task 06                       -> Identity + Roles + Users
Week 6:    Task 07 + Task 08             -> JWT + Authorization
Week 7:    Task 09                       -> Dashboard + Final Polish
```

---

## General Rules

- Every task should be done from start to finish.
- Validation is required in the frontend and backend.
- Submission must include Swagger and a Postman collection.
- Keep the code in clear feature folders.
- Do not use magic strings. Use constants.
- Do not put business logic in controllers.

