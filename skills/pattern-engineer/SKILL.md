---
name: pattern-engineer
description: Studies implementation plans and code to consider whether design patterns could improve structure, communication, or scalability. Use after Code Smeller identifies issues, or when planning new features. Encourages critical evaluation, not reflexive pattern application.
---

# Pattern Engineer

Evaluate whether design patterns are appropriate for a given problem. Focus on critical analysis, not pattern promotion.

## When to Use

- After Code Smeller identifies structural issues
- When planning implementation of new features
- "Should I use a pattern here?"
- "Which pattern fits this problem?"
- Reviewing implementation plans for architectural considerations

## Core Principle

**Problem-first, not pattern-first.** A pattern is only valuable if:
1. A real problem exists
2. The pattern actually solves it
3. The solution's benefits outweigh its costs

## Evaluation Framework

### 1. Problem Validation

Before considering any pattern, establish:

**Is there actually a problem?**
- What specific pain point are we addressing?
- Is this a current problem or an anticipated one?
- How severe is it? (blocking, friction, or minor annoyance)

**What's the cost of doing nothing?**
- Can we live with the current approach?
- Will this get worse over time, or is it stable?
- Are we solving a problem that doesn't exist yet?

### 2. Problem Classification

Map the problem to a category:

**Creation problems** → Creational patterns
- Object construction is complex or scattered
- Need flexibility in what gets created
- Dependencies are hard-coded

**Structure problems** → Structural patterns
- Interfaces don't match
- Need to compose objects in new ways
- Want to add behavior without changing classes

**Behavior problems** → Behavioral patterns
- Algorithms need to vary
- Objects need to communicate without tight coupling
- State-dependent behavior is complex

## Pattern Quick Reference

When evaluating solutions, consider all patterns in the relevant category:

### Creational Patterns
- **Singleton**: Ensures exactly one instance exists with global access. Use when multiple instances would cause bugs or resource conflicts.
- **Factory Method**: Lets subclasses decide which class to instantiate. Use when creation logic varies by context and callers shouldn't know concrete types.
- **Abstract Factory**: Creates families of related objects without specifying concrete classes. Use when products must be used together consistently.
- **Builder**: Constructs complex objects step-by-step. Use when objects have many optional parameters or require multi-step initialization.
- **Prototype**: Creates new objects by cloning existing ones. Use when object creation is expensive or configuration is determined at runtime.

### Structural Patterns
- **Adapter**: Converts one interface to another that clients expect. Use when integrating incompatible code or third-party libraries.
- **Bridge**: Separates abstraction from implementation so both can vary. Use to avoid class explosion from combining two hierarchies.
- **Composite**: Treats individual objects and compositions uniformly. Use for tree structures where operations apply to both leaves and branches.
- **Decorator**: Adds responsibilities to objects dynamically. Use to extend behavior without subclassing, especially for stackable enhancements.
- **Facade**: Provides simplified interface to a complex subsystem. Use to hide complexity and provide a clean entry point.
- **Flyweight**: Shares common state among many similar objects. Use when memory is constrained and objects differ only in extrinsic state.
- **Proxy**: Controls access to another object. Use for lazy loading, access control, logging, or remote access.

### Behavioral Patterns
- **Chain of Responsibility**: Passes requests along a chain of handlers. Use when multiple objects might handle a request and the handler isn't known upfront.
- **Command**: Encapsulates requests as objects. Use for queuing, logging, undo/redo, or decoupling invoker from executor.
- **Interpreter**: Defines grammar representation and interpreter. Use for simple languages or expression parsing (rarely needed).
- **Iterator**: Provides sequential access without exposing internals. Use for uniform traversal of different collection types.
- **Mediator**: Centralizes complex communication between objects. Use when many objects interact in well-defined but complex ways.
- **Memento**: Captures and restores object state without exposing internals. Use for undo/redo, snapshots, or checkpoints.
- **Observer**: Notifies dependents of state changes. Use for event systems, data binding, or one-to-many dependencies.
- **State**: Alters behavior when internal state changes. Use when object behavior varies significantly by state.
- **Strategy**: Encapsulates interchangeable algorithms. Use when algorithm varies and should be selected at runtime.
- **Template Method**: Defines algorithm skeleton with customizable steps. Use when algorithm structure is fixed but steps vary.
- **Visitor**: Adds operations to object structures without changing them. Use when adding many operations to stable class hierarchies.

## Evaluation Framework

### 3. Pattern Fit Analysis

For each candidate pattern, evaluate:

**Fit score:**
- Does the pattern's intent match our problem? (not just superficially similar)
- Do we have the pattern's preconditions? (e.g., do we actually have families of products for Abstract Factory?)
- Would the pattern's structure work in our context?

