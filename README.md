# Task Boards

A lightweight kanban app in a single HTML file. It organises tasks into **boards**. Each board holds **groups**, and each group has three columns: **To do**, **In progress** and **Done**.

No install, no build step, no server: open `task-boards.html` in a browser and start working.

---

## Features

### Boards
- Create as many boards as you need, one per project, team or area of life, for example.
- Boards appear as tabs across the top. Click a tab to switch boards.
- **Rename board** edits the name inline. Press Enter to save or Esc to cancel.
- **Delete board** removes the board with all its groups and tasks, after an inline confirmation.
- The last board you opened is remembered on that device.

### Groups
- Each board contains any number of groups, for example features, sprints or clients.
- Every group is a row spanning the three columns.
- The group header shows:
  - the group's colour marker
  - a done count (`done / total`)
  - a progress bar split into to do, in progress and done
- **Edit** lets you change the group's name and colour in one place.
- **Delete** removes the group and its tasks, after an inline confirmation.
- The ▾ / ▸ button collapses a group or expands it again.

### Tasks
- New tasks are always created in **To do**. The other columns only receive tasks moved into them.
- Each task has a title, optional notes and an optional colour.
- The add form stays open after each task, and keeps the last colour you picked, for quick entry of several tasks.
- **Edit** changes the title, notes and colour.
- **✕** deletes a task, after an inline confirmation.
- Tasks in **Done** are shown struck through.

### Moving tasks
- **Drag and drop** cards between columns, between groups on the same board, or to a new position within a column.
- The **◂ / ▸** buttons on each card move it one column left or right. These are useful on touch screens, where drag and drop isn't available.

### Colours
- Nine colours plus "no colour": red, orange, yellow, green, teal, blue, purple, pink and grey.
- A **group colour** tints the group's columns and adds a stripe beside its name.
- A **task colour** gives the card a coloured left edge and a soft background tint.
- Colours are set in the **Edit** form of a group or task, and when adding a task.

### Backup
- **Export backup** downloads every board, group and task, with their colours, as a dated `.json` file, for example `task-boards-2026-09-25.json`.
- **Import backup** loads a backup file. It asks before replacing all current data.
- Use backups to protect your data, or to move tasks between browsers, computers, or the local and online versions.

### Keyboard
| Where | Key | Action |
|---|---|---|
| Any name or title field | Enter | Save |
| Any edit form | Esc | Cancel |
| Delete confirmation | Esc | Keep the item |

### Layout
- Responsive. On narrow screens the columns stack vertically inside each group, with a label on each column.
- Follows your system's light or dark theme.

---

## Running locally

1. Download `task-boards.html`.
2. Open it in a modern browser, such as Chrome, Edge, Firefox or Safari, by double-clicking it or dragging it into a browser window.

That's it. It works offline. Only the Onest web font needs internet, and without it the page falls back to your system font.

### Where the data is stored

| Version | Storage |
|---|---|
| Local file | The browser's local storage, on your machine |
| Online (claude.ai link) | The artifact's own database, synced across devices, with a local copy in the browser |

The two versions **don't sync with each other**. Use Export and Import to move data between them.

**Keep your local data safe:**
- Use the same browser each time. Each browser keeps its own data.
- Keep the file in the same place.
- Clearing browser site data erases the board. Export a backup regularly.

---

## Backup file format

The backup is plain JSON:

```json
{
  "app": "task-boards",
  "version": 1,
  "exported": "2026-09-25T10:00:00.000Z",
  "boards": [ { "id": "…", "name": "Work" } ],
  "groups": [ { "id": "…", "boardId": "…", "name": "Sprint 12", "color": "blue", "collapsed": false } ],
  "tasks":  [ { "id": "…", "groupId": "…", "status": "todo", "title": "Write smoke tests", "notes": "", "color": "red", "created": 1790000000000 } ]
}
```

- `status` is one of `todo`, `doing` or `done`.
- `color` is one of `red`, `orange`, `yellow`, `green`, `teal`, `blue`, `purple`, `pink`, `grey`, or `null` for no colour.
- The order of the `tasks` array is the order of cards within each column.

---

## Tech notes

- A single self-contained HTML file with vanilla JavaScript and CSS. It has no dependencies apart from the optional Google Font.
- All state is one JSON object that is re-rendered on every change.
- Saves are debounced, about 0.7 s after the last change. Every change carries a revision number, so an older saved copy never overwrites newer work.
- Built-in browser pop-ups (`prompt`/`confirm`) aren't used. All editing and confirmations happen inline, so the app also works in sandboxed frames.
