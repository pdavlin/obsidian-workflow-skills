---
name: add-frontmatter
description: Analyze Obsidian notes and add or update YAML frontmatter properties using the Obsidian CLI. Supports meeting notes, daily notes, reference notes, and project notes with consistent property naming.
---

# Add Frontmatter

Analyze Obsidian notes and add intelligent YAML frontmatter properties to enhance organization and discoverability.

## Step 1: Identify Notes to Process

For a single file, read it with the CLI:
```bash
obsidian read file="Note Name"
```

For a folder, list files:
```bash
obsidian files folder="folder/path"
```

Check existing properties:
```bash
obsidian properties file="Note Name"
```

## Step 2: Analyze Note Content

For each note, examine:
- Main topics and themes
- Note type (meeting, daily, reference, project)
- Key entities (people, projects, dates)
- Existing properties (preserve valid ones)
- Title quality (add/improve if needed)

## Step 3: Apply Properties

Use the CLI to set properties on each note:

```bash
obsidian property:set name="type" value="meeting" file="Note Name"
obsidian property:set name="date" value="2025-10-09" type=date file="Note Name"
obsidian property:set name="tags" value="meeting, project-name" type=list file="Note Name"
obsidian property:set name="project" value="Project Name" file="Note Name"
```

Fix deprecated formats:
- `tag` to `tags`
- `alias` to `aliases`
- `cssclass` to `cssclasses`

Use `property:remove` to clean up deprecated names after migrating values:
```bash
obsidian property:remove name="tag" file="Note Name"
```

## Standard Properties by Note Type

**Meeting Notes:** type, date, attendees, project, tags, action_items, status
**Daily Notes:** type=daily-note, date, tags=[daily], highlights
**Reference Notes:** type=reference, source, author, date_saved, tags, key_concepts
**Project Notes:** type=project, status, deadline, stakeholders, tags, priority

## Property Guidelines

### Naming Conventions
- Use lowercase with underscores: `date_created`, `action_items`
- Be consistent with existing vault patterns

### Value Types
- **Text**: Simple strings
- **List**: Comma-separated for the CLI `type=list`
- **Date**: ISO format YYYY-MM-DD with `type=date`
- **Number**: Use `type=number`
- **Checkbox**: Use `type=checkbox`

## Special Cases

### Untitled Notes
Generate title from:
1. First heading if it exists
2. First paragraph summary
3. Main topic discussed

### Bulk Processing
When processing folders:
- Maintain consistency across similar notes
- Use same property names for same concepts
- Report summary of changes made

### Existing Properties
- Preserve valid existing properties
- Update deprecated formats
- Merge new properties carefully
- Never delete without reason

Properties should enhance organization, not clutter. Only add what provides value for finding and connecting notes.
