---
categories:
  - "[[Learning]]"
subjects:
  - "[[Technology]]"
type: mission
status: complete
description: "Phase 0 mission — stand up dbt+DuckDB, seed Jaffle Shop, ship stg_customers with passing tests."
tags:
  - sql
  - dbt
  - duckdb
  - data-engineering
created: 2026-06-27
---

# Mission: Environment & First Model (Phase 0 → into Phase 1)

Part of [[SQL-dbt-Reskilling-Campaign-Brief]]. Tracked in [[SQL-dbt Campaign Tracker]].
Today's reading: [[SQL-dbt Lesson 01 — Staging Models & the Staging Contract]].

> **Mission goal:** a materialised model and a passing test on day one. The test suite is the win.

---

## Definition of Done (this mission)

- [x] Python venv + `dbt-core` and `dbt-duckdb` installed; `dbt --version` works
- [x] dbt project scaffolded; DuckDB `profiles.yml` configured; `dbt debug` passes
- [x] Jaffle Shop raw seeds loaded (`dbt seed`)
- [x] `stg_customers` written — staging contract honoured (rename/recast only)
- [x] `unique` + `not_null` tests on `customer_id`
- [x] `dbt run` && `dbt test` → **green**
- [x] First commit
- [x] Push to GitHub — remote `cwoodrow-forge/dbt-learning`, `main` in sync

**Phase 0 complete (2026-06-28).** All staging models built and the repo is pushed. Next stop: [[SQL-dbt Phase 1 — Reading & Reshaping Data]].

---

## What got built (2026-06-27)

| Artifact | Where |
|---|---|
| Repo | `~/dev/dbt-learning` (git, 3 commits, pushed to `cwoodrow-forge/dbt-learning`) |
| Engine | DuckDB via `dbt-duckdb` 1.10, `dbt-core` 1.11 (Python 3.12 venv) |
| Seeds | `raw_customers` (100), `raw_orders` (99), `raw_payments` (113) |
| Models | `stg_customers`, `stg_orders`, `stg_payments` (all views) |
| Tests | `unique`/`not_null` on each key + FK `not_null`s — **14 PASS** (`dbt build`, 2026-06-28) |

The staging model in full — note the shape, you'll repeat it everywhere:

```sql
with source as (
    select * from {{ ref('raw_customers') }}
),
renamed as (
    select
        id as customer_id,
        first_name,
        last_name
    from source
)
select * from renamed
```

---

## STTM lens (the mapping this proves)

| STTM element | This mission |
|---|---|
| Origin data product (immutable) | `raw_customers` seed |
| Staging model (1:1, rename/recast) | `stg_customers` |
| Target contract | `unique` + `not_null` on `customer_id` |

---

## Open thread → next session (Phase 1)

- Write `stg_orders` and `stg_payments` (same import → rename → final shape).
- First aggregated model: **orders per customer** — meet `GROUP BY` and the idea of **grain**.
- Refactor any model into the **import CTEs → logical CTEs → final select** idiom.

---

## Blocked / needs Carl

- ~~**GitHub push** blocked~~ — **resolved 2026-06-28.** Remote `origin` → `https://github.com/cwoodrow-forge/dbt-learning.git`, `main` pushed and in sync. DoD fully met.
