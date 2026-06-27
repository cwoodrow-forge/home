# Recipes

Individual recipes, sauces, dressings, sides, and bakes — your personal cookbook.

**Type values:** `starter` / `main` / `side` / `dessert` / `bread` / `sauce` / `ingredient`

---

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: Title
  note.type:
    displayName: Type
  note.subjects:
    displayName: Subjects
  note.created:
    displayName: Created
views:
  - type: table
    name: All
    order:
      - file.name
      - type
      - created
    sort:
      - property: type
        direction: ASC
      - property: file.name
        direction: ASC

```
