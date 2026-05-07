# Task 18 — Statistics Dashboard UI

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 2 Days |
| **Type** | Frontend Only |
| **Depends On** | Task 17 — Frontend Authorization, Backend Task 09 — Statistics API |
| **Deliverable** | Statistics dashboard page for authorized users |

---

## Goal

Build the dashboard page that consumes the statistics endpoint. Show the key system numbers in a clear admin view with proper loading and authorization handling.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Stats Cards** | Show numbers in cards |
| **Angular Pipes** | Format numbers and dates |
| **Skeleton Loading** | Show loading state |
| **Chart Library** | Optional charts |
| **HttpClient** | Load dashboard data |

---

## API Dependencies

- `GET /api/statistics`

---

## Deliverables

- [ ] Create a `statistics` page with cards
- [ ] Show total products
- [ ] Show available products
- [ ] Show out of stock products
- [ ] Show discontinued products
- [ ] Show total status changes
- [ ] Show total users
- [ ] Show skeleton loading while data loads
- [ ] Protect the route with `statistics:view`

---

## Validation Requirements

| Case | Rule |
|---|---|
| User without `statistics:view` | Redirect to `/forbidden` |
| API error | Show a clear error message |

---

## Tips

### Angular
1. Create a reusable stats card component.
2. Use skeleton loading while the data loads.
3. Use the Angular `number` pipe to format big numbers.