# Literature Notes

Synthesis of everything you read, watch, and listen to.

A literature note captures key ideas from a source — a book, article, video, podcast, or course. It's not a summary of the whole thing; it's your highlights and your own interpretation of the best ideas.

**Type values:** `book` / `article` / `video` / `podcast` / `course`
**Status flow:** `saved → inprogress → complete`

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
      - type
      - subjects
      - status
      - created
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
      - type
  - type: table
    name: Complete
    filters:
      and:
        - status == "complete"
    order:
      - file.name
      - type
      - subjects
```
