---
name: code-research
description: Use when researching library documentation, framework APIs, or system integrations. Triggers on "how to use X", version-specific implementations, or library feature lookups.
---

# Code Research

## Overview

Trust-first, version-accurate documentation retrieval using Context7. Never substitute general knowledge for verified documentation.

**Prerequisite:** Context7 MCP server installed (`resolve-library-id`, `query-docs` tools).

## When to Use

- Implementing library features or APIs
- Version-specific questions (e.g., "React Router v5")
- Unfamiliar library patterns

**When NOT to use:** General coding questions not tied to specific libraries.

## Quick Reference

| User Provides | Action |
|---------------|--------|
| Direct ID (`/vercel/next.js`) | Skip to Retrieval Phase |
| Library name only | Run Resolution Phase first |
| Vague request ("tell me about X") | Ask for specific topic BEFORE calling tools |

## Core Workflow

### 1. Input Analysis (Critical)

**Check for direct Context7 ID** (format: `/org/project` or `/org/project/version`):
- YES → Skip to Retrieval Phase (saves ~7k tokens)
- NO → Proceed to Resolution Phase

**Check for vague requests:**
- "Tell me about X" or "How does X work?" → Ask user for specific topic first

### 2. Resolution Phase

Call `resolve-library-id` with library name and user's query.

**Selection Logic (in priority order):**

| Criterion | Rule |
|-----------|------|
| Trust Score | Must be ≥0.5. If lower, ask user to confirm from list. |
| Version Match | Must support user's specified version. v5 ≠ v6. |
| Snippet Count | Prefer higher (more code examples). |

### 3. Retrieval Phase

Call `query-docs` with exact ID string from Resolution.

**Query specificity:** Never query for "general info". Use the specific problem:
- ❌ "Prisma overview"
- ✅ "Prisma many-to-many relations with explicit join table"

### 4. Synthesis & Output

**Context Header (required):**
```
> [!INFO] Source: {Library} (Trust: {Score}) | ID: {ID}
```

**Implementation Guide:** Concise steps verified against fetched docs.

**Code Snippets:** Must come from fetched documentation.

## Anti-Hallucination Protocol

**If docs don't contain the answer:**

> "The current documentation context for {Library} does not cover this specific topic."

**Do NOT:**
- Invent code patterns
- Supplement with "general knowledge"
- Extrapolate from unrelated examples

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Calling `resolve-library-id` when ID provided | Check for `/org/project` format first |
| Ignoring Trust Score | Always evaluate. <0.5 = ask user |
| Accepting wrong version | Verify version explicitly matches user's |
| Querying vague topics | Ask user to specify before calling tools |
| Falling back to training data | State gaps explicitly. Docs only. |

## Red Flags - STOP

- About to use "based on my knowledge" after tool failure
- Selecting library without checking Trust Score
- Version in docs doesn't match user's version
- Query is generic ("overview", "introduction")
