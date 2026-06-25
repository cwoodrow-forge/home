# Warhammer

Army notes, faction references, painting palettes, and game rules for Horus Heresy, Legions Imperialis, and related games.

**Type values:** `army` / `faction` / `painting` / `game` / `campaign`

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
