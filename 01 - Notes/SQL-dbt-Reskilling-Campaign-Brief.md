---
categories:
  - "[[Learning]]"
subjects:
  - "[[Technology]]"
type: campaign
status: active
description: "Self-directed SQL and dbt reskilling campaign for BigQuery data engineering, built around tested source-to-target data products."
tags:
  - sql
  - dbt
  - bigquery
  - duckdb
  - data-engineering
created: 2026-06-27
---

# SQL + dbt Reskilling Campaign — Brief

> **Authoritative spec.** This is the single source of truth for the campaign. Carl and Claude Code both build from this document. Decisions recorded here are locked unless explicitly revised in the vault.

---

## 1. Purpose

Reskill from an infrastructure / architecture background into **hands-on analytics engineering**: writing set-based SQL in dbt against BigQuery, to the point of independent competence.

**Definition of Done (the whole campaign):**
> Given an unseen source-to-target mapping spec, independently build a tested 3-layer dbt model (staging → intermediate → mart), run it, and validate that the target contract holds — with no scaffolding and no hand-holding.

**Timeframe:** 2–3 months, daily short sessions.

**Success is confidence, not coverage.** The goal is to *know* the role is within reach, not to memorise every SQL feature. Pure analytics SQL — the dbt/BigQuery 80%. Transactional SQL, DDL admin, and stored-procedure work are explicitly out of scope.

---

## 2. Who This Is For (context Claude Code should hold)

- Strong on infrastructure, CI/CD (Jenkins), orchestration (Composer/Airflow), Git, GCP, Python pipelines, and **architecture principles**. Move fast here — do not teach Git, environments, or CI/CD.
- New to **practical SQL**: has written basic `SELECT`s and understands joins conceptually, but lacks muscle memory and set-based fluency. Slow down here.
- Has previously *architected* dbt layering, SCD Type 2, and BigQuery cost patterns conceptually. This campaign converts that architectural knowledge into **build** capability.
- **Real learning curve:** declarative, set-based thinking — not syntax. Window functions are where it clicks. Design straight at this.
- **Failure mode to design against:** loses momentum when work turns theoretical and unrewarding. Needs small, frequent, *felt* wins. Every active session must end on a passing test and a commit.
- **Imposter syndrome** is in play. The test suite is the antidote: objective proof of capability that does not care about background.

---

## 3. Locked Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Early SQL environment | **DuckDB** (local, free, instant) | Zero-cost iteration while drilling fundamentals; no BigQuery bytes-scanned charges during careless practice |
| Gym dataset | **Jaffle Shop** (customers / orders / payments) | Purpose-built for dbt, clean, relational; fast wins weeks 1–8 |
| Platform dataset | **`thelook_ecommerce`** (BigQuery public) | Rich, multi-table, time-series; ideal for windows, SCD2, incremental, partitioning |
| Optional personal capstone | **Octopus Energy data** | Real and motivating; thinner for joins, so used as a stretch personal project |
| Learning workspace home | **Carl's Second Brain** (the workshop vault), as a `[[Learning]]` campaign | Built for living, changing notes; sits beside the existing Legion Data Engineer Campaign |
| Reference / knowledge home | **Vault of Moravec** (the LLM wiki), via the Librarian's ingest workflow | Receives *mature* distilled concepts only, after they're learned |
| dbt runtime | **dbt-core**, local on the Mac | Mirrors the day-to-day work environment |
| Spec format | **Source-to-Target Mapping (STTM) document** | Mirrors Carl's real work; maps cleanly onto dbt layers |

### The origin → foundational pipeline (why two vaults)

The two vaults mirror Carl's own professional architecture:

- **Second Brain = system of record** — raw, mutable, in-progress learning (origin data product).
- **LLM Wiki = curated foundational layer** — immutable, governed, queryable distilled knowledge (foundational data product).
- **The pipeline:** learn in the workshop → distil durable concepts → the Librarian *ingests* mature ones into the library.

The dbt project code lives in **neither vault** — it sits in a Git repo on disk.

---

## 4. The STTM → dbt Mapping (the core conceptual bridge)

