# Brainstorming Skill Guide

A practical guide for understanding and using the Superpowers brainstorming workflow.

---

## What Is the Brainstorming Skill?

The brainstorming skill turns rough ideas into validated designs through **collaborative dialogue**. It's the entry point to the Superpowers workflow - ensuring you think before you code.

**Location:** `skills/brainstorming/SKILL.md`

---

## When It Activates

The skill triggers **automatically** before any creative work:
- "I want to build a task management app"
- "Let's add user authentication"
- "I have an idea for a new feature"

You can also **explicitly invoke it**:
```
/superpowers:brainstorm
```

---

## Activation Model

The skill is **activated once**, then Claude follows its process across multiple conversation turns:

```
Turn 1: User says "I want to build X"
        └── Claude invokes brainstorming skill (loaded into context)
        └── Claude starts following the process

Turn 2-N: Conversation continues
          └── Skill content is already in context
          └── Claude continues following the same process
          └── No re-invocation needed

Final turn: Design validated, saved to docs/plans/
            └── Claude asks "Ready to set up for implementation?"
            └── If yes → invokes writing-plans skill
```

**Key point:** Skills are loaded once and followed until complete - not re-activated every turn.

---

## The Brainstorming Process

### Phase 1: Understanding the Idea (Iterate Until Clear)

- Claude explores project context (files, docs, commits)
- Asks **ONE question at a time**
- Prefers multiple-choice when possible
- Keeps asking until purpose/constraints/success criteria are clear

### Phase 2: Exploring Approaches (Iterate on Options)

- Proposes 2-3 different approaches
- Explains trade-offs for each
- Leads with recommended option
- You discuss until one approach is selected

### Phase 3: Presenting Design (Iterate Per Section)

- Presents 200-300 word sections
- Asks "does this look right?" after each
- Goes back to clarify if something's off
- Covers: architecture, components, data flow, errors, testing

### Phase 4: Output

- Saves validated design to `docs/plans/YYYY-MM-DD-<topic>-design.md`
- Commits the design document to git

---

## Key Principles

| Principle | Description |
|-----------|-------------|
| **One question at a time** | Don't overwhelm with multiple questions |
| **Multiple choice preferred** | Easier to answer than open-ended |
| **YAGNI ruthlessly** | Remove unnecessary features from all designs |
| **Explore alternatives** | Always propose 2-3 approaches before settling |
| **Incremental validation** | Present design in sections, validate each |
| **Be flexible** | Go back and clarify when something doesn't make sense |

---

## The Skill Chain

Brainstorming is the first skill in a connected workflow:

```
brainstorming ──outputs──▶ Design Document (docs/plans/*-design.md)
      │
      │ "Ready to set up for implementation?"
      ▼
writing-plans ──outputs──▶ Implementation Plan (docs/plans/*.md)
      │
      │ "Two execution options..."
      ▼
executing-plans  OR  subagent-driven-development
```

### Skill Transitions

| From | To | Trigger |
|------|----|---------|
| brainstorming | using-git-worktrees | "Ready to set up for implementation?" (user confirms) |
| using-git-worktrees | writing-plans | Worktree created and tests pass |
| writing-plans | executing-plans | User chooses "Parallel Session" |
| writing-plans | subagent-driven-development | User chooses "Subagent-Driven" |

---

## Design vs Plan: Key Differences

| Brainstorming Output | Writing-Plans Output |
|---------------------|---------------------|
| **Design document** | **Implementation plan** |
| What to build | How to build it |
| Architecture, components, data flow | Exact files, code snippets, test commands |
| High-level decisions | Bite-sized tasks (2-5 min each) |
| Iterative refinement | Executable steps |

---

## Why Separate Execution Skills?

Without an execution skill, Claude might:
- Try to implement everything at once
- Not stop for feedback
- Skip verification steps
- Not follow TDD properly

### Without executing-plans:
```
Claude: "Here's the plan with 12 tasks. Let me implement them all..."
        *writes 2000 lines of code*
        *introduces subtle bug in task 7*
        *keeps going*
        *tests fail at the end*
        *debugging nightmare*
```

### With executing-plans:
```
Claude: "I'll execute tasks 1-3, then check in."
        *implements 3 tasks*
        "Here's what I did. Ready for feedback."

You: "Task 2 looks wrong, the API changed"

Claude: "Got it, fixing task 2..."
```

---

## Execution Options

After writing-plans completes, you choose between:

| Option | How It Works | When to Use |
|--------|--------------|-------------|
| **executing-plans** | Batch execution (3 tasks), human checkpoints | When you want control between batches |
| **subagent-driven-development** | Fresh agent per task + 2-stage review | When you want faster autonomous execution |

### Subagent-Driven Development Details

1. **Fresh subagent per task** - No context pollution
2. **Two-stage review per task:**
   - Spec compliance review (does it match requirements?)
   - Code quality review (is it well-written?)
3. Review loops continue until both pass

---

## Example Conversation Flow

```
You: "I want to build something that helps me track my reading habits,
      but I'm not sure if it should be a CLI tool, a web app, or something else."

Claude: (activates brainstorming)
        "Let me understand what you're looking for. What's the main way
        you'd interact with this - would you be logging books while
        reading, or reviewing your history later, or both?"

You: "Mostly logging as I finish books, and occasionally looking at stats"

Claude: "Got it. For the logging part - would you want to capture just
        titles, or also notes/ratings/quotes?"

... (continues one question at a time) ...

Claude: "Here's the first section of the design - the data model..."
        (200-300 words)
        "Does this look right so far?"

You: "Yes, but I'd also want to track page count"

Claude: "Good point. Updated. Here's the next section - the CLI interface..."

... (continues section by section) ...

Claude: "Design complete. I've saved it to docs/plans/2026-01-01-reading-tracker-design.md
        Ready to set up for implementation?"

You: "Yes"

Claude: (invokes using-git-worktrees, then writing-plans)
```

---

## File Locations

| What | Where |
|------|-------|
| Design documents | `docs/plans/YYYY-MM-DD-<topic>-design.md` |
| Implementation plans | `docs/plans/YYYY-MM-DD-<feature>.md` |
| Git worktrees | `.worktrees/` or `~/.config/superpowers/worktrees/` |

---

## Quick Reference

| Phase | Skill | Turns | Output |
|-------|-------|-------|--------|
| Brainstorming | `brainstorming` | Multiple (until design done) | Design document |
| Workspace setup | `using-git-worktrees` | 1-2 | Isolated git worktree |
| Planning | `writing-plans` | 1-2 | Implementation plan |
| Execution | `executing-plans` or `subagent-driven-development` | Multiple | Working code |
| Completion | `finishing-a-development-branch` | 1-2 | Merged/PR'd work |

---

## Summary

1. **Brainstorming is iterative** - Stay in it until the design is solid
2. **One question at a time** - Claude guides you through refinement
3. **You control transitions** - Move to planning only when ready
4. **Skills chain together** - Each outputs what the next needs
5. **Execution has safeguards** - Batch processing prevents runaway implementation
