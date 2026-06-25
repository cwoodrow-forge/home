# Learning

Learning notes — courses, tutorials, coding practice, skill-building logs and structured study sessions.

**Tag values:** `python` / `coding` / `sql` / `ai` / `warhammer` / `course`

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
