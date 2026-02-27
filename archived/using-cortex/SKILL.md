---
name: using-cortex
description: Use at the start of any conversation to understand Cortex capabilities and available skills
---

# Using Cortex

## Overview

Cortex provides a structured workflow for software development with Claude Code. It guides you from idea to implementation through proven patterns.

## Available Skills

| Skill | When to Use |
|-------|-------------|
| `cortex:brainstorming` | Before any creative work - exploring rough ideas, designing features, building components |
| `cortex:feature-builder` | When adding a new feature to an existing codebase - analyzes docs and code patterns to create a spec and implementation plan |
| `cortex:executing-plans` | When you have a written implementation plan to execute with review checkpoints |
| `cortex:writing-skills` | When creating, editing, or testing new skills for Claude Code |
| `cortex:code-smeller` | When reviewing code quality, identifying structural problems, or assessing code health |
| `cortex:pattern-engineer` | After Code Smeller identifies issues, or when planning new features and considering design patterns |

## Skill Categories

**Development Workflow:**
- brainstorming → executing-plans (for rough ideas)
- feature-builder → executing-plans (for clear feature requests)

**Code Quality:**
- code-smeller → pattern-engineer

**Meta:**
- writing-skills

## The Core Workflow

**Path A: Rough idea → Implementation**
1. **Brainstorm** - Refine rough ideas through dialogue, explore approaches, validate design
2. **Execute** - Implement the plan in batches with human checkpoints

**Path B: Clear feature → Implementation**
1. **Feature Build** - Analyze codebase, create technical spec and implementation plan
2. **Execute** - Implement the plan in batches with human checkpoints

## How Skills Work

- Skills load on-demand when their description matches your task
- You can explicitly invoke skills using the Skill tool
- Each skill provides a structured process to follow

## Quick Start

Just describe what you want to build. Cortex will activate the appropriate skill automatically.
