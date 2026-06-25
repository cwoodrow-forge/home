# AI Prompts

Reusable prompts for Claude, ChatGPT, or any AI assistant. Copy, paste, and create.

---

```base
filters:
  and:
    - file.hasLink(this.file)
properties:
  file.name:
    displayName: Prompt Name
  note.subjects:
    displayName: Use Case
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
