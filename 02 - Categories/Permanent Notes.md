# Permanent Notes

Your atomic ideas — one concept per note, in your own words, built to last.

A permanent note distills one idea extracted from a literature note, an experience, or original thinking. It's atomic (one idea only), written in your own words, and connected to other permanent notes.

**Status flow:** `seedling → mature`

---

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: Title
  note.subjects:
    displayName: Subjects
  note.status:
    displayName: Status
  note.created:
    displayName: Created
views:
  - type: table
    name: All
    order:
      - file.name
      - subjects
      - status
      - created
    sort:
      - property: created
        direction: DESC
  - type: table
    name: Seedlings
    filters:
      and:
        - status == "seedling"
    order:
      - file.name
      - created
  - type: table
    name: Mature
    filters:
      and:
        - status == "mature"
    order:
      - file.name
      - subjects
```
