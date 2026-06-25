# Reviews

Daily, weekly, and monthly reviews — your system for reflection and recalibration.

**Type values:** `daily` / `weekly` / `monthly`

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
  note.created:
    displayName: Date
views:
  - type: table
    name: All
    order:
      - file.name
      - type
      - created
    sort:
      - property: created
        direction: DESC
  - type: table
    name: Weekly
    filters:
      and:
        - type == "weekly"
    order:
      - file.name
      - created
    sort:
      - property: created
        direction: DESC
```
