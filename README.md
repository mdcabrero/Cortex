# Cortex

Cortex is a skills library for Claude Code that provides structured workflows for software development - from brainstorming to implementation.

## How it works

It starts from the moment you fire up your coding agent. As soon as it sees that you're building something, it *doesn't* just jump into trying to write code. Instead, it steps back and asks you what you're really trying to do.

Once it's teased a spec out of the conversation, it shows it to you in chunks short enough to actually read and digest.

After you've signed off on the design, you can work through an implementation plan with clear checkpoints for review and feedback.

## Installation

### Claude Code (via Plugin Marketplace)

In Claude Code, register the marketplace first:

```bash
/plugin marketplace add [marketplace-url]
```

Then install the plugin:

```bash
/plugin install cortex
```

### Verify Installation

Check that commands appear:

```bash
/help
```

```
# Should see:
# /cortex:brainstorm - Interactive design refinement
# /cortex:execute-plan - Execute plan in batches
```

## The Basic Workflow

**Path A: Rough idea → Implementation**
1. **brainstorming** - Refines rough ideas through questions, explores alternatives, presents design in sections for validation
2. **executing-plans** - Executes in batches with human checkpoints

**Path B: Clear feature → Implementation**
1. **feature-builder** - Analyzes codebase (docs + code patterns), creates technical specification and implementation plan
2. **executing-plans** - Executes in batches with human checkpoints

## What's Inside

### Skills Library

**Development Workflow**
- **brainstorming** - Socratic design refinement for rough ideas
- **feature-builder** - Codebase-aware feature planning and specification
- **executing-plans** - Batch execution with checkpoints

**Code Quality**
- **code-smeller** - Analyze code for structural problems and scalability concerns
- **pattern-engineer** - Evaluate whether design patterns are appropriate for a problem

**Meta**
- **writing-skills** - Create new skills following best practices
- **using-cortex** - Introduction to the skills system

## Philosophy

- **Think before you code** - Brainstorm and plan first
- **Systematic over ad-hoc** - Process over guessing
- **Complexity reduction** - Simplicity as primary goal
- **Human checkpoints** - Review between execution batches
- **Problem-first patterns** - Only apply design patterns when they solve real problems

## Contributing

Skills live directly in this repository. To contribute:

1. Fork the repository
2. Create a branch for your skill
3. Follow the `writing-skills` skill for creating and testing new skills
4. Submit a PR

See `skills/writing-skills/SKILL.md` for the complete guide.

## Updating

Skills update automatically when you update the plugin:

```bash
/plugin update cortex
```

## License

MIT License - see LICENSE file for details
