# Vault Guide — Carl's Second Brain

**Updated:** 2026-06-21

This file is read automatically by Claude Code as project instructions. It is also the primary human-readable guide to how this vault is structured and maintained.

---

## What This Vault Is

A personal second brain built in Obsidian, organised around five main areas of life:

- **Horus Heresy** — painting, armies, game systems, hobby projects
- **Cooking** — 75+ recipes, cookbook notes, technique references
- **Python & Technology** — learning missions, data engineering, coding practice
- **Personal Finance** — pensions, investing, retirement planning, tax
- **Content Creation** — newsletters, tweets, YouTube scripts, permanent notes

**179 notes. All flat in `01 - Notes/`. Navigation is via categories and subjects — no folder hierarchy.**

---

## Folder Structure

```
Home/
├── 00 - Inbox/       ← Transit zone. Drop captures here, then /process-inbox
├── 01 - Notes/       ← ALL notes, completely flat. No subfolders.
├── 02 - Categories/  ← 16 category container notes (Bases query hubs)
├── 03 - Subjects/    ← 11 subject container notes (cross-cutting lenses)
├── 04 - System/      ← Templates, Attachments, Bin
│   ├── Attachments/  ← All binary files (images, PDFs). Auto-managed by Obsidian.
│   ├── Bin/          ← Orphaned attachments awaiting manual deletion
│   └── Templates/    ← Note templates
├── Excalidraw/       ← Excalidraw drawings (.excalidraw.md)
├── .claude/
│   └── commands/     ← Slash command skills for Claude Code
├── HOME.md           ← Vault entry point and navigation hub
└── CLAUDE.md         ← This file
```

Each folder has its own `CLAUDE.md` explaining what lives inside.

---

## Navigation Mechanic — Bases Queries

Every note in `01 - Notes/` has a `categories:` YAML property containing a wikilink, e.g. `"[[Warhammer]]"`. Each category container note in `02 - Categories/` runs an Obsidian Bases query:

```
filters:
  and:
    - file.hasLink(this.file)
```

This automatically surfaces every note that links to it. **Filing a note = adding the right wikilink to `categories:`.**

No manual sorting. No folder hierarchy. Categories and subjects are the entire navigation layer.

---

## OKF Property Schema

All notes follow the Open Knowledge Format. Fields in this order:

```yaml
---
categories:
  - "[[Category Name]]"     # Required — links to 02 - Categories/
subjects:
  - "[[Subject Name]]"      # Optional — links to 03 - Subjects/
type: concept               # Required — per OKF spec v0.1 (see type values below)
status: seedling            # Optional — see status flows below
description: "..."          # Required — one sentence, max 20 words, specific
resource: https://...       # Optional — source URL for sourced notes
tags:                       # Optional — content-level tags
  - tag-name
created: YYYY-MM-DD         # Required
published: YYYY-MM-DD       # For published content only
---
```

**Type values by category:**

| Category | Valid `type:` values |
|---|---|
| `[[Permanent Notes]]` | `concept`, `moc` |
| `[[Literature Notes]]` | `book`, `article`, `video`, `podcast`, `course` |
| `[[Reviews]]` | `daily`, `weekly`, `monthly` |
| `[[AI Prompts]]` | `prompt`, `workflow` |
| `[[SOPs]]` | `sop` |
| `[[Reference Guides]]` | `guide`, `framework`, `reference` |
| `[[Projects]]` | `project`, `campaign`, `tracker` |
| `[[Recipes]]` | `starter`, `main`, `side`, `dessert`, `bread`, `sauce`, `ingredient` |
| `[[Warhammer]]` | `army`, `faction`, `painting`, `game`, `campaign`, `moc` |
| `[[Lifestyle]]` | `finance`, `concept`, `account`, `strategy`, `reference` |
| `[[Learning]]` | `lesson`, `mission`, `project`, `campaign`, `moc` |
| `[[Diary]]` | `daily`, `journal`, `newsletter`, `tweet`, `youtube`, `review` |
| `[[Newsletters]]` | `newsletter` |
| `[[Tweets]]` | `tweet` |
| `[[YouTube Videos]]` | `video` |
| `[[Personal]]` | `biography`, `record`, `memoir` |

