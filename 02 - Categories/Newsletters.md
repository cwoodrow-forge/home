# Newsletters

All newsletter drafts and published issues.

**Status flow:** `idea → inprogress → ready → published → archived`

---

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: Title
  note.status:
    displayName: Status
  note.created:
    displayName: Created
  note.published:
    displayName: Published
views:
  - type: table
    name: All
    order:
      - file.name
      - status
      - created
      - published
    sort:
      - property: created
        direction: DESC
  - type: table
    name: In Progress
    filters:
      and:
        - status == "inprogress"
    order:
      - file.name
      - created
  - type: table
    name: Ready
    filters:
      and:
        - status == "ready"
    order:
      - file.name
  - type: table
    name: Published
    filters:
      and:
        - status == "published"
    order:
      - file.name
      - published
    sort:
      - property: published
        direction: DESC
```
