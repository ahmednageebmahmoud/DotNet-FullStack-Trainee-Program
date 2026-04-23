# Task 09 — Statistics Dashboard

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Full Stack |
| **Depends On** | Task 08 — Apply Authorization |
| **Deliverable** | Statistics dashboard for admin users |

---

## Goal

Build a dashboard page with system statistics. Show product counts, user counts, and status change counts.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Stats Cards** | Show numbers in cards |
| **Angular Pipes** | Format numbers and dates |
| **Chart Library** | Optional charts |
| **Skeleton Loading** | Show loading state |

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **Aggregation Queries** | Use count and group queries |
| **CQRS Query** | Create `GetStatisticsQuery` |
| **DTO Projection** | Return only needed data |
| **[Authorize]** | Protect with `statistics:view` |

---

## Deliverables

### Frontend — Angular
- [ ] Create a `statistics` page with cards
- [ ] Show total products
- [ ] Show available products
- [ ] Show out of stock products
- [ ] Show discontinued products
- [ ] Show total status changes
- [ ] Show total users
- [ ] Show skeleton loading while data loads
- [ ] Protect the route with `statistics:view`

### Backend — ASP.NET Core
- [ ] Create `GET /api/statistics`
- [ ] Protect it with `[Authorize(Policy = "statistics:view")]`
- [ ] Build `GetStatisticsQuery` and handler
- [ ] Return a DTO with all needed numbers

---

## Response Shape

The response should group statistics into three sections:
- **products**: `total`, `available`, `outOfStock`, `discontinued`
- **statusChanges**: `total`
- **users**: `total`, `active`, `inactive`

---

## Validation Requirements

### Frontend
| Case | Rule |
|---|---|
| User without `statistics:view` | Redirect to `/forbidden` |
| API error | Show a clear error message |

### Backend
| Case | Rule |
|---|---|
| No token | Return `401 Unauthorized` |
| No `statistics:view` claim | Return `403 Forbidden` |

---

## Tips

### Angular
1. Create a reusable stats card component.
2. Use skeleton loading while the data loads.
3. Use the Angular `number` pipe to format big numbers.

### Backend
1. Use projection so you do not load full tables.
2. Keep the statistics query fast.
3. Add caching later if needed.
