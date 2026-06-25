# New Cookbook

Creates a new cookbook reference note in `01 - Notes/` following the vault's standard cookbook format.

## Usage

```
/new-cookbook [Book Title | Author]
```

Can also be called internally by `/process-inbox` when a recipe note references a book that has no existing vault note.

---

## Instructions

### Step 1 — Parse arguments

`$ARGUMENTS` may be supplied in any of these forms:
- `Book Title` — title only
- `Book Title | Author Name` — title and author separated by a pipe
- Nothing — prompt the user for title and author before proceeding

If only a title is provided, proceed without an author (leave the `author:` field as a placeholder and note it in the confirmation).

### Step 2 — Check for an existing note

Before creating anything, check whether a note for this book already exists:

```bash
ls "01 - Notes/" | grep -i "<book title>"
```

- If a matching note is found, **stop**. Report the existing file path to the user and do not create a duplicate.
- If no match is found, proceed.

### Step 3 — Infer book style and tags

Based on the title and author, infer a short style description (1–2 sentences) for the header block. Use what you know about the book. If you have no knowledge of it, use a neutral placeholder:

> *Style description not yet added — update after cooking from the book.*

Choose appropriate tags from:
- `cookbook` — always include
- `healthy-eating` — if the book is diet/calorie-focused
- `baking` — if primarily a baking book
- `vegetarian` / `vegan` — if the book is plant-based
- Any other specific tag that clearly applies (e.g. `italian`, `asian`, `hairy-bikers`)

### Step 4 — Create the cookbook note

**Filename:** Use the exact book title with no suffix. No "- Literature Note", no date prefix.

Example: `The Hairy Dieters Fast Food.md`, `Happy Days with the Naked Chef.md`

Write the file to `01 - Notes/<Book Title>.md` using this exact template:

```markdown
---
categories:
  - "[[Literature Notes]]"
subjects:
  - "[[Cooking]]"
type: book
status: inprogress
description: "<Author>'s <Book Title> — <one phrase summary of the book's focus>."
tags:
  - cookbook
  <additional tags>
author: <Author Name>
created: <today's date YYYY-MM-DD>
---

# <Book Title>

**Author:** <Author Name>
**Style:** <Style description — 1–2 sentences on cooking style, influences, and what makes the book distinctive.>

> Recipes from this book are captured in the vault. Click any link to open the recipe. All carry `Source: <Book Title>` in their body, so Obsidian backlinks also provide reverse navigation from each recipe back to this note.

---

## Fish & Seafood

| Recipe | Healthy |
|---|---|

---

## Meat & Poultry

| Recipe | Protein | Healthy |
|---|---|---|

---

## Vegetarian Mains

| Recipe | Healthy |
|---|---|

---

## Sides & Vegetables

| Recipe | Healthy |
|---|---|

---

## Sauces, Dressings & Condiments

| Recipe | Notes |
|---|---|

---

## Desserts & Baked

| Recipe | Healthy |
|---|---|
```

### Step 5 — Add the triggering recipe (if called from process-inbox)

If this skill was invoked during a `/process-inbox` run because a recipe note referenced this book:

1. Add the recipe to the correct section table in the new cookbook note immediately after creating it.
2. Determine the correct section from the recipe's `type:` and `protein:` fields:

| Condition | Section |
|---|---|
| `protein: fish` or `protein: seafood` | `## Fish & Seafood` |
| `protein: chicken/beef/lamb/pork/duck/poultry` | `## Meat & Poultry` |
| `protein: vegetarian` AND `type: main` | `## Vegetarian Mains` |
| `type: side` | `## Sides & Vegetables` |
| `type: sauce` or `type: ingredient` | `## Sauces, Dressings & Condiments` |
| `type: dessert` or `type: bread` | `## Desserts & Baked` |

**Row format:**

For Fish & Seafood, Vegetarian Mains, Sides, Desserts:
```
| [[Recipe Name]] | ✓ or ✗ reason |
```

For Meat & Poultry:
```
| [[Recipe Name]] | protein | ✓ or ✗ reason |
```

For Sauces & Condiments:
```
| [[Recipe Name]] | brief note |
```

Healthy column: `✓` if `healthy: true`, otherwise `✗ reason` (one or two words — e.g. `✗ cream`, `✗ pastry`, `✗ batter`).

### Step 6 — Confirm

Report back:
- The filename created and its location
- The frontmatter applied (show the YAML block)
- Whether a recipe was added to a section table (if triggered from process-inbox)
- Any fields left as placeholders (e.g. author unknown, style description generic)

---

## Rules

- **Never create a duplicate** — always check for an existing note first
- **Never add "- Literature Note" to the filename** — the title alone is the filename
- **Never create subfolders** — always write to `01 - Notes/` flat
- **`description:` is mandatory** — always write a concrete one-sentence description
- **`status: inprogress`** — new cookbooks always start here; only set `complete` when the user explicitly says so
- If author is unknown, omit the `author:` field rather than guessing
