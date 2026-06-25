# Tweets

Individual tweets and Substack notes — ready to publish or already live.

**Status flow:** `idea → ready → published → archived`

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
  note.subjects:
    displayName: Subjects
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
      - subjects
      - created
    sort:
      - property: created
        direction: DESC
  - type: table
    name: Ready
    filters:
      and:
        - status == "ready"
    order:
      - file.name
      - subjects
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
