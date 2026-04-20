# Task 06 — Add Roles, Claims & Users

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 5 Days |
| **Type** | Full Stack |
| **Depends On** | Task 05 — Refactor and Apply CQRS |
| **Deliverable** | ASP.NET Core Identity + roles + claims + users page |

---

## Goal

Set up roles and claims with ASP.NET Core Identity. Create roles for the system and connect permissions to each role. Then build a page to add a new user and choose a role for that user, and a page to show the users list.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Reactive Forms** | Build the add user form |
| **Dropdown** | Choose a role |
| **Password Strength Indicator** | Show password strength |
| **Tailwind CSS** | Style the page |

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **ASP.NET Core Identity** | Authentication and authorization system |
| **IdentityDbContext** | Database context for identity |
| **Roles** | User roles in the system |
| **Claims** | Permissions for roles or users |
| **RoleManager<IdentityRole>** | Manage roles |
| **UserManager<ApplicationUser>** | Manage users |
| **Password Hashing** | Built into Identity |
| **Data Seeding** | Add first data automatically |
| **CQRS (MediatR)** | Create a user command |

---

## Deliverables

### Backend — ASP.NET Core (Roles & Claims)
- [ ] Install `Microsoft.AspNetCore.Identity.EntityFrameworkCore`
- [ ] Create `ApplicationUser` from `IdentityUser`
- [ ] Update `ApplicationDbContext` to use `IdentityDbContext<ApplicationUser>`
- [ ] Run a migration for Identity tables
- [ ] Create the three roles as constants
- [ ] Create claims for each role
- [ ] Add a data seeder for roles and claims
- [ ] Create `GET /api/roles`
- [ ] Create `GET /api/roles/{id}/claims`

### Backend — ASP.NET Core (Users)
- [ ] Create `POST /api/users`
- [ ] Create `GET /api/users`
- [ ] Create `GET /api/users/{id}`
- [ ] Check that the role exists before create
- [ ] Check that the email is unique

### Frontend — Angular
- [ ] Create an `add-user` page with a Reactive Form
- [ ] Load roles into a dropdown from the API
- [ ] Show a password strength indicator
- [ ] Add confirm password validation
- [ ] Create a `users-list` page
- [ ] Connect the forms to the API

### Expected Folder Structure

```
YourProject/
├── Controllers/
│   ├── ...
│   ├── RolesController.cs                      ← GET /api/roles, GET /api/roles/{id}/claims
│   └── UsersController.cs                      ← POST /api/users, GET /api/users, GET /api/users/{id}
│
├── Application/
│   ├── ...
│   ├── Roles/                                  ← new feature folder
│   │   └── Queries/
│   │       ├── GetAllRoles/
│   │       │   ├── GetAllRolesQuery.cs
│   │       │   └── GetAllRolesQueryHandler.cs
│   │       └── GetRoleClaims/
│   │           ├── GetRoleClaimsQuery.cs
│   │           └── GetRoleClaimsQueryHandler.cs
│   │
│   └── Users/                                  ← new feature folder
│       ├── Commands/
│       │   └── CreateUser/
│       │       ├── CreateUserCommand.cs         ← record : IRequest<Result<int>>
│       │       ├── CreateUserCommandHandler.cs
│       │       └── CreateUserCommandValidator.cs
│       └── Queries/
│           ├── GetAllUsers/
│           │   ├── GetAllUsersQuery.cs
│           │   └── GetAllUsersQueryHandler.cs
│           └── GetUserById/
│               ├── GetUserByIdQuery.cs
│               └── GetUserByIdQueryHandler.cs
│
├── Entities/
│   ├── ...
│   └── ApplicationUser.cs                      ← extends IdentityUser (FullName, CreatedAt, IsActive)
│
├── Constants/                                  ← new folder
│   ├── AppRoles.cs                             ← static class with role name constants
│   └── AppClaims.cs                            ← static class with claim name constants
│
├── Data/
│   ├── ApplicationDbContext.cs                 ← now extends IdentityDbContext<ApplicationUser>
│   ├── Seeders/
│   │   └── RolesAndClaimsSeeder.cs             ← seeds roles + claims on startup
│   └── ...
│
├── Contracts/
│   ├── ...
│   ├── Roles/
│   │   ├── RoleResponse.cs
│   │   └── RoleClaimResponse.cs
│   └── Users/
│       └── UserResponse.cs
│
├── ...
├── Program.cs                                  ← register Identity, seed roles & claims
└── appsettings.json
```

---

## Roles and Claims

### Roles

- ProjectManager
- Supervisor
- WarehouseManager

### Claims by Role

**ProjectManager:** `products:view`, `products:create`, `products:delete`, `products:change-status`, `users:view`, `users:create`, `statistics:view`

**Supervisor:** `products:view`, `products:create`, `products:change-status`, `statistics:view`

**WarehouseManager:** `products:view`, `products:create`, `products:change-status`

### `ApplicationUser`

Extend `IdentityUser` and add `FullName`, `CreatedAt`, and `IsActive` fields.

> Note: `ApplicationUser` extends `IdentityUser` (not `BaseEntity`), so it uses a `string` (GUID) for its `Id` instead of `int`. This is the default behavior of ASP.NET Core Identity.

---

## Data Models

### Create User — Request Body Fields

`fullName`, `email`, `password`, `confirmPassword`, and `role`.

### Roles — Response Fields

`id` (string) and `name`.

### Role Claims — Response Fields

`type` and `value`.

### Create User — Response Fields

`id` (string), `fullName`, `email`, `role`, `isActive`, and `createdAt`.

---

## Validation Requirements

### Data Seeding
| Case | Rule |
|---|---|
| Data seeder | Do not add the same role twice |
| Data seeder | Do not add the same claim twice |

### How the Seeder Works

1. Create a static class `RolesAndClaimsSeeder` with a method like `SeedAsync(IServiceProvider serviceProvider)`.
2. Inside the method, get `RoleManager<IdentityRole>` from the service provider.
3. Loop through all roles in `AppRoles`. For each role, check if it exists using `RoleExistsAsync()`. If not, create it with `CreateAsync()`.
4. After creating the role, loop through the claims for that role. For each claim, get the existing claims using `GetClaimsAsync()`, and only add the claim if it is not already there using `AddClaimAsync()`.
5. Call the seeder in `Program.cs` after building the app and before `app.Run()`:

```csharp
using (var scope = app.Services.CreateScope())
{
    await RolesAndClaimsSeeder.SeedAsync(scope.ServiceProvider);
}
```

This approach is safe to run many times — it will never create duplicate roles or claims.

### Frontend
| Field | Rules |
|---|---|
| **FullName** | Required, min 3, max 100 |
| **Email** | Required, valid email |
| **Password** | Required, min 8, upper + lower + number + symbol |
| **ConfirmPassword** | Must match password |
| **Role** | Required |

### Backend
| Validator or Case | Rules |
|---|---|
| `CreateUserCommandValidator` | Same rules as frontend |
| Email | Must be unique |
| Role | Must exist |

### Password Rules

At least 8 characters with a mix of uppercase, lowercase, number, and special character.

---

## Tips

### Backend
1. Put role names in a static `AppRoles` class.
2. Put claim names in a static `AppClaims` class.
3. Make the data seeder safe to run many times.
4. Check the connection string before running Identity migrations.
5. Check `IdentityResult` after `CreateAsync()`.
6. Add the role after the user is created.
7. Using email as username is a common choice.

### Angular
1. Put the password match validator on the whole form group.
2. Load roles from the API, not from hard-coded values.
3. Show password strength with simple text or color.
