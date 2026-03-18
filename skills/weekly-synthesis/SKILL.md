---
name: weekly-synthesis
description: Create a comprehensive synthesis of the week's work and thinking using the Obsidian CLI. Reads daily notes, gathers tasks and activity, identifies patterns, and produces a structured weekly summary note.
---

# Weekly Synthesis

Create a comprehensive synthesis of the week's work and thinking.

## Analysis Process

1. **Gather Week's Work**
   - Read each daily note from the past week (Monday through today):
     ```bash
     obsidian read path="Daily/YYYY-MM-DD.md"
     ```
   - Search for notes containing this week's dates:
     ```bash
     obsidian search query="YYYY-MM-DD" limit=30
     ```
   - Check tasks completed this week:
     ```bash
     obsidian tasks done
     ```
   - Check open tasks:
     ```bash
     obsidian tasks todo
     ```
   - Get recently opened files for activity context:
     ```bash
     obsidian recents
     ```

2. **Identify Patterns**
   - Recurring themes
   - Common challenges
   - Breakthrough moments
   - Energy patterns (what energized vs drained)

3. **Synthesize Learning**
   - Key insights that emerged
   - How thinking evolved
   - Connections discovered
   - Questions answered and raised

4. **Assess Progress**
   - Projects advanced
   - Areas maintained
   - Resources added

## Write the Synthesis

Create a new note for the synthesis:

```bash
obsidian create name="Weekly Synthesis YYYY-MM-DD" path="Notes/Weekly Synthesis YYYY-MM-DD.md" content="..." silent
```

## Output Format

```markdown
# Weekly Synthesis - Week of [Monday date]

## Week at a Glance
- Notes created: [X]
- Projects active: [List]
- Major accomplishments: [List]

## Key Themes

### Theme 1: [Name]
- Where it appeared: [contexts]
- Why it matters: [significance]
- Next actions: [what to do]

## Major Insights
1. [Insight with context]
2. [Insight with context]

## Progress by Project

### [Project Name]
- What advanced:
- What's blocked:
- Next week's focus:

## Questions Emerged
- [Question 1 - and why it matters]

## Energy Audit
- What gave energy:
- What drained energy:
- What to adjust:

## Connections Made
- [[Note A]] and [[Note B]]: [Why significant]

## Next Week's Intentions
1. [Primary focus]
2. [Secondary focus]
3. [Thing to explore]
```

## Follow-up Actions

- Archive completed projects
- Update project status
- Plan next week's focus
