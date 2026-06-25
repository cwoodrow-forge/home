# Process Inbox Note

Processes a note from `00 - Inbox/`, adds OKF-aligned frontmatter, and moves it to `01 - Notes/`.

## Usage

```
/process-inbox [filename.md]
```

If no filename is provided, list the contents of `00 - Inbox/` and ask the user to choose.

---

## Instructions

You are processing a note from the vault Inbox (`00 - Inbox/`). Follow these steps precisely.

### Step 1 — Identify the note

- If `$ARGUMENTS` is provided, the target file is `00 - Inbox/$ARGUMENTS`
- If no argument, run `ls "00 - Inbox/"` and present the list to the user. Ask which note to process, then proceed.

### Step 2 — Read the note

Read the full content of the target file. Note its current frontmatter (if any) and body content.

### Step 3 — Analyse content and determine frontmatter

Based on the content, determine the following fields:

**`categories:` (Required — choose one)**

| Category | Use when the note is... |
|---|---|
| `[[Permanent Notes]]` | An atomic idea, concept, or mental model |
| `[[Literature Notes]]` | Notes from a book, article, video, or podcast |
| `[[Newsletters]]` | A newsletter draft or published issue |
| `[[Tweets]]` | A tweet or Substack note |
| `[[YouTube Videos]]` | A video script or idea |
| `[[Projects]]` | A project plan, tracker, or container |
| `[[Reviews]]` | A daily, weekly, or monthly review |
| `[[AI Prompts]]` | A reusable AI prompt |
| `[[SOPs]]` | A standard operating procedure |
| `[[Reference Guides]]` | Reference material, frameworks, how-to guides |
| `[[Recipes]]` | A food recipe |
| `[[Warhammer]]` | Warhammer hobby — painting, army, game, lore |
| `[[Lifestyle]]` | Personal finance, household, pensions, investing, budgeting |
| `[[Personal]]` | Family history, ancestry, life events, memoir |
| `[[Learning]]` | Python lessons, coding practice, structured study sessions, courses |
| `[[Diary]]` | Any note whose filename starts with a date — daily captures, journal entries, content pieces, reviews |

**`subjects:` (Optional — add any that apply)**

Hobby / Cooking / Technology / Finance / Creativity / Productivity / Philosophy / Business / Psychology / Health / Relationships

**`type:` (Required — per OKF spec v0.1; every note must have a non-empty type)**

| Category | Type values |
|---|---|
| Permanent Notes | `concept`, `moc` |
| Literature Notes | `book`, `article`, `video`, `podcast`, `course` |
| Newsletters | `newsletter` |
| Tweets | `tweet` |
| YouTube Videos | `video` |
| Projects | `project`, `campaign`, `tracker` |
| Reviews | `daily`, `weekly`, `monthly` |
| AI Prompts | `prompt`, `workflow` |
| SOPs | `sop` |
| Reference Guides | `guide`, `framework`, `reference` |
| Recipes | `starter`, `main`, `side`, `dessert`, `bread`, `sauce`, `ingredient` |
| Warhammer | `army`, `faction`, `painting`, `game`, `campaign`, `moc` |
| Lifestyle | `finance` (default) — or `concept`, `account`, `strategy`, `reference` |
| Personal | `biography`, `record`, `memoir` |
| Learning | `lesson`, `mission`, `project`, `campaign`, `moc` |
| Diary | `daily`, `journal`, `newsletter`, `tweet`, `youtube`, `review` |

**`status:` (Optional — use the right flow for the category)**

| Category | Status flow |
|---|---|
| Permanent Notes | `seedling → mature` |
| Literature Notes | `saved → inprogress → complete` |
| Newsletters, YouTube Videos | `idea → inprogress → ready → published` |
| Tweets | `idea → ready → published` |
| Projects | `someday → active → complete` |

Set to the earliest status in the flow for new notes (e.g. `seedling`, `saved`, `idea`, `someday`).

**`description:` (Required — OKF field)**

Write a single sentence (max 20 words) that a human or AI agent can read to understand what this note is about without reading the body. Be specific and concrete — avoid vague phrases like "notes on" or "thoughts about".

Good: `"Palette recipe for painting Blood Angels infantry at Legions Imperialis scale."`
Bad: `"Notes about painting Blood Angels."`

**`tags:` (Optional — preserve existing, add relevant)**

