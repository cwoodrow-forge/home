# 00 - Inbox — Folder Guide

This is a **transit zone only**. Files land here temporarily and must be processed.

---

## What Happens Here

When you capture something quickly — a voice note, a web clip, a rough idea — drop it in the Inbox. Then process it:

1. Add the correct `categories:` wikilink
2. Add `subjects:` if relevant
3. Set `type:` — **required** per OKF spec (see type values in root `CLAUDE.md`)
4. Write a `description:` — one sentence, max 20 words, specific and concrete
5. Set `status:` if the category uses one
6. Move the file to `01 - Notes/`

**The Inbox should always be empty after processing.**

---

## Processing Checklist

For each file in the Inbox:
- [ ] What category is this? → Add `categories:` wikilink
- [ ] What subject(s) does it relate to? → Add `subjects:`
- [ ] What is the sub-type within that category? → Set `type:` (required)
- [ ] Write a concrete one-sentence `description:`
- [ ] Is there an existing note this should connect to?
- [ ] Move to `01 - Notes/`

---

## When Using Claude Code

Run `/process-inbox [filename.md]` — Claude will:
1. Read the file and analyse its content
2. Assign the correct `categories:`, `subjects:`, `type:`, and `description:`
3. Add any category-specific fields (e.g. recipe protein/cook_time, status)
4. Move the file to `01 - Notes/` with complete OKF-compliant frontmatter
