# Task 19 - Backend and Frontend Refactor

---

## Task Information

| Field | Details |
|---|---|
| **Level** | Advanced |
| **Estimated Duration** | 3 Days |
| **Type** | Backend + Frontend |
| **Depends On** | Backend Tasks 01-09 + Frontend Tasks 10-18 |
| **Deliverable** | Correct HTTP status codes for existing result responses, exception handling, audit tracking, and frontend invalid-request messages |

---

## Goal

Refactor the application so existing result pattern responses set the correct HTTP status code, exceptions are returned using the result pattern, entity audit fields are filled automatically during persistence, and frontend invalid-request messages appear correctly to the user.

---

## Required Technologies

### Backend - ASP.NET Core

| Technology | Description |
|---|---|
| **Middleware** | Intercept responses and exceptions in the request pipeline |
| **Result Pattern** | Existing controller return shape that already contains success, failure, and status code information |
| **Entity Framework Core** | Fill audit information before saving changes |
| **ASP.NET Core Identity / Claims** | Read the current authenticated username |
| **HTTP Status Codes** | Bind result status codes to the actual HTTP response status code |

### Frontend - Angular

| Technology | Description |
|---|---|
| **HTTP Interceptor** | Handle invalid API responses globally |
| **Alert Service** | Display validation and error messages consistently |
| **Reactive Forms** | Show invalid request messages beside form fields or as page-level alerts |
| **RxJS** | Transform API errors into UI-friendly messages |

---

## Backend Deliverables

- [ ] Add middleware that only reads the status code from the existing result pattern response and applies it to `HttpResponse.StatusCode`
- [ ] Ensure existing successful result responses return the correct success status code, such as `200`, `201`, or `204`
- [ ] Ensure existing failed result responses return the correct failure status code, such as `400`, `401`, `403`, `404`, or `409`
- [ ] Add exception middleware that catches unhandled exceptions
- [ ] Return exceptions using the same result pattern shape used by normal API failures
- [ ] Hide internal exception details from the client in production
- [ ] Register the exception middleware before endpoint execution
- [ ] Register the result-status-code middleware in the correct position in the request pipeline
- [ ] Add audit information support for created, modified, and deleted entities
- [ ] Fill `CreatedBy` from the current identity username when a new entity is created
- [ ] Fill `ModifiedBy` from the current identity username when an entity is updated
- [ ] Fill `DeletedBy` from the current identity username when an entity is soft deleted
- [ ] Fill matching timestamp fields such as `CreatedAt`, `ModifiedAt`, and `DeletedAt`
- [ ] Keep audit logic centralized in the EF Core save pipeline, interceptor, or `DbContext`
- [ ] Do not require controllers or handlers to set audit fields manually

---

## Frontend Deliverables

- [ ] Show invalid request messages successfully in the UI
- [ ] Avoid showing raw technical exception text to users

---

## Validation Requirements

| Case | Expected Result |
|---|---|
| Controller returns `Result.Success` | Middleware updates only the HTTP status code to match the result success code |
| Controller returns `Result.Failure` | Middleware updates only the HTTP status code to match the result failure code |
| Validation failure | API returns result pattern response with `400 Bad Request` |
| Not found failure | API returns result pattern response with `404 Not Found` |
| Unauthorized request | API returns result pattern response with `401 Unauthorized` |
| Forbidden request | API returns result pattern response with `403 Forbidden` |
| Unhandled exception | API returns result pattern response with `500 Internal Server Error` |
| Create entity | `CreatedBy` and `CreatedAt` are filled automatically |
| Update entity | `ModifiedBy` and `ModifiedAt` are filled automatically |
| Soft delete entity | `DeletedBy` and `DeletedAt` are filled automatically |
| Invalid frontend request | User sees the backend error message successfully |

---

## Tips

### Backend

1. The result-status-code middleware should only bind the existing result status code to `HttpResponse.StatusCode`.
2. Use an abstraction such as `ICurrentUserService` to read the current identity username.
3. Prefer one centralized audit implementation instead of repeating audit assignments in handlers.
4. Make sure middleware ordering is documented in `Program.cs`.

### Frontend

1. Keep parsing logic inside a shared HTTP error handler or interceptor.
2. Map backend validation errors to form controls when field names are available.
3. Fall back to a clear general message when field names are not available.
