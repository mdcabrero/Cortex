---
name: feature-builder
description: Use when adding a new feature to an existing application. Analyzes codebase documentation and code patterns to create a technical specification and implementation plan.
---

# Feature Builder

## Overview

Design and plan individual features for existing applications by deeply understanding the codebase first. Produces a combined technical specification and implementation plan ready for execution.

## When to Use

- Adding a new feature to an existing codebase
- User knows what feature they want (idea is clear)
- Need to understand how feature fits into existing architecture
- Want a structured plan before implementation

## When NOT to Use

- **Exploring rough ideas** - Use `cortex:brainstorming` first
- **Already have a plan** - Use `cortex:executing-plans` directly
- **Improving existing code quality** - Use `cortex:code-smeller`
- **Starting a brand new project** - Use `cortex:brainstorming` for initial design

## The Process

### Phase 1: Codebase Discovery

Before designing anything, understand what exists.

**Documentation review:**
- Read README.md for project overview
- Check /docs folder for architecture docs, API specs, guides
- Review any existing design documents

**Code exploration:**
- Identify the application architecture (monolith, microservices, modules)
- Map existing features and their locations
- Note conventions: naming, file structure, folder organization
- Understand the tech stack and dependencies
- Review testing patterns (unit, integration, e2e)

**Present findings:**
- Summarize the codebase structure in 100-200 words
- Ask user to confirm understanding before proceeding

### Phase 2: Feature Design

Define what the feature does and how it fits.

**Scope definition:**
- What is IN scope for this feature
- What is explicitly OUT of scope
- Dependencies on other features (if any)

**Component design:**
- List components to create or modify
- For each component: purpose, responsibility, interfaces
- Data models and schema changes (if applicable)
- API contracts (if applicable)

**Edge cases:**
- Error scenarios and handling
- Boundary conditions
- User experience considerations

**Present design:**
- Break into sections of 200-300 words
- Ask for validation after each section
- Be ready to revise based on feedback

### Phase 3: Integration Mapping

Identify how the feature connects to existing code.

**Integration points:**
- Which existing files/modules need modification
- Which are new files to create
- Database migrations required
- Configuration changes needed

**Compatibility:**
- Backward compatibility considerations
- Breaking changes (if any)
- Feature flags needed

**Testing requirements:**
- What needs unit tests
- Integration test scenarios
- Manual testing checklist

### Phase 4: Implementation Planning

Create an actionable plan for `cortex:executing-plans`.

**Task breakdown:**
- Break into discrete, independent tasks where possible
- Order by dependency (what must come first)
- Each task should be completable in one sitting

**For each task, specify:**
- Files to create or modify
- What exactly to implement
- How to verify it works (acceptance criteria)

**Group tasks into batches:**
- Batch 1: Foundation (models, schemas, core logic)
- Batch 2: Features (main functionality)
- Batch 3: Integration (connecting pieces)
- Batch 4: Polish (error handling, edge cases, tests)

## Key Principles

- **Codebase-first** - Let existing patterns guide your design
- **One feature, complete** - Better to finish one than start many
- **Explicit boundaries** - Always define in-scope vs out-of-scope
- **Verifiable tasks** - Every task needs "how to confirm it works"
- **Integration awareness** - Know what existing code you're touching
- **Match conventions** - Follow the project's existing style

## Output Format

Write the final specification and plan to `docs/plans/YYYY-MM-DD-<feature>-spec.md`:

```markdown
# Feature: [Feature Name]

## Technical Specification

### Overview
[1-2 paragraph description of what the feature does and why]

### Scope
- **In scope:** [What this feature includes]
- **Out of scope:** [What this feature does NOT include]

### Architecture
[How this feature fits into the existing codebase - diagram if helpful]

### Components
| Component | Type | Purpose |
|-----------|------|---------|
| [Name] | new/modified | [What it does] |

### Data Model
[Schema changes, new models, relationships]

### API Design
[Endpoints, request/response contracts - if applicable]

### Integration Points
[Where this connects to existing code, what gets modified]

---

## Implementation Plan

### Prerequisites
- [ ] [Any setup needed before starting]

### Batch 1: Foundation
#### Task 1.1: [Task Name]
- **Files:** [paths]
- **Do:** [what to implement]
- **Verify:** [how to confirm it works]

### Batch 2: Features
#### Task 2.1: [Task Name]
...

### Batch 3: Integration
...

### Batch 4: Polish
...

### Testing Strategy
- Unit tests: [what to cover]
- Integration tests: [scenarios]
- Manual testing: [checklist]

### Rollout Notes
[Feature flags, migrations, deployment considerations]
```

## Integration with Other Skills

| Skill | Relationship |
|-------|--------------|
| `cortex:brainstorming` | Use first if idea needs exploration |
| `cortex:executing-plans` | Use after to implement the plan |
| `cortex:code-smeller` | Can inform design by identifying existing issues |
| `cortex:pattern-engineer` | Can help with architecture decisions |

## Anti-Patterns

**Skipping codebase analysis**
Don't design features without understanding the existing code. You'll create inconsistent implementations.

**Over-scoping**
Feature Builder is for ONE feature. If scope creeps into multiple features, stop and break it down.

**Ignoring existing patterns**
If the codebase uses a certain pattern (e.g., repository pattern, specific folder structure), match it. Don't introduce new patterns without good reason.

**Premature optimization**
Focus on making it work correctly first. Performance optimization comes later unless it's a core requirement.

**Missing verification steps**
Every task MUST have a "how to verify" step. "It compiles" is not sufficient - describe what behavior to check.

**Designing in isolation**
Always present the design to the user in sections and get validation. Don't write a 1000-word spec and drop it all at once.
