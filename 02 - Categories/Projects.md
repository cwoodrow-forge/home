# Projects

Container notes for active and future projects.

Each project has one container note here. All files related to that project link back to it via a `project:` property in their YAML — those subordinate files get their own specific category (e.g., `[[Newsletters]]`, `[[SOPs]]`), never `[[Projects]]`.

**Status flow:** `someday → active → complete → archived`

---

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: Project
  note.status:
    displayName: Status
  note.created:
    displayName: Created
views:
  - type: table
    name: All
    order:
      - file.name
      - status
      - created
    sort:
      - property: status
        direction: ASC
  - type: table
    name: Active
    filters:
      and:
        - status == "active"
    order:
      - file.name
  - type: table
    name: Someday
    filters:
      and:
        - status == "someday"
    order:
      - file.name
```
