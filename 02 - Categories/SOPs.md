# SOPs

Standard Operating Procedures — step-by-step workflows for your most repeated processes.

---

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: SOP Name
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