Every spec in this campaign is a source-to-target mapping document, because that is the shape of Carl's real work and it maps one-to-one onto dbt:

| STTM element | dbt artifact | Rule |
|---|---|---|
| **Origin data product** (immutable system of record) | **Staging models** (`stg_*`) | 1:1 with source. Rename + recast only. No business logic. |
| **Transformation logic** (joins, business rules, SCD2) | **Intermediate models** (`int_*`) | Where the real reshaping happens. |
| **Foundational data product** (curated target schema) | **Mart models** | The target schema the STTM defines — grain, columns, contract. |
| **Target schema definition** (keys, not-null, allowed values, lineage) | **`schema.yml` + tests** | The mapping's column rules *are* the test suite and data contract. |

This is the campaign's central insight: **dbt is a notation for something Carl already understands.** Staging is the origin product. The mart is the foundational product. Tests are the contract. Implement origin → foundational; prove the contract with tests.

### STTM template (used for every mission spec)

```markdown
# STTM: <Foundational Product Name>

## Source (Origin Data Product — immutable)
| Table | Column | Type | Notes / Grain |
|-------|--------|------|---------------|
| raw_orders | id | int | PK, one row per order |
| raw_orders | user_id | int | FK → raw_customers.id |
| raw_orders | order_date | date | |
| ... | | | |

**Source grain:** one row per <X>.

## Target (Foundational Data Product — curated)
| Column | Type | Grain | Contract (tests) |
|--------|------|-------|------------------|
| customer_id | int | one row per customer | unique, not_null |
| lifetime_orders | int | | not_null, >= 0 |
| first_order_date | date | | not_null |
| ... | | | |

**Target grain:** one row per <Y>.

## Column-Level Mapping
| Target column | Source column(s) | Transformation rule | dbt layer |
|---------------|------------------|---------------------|-----------|
| customer_id | raw_customers.id | direct | staging |
| lifetime_orders | raw_orders.id | count, grouped by user_id | intermediate |
| first_order_date | raw_orders.order_date | min, grouped by user_id | intermediate |
| ... | | | |

## Acceptance criteria
- [ ] `dbt run` succeeds across all layers
- [ ] `dbt test` green — every target contract rule passes
- [ ] Grain assertion holds (uniqueness on the target key)
- [ ] `dbt docs` renders the lineage origin → foundational
```

---

## 5. Vault Integration (Second Brain schema)

Everything maps to existing types — no custom schema needed.

| Artifact | Category | `type:` | Status flow | Notes |
|---|---|---|---|---|
| This campaign brief | `[[Learning]]` | `campaign` | `active → complete` | Cross-link to `[[00. Campaign Overview]]` (Legion Data Engineer Campaign) as a sibling |
| Each phase | `[[Learning]]` | `mission` | `active → complete` | One mission note per phase |
| Train-readable concept notes | `[[Learning]]` | `lesson` | — | Subject `[[Technology]]`; include `#flashcard` lines for the Spaced Repetition plugin |
| Durable mental models | `[[Permanent Notes]]` | `concept` | `seedling → mature` | e.g. *Set-Based Thinking*, *Grain*, *Window Frame* — these are the **wiki ingest candidates** |
| Progress tracker | `[[Projects]]` | `tracker` | `active → complete` | Streak / checklist; momentum made visible |
| Weekly check-ins | `[[Reviews]]` | `weekly` | — | What built, what stuck, what to revisit |

Filing = adding the `categories:` wikilink. The Bases queries surface everything automatically. All notes stay flat in `01 - Notes/`.

---

## 6. The Campaign Arc

Each phase ends with something that **runs and passes**. dbt and tests appear in week one — they are the dopamine engine and the definition of done.

### Phase 0 — Setup & First Blood (Days 1–3)
**Mission: Environment & First Model**

- Python venv; install `dbt-core` + `dbt-duckdb`; install DuckDB.
- `dbt init`; configure `profiles.yml` for DuckDB.
- Init Git repo; push to GitHub.
- Seed Jaffle Shop raw data.
- Write `stg_customers`; add `unique` + `not_null` tests on the key.
- `dbt run` → `dbt test` → **green**. Commit.

