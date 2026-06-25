---
categories:
  - "[[Projects]]"
subjects:
  - "[[Subject Name]]"
type: project   # project / campaign / tracker
status: someday
description: ""
created: {{date:YYYY-MM-DD}}
---
# Project Name

**Goal:** What does success look like for this project?

---

## Project Files

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: Title
  note.categories:
    displayName: Category
  note.status:
    displayName: Status
views:
  - type: table
    name: All
    order:
      - file.name
      - categories
      - status
```

---

## Milestones

- [ ]
- [ ]
- [ ]

---

## Notes

