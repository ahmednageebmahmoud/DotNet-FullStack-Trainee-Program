# Task 05 — Refactor and Apply CQRS

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🔴 Advanced |
| **Estimated Duration** | 4 Days |
| **Type** | Backend Only |
| **Depends On** | Task 01 + Task 02 + Task 03 + Task 04 |
| **Deliverable** | Backend refactor with CQRS and MediatR |

---

## Goal

Refactor the backend to use CQRS. Separate write actions from read actions. Use MediatR so controllers stay small and clean.

---

## Required Technologies

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **MediatR** | Send commands and queries |
| **CQRS Pattern** | Split reads and writes |
| **Command** | Change data |
| **Query** | Read data |
| **Handler** | Run one command or query |
| **FluentValidation** | Validate requests |
| **Result Pattern** | Return success or failure clearly |

---

## Deliverables

### Expected Folder Structure

```
YourProject/                                    ← single ASP.NET Core Web API project
├── Controllers/
│   ├── ProductsController.cs                   ← thin, only calls _mediator.Send()
│   └── ProductStatusHistoriesController.cs
│
├── Application/                                ← CQRS layer (commands, queries, handlers)
│   ├── Common/
│   │   ├── Behaviors/
│   │   │   └── ValidationBehavior.cs           ← runs FluentValidation before every handler
│   │   └── Results/
│   │       └── Result.cs                       ← Result<T> pattern
│   │
│   └── Products/                               ← one folder per feature
│       ├── Commands/                           ← write operations
│       │   ├── CreateProduct/
│       │   │   ├── CreateProductCommand.cs     ← record : IRequest<Result<int>>
│       │   │   ├── CreateProductCommandHandler.cs
│       │   │   └── CreateProductCommandValidator.cs
│       │   ├── DeleteProduct/
│       │   │   ├── DeleteProductCommand.cs
│       │   │   ├── DeleteProductCommandHandler.cs
│       │   │   └── DeleteProductCommandValidator.cs
│       │   └── ChangeProductStatus/
│       │       ├── ChangeProductStatusCommand.cs
│       │       ├── ChangeProductStatusCommandHandler.cs
│       │       └── ChangeProductStatusCommandValidator.cs
│       │
│       └── Queries/                            ← read operations
│           ├── GetAllProducts/
│           │   ├── GetAllProductsQuery.cs      ← record : IRequest<Result<PaginatedResult<ProductResponse>>>
│           │   ├── GetAllProductsQueryHandler.cs
│           │   └── GetAllProductsQueryValidator.cs
│           └── GetProductById/
│               ├── GetProductByIdQuery.cs
│               └── GetProductByIdQueryHandler.cs
│
├── Entities/
│   ├── Common/
│   │   ├── BaseEntity.cs
│   │   ├── AuditableEntity.cs
│   │   └── SoftDeleteEntity.cs
│   ├── Product.cs
│   └── ProductStatusHistory.cs
│
├── Enums/
│   └── ProductStatus.cs
│
├── Data/
│   ├── ApplicationDbContext.cs
│   ├── Interceptors/
│   │   └── AuditInterceptor.cs                ← fills CreatedAt, UpdatedAt, IsDeleted
│   └── Migrations/
│
├── Contracts/                                  ← request and response DTOs
│   └── Products/
│       ├── ProductResponse.cs
│       └── PaginatedResult.cs
│
├── Mappings/
│   └── ProductMappingProfile.cs               ← AutoMapper profile
│
├── Program.cs                                  ← register MediatR, FluentValidation, DbContext
└── appsettings.json
```

### Backend Tasks
- [ ] Install MediatR and FluentValidation
- [ ] Convert create product to a command and handler
- [ ] Convert get all products to a query and handler
- [ ] Convert get product by id to a query and handler
- [ ] Convert delete product to a command and handler
- [ ] Convert change product status to a command and handler
- [ ] Add FluentValidation to commands
- [ ] Add validation pipeline behavior
- [ ] Keep controllers thin

---

## Hints

- Use `record` types for commands and queries — they are clean, immutable, and need no extra boilerplate.
- Controllers should only call `_mediator.Send()` and return the result. No business logic inside.
- Add a MediatR pipeline behavior for validation so FluentValidation runs automatically before every handler without touching each handler individually.

---

## Validation Requirements

| Command or Query | Rules |
|---|---|
| `CreateProductCommand` | Same rules as Task 01 |
| `ChangeProductStatusCommand` | Valid status and product exists |
| `DeleteProductCommand` | ProductId must be more than 0 |
| `GetAllProductsQuery` | PageNumber >= 1, PageSize 1 to 100 |

---

## Tips

