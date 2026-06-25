# 01 - Notes — Folder Guide

All notes live here, completely flat. No subfolders, no exceptions.

---

## What Lives Here

Everything you create or synthesize:
- Permanent notes and literature notes (knowledge layer)
- All content (newsletters, tweets, YouTube scripts)
- Projects (container notes)
- AI Prompts, SOPs, Reference Guides
- Reviews and journals

---

## Property Schema

```yaml
---
categories:
  - "[[Category Name]]"   # Required — links the note to a category hub
subjects:
  - "[[Subject Name]]"    # Optional — add one or more subject lenses
type: concept             # Required — per OKF spec v0.1
status: seedling          # Optional — see status flows below
created: YYYY-MM-DD
published: YYYY-MM-DD     # For published content only
---
```

---

## Status Flows by Category

| Category | Status flow |
|---|---|
| Permanent Notes | `seedling → mature` |
| Literature Notes | `saved → inprogress → complete` |
| Newsletters, YouTube Videos | `idea → inprogress → ready → published` |
| Tweets | `idea → ready → published` |
| Projects | `someday → active → complete` |

---

## All Categories — Type Values

| Category | Valid `type:` values |
|---|---|
| `[[Permanent Notes]]` | `concept`, `moc` |
| `[[Literature Notes]]` | `book`, `article`, `video`, `podcast`, `course` |
| `[[Newsletters]]` | `newsletter` |
| `[[Tweets]]` | `tweet` |
| `[[YouTube Videos]]` | `video` |
| `[[Projects]]` | `project`, `campaign`, `tracker` |
| `[[Reviews]]` | `daily`, `weekly`, `monthly` |
| `[[AI Prompts]]` | `prompt`, `workflow` |
| `[[SOPs]]` | `sop` |
| `[[Reference Guides]]` | `guide`, `framework`, `reference` |
| `[[Recipes]]` | `starter`, `main`, `side`, `dessert`, `bread`, `sauce`, `ingredient` |
| `[[Warhammer]]` | `army`, `faction`, `painting`, `game`, `campaign`, `moc` |
| `[[Lifestyle]]` | `finance`, `concept`, `account`, `strategy`, `reference` |
| `[[Personal]]` | `biography`, `record`, `memoir` |
| `[[Learning]]` | `lesson`, `mission`, `project`, `campaign`, `moc` |
| `[[Diary]]` | `daily`, `journal`, `newsletter`, `tweet`, `youtube`, `review` |

---

## File Naming

- **Newsletters:** `YYYY-MM-DD-slug.md`
- **Tweets:** `YYYY-MM-DD-slug-tweet.md`
- **Reviews:** `YYYY-MM-DD - Weekly Review.md`
- **Everything else:** descriptive title, no date prefix

---

## Rules

- Always flat — never create subfolders here
- Every note needs at least one `categories:` wikilink
- Archiving = set `status: archived`, never move to a separate folder
