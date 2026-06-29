---
categories:
  - "[[Learning]]"
subjects:
  - "[[Technology]]"
type: lesson
description: "Train-readable lesson on aggregation, GROUP BY, HAVING vs WHERE, and the central idea of grain."
tags:
  - sql
  - dbt
  - flashcard
created: 2026-06-28
---

# Lesson 02 — Aggregation, GROUP BY & Grain

*Part of [[SQL-dbt-Reskilling-Campaign-Brief]] · read on the train, build in the evening.*
*Mission: [[SQL-dbt Phase 1 — Reading & Reshaping Data]].*

---

## The one idea

**Grain is what one row means.** Your staging models have *source grain* — one row per order, one row per payment. The single most important move in analytics SQL is **changing the grain on purpose**: turning "one row per order" into "one row per customer."

`GROUP BY` is the tool that does it. When you group, you are declaring a new grain — and everything in your `SELECT` must be either (a) the thing you grouped by, or (b) an **aggregate** that collapses the many rows in each group down to one number.

> Staging answered *"what is in the source?"* Aggregation answers *"one row per **what**, and what do I want to know about it?"*

---

## How GROUP BY actually works

Think of it as three steps the database does for you:

1. **Pile the rows into buckets** — one bucket per distinct value of the `GROUP BY` column.
2. **Run an aggregate over each bucket** — `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`.
3. **Emit one row per bucket.**

```sql
select
    customer_id,
    count(order_id)      as lifetime_orders,
    min(order_date)      as first_order_date,
    max(order_date)      as latest_order_date
from {{ ref('stg_orders') }}
group by customer_id
```

Input: 99 order rows. Output: one row per customer. **The grain changed** — and `customer_id` is the new key.

**The golden rule:** every non-aggregated column in the `SELECT` *must* appear in `GROUP BY`. If you select `customer_id` and `order_date` but only group by `customer_id`, the database can't pick *which* `order_date` to show — so it errors. Either aggregate it (`max(order_date)`) or group by it.

---

## The aggregates you'll live in

| Function | Returns | Watch for |
|---|---|---|
| `count(*)` | rows in the bucket | counts everything, incl. nulls |
| `count(col)` | non-null values in `col` | silently skips nulls |
| `count(distinct col)` | distinct non-null values | dedupes |
| `sum` / `avg` | total / mean | ignore nulls (≠ treating null as 0) |
| `min` / `max` | smallest / largest | work on dates too |

---

## HAVING vs WHERE — the classic trap

Both filter. The difference is **when** they run:

- **`WHERE` runs first** — on individual rows, *before* grouping. "Which rows go into the buckets?"
- **`HAVING` runs last** — on the grouped results, *after* aggregation. "Which buckets do I keep?"

```sql
select customer_id, count(order_id) as orders
from {{ ref('stg_orders') }}
where status != 'cancelled'   -- filter rows BEFORE grouping
group by customer_id
having count(order_id) > 3    -- filter GROUPS after aggregating
```

You **cannot** put `count(order_id) > 3` in `WHERE` — at `WHERE` time the count doesn't exist yet. That ordering (`WHERE` → `GROUP BY` → `HAVING`) is the whole lesson.

---

## Why this is "set-based thinking"

Coming from procedural code, the instinct is *loop over orders, keep a running tally per customer*. SQL refuses that frame. You declare **the shape of the answer** — "one row per customer, with their order count" — and the engine figures out the how. You describe the destination grain; you don't walk the path. That mental flip is the real curriculum, not the keywords. (Seedling: [[Set-Based Thinking]].)

---

## The contract: prove the new grain

When a model changes grain, the new key gets the same treatment staging keys got — because a `unique` failure here means your grain is wrong (a join fanned out, or the group key wasn't actually unique):

```yaml
models:
  - name: int_orders_per_customer
    columns:
      - name: customer_id
        data_tests:
          - unique     # proves: genuinely one row per customer
          - not_null
```

`unique` on the grain key is your **grain assertion** — green means "one row per customer" is true, not just intended.

---

## Flashcards

What does "grain" mean for a table or model? :: What a single row represents (e.g. one row per order, or one row per customer). #flashcard

What does `GROUP BY` do to a table's grain? :: It changes it — collapsing many rows into one row per distinct group value, defining a new grain. #flashcard

What is the golden rule of `GROUP BY`? :: Every column in the SELECT must either be in the GROUP BY or wrapped in an aggregate function. #flashcard

What is the difference between `WHERE` and `HAVING`? :: WHERE filters individual rows before grouping; HAVING filters grouped results after aggregation. #flashcard

Why can't you filter on `count(...) > 3` in a `WHERE` clause? :: WHERE runs before grouping, so the aggregate doesn't exist yet — use HAVING. #flashcard

What is the logical run order of WHERE, GROUP BY, and HAVING? :: WHERE → GROUP BY → HAVING. #flashcard

Difference between `count(*)` and `count(col)`? :: `count(*)` counts all rows; `count(col)` counts only non-null values of that column. #flashcard

When a model changes grain, what test proves it's correct? :: A `unique` test on the new grain key — it's the grain assertion. #flashcard

What is "set-based thinking"? :: Declaring the shape/grain of the answer you want and letting the engine compute it, rather than looping row-by-row. #flashcard

---

## Tonight's build

Write **`int_orders_per_customer`** in `models/intermediate/` using the import → logical → final-select CTE shape: import `stg_orders`, group by `customer_id` to get `lifetime_orders`, `first_order_date`, `latest_order_date`. Add `unique` + `not_null` on `customer_id` in `schema.yml`. `dbt build` → green → commit. (See [[SQL-dbt Phase 1 — Reading & Reshaping Data]].)
