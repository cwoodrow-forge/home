# Business

Entrepreneurship, monetization, strategy, audience building, and marketing.

---

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
  note.created:
    displayName: Created
views:
  - type: table
    name: All
    order:
      - file.name
      - categories
      - status
      - created
    sort:
      - property: created
        direction: DESC
```