**Disqualifiers:**
- Pattern solves a different problem than we have
- We'd be forcing our problem into the pattern's shape
- Only one instance of the problem exists (pattern overhead not justified)

### 4. Trade-off Evaluation

Every pattern has costs. Be explicit:

**Benefits to quantify:**
- What specific flexibility do we gain?
- How much duplication is eliminated?
- What coupling is removed?

**Costs to quantify:**
- How many new classes/interfaces?
- How much indirection is added?
- What's the learning curve for the team?
- How does it affect debugging and tracing?

**The test:** Can you articulate both sides clearly? If you can only see benefits, you haven't analyzed deeply enough.

### 5. Integration Impact

Consider the ripple effects:

- How much existing code must change?
- What new dependencies are introduced?
- How does this affect testing? (more mocks needed? harder to set up?)
- Does this align with existing patterns in the codebase?
- Will this make the codebase more or less consistent?

## Anti-Over-Engineering Checklist

Before recommending any pattern, answer honestly:

- [ ] **Is the problem real and current?** Not hypothetical or anticipated
- [ ] **Have I seen this problem cause actual pain?** Not just theoretical concern
- [ ] **Is this the simplest solution?** Could a function, conditional, or simple refactor work?
- [ ] **Will this be used more than once?** Patterns for one-off cases are waste
- [ ] **Does the team know this pattern?** Unknown patterns have hidden costs
- [ ] **Am I pattern-matching the pattern?** Seeing patterns everywhere because I just learned them?

If you can't check all boxes, **don't recommend the pattern**.

## Decision Framework

### Recommend a pattern when:

- Clear, recurring problem exists
- Pattern directly addresses the problem's root cause
- Benefits significantly outweigh costs
- Simpler solutions have been considered and rejected
- Team can maintain it

### Avoid patterns when:

- Problem is speculative ("we might need this")
- Single occurrence (no recurring benefit)
- Simpler solution works (function, conditional, direct code)
- Team unfamiliar and no time to learn
- Codebase doesn't use patterns consistently
- You're adding flexibility that won't be used

### Consider alternatives first:

- **Before Factory:** Can you just use a constructor?
- **Before Strategy:** Can you just use a function parameter?
- **Before Observer:** Can you just call the method directly?
- **Before Singleton:** Can you use dependency injection?
- **Before any pattern:** Can you delete the code instead?

## Output Format

```markdown
## Pattern Evaluation: [Problem Description]

### Problem Assessment

**Problem:** [Specific issue being addressed]
**Severity:** [Critical / High / Medium / Low]
**Evidence:** [Where this problem manifests]
**Cost of inaction:** [What happens if we do nothing]

### Analysis

**Problem category:** [Creation / Structure / Behavior]
**Candidate patterns:** [List with brief rationale for each]

### Recommendation

**Recommended approach:** [Pattern name OR "No pattern needed"]

**If pattern recommended:**
- Why this pattern fits: [Specific alignment with problem]
- Key trade-offs: [What we gain vs. what we pay]
- Integration impact: [How this affects existing code]
- Implementation notes: [Any context-specific considerations]

**If no pattern recommended:**
- Why patterns don't fit: [Specific reasons]
- Alternative approach: [What to do instead]
- Conditions that would change this: [When to reconsider]

### Anti-Over-Engineering Check

- [x] Problem is real and current
- [x] Simplest solution considered
- [x] Benefits outweigh costs
- [x] Team can maintain this
```

## What This Skill Does NOT Do

- **Prescribe patterns by default** - Patterns are tools, not goals
- **Ignore simpler solutions** - Always consider non-pattern approaches first
- **Assume patterns are better** - Sometimes direct code is the right answer
- **Recommend based on pattern knowledge** - "I know this pattern" isn't a reason to use it

## Critical Thinking Prompts

Ask yourself before any recommendation:

1. **Would I recommend this if I'd never heard of design patterns?** Or am I seeing patterns because I know them?
2. **What would a senior engineer who hates over-engineering say?** Channel the skeptic.
3. **If this pattern didn't exist, how would I solve this?** Sometimes that solution is better.
4. **Am I solving today's problem or tomorrow's?** Solve today's. Tomorrow might never come.
5. **Can I explain the benefit in one sentence without jargon?** If not, the benefit might not be real.

## Integration with Other Skills

Pattern Engineer works with other skills in the ecosystem:

- **Code Smeller → Pattern Engineer**: Code Smeller identifies problems; Pattern Engineer evaluates pattern-based solutions
- **Pattern Quick Reference**: See section above for all 23 GoF patterns with brief descriptions
