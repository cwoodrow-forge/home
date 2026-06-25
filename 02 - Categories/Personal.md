# Personal

Personal notes — family history, ancestry, life events and anything that doesn't fit a work or hobby category.

**Tag values:** `family-history` / `wwii` / `ancestry` / `memoir`

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