**Win:** a materialised model and a passing test on day one.

### Phase 1 — SQL Fundamentals through dbt (Weeks 1–3)
**Mission: Reading & Reshaping Data**

- `SELECT`, aliasing, `WHERE`, `ORDER BY`, `LIMIT` — as staging models.
- **The JOIN family** — inner/left, and the mental model of **cardinality and grain** (fan-out, why a join can multiply rows). *The big conceptual lesson.*
- Aggregation — `GROUP BY`, `COUNT/SUM/AVG`, `HAVING` vs `WHERE`.
- **CTEs** — the dbt idiom: import CTEs → logical CTEs → final select. Refactor earlier models into this shape.

**Build:** clean staging models for all Jaffle Shop sources + a first aggregated model (orders per customer).
**Permanent notes:** *Set-Based Thinking*, *Grain*.

### Phase 2 — Analytics SQL (Weeks 3–6)
**Mission: Windows, Time, and Edge Cases**

- **Window functions I** — `OVER`, `PARTITION BY`, `ROW_NUMBER`, `RANK`. The mental model: a calculation across related rows *without collapsing them*. (Where set-based thinking lands.)
- **Window functions II** — `LAG`/`LEAD`, running totals, the window frame clause.
- Deduplication with `QUALIFY ROW_NUMBER()` (works in DuckDB and BigQuery).
- Dates & time — date math, truncation, date spines.
- `CASE`, conditional aggregation (`SUM(CASE WHEN ...)`), pivot patterns.
- `NULL` handling, `COALESCE`, three-valued-logic traps.

**Build:** an intermediate model with windowed metrics (order sequence number, days-between-orders, running spend per customer).
**Permanent notes:** *Window Frame*, *Three-Valued Logic*.

### Phase 3 — dbt as a Discipline (Weeks 5–8, overlaps Phase 2)
**Mission: Building a Layered Data Product**

- Project structure — staging / intermediate / marts; naming; the **staging contract** (1:1 with source, rename/recast only).
- `source()`, source freshness; `ref()` and the DAG.
- **Tests** — generic (`unique`, `not_null`, `accepted_values`, `relationships`), singular tests, and how they encode the STTM target contract.
- Documentation — `schema.yml`, `dbt docs generate/serve`.
- Materializations — `view` vs `table` vs `incremental`; when each.
- Light Jinja — `ref`/`source`, vars, one simple macro, `{{ this }}`. Just enough, no more.

**Build:** a complete staging → intermediate → mart "customer orders" data product for Jaffle Shop — fully tested and documented. **DoD becomes demonstrable on DuckDB here.**

### Phase 4 — BigQuery & GoogleSQL (Weeks 7–9)
**Mission: Onto the Platform**

- BigQuery setup; `dbt-bigquery` adapter; profiles; **sandbox / free-tier discipline**.
- GoogleSQL dialect vs DuckDB — `STRUCT`/`ARRAY` basics, `SAFE.` functions, `QUALIFY`, date functions.
- **Cost model** — bytes scanned, partition pruning, clustering, `--dry-run` cost estimation, why `SELECT *` is expensive.
- Partitioning & clustering via `dbt-bigquery` config.
- Incremental models — `is_incremental()`, incremental strategy, merge behaviour.
- **SCD Type 2 via dbt snapshots** — Carl has architected these; now build one against `thelook_ecommerce`.

**Build:** port the mart to BigQuery on `thelook_ecommerce` — partitioned + clustered, with one incremental model and one snapshot.

### Phase 5 — Capstone (Weeks 9–12)
**Mission A — Foundational Data Product (Guided):** a full STTM handed over; build origin (staging) → foundational (mart) with intermediate transforms, SCD2 where the mapping calls for it, full tests = target contract, docs. Reviewed at checkpoints.

**Mission B — Foundational Data Product (Solo):** a fresh STTM, no scaffolding, no checkpoints until done. Build independently, run, validate. **This is the DoD exam and the imposter-syndrome killer.**

**Mission C (optional):** Octopus Energy data as a personal foundational data product.

