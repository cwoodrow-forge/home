# Finance

Personal finance notes — investments, pensions, budgeting, and wealth management.

**Type values:** `concept` / `account` / `strategy` / `reference`

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
      - property: file.name
        direction: ASC
```
