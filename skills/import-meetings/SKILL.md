---
name: import-meetings
description: Pull meeting notes from Granola for a given date and create Obsidian notes using the vault's meeting template structure. Accepts a date (YYYY-MM-DD), "today", or "yesterday". Use when the user wants to import, pull, sync, or create meeting notes from Granola.
argument-hint: <date | today | yesterday>
---

# Import Meetings from Granola

Pull meetings from Granola for a specific date and create Obsidian notes following the vault's meeting note conventions.

## Input

The user provides a date argument: a literal date (YYYY-MM-DD), "today", or "yesterday".

- Resolve "today" and "yesterday" to YYYY-MM-DD before calling the Granola API.

## Step 1: Fetch Meetings from Granola

Use `mcp__granola__list_meetings` with a custom date range covering the target date:

```
time_range: "custom"
custom_start: "YYYY-MM-DD"
custom_end: "YYYY-MM-DD"  (same date, or next day for end-exclusive ranges)
```

If no meetings are found, tell the user and stop.

## Step 2: Get Meeting Details

For each meeting returned, call `mcp__granola__get_meetings` with the meeting IDs to get:
- Title
- Attendees
- AI-generated summary/notes
- Any private notes

## Step 3: Determine File Location

Suggest a file path in `Notes/Meetings/` based on the meeting title and attendees. Use your best guess based on existing vault structure. Present the proposed paths to the user for confirmation before creating files.

Guidelines for path guessing:
- Look for org/company cues in attendees or title to pick a subfolder
- Use the Obsidian CLI to check what folders exist:
  ```bash
  obsidian folders folder="Notes/Meetings"
  ```
- For recurring meetings (standups, retros, etc.), use `YYYY-MM-DD Title.md` naming
- For one-off meetings, use a descriptive title without date prefix
- When unsure, place directly in `Notes/Meetings/`

## Step 4: Create Notes

For each meeting, create an Obsidian note using the CLI:

```bash
obsidian create path="Notes/Meetings/[path].md" content="..." silent
```

### Frontmatter format

```yaml
---
category: "[[Meetings]]"
type:
date: YYYY-MM-DD
org:
loc:
people:
  - "[[Person Name]]"
topics:
  - topic-slug
tags:
  - meetings
---
```

Frontmatter rules:
- `date`: The meeting date in YYYY-MM-DD
- `people`: Each attendee as a wikilink `"[[Full Name]]"`. Omit the current user.
- `org`: Wikilink to the organization if identifiable, otherwise leave empty
- `type`: Wikilink to meeting type if identifiable (e.g., `"[[Standup]]"`, `"[[Retro]]"`)
- `topics`: Lowercase slugs derived from key subjects discussed
- `tags`: Always include `meetings`, add others based on content (e.g., org name, meeting type)
- `loc`: Meeting platform if known (Zoom, Teams, Google Meet, etc.)

### Body content

After the frontmatter, include the Granola AI summary/notes formatted as clean markdown. Use `###` headings to organize sections. Preserve the substance but clean up formatting.

At the end of the note, add a link back to the Granola note:

```markdown
---

Granola meeting notes: [link](granola-url)
```

## Step 5: Confirm

After creating notes, list what was created with paths and titles. Set properties using the CLI if any couldn't be included inline:

```bash
obsidian property:set name="topics" value="topic1, topic2" type=list path="Notes/Meetings/[path].md"
```

## Important

- Always present proposed file paths to the user before creating files
- Never overwrite existing notes without explicit confirmation
- If a note already exists at the proposed path, flag it and ask the user what to do
- Strip any PII or sensitive content that shouldn't live in the vault (credentials, tokens, etc.)
