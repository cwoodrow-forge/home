# Diary

Date-prefixed notes — daily captures, journal entries, published content pieces, and weekly reviews. Any note whose filename begins with a date lives here.

**Type values:** `daily` / `journal` / `newsletter` / `tweet` / `youtube` / `review`

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
  note.status:
    displayName: Status
  note.created:
    displayName: Created
views:
  - type: table
    name: All
    order:
      - file.name
      - type
      - status
      - created
    sort:
      - property: file.name
        direction: ASC
```
