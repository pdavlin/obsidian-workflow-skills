---
name: daily-review
description: Conduct an end-of-day review using the Obsidian CLI to capture progress, insights, and set up tomorrow's priorities. Use when the user wants to review their day.
---

# Daily Review

Conduct an end-of-day review to capture progress and set up tomorrow.

## Review Process

1. **Read Today's Daily Note**
   ```bash
   obsidian daily:read
   ```

2. **Find Today's Activity**
   - Search for notes modified or created today:
     ```bash
     obsidian search query="YYYY-MM-DD" limit=20
     ```
   - Check tasks completed today:
     ```bash
     obsidian tasks daily done
     ```
   - Check tasks still open:
     ```bash
     obsidian tasks daily todo
     ```

3. **Progress Assessment**
   - What was accomplished?
   - What got stuck or blocked?
   - What unexpected discoveries emerged?

4. **Capture Insights**
   - Key learnings from today
   - New connections discovered
   - Questions that arose

5. **Tomorrow's Setup**
   - Top 3 priorities
   - Open loops to close
   - Questions to explore

## Write the Review

Append the review to today's daily note:

```bash
obsidian daily:append content="## Daily Review\n\n### Accomplished\n- ...\n\n### Progress Made\n- ...\n\n### Blocked/Stuck\n- ...\n\n### Tomorrow's Focus\n1. ...\n2. ...\n3. ..."
```

## Output Format

```markdown
## Daily Review

### Accomplished
- [Completed item 1]
- [Completed item 2]

### Progress Made
- [Project/Area]: [What moved forward]

### Insights
- [Key realization or connection]

### Blocked/Stuck
- [What didn't progress and why]

### Discovered Questions
- [New question that emerged]

### Tomorrow's Focus
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]

### Open Loops
- [ ] [Thing to remember]
- [ ] [Person to follow up with]
```
