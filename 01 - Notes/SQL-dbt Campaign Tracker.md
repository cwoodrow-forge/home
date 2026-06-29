---
categories:
  - "[[Projects]]"
subjects:
  - "[[Technology]]"
type: tracker
status: active
description: "Progress tracker for the SQL + dbt reskilling campaign — streak, phase checklist, and session log."
tags:
  - sql
  - dbt
  - data-engineering
created: 2026-06-27
---

# SQL + dbt Campaign Tracker

**Goal:** Build a tested 3-layer dbt model from an unseen STTM, unaided. Momentum made visible — every active session ends on a passing test and a commit.

Spec: [[SQL-dbt-Reskilling-Campaign-Brief]] · Current mission: [[SQL-dbt Phase 1 — Reading & Reshaping Data]]

---

## 🔥 Streak

**Current streak: 2 days** · Last session: 2026-06-28 · Sessions logged: 2

> Rule: a session only counts if it ends on a **green `dbt test`** and a **commit**.

---

## Phase Checklist

- [x] **Phase 0 — Setup & First Blood** ✅ *(complete 2026-06-28)*
  - [x] Environment: venv, dbt-core, dbt-duckdb
  - [x] dbt project + DuckDB profile, `dbt debug` green
  - [x] Seed Jaffle Shop
  - [x] `stg_customers` + tests, `dbt run`/`test` green, commit
  - [x] `stg_orders` + `stg_payments` + tests — `dbt build` 14 PASS
  - [x] Push to GitHub — `cwoodrow-forge/dbt-learning`, `main` in sync
- [ ] **Phase 1 — SQL Fundamentals through dbt** (Weeks 1–3) *(in progress)*
  - [ ] Lesson 02 read — aggregation, `GROUP BY`, grain
  - [ ] `int_orders_per_customer` (first grain change) + tests green
  - [ ] Joins + cardinality/fan-out lesson
- [ ] **Phase 2 — Analytics SQL** (Weeks 3–6)
- [ ] **Phase 3 — dbt as a Discipline** (Weeks 5–8)
- [ ] **Phase 4 — BigQuery & GoogleSQL** (Weeks 7–9)
- [ ] **Phase 5 — Capstone** (Weeks 9–12)

---

## 🌱 Permanent-note candidates (wiki ingest pipeline)

Distil these into [[Permanent Notes]] as they mature, then ingest into the Vault of Moravec:

- [ ] *Set-Based Thinking* — Phase 1
- [ ] *Grain* — Phase 1
- [ ] *Window Frame* — Phase 2
- [ ] *Three-Valued Logic* — Phase 2

---

## Session Log

| Date | Phase | What built | Test result | Commit |
|---|---|---|---|---|
| 2026-06-27 | 0 | dbt+DuckDB scaffold, Jaffle Shop seeds, `stg_customers` | 🟢 2 PASS | `eebdafc` |
| 2026-06-28 | 0 | `stg_orders` + `stg_payments` + tests; pushed to GitHub | 🟢 14 PASS | `ed2f892` |

---

## Linked Campaign Notes

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: Title
  note.categories:
    displayName: Category
  note.status:
    displayName: Status
views:
  - type: table
    name: All
    order:
      - file.name
      - categories
      - status
```
