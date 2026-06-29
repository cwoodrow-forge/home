---
categories:
  - "[[Learning]]"
subjects:
  - "[[Technology]]"
type: lesson
description: Train-readable lesson on the dbt staging layer — the staging contract, the CTE shape, and ref().
tags:
  - sql
  - flashcard
  - "#dbt"
created: 2026-06-27
---

# Lesson 01 — Staging Models & the Staging Contract

*Part of [[SQL-dbt-Reskilling-Campaign-Brief]] · read on the train, build in the evening.*

---

## The one idea

A **staging model** is the clean, polite front door to one raw source. It does **exactly one job**: present that source with tidy names and correct types — and **nothing else**.

This is the **staging contract**:
- **1:1 with the source** — one staging model per raw table, same grain (same number of rows).
- **Rename and recast only** — `id → customer_id`, cast text to dates. No joins, no filters that drop rows, no business logic.
- Business logic lives **downstream** (intermediate + mart). Keeping staging dumb is what keeps the whole project debuggable.

Map it to what you already know: the raw seed is the **origin data product** (immutable system of record). Staging is the first, faithful read of it.

---

## The shape you'll type a hundred times

```sql
with source as (
    select * from {{ ref('raw_customers') }}
),
renamed as (
    select
        id as customer_id,   -- rename
        first_name,
        last_name
    from source
)
select * from renamed
```

Two things doing the heavy lifting:

1. **CTEs** (`with ... as (...)`) — named, stackable steps. Read top-to-bottom like a recipe. This is the dbt house style: *import CTEs* (pull sources in) → *logical CTEs* (do the work) → *final select*.
2. **`{{ ref('raw_customers') }}`** — dbt's reference function. You never hard-code a table name; `ref()` tells dbt "this model depends on that one," which builds the **DAG** (run order) and makes lineage real.

---

## The contract becomes a test

The mapping's column rules *are* the test suite. In `schema.yml`:

```yaml
models:
  - name: stg_customers
    columns:
      - name: customer_id
        data_tests:
          - unique      # no two rows share a customer_id
          - not_null    # every row has one
```

`dbt test` turns those two words into SQL that tries to find a violating row. **Zero rows = green = the contract holds.** Green/red is your dopamine loop and your definition of done.

---

## Worked example (what "green" looked like today)

```
dbt seed   → raw_customers (100), raw_orders (99), raw_payments (113)
dbt run    → stg_customers ......... OK (view)
dbt test   → not_null_stg_customers_customer_id ... PASS
             unique_stg_customers_customer_id ..... PASS
```

A view, and two passing tests. That's a shipped data product in miniature.

---

## Flashcards

What are the only two operations allowed in a staging model? :: Renaming columns and recasting types — 1:1 with the source, no business logic. #flashcard

What does `{{ ref('model_name') }}` do in dbt? :: References another model so dbt builds dependencies/lineage (the DAG) instead of you hard-coding table names. #flashcard

What is the standard dbt CTE pattern? :: Import CTEs (pull sources) → logical CTEs (do the work) → a final select. #flashcard

In a dbt generic test, what result means the test passes? :: Zero returned rows — the test queries for contract violations, and finding none = green. #flashcard

What does the `unique` test assert, and what does `not_null` assert? :: `unique`: no duplicate values in the column; `not_null`: every row has a value. #flashcard

Why keep business logic OUT of staging? :: To preserve a faithful 1:1 view of the source and keep the project debuggable; logic belongs in intermediate/mart layers. #flashcard

---

## Tonight's build

Write `stg_orders` and `stg_payments` using the exact shape above. Add `unique` + `not_null` on each table's key. `dbt run && dbt test` → green → commit. (See [[SQL-dbt Phase 0 — Environment & First Model]].)
