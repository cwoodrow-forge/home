# Reference Guides

Frameworks, checklists, and reference material you return to regularly.

---

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: Title
  note.subjects:
    displayName: Area
  note.created:
    displayName: Created
views:
  - type: table
    name: All
    order:
      - file.name
      - subjects
      - created
    sort:
      - property: file.name
        direction: ASC
```
