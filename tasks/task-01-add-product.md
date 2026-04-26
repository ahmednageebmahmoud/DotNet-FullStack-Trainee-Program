# Task 01 — Add Product API & Persistence

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟢 Beginner |
| **Estimated Duration** | 4 Days |
| **Type** | Backend Only |
| **Deliverable** | .NET API + SQL database |
| **Frontend Follow-Up** | Task 12 — Add Product Page |

---

## Goal

Build the backend foundation for products. Create the product entity, save it in SQL Server, and expose an API endpoint for creating a product.

---

## Required Technologies

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

Apply these rules on the create product request DTO:

| Field | Rules |
|---|---|
| **Name** | Required, min 3, max 200 |
| **Description** | Optional, max 1000 |
| **Price** | Required, more than 0 |
| **Quantity** | Required, 0 or more |

---

## Tips

### Backend
1. Use a base entity for the `Id` field.
2. Use an audit entity for audit fields.
3. Keep validation in the contract layer.
4. Use Swagger to test APIs quickly.
5. Use `[ApiController]` to handle validation automatically.
6. Use AutoMapper for mapping.
7. Use a standard API response structure that includes a message.
8. Do not return entities directly; use response DTOs.