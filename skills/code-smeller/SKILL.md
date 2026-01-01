---
name: code-smeller
description: Analyzes codebases and scripts to detect structural problems, scalability concerns, and non-obvious architectural issues. Use when asked to review code quality, identify potential problems, or assess code health. Produces actionable analysis, not pattern recommendations.
---

# Code Smeller

Analyze code for structural problems and scalability concerns. Focus on identifying issues, not prescribing solutions.

## When to Use

- Code review requests
- "What's wrong with this code?"
- "Is this code scalable?"
- "Review this architecture"
- Pre-refactoring assessment

## Analysis Framework

### 1. Scope the Analysis

Before diving in, clarify:
- What are we analyzing? (single file, module, entire codebase)
- What's the context? (new code, legacy, prototype, production)
- What matters most? (performance, maintainability, extensibility)

### 2. Problem Categories

Examine code through these lenses:

**Coupling Issues** (how things depend on each other)
- Classes that know too much about other classes' internals
- Changes that ripple across many files
- Circular dependencies
- Hard-coded references to concrete implementations

**Cohesion Issues** (how things belong together)
- Classes with multiple unrelated responsibilities
- Methods that do too many things
- Data and behavior that should be together but aren't
- Utility classes that are dumping grounds

**Complexity Issues** (how hard things are to understand)
- Deeply nested conditionals
- Long methods or classes
- Complex control flow
- Magic numbers and unclear naming

**Extensibility Issues** (how hard things are to change)
- Modification required for each new variant
- Switch statements on type
- Inheritance hierarchies that need constant updating
- Behavior changes requiring source code changes

**Creation Issues** (how objects come into existence)
- Construction logic scattered across codebase
- Hard-coded dependency instantiation
- Complex initialization sequences
- Unclear ownership of object lifecycle

### 3. Scalability Concerns

Look for issues that compound as the system grows:

- Single points that everything depends on
- Linear search through growing collections
- State that must be synchronized across components
- Operations that don't compose or parallelize
- Assumptions that break with more users/data/features

### 4. Severity Assessment

| Severity | Criteria |
|----------|----------|
| **Critical** | Blocks development, causes bugs, or prevents scaling |
| **High** | Significant maintenance burden, frequent pain point |
| **Medium** | Noticeable friction, should address eventually |
| **Low** | Minor improvement, fix opportunistically |

## Analysis Process

1. **Read the code** - Understand what it does before judging
2. **Map dependencies** - What depends on what?
3. **Identify responsibilities** - What is each unit doing?
4. **Trace change paths** - What happens when requirements change?
5. **Find patterns** - Are issues isolated or systemic?

## Key Questions to Ask

**About structure:**
- If I need to add a new feature, how many files change?
- Can I test this unit in isolation?
- Can I understand this code without reading everything else?

**About behavior:**
- Where does this behavior live? Is it scattered?
- What happens when this state changes?
- Are there implicit contracts or assumptions?

**About growth:**
- What breaks if we have 10x more [users/data/features]?
- What are we assuming won't change?
- Where are the bottlenecks?

## Output Format

```markdown
## Code Analysis: [Target Description]

**Scope:** [What was analyzed]
**Context:** [Relevant background]

### Critical Issues

[List critical issues first—these block progress or cause real problems]

- **[Issue Name]** | Severity: Critical
  - Location: [file:line or general area]
  - Problem: [What's wrong]
  - Impact: [Why it matters]
  - Evidence: [Specific code that demonstrates this]

### High-Priority Issues

[Issues that cause significant ongoing friction]

### Medium-Priority Issues

[Things to address when touching this code]

### Observations

[Patterns noticed, potential concerns that aren't issues yet, areas that warrant monitoring]

### Recommendations

[Prioritized list of what to address first]

1. [Most important action]
2. [Next action]
...
```

## What This Skill Does NOT Do

- **Prescribe specific patterns** - Identify problems, not solutions
- **Rewrite code** - Analyze, don't implement
- **Judge coding style** - Focus on structural issues, not formatting
- **Assume intent** - Ask if unclear whether something is intentional

## Critical Thinking Prompts

Before flagging an issue, consider:

1. **Is this actually a problem?** Or just different from how I'd do it?
2. **What's the context?** Prototype code has different standards than production.
3. **What's the cost of fixing it?** Is the cure worse than the disease?
4. **Is this a pattern or a one-off?** Systemic issues matter more than isolated quirks.
5. **Am I seeing the full picture?** Is there context I'm missing?

## Integration with Other Skills

Code Smeller identifies problems. Other skills help with solutions:

- **Pattern Engineer** - Considers whether patterns might help and which are the ideal patterns to be applied
- **Pattern Detector** - Identifies existing patterns that might explain structure
