# Task 01 — Add Product

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟢 Beginner |
| **Estimated Duration** | 4 Days |
| **Type** | Full Stack |
| **Deliverable** | Angular app + .NET API + SQL database |

---

## Goal

Build a simple Add Product page. The frontend should use Angular and Reactive Forms. The backend should use ASP.NET Core and save data in SQL Server.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Angular 17+** | Main frontend framework |
| **Tailwind CSS** | Page styling |
| **Reactive Forms** | Build and validate the form |
| **HttpClient** | Send requests to the API |
| **HTTP Interceptor** | Add common request settings |
| **Alert Service** | Show success and error messages |
| **Environment Files** | Store the API base URL |

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **ASP.NET Core Web API** | Build the API |
| **Entity Framework Core** | Work with the database |
| **SQL Server** | Store product data |
| **Swagger / OpenAPI** | Test and document the API |
| **Data Annotations** | Validate request data |
| **Audit Fields** | Save created date and user |

---

## Deliverables

### Frontend — Angular
- [ ] Create a new Angular project with Tailwind CSS
- [ ] Create a product feature or standalone component
- [ ] Create an `add-product` component with a Reactive Form
- [ ] Create a `ProductService` for API calls
- [ ] Create an `HttpInterceptor` to add `Content-Type: application/json`
- [ ] Create an `AlertService` for messages
- [ ] Connect the form to the API

### Backend — ASP.NET Core
- [ ] Create a new ASP.NET Core Web API project
- [ ] Create a `BaseEntity` base class with the `Id` field
- [ ] Create an `AuditableEntity` base class that extends `BaseEntity` with `CreatedAt` and `CreatedBy`
- [ ] Create the `Product` entity and make it extend `AuditableEntity`
- [ ] Create `ApplicationDbContext` and connect it to SQL Server
- [ ] Run a migration and create the database
- [ ] Create `POST /api/products`
- [ ] Validate the request DTO
- [ ] Enable Swagger and test the endpoint
- [ ] Test the API in Postman

---

## Database Schema

### `Products` Table
```sql
Products
├── Id            (int, PK, Identity)
├── Name          (nvarchar(200), NOT NULL)
├── Description   (nvarchar(1000), NULL)
├── Price         (decimal(18,2), NOT NULL)
├── Quantity      (int, NOT NULL)
├── CreatedAt     (datetime2, NOT NULL)
└── CreatedBy     (nvarchar(100), NOT NULL)
```

---

## Validation Requirements

### Frontend Validation
| Field | Rules |
|---|---|
| **Name** | Required, min 3, max 200 |
| **Description** | Optional, max 1000 |
| **Price** | Required, more than 0 |
| **Quantity** | Required, 0 or more |

- Show an error message under each field when needed
- Disable the submit button while saving
- Show a loading spinner while waiting

### Backend Validation

Use Data Annotations on the request DTO to validate all fields with the same rules defined in the frontend table above.

---

## Tips

### Angular
1. Use `FormGroup`.
2. Create a helper method for error messages.
3. Use one alert service for all messages.
4. Put the API URL in the environment file.

### Backend 

1. Use a base entity for the Id field.
2. Use an audit entity for audit fields.
3. Keep validation in the Contract.
4. Use Swagger to test APIs quickly.
5. Use `[ApiController]` to handle validation automatically.
6. Use AutoMapper for mapping.
7. Use a standard API response structure (must include message).
8. Do not return entities directly; use response DTOs.s