# Lifestyle

Personal finance, household management, budgeting, pensions, investing and wealth planning.

**Tag values:** `pensions` / `investing` / `taxes` / `retirement` / `accountancy`

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
  note.tags:
    displayName: Tags
  note.created:
    displayName: Created
views:
  - type: table
    name: All
    order:
      - file.name
      - type
      - tags
      - created
    sort:
      - property: file.name
        direction: ASC
```