Keep any tags already present. Add content-level tags that describe the subject matter (not the category — that's what `categories:` is for).

**`created:` (Required)**

Use today's date in `YYYY-MM-DD` format.

**`resource:` (Optional — OKF field)**

If the note is sourced from a URL (article, blog post, video), include it here.

**Recipe-only fields (Required if `categories: [[Recipes]]`)**

Also determine and add these fields to the frontmatter:

| Field | Values |
|---|---|
| `protein:` | `fish` / `seafood` / `chicken` / `beef` / `lamb` / `pork` / `duck` / `poultry` / `vegetarian` |
| `cook_time:` | Integer — total minutes from prep to plate |
| `healthy:` | `true` or `false` — false if heavy cream, pastry, batter, or pasta-based |
| `dietary:` | `vegetarian` — only add if the dish contains no meat or fish |

### Step 4 — Build the updated frontmatter

Construct a clean YAML block. Always put fields in this order:
1. `categories:`
2. `subjects:` (if applicable)
3. `type:` (**always include** — required per OKF spec)
4. `status:` (if applicable)
5. `description:`
6. `resource:` (if applicable)
7. `tags:` (if applicable)
8. `created:`
9. `published:` (only for published content)
10. `protein:` / `cook_time:` / `healthy:` / `dietary:` (recipes only)

If the note already has frontmatter, **merge** — preserve existing values unless they're wrong, add missing OKF fields.

### Step 5 — Write the updated note

Edit the file in `00 - Inbox/` with the new frontmatter. Preserve the full body content exactly — do not summarise, rewrite, or remove anything.

### Step 6 — Move to `01 - Notes/`

Run:
```bash
mv "00 - Inbox/FILENAME.md" "01 - Notes/FILENAME.md"
```

### Step 7 — Check for a new cookbook source (recipes only)

**Only applies if the note is a recipe.**

Scan the note body for a source book reference. Look for any of these patterns:
- `Source: <Book Title>` (in a Reference source section)
- `Page: <number>` alongside a book title
- Any named cookbook in the body text

If a source book is identified:

0. **Convert the `Source:` line to a wikilink** — edit the recipe note body so the source reads as a bidirectional Obsidian link:
   ```
   Source: [[Book Title]]
   ```
   Use the exact filename of the book note (without `.md`). This must be done before moving the file, or immediately after — either way, the final note in `01 - Notes/` must contain the wikilink form, not plain text.

1. Check whether a note for that book already exists in `01 - Notes/`:
   ```bash
   ls "01 - Notes/" | grep -i "<book title>"
   ```

2. **If no note exists** — invoke `/new-cookbook` with the book title and author (if known from the note body). Pass the current recipe's details so Step 5 of that skill can seed the first table row immediately.

3. **If a note already exists** — open that note and append the recipe to the correct section table (same section logic as Step 5 of `/new-cookbook`). Do not create a new cookbook note.

4. Note the outcome in your Step 8 confirmation.

---

### Step 9 — Update Index (recipes and Warhammer notes only)

**If the note is a recipe**, append it to `01 - Notes/Recipe Index.md` in the correct table section.

**Which section to append to:**

| Condition | Section |
|---|---|
| `protein: fish` or `protein: seafood` | `## Mains — Fish & Seafood` |
| `protein: chicken/beef/lamb/pork/duck/poultry` | `## Mains — Meat & Poultry` |
| `protein: vegetarian` AND `type: main` | `## Mains — Vegetarian` |
| `type: side` | `## Sides & Vegetables` |
| `type: sauce`, `dressing`, or `ingredient` | `## Sauces, Dressings & Condiments` |
| `type: dessert` or `type: bread` | `## Desserts & Baked` |

**Row format to append** (match the existing table style exactly):

For mains:
```
| [[Recipe Name]] | protein | cook_time min | ✓ or ✗ reason |
```

For sides/sauces/desserts (no protein column):
```
| [[Recipe Name]] | cook_time min | ✓ or ✗ notes |
```

For the healthy column: use `✓` if healthy is true, or `✗ reason` (one or two words explaining why — e.g. `✗ cream`, `✗ pasta`, `✗ pastry`).

Append the row at the **end of the correct table**, before the next `---` or `##` heading.

Read `01 - Notes/Recipe Index.md` first so you can insert precisely. Use the Edit tool to add the row.

If the recipe doesn't clearly fit any section, append it to the closest match and note the decision in your confirmation.

**If the note is a Warhammer note**, append it to `01 - Notes/Warhammer Index.md` in the correct table section.

**Which section to append to:**

| Condition | Section |
|---|---|
| `type: game` or `type: campaign` | `## Game Systems & Campaign` |
| `type: faction` | `## Factions` |
| Loyalist Space Marine legion palette | `## Space Marine Legions — Loyalist` |
| Traitor Space Marine legion palette | `## Space Marine Legions — Traitor` |
| Loyalist titan legion palette | `## Titan Legions — Loyalist` |
| Traitor titan legion palette | `## Titan Legions — Traitor` |
| Knights, Auxilia, Xenos | `## Knights & Auxilia` |
| General painting technique or MOC | `## Techniques & Methods` |

**Row format** — match the existing table style for the section exactly. For painting notes include: Note link, allegiance (Loyalist/Traitor), scale (if known), key colours (2–3 words), status (✓ Palette complete / ⚠ In progress / ⚠ Empty).

Also update the **Collection Status Summary** table count if adding to a new row category.

Read `01 - Notes/Warhammer Index.md` first so you can insert precisely. Use the Edit tool to add the row.

### Step 10 — Confirm

Report back:
- The filename and where it was moved
- The frontmatter that was applied (show the YAML block)
- Which section of the Recipe Index it was added to (if a recipe)
- Cookbook outcome (if a recipe): new cookbook note created / existing cookbook note updated / no source book found
- Any decisions that weren't obvious (e.g. why you chose a particular category)

---

## Rules

- Never create subfolders in `01 - Notes/` — it is always flat
- Never overwrite existing `categories:` if already correctly set — just add missing OKF fields
- If content is ambiguous between two categories, choose the more specific one and note why
- The `description:` field is mandatory — never skip it
- Do not rename files unless the user asks