1. Use `record` for commands and queries when possible.
2. Keep business logic out of controllers.
3. Organize folders by feature, not only by type.
4. Use one validation pipeline instead of repeating validation in every handler.
5. Register MediatR in `Program.cs`.

---

## Helper: `record` vs `class`

> Use this to decide which one to use when writing commands, queries, and responses.

| Feature | `record` | `class` |
|---|---|---|
| **Equality** | Compares by value automatically | Compares by reference (memory address) |
| **Immutability** | Properties are `init`-only by default | Properties are mutable by default |
| **Boilerplate** | No need to write `Equals`, `GetHashCode`, or `ToString` | You must write them manually |
| **Best for** | Commands, Queries, DTOs, response models | Entities, services, repositories |
| **Copying** | Built-in `with` expression to copy and change one field | No built-in copy support |

### Example

```csharp
// record — clean, immutable, value-based equality
public record CreateProductCommand(string Name, decimal Price, int Quantity)
    : IRequest<Result<int>>;

// class — mutable, reference-based equality
public class ProductService
{
    public void DoSomething() { }
}
```

### When to use `record`
- Commands: `CreateProductCommand`, `DeleteProductCommand`, `ChangeProductStatusCommand`
- Queries: `GetAllProductsQuery`, `GetProductByIdQuery`
- Response DTOs: `ProductResponse`, `PaginatedResult<T>`

### When to use `class`
- Entities: `Product`, `ProductStatusHistory`
- Handlers: `CreateProductCommandHandler`
- Services: `ProductService`
- DbContext: `ApplicationDbContext`

---

## Helper: CQRS vs MediatR

> These two things are often confused. One is a pattern, the other is a library.

### CQRS — the pattern

CQRS stands for **Command Query Responsibility Segregation**. It is an architectural idea, not a library.

The rule is simple:

| Type | Purpose | Changes data? |
|---|---|---|
| **Command** | Do something — create, update, delete | Yes |
| **Query** | Ask for something — read data | No |

You split your operations into two separate paths so reads and writes never mix.

```
Request comes in
     │
     ├── Is it reading data?  → Query  → QueryHandler  → return data
     └── Is it writing data? → Command → CommandHandler → return result
```

**Without CQRS** — one service does everything:
```csharp
public class ProductService
{
    public Task<Product> GetById(int id) { ... }     // read
    public Task Create(CreateProductDto dto) { ... } // write
    public Task Delete(int id) { ... }               // write
    // grows forever, hard to maintain
}
```

**With CQRS** — each operation is isolated:
```csharp
// Read side
public record GetProductByIdQuery(int Id) : IRequest<Result<ProductResponse>>;

// Write side
public record CreateProductCommand(string Name, decimal Price) : IRequest<Result<int>>;
public record DeleteProductCommand(int Id) : IRequest<Result>;
```

---

### MediatR — the library

MediatR is a .NET library that **implements the Mediator pattern**. It connects a request to its handler so your controller does not need to know which class does the work.

```
Controller  →  _mediator.Send(command)  →  MediatR  →  finds the right Handler  →  runs it
```

Without MediatR you would inject every service into the controller:
```csharp
// messy — controller knows too much
public ProductsController(
    IProductService productService,
    IProductStatusService statusService,
    IProductHistoryService historyService) { ... }
```

With MediatR the controller only needs one dependency:
```csharp
// clean controller
public ProductsController(IMediator mediator)
{
    _mediator = mediator;
}

[HttpPost]
public async Task<IActionResult> Create(CreateProductCommand command)
{
    var result = await _mediator.Send(command);
    return Ok(result);
}
```

---

### How CQRS and MediatR work together

CQRS tells you **what to separate**. MediatR gives you **the tool to wire it up**.

```
┌─────────────────────────────────────────────────────┐
│                    Controller                       │
│          _mediator.Send(new CreateProductCommand()) │
└────────────────────┬────────────────────────────────┘
                     │ MediatR routes automatically
          ┌──────────┴──────────┐
          │                     │
   ┌──────▼──────┐       ┌──────▼──────┐
   │  Commands   │       │   Queries   │   ← CQRS separation
   │  (write)    │       │   (read)    │
   └──────┬──────┘       └──────┬──────┘
          │                     │
   ┌──────▼──────┐       ┌──────▼──────┐
   │   Handler   │       │   Handler   │
   │  writes DB  │       │  reads DB  │
   └─────────────┘       └─────────────┘
```

| Question | Answer |
|---|---|
| What is CQRS? | A pattern — split reads and writes |
| What is MediatR? | A library — routes requests to handlers |
| Do I need both? | No — you can use CQRS without MediatR, but MediatR makes it much cleaner |
| What does `IRequest<T>` mean? | The command or query returns a value of type `T` |
| What does `IRequestHandler<TRequest, TResponse>` mean? | The class that handles one specific command or query |
