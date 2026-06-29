---
categories:
  - "[[Learning]]"
subjects:
  - "[[Technology]]"
type: mission
status: active
description: "Phase 1 mission — SQL fundamentals through dbt: joins, aggregation, grain, and the CTE idiom on Jaffle Shop."
tags:
  - sql
  - dbt
  - duckdb
  - data-engineering
created: 2026-06-28
---

# Mission: Reading & Reshaping Data (Phase 1)

Part of [[SQL-dbt-Reskilling-Campaign-Brief]]. Tracked in [[SQL-dbt Campaign Tracker]].
Follows [[SQL-dbt Phase 0 — Environment & First Model]] (complete).
First reading: [[SQL-dbt Lesson 02 — Aggregation, GROUP BY & Grain]].

> **Mission goal:** move from a faithful 1:1 read of a source (staging) to *reshaping* it — change the grain on purpose and prove the new grain holds. This is where set-based thinking starts.

---

## The big conceptual lesson

**Grain** = what one row means. Staging keeps the source grain (one row per order). The moment you `GROUP BY`, you *choose a new grain* (one row per customer). Most SQL bugs are grain bugs: a join fans rows out, an aggregate double-counts, a uniqueness test goes red. Learn to name the grain of every model out loud.

The JOIN family and aggregation are the two tools that change grain — and the `unique` test on the new key is how you prove you got it right.

---

## Definition of Done (this mission)

- [ ] **Lesson 02 read** — aggregation, `GROUP BY`, `HAVING` vs `WHERE`, grain
- [ ] **`int_orders_per_customer`** built — first model that *changes grain* (one row per customer)
- [ ] `unique` + `not_null` on `customer_id` (the new grain key) — **green**
- [ ] Lesson 03 — the JOIN family + cardinality/fan-out (the row-multiplication trap)
- [ ] A model that joins `stg_orders` → `stg_payments` and aggregates spend per order without double-counting
- [ ] Every model refactored into the **import CTEs → logical CTEs → final select** idiom
- [ ] Permanent-note seedlings started: [[Set-Based Thinking]], [[Grain]]
- [ ] Every active session ends on a green `dbt test` + a commit

---

## Build targets (in order)

1. **`int_orders_per_customer`** — `count(order_id)` and `min/max(order_date)` grouped by `customer_id`. The "orders per customer" model. Meet `GROUP BY` and grain.
2. **Joins** — bring `stg_payments` to `stg_orders`; sum amount per order. Watch what a one-to-many join does to row counts.
3. **`HAVING`** — filter on an aggregate (e.g. customers with > 3 orders) and feel why it's not `WHERE`.

---

## STTM lens (the mapping this proves)

| STTM element | This mission |
|---|---|
| Origin data product | `raw_*` seeds → `stg_*` models (done in Phase 0) |
| Transformation logic | `int_orders_per_customer` — regrains by customer |
| Target contract | `unique` + `not_null` on the new `customer_id` grain key |

---

## Open thread → next session

- After grain lands, Phase 2 opens: **window functions** — calculating across related rows *without collapsing them*. That's where set-based thinking fully clicks.
