---
name: agent-summary
description: Log a summary of this Claude Code session to today's Obsidian daily note using the Obsidian CLI. Use when the user wants to capture what was accomplished in a session.
---

# Agent Summary

Log a summary of this Claude Code session to today's Obsidian Daily Note using the Obsidian CLI.

## Instructions

1. **Identify Context**
   - Determine the project name from the current working directory (use the folder name)
   - Get the current time in HH:MM format
   - Get today's date in YYYY-MM-DD format

2. **Generate Summary**
   - Review the conversation history for this session
   - Identify: files modified, features implemented, bugs fixed, decisions made
   - Note any blockers or open questions
   - Keep it concise: 1-3 bullet points

3. **Write to Daily Note**
   - First check if today's daily note exists:
     ```bash
     obsidian daily:read
     ```
   - If it does not exist, create it from the daily note template:
     ```bash
     obsidian daily
     ```
   - Append the summary:
     ```bash
     obsidian daily:append content="### project-name (HH:MM)\n- Completed: ...\n- Modified: ...\n- Open: ..."
     ```

4. **Format**
   Use this format for entries:
   ```
   ### project-name (HH:MM)
   - Completed: [what was done]
   - Modified: [key files touched]
   - Open: [blockers or next steps, if any]
   ```

## Example Output

```markdown
### my-project (14:32)
- Completed: Fixed authentication redirect loop in login flow
- Modified: src/auth/callback.ts, src/middleware/session.ts
- Open: Need to add unit tests for edge cases
```

## Important

- Use `\n` for newlines in the `content` parameter
- Don't include sensitive information (API keys, credentials, internal URLs)
