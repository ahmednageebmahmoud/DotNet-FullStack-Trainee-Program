# Task 09 — Statistics API

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟡 Intermediate |
| **Estimated Duration** | 3 Days |
| **Type** | Backend Only |
| **Depends On** | Task 08 — Apply Authorization |
| **Deliverable** | Statistics endpoint for admin users |
| **Frontend Follow-Up** | Task 18 — Statistics Dashboard UI |

---

## Goal

Build an endpoint with system statistics. Return product counts, user counts, and status change counts.

---

## Required Technologies

### Backend — ASP.NET Core
| Technology | Description |
|---|---|
| **Aggregation Queries** | Use count and group queries |
| **CQRS Query** | Create `GetStatisticsQuery` |
| **DTO Projection** | Return only needed data |
| **[Authorize]** | Protect with `statistics:view` |

---

## Deliverables

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

| Case | Rule |
|---|---|
| No token | Return `401 Unauthorized` |
| No `statistics:view` claim | Return `403 Forbidden` |

---

## Tips

### Backend
1. Use projection so you do not load full tables.
2. Keep the statistics query fast.
3. Add caching later if needed.
