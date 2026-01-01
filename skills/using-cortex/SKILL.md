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
| `cortex:brainstorming` | Before any creative work - designing features, building components, adding functionality |
| `cortex:executing-plans` | When you have a written implementation plan to execute with review checkpoints |
| `cortex:writing-skills` | When creating, editing, or testing new skills for Claude Code |
| `cortex:code-smeller` | When reviewing code quality, identifying structural problems, or assessing code health |
| `cortex:pattern-engineer` | After Code Smeller identifies issues, or when planning new features and considering design patterns |

## Skill Categories

**Development Workflow:**
- brainstorming → executing-plans

**Code Quality:**
- code-smeller → pattern-engineer

**Meta:**
- writing-skills

## The Core Workflow

1. **Brainstorm** - Refine ideas through dialogue, explore approaches, validate design
2. **Plan** - Break work into bite-sized tasks with verification steps
3. **Execute** - Implement in batches with human checkpoints

## How Skills Work

- Skills load on-demand when their description matches your task
- You can explicitly invoke skills using the Skill tool
- Each skill provides a structured process to follow

## Quick Start

Just describe what you want to build. Cortex will activate the appropriate skill automatically.