**Exit criteria:** an unseen STTM produces a tested 3-layer dbt model that runs and whose target contract passes — unaided.

---

## 7. Daily Rhythm (designed for the two windows)

**Train (passive, 20–40 min):** read the day's `lesson` note (written to be read on a phone, no execution), review `#flashcard`s, study the worked example, and arrive home knowing exactly what to build. No tooling friction on a moving train.

**Evening (active, 30–60 min):** build the model, make tests go green, commit. **Every evening ends on a passing test and a commit** — the deliberate dopamine hit, and the exact loop of the real job.

---

## 8. Feedback & Assessment (mixed, momentum-first)

- **Tests** — primary automated loop; green/red is instant feedback and is the DoD currency.
- **Weekly mini-spec** — a small STTM built solo, then reviewed.
- **On-demand code review** — eyes on SQL/dbt whenever wanted.
- **Spaced-repetition flashcards** — retention on the train.
- **Visible progress tracker** — streaks/checklist so progress is *felt*, not just real.

---

## 9. Cost Guardrails

- Phases 0–3 run entirely on **DuckDB** — free, local, no metering.
- BigQuery only from Phase 4, with **partition pruning** and `--dry-run` cost checks taught *before* any heavy query.
- Stay within the monthly free allowance / available credits; never `SELECT *` on a large unpartitioned scan.
- Account is a regular GCP account (not sandbox), so cost discipline is a *taught skill*, not just a guardrail — which is itself role-relevant.

---

## 10. Day-One Setup (concrete steps for Claude Code)

Before scaffolding, **read in this order:**
1. Second Brain (Home) `CLAUDE.md` (workshop vault — project instructions) and the relevant folder-level `CLAUDE.md` files.
2. `01 - Notes/00. Campaign Overview.md` (Legion Data Engineer Campaign) — so this campaign slots in as a sibling, not a guess.
3. Vault of Moravec `CLAUDE.md` (the LLM wiki) — so the eventual ingest path is understood.

**Then scaffold:**
1. Create the dbt repo on disk (e.g. `~/dev/dbt-learning`), `git init`, push to GitHub.
2. Set up the Python venv; install `dbt-core`, `dbt-duckdb`; verify `dbt --version`.
3. `dbt init`; configure DuckDB `profiles.yml`; confirm `dbt debug` passes.
4. Seed Jaffle Shop raw data.
5. Write `stg_customers` + `unique`/`not_null` tests; `dbt run` && `dbt test` → **green**; commit.
6. Create in the Second Brain: this campaign note (cross-linked to the Legion campaign), the Phase 0/1 `mission` note, the day-one `lesson` note (train-readable, with flashcards), and the `tracker`.

**End state of session one:** a passing `dbt test`, a first commit, and a campaign visible in the vault beside the Legion campaign.

---

## 11. What Lives Where (summary)

| Thing | Home |
|---|---|
| dbt project, models, tests, seeds, `.sql` | **Git repo on disk** (`~/dev/dbt-learning`) |
| Roadmap, missions, lessons, flashcards, tracker | **Second Brain** (`[[Learning]]` / `[[Projects]]` / `[[Reviews]]`) |
| Mature distilled concepts, references | **Vault of Moravec** (via Librarian ingest, after learning) |

---

## 12. Campaign Notes (live)

Sibling campaign: [[00. Campaign Overview]] (Legion Data Engineer Campaign).

| Note | Type | Status |
|---|---|---|
| [[SQL-dbt Phase 0 — Environment & First Model]] | mission | complete |
| [[SQL-dbt Phase 1 — Reading & Reshaping Data]] | mission | active |
| [[SQL-dbt Lesson 01 — Staging Models & the Staging Contract]] | lesson | — |
| [[SQL-dbt Lesson 02 — Aggregation, GROUP BY & Grain]] | lesson | — |
| [[SQL-dbt Campaign Tracker]] | tracker | active |

dbt project lives on disk at `~/dev/dbt-learning` (not in either vault).

---

*Build from this. Revise it in the vault if reality diverges — it is the spec, and specs are living contracts.*