**Recipe-only additional fields:**
```yaml
protein: fish               # fish/seafood/chicken/beef/lamb/pork/duck/poultry/vegetarian
cook_time: 20               # integer, total minutes
healthy: true               # false if cream, pastry, batter or pasta-heavy
dietary: vegetarian         # only if no meat or fish
```

**Status flows by category:**

| Category | Flow |
|---|---|
| Permanent Notes | `seedling → mature` |
| Literature Notes | `saved → inprogress → complete` |
| Newsletters, YouTube Videos | `idea → inprogress → ready → published` |
| Tweets | `idea → ready → published` |
| Projects | `someday → active → complete` |

---

## The 16 Categories

| Category | What it contains |
|---|---|
| `[[Permanent Notes]]` | Atomic ideas, concepts, mental models |
| `[[Literature Notes]]` | Books and cookbooks — notes and MOCs |
| `[[Newsletters]]` | Newsletter drafts and published issues |
| `[[Tweets]]` | Tweets and Substack notes |
| `[[YouTube Videos]]` | Video scripts and metadata |
| `[[Projects]]` | Project plans, trackers, container notes |
| `[[Reviews]]` | Daily, weekly, monthly reviews |
| `[[AI Prompts]]` | Reusable AI prompts |
| `[[SOPs]]` | Standard operating procedures |
| `[[Reference Guides]]` | Reference material, frameworks, how-to guides |
| `[[Recipes]]` | Food recipes — mains, sides, sauces, desserts |
| `[[Warhammer]]` | Horus Heresy hobby — painting, armies, game systems, lore |
| `[[Lifestyle]]` | Personal finance, pensions, investing, tax, budgeting |
| `[[Personal]]` | Family history, ancestry, life events, memoir |
| `[[Learning]]` | Python lessons, coding missions, structured study |
| `[[Diary]]` | Any note whose filename starts with a date |

---

## The 11 Subjects

Subjects are cross-cutting lenses. A note can have multiple subjects.

| Subject | What it covers |
|---|---|
| `[[Hobby]]` | Horus Heresy, Warhammer painting, miniature making, resin printing |
| `[[Cooking]]` | Recipes, cookbooks, technique and flavour |
| `[[Technology]]` | Python, data engineering, coding, AI tools, platform engineering |
| `[[Finance]]` | Personal finance, retirement, investing, pensions and tax |
| `[[Creativity]]` | Creative process, content creation, writing, artistic thinking |
| `[[Productivity]]` | Systems, focus, time, workflow |
| `[[Philosophy]]` | Big ideas, meaning, ethics, worldview |
| `[[Business]]` | Entrepreneurship, monetization, strategy, marketing |
| `[[Psychology]]` | Human behaviour, mindset, mental models |
| `[[Health]]` | Physical and mental wellbeing, habits |
| `[[Relationships]]` | Connection, communication, community |

---

## Key Index Files

Read these before working on a specific domain — they replace reading dozens of individual notes:

| File | Purpose |
|---|---|
| `01 - Notes/Warhammer Index.md` | Master index of 24 Warhammer notes — read before any Warhammer task |
| `01 - Notes/Recipe Index.md` | All 75 recipes with protein, cook time, health rating |
| `01 - Notes/Horus Heresy Project Inspiration.md` | MOC of all hobby project ideas |
| `01 - Notes/00. Campaign Overview.md` | Legion Data Engineer Campaign — Python learning roadmap |

---

## Claude Code Skills

Skills live in `.claude/commands/` and are invoked as slash commands:

| Skill | Command | What it does |
|---|---|---|
| Process Inbox | `/process-inbox [filename.md]` | Adds OKF frontmatter to an inbox note and moves it to `01 - Notes/` |
| Check Attachments | `/check-attachments` | Scans `04 - System/Attachments/` for orphaned files and moves them to `04 - System/Bin/` |

---

## Key Rules

- **`01 - Notes/` is always flat** — never create subfolders, no exceptions
- **`00 - Inbox/` is a transit zone** — always process with `/process-inbox`, never leave notes there permanently
- **Filing = adding the wikilink** — the category container notes find the note automatically via Bases
- **`description:` is mandatory** — every note needs one. Max 20 words, specific and concrete
- **Attachments** go to `04 - System/Attachments/` — configured automatically by Obsidian
- **Bin** (`04 - System/Bin/`) holds orphaned attachments — delete manually, never auto-delete
