# 02 - Categories — Folder Guide

This folder contains **10 category container notes**. Each one is a navigation hub that automatically surfaces all notes linked to it.

---

## How It Works

Each category note contains an Obsidian Bases query:

```
filters:
  and:
    - file.hasLink(this.file)
```

Any note in `01 - Notes/` that has `categories: ["[[Permanent Notes]]"]` in its YAML will automatically appear in the `Permanent Notes.md` container note. No manual sorting needed.

---

## The 10 Categories

| File | What it surfaces |
|---|---|
| `Permanent Notes.md` | Atomic ideas and mental models |
| `Literature Notes.md` | Notes from books, articles, videos, podcasts |
| `Newsletters.md` | Newsletter drafts and issues |
| `Tweets.md` | Individual tweets and Substack notes |
| `YouTube Videos.md` | Video scripts and metadata |
| `Projects.md` | Project container notes |
| `Reviews.md` | Daily, weekly, monthly reviews |
| `AI Prompts.md` | Reusable AI prompts |
| `SOPs.md` | Standard operating procedures |
| `Reference Guides.md` | Reference material and frameworks |

---

## Rules

- Never add notes directly to this folder
- Never modify the Bases query in container notes
- To add a new category: create a new container note here with the same Bases query template
