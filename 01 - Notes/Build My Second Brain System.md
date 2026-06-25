---
categories:
  - "[[Projects]]"
subjects:
  - "[[Productivity]]"
  - "[[Business]]"
type: project
status: active
description: "Active project: set up a Zettelkasten second brain in Obsidian with 50+ connected permanent notes and a weekly content workflow."
created: 2026-01-01
---
# Build My Second Brain System

**Goal:** Set up a working Zettelkasten-based second brain in Obsidian that I actually use consistently and that feeds my content creation.

**Success looks like:** 50+ connected permanent notes, weekly content creation workflow running, publishing consistently.

---

## Project Files

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

---

## Milestones

- [ ] Set up vault structure (folders, CLAUDE.md files, categories)
- [ ] Configure Obsidian settings (templates, attachments folder, themes)
- [ ] Process first 5 books into literature notes
- [ ] Write first 20 permanent notes
- [ ] Run the Content Writing System SOP for the first newsletter
- [ ] Publish first piece of content using notes from the vault
- [ ] Build a weekly review habit

---

## Notes

- Start with the [[Content Acquisition SOP]] to build the input system first
- Don't organize before you have enough notes to organize
- The goal for week 1 is just to have notes that link to each other — nothing else
