---
categories:
  - "[[Projects]]"
subjects:
  - "[[Productivity]]"
  - "[[Business]]"
type: concept
status: seedling
description: "OKF compliance project for this vault — vendor-neutral YAML spec making notes readable by humans and AI agents alike."
created: 2026-06-17
---

# Open Knowledge Format (OKF) — Project Idea

> Source: [Google Cloud Blog — How the Open Knowledge Format can improve data sharing](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing)

---

## What is OKF?

A vendor-neutral open spec (v0.1) for representing metadata, context, and curated knowledge in a way that both humans and AI agents can read. It's a **directory of markdown files with YAML frontmatter** — no SDK, no proprietary platform, no complex runtime.

Each file has a small YAML header (`type`, `title`, `description`, `resource`, `tags`, `timestamp`) plus human-readable markdown body. Markdown links between files create a traversable knowledge graph.

**Key insight**: Knowledge-as-code. Lives in git, survives tool migrations, works with any LLM, readable by humans and agents equally.

### OKF is domain-agnostic

Google launched it against BigQuery datasets, but the spec is entirely general. The only required field is `type` — and you define what types mean. Any discrete piece of knowledge with a name, a type, relationships to other things, and a body of content qualifies:

| Domain | Example concepts |
|---|---|
| Data engineering | Tables, metrics, APIs, pipelines |
| Personal knowledge | Mental models, book notes, ideas |
| Creative work | Recipes, painting palettes, scripts |
| Projects | Plans, SOPs, runbooks |
| Finance | Investment strategies, account types |

**This vault already implements the OKF pattern.** The YAML frontmatter, wikilinks, and `type:` values added during categorisation are OKF concepts in all but name.

---

## Vault OKF Compliance — Current State

| OKF field | Vault equivalent | Status |
|---|---|---|
| `type` | `type:` | ✅ Added to all notes |
| `title` | Filename | ✅ Implicit |
| `tags` | `tags:` | ✅ Present on most notes |
| `timestamp` | `created:` | ✅ Present on most notes |
| Markdown links | Wikilinks | ✅ Throughout vault |
| `description` | — | ❌ Missing — the key gap |
| `resource` | — | ❌ Missing (only relevant for sourced notes) |

The one field that would complete OKF compliance is `description:` — a single human+agent-readable sentence summarising what the note is. Once present on every note, the vault becomes a fully navigable knowledge bundle that any agent can traverse without reading full content.

---

## The Problem It Solves

- Metadata and context scattered across wikis, catalogs, code comments, and people's heads
- Each AI agent builder has to reinvent context-assembly from scratch
- Knowledge locked in proprietary platforms that don't survive migrations

OKF creates a portable, version-controlled, agent-readable layer between your knowledge and your AI tools — whether those tools are Claude, a future agent, or something that doesn't exist yet.

---

## How This Could Become a Project

### Option A — Add `description:` to this vault
The single highest-leverage change. Add a one-liner `description:` field to each note going forward (via the `/process-inbox` skill, which does this automatically). Retroactively add to existing notes over time.

**Effort**: Very Low ongoing (automated for new notes via skill).  
**Value**: Vault becomes fully OKF-compliant. Agents can find and reason about notes without reading full content.

### Option B — Build a Vault Export Bundle
Write a small Python script to export the vault as a clean OKF bundle — filtered by category, subject, or status. Feed this to Claude or any other agent as a portable knowledge context.

**Effort**: Medium. Python script, ~50 lines.  
**Value**: Portable knowledge context usable outside Obsidian, shareable, versionable.

### Option C — Document Data Assets (BigQuery / SQL)
Use Google's reference implementation (enrichment agent on GitHub) to auto-document a BigQuery dataset or local SQL database. Agent walks the dataset, drafts OKF docs for every table/view, enriches with schema and joins.

**Effort**: Medium-High. Requires GCP access and adapting the reference implementation.  
**Value**: Auto-generated documentation that stays current and is immediately AI-consumable.

---

## Next Actions

- [ ] Read the OKF spec: [github.com/GoogleCloudPlatform/knowledge-catalog](https://github.com/GoogleCloudPlatform/knowledge-catalog/tree/main/okf)
- [ ] Use `/process-inbox` skill for all new notes — builds `description:` habit from day one
- [ ] Retroactively add `description:` to high-value existing notes (Permanent Notes first)
- [ ] Explore vault export bundle script (Option B)
- [ ] Try static HTML visualiser on an exported bundle (no backend needed)

---

## Resources

- **Spec + reference implementations**: [GoogleCloudPlatform/knowledge-catalog](https://github.com/GoogleCloudPlatform/knowledge-catalog)
- **Google Cloud Knowledge Catalog**: Updated to ingest OKF and serve to agents
- **Sample bundles**: GA4 e-commerce, Stack Overflow, Bitcoin datasets (in repo)
- **Vault skill**: [[.claude/commands/process-inbox.md]] — auto-adds OKF frontmatter to Inbox notes
- **Related**: [[Python Data Analysis commands]], [[SQL Joins]], [[Setting up Obsidian + Claude AI]]
- **Obsidian LLM plugin:** https://community.obsidian.md/plugins/karpathywiki#-installation
