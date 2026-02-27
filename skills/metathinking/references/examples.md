# Metathinking — Reference Examples

These examples demonstrate how the metathinking pipeline works across different domains. The critical pattern to internalize: a genuine frame-break changes the *kind* of solution, not its parameters.

---

## System Architecture

**Problem:** "How should we handle real-time notifications in our app?"

**Conventional search space:** WebSockets vs. Server-Sent Events vs. polling vs. push notifications — all variations of "the server pushes data to the client."

**Hidden assumption:** "The server must actively notify the client when something changes."

**Frame-break:** What if the client already has the information and just doesn't know it yet? A local-first architecture with CRDTs where both peers converge — no notification system at all, just eventual consistency. The "notification" is the data itself arriving through sync.

---

## Data Modeling

**Problem:** "How should we structure the permissions table for our multi-tenant SaaS?"

**Conventional search space:** RBAC vs. ABAC vs. ACLs vs. permission bitmasks — all variations of "permissions are stored as structured records that are checked at runtime."

**Hidden assumption:** "Permissions are data that must be queried."

**Frame-break:** What if permissions are *code* — compiled policy functions that return yes/no, versioned alongside the application, with no database table at all? OPA/Rego-style. The "permissions table" becomes a policy repository. You don't query permissions; you evaluate them.

---

## API Design

**Problem:** "Should our API use REST or GraphQL?"

**Conventional search space:** REST vs. GraphQL vs. gRPC vs. tRPC — all variations of "the client sends a request, the server sends a response."

**Hidden assumption:** "The client and server must communicate through request-response cycles."

**Frame-break:** What if the client never talks to the server directly? A shared replicated data layer (like Replicache or ElectricSQL) where the client writes to a local database and sync happens in the background. There is no "API" in the traditional sense — just a sync protocol. The client never waits for a response because it already has the data locally.

---

## Performance Optimization

**Problem:** "How do we speed up this slow database query that joins five tables?"

**Conventional search space:** Add indexes, denormalize, add a caching layer, rewrite the query, use materialized views — all variations of "make the existing operation faster."

**Hidden assumption:** "The query must exist."

**Frame-break:** What if you precompute the result at write time instead of read time? An event-driven projection that maintains the denormalized view as a read model, updated whenever the source data changes. The "query" becomes a single-key lookup because the join already happened when the data was written. The slow query doesn't get faster — it gets deleted.

---

## Testing Strategy

**Problem:** "How should we test this complex state machine with 12 states and 30+ transitions?"

**Conventional search space:** Unit tests for each transition, integration tests for common paths, state transition table tests — all variations of "write test cases that exercise the state machine."

**Hidden assumption:** "Tests must be hand-written scenarios that we enumerate."

**Frame-break:** What if the tests write themselves? Property-based testing (like fast-check or Hypothesis) that generates random sequences of events and asserts invariants: "no matter what sequence of actions occurs, the system never enters an invalid state." You define *properties* that must always hold, not *scenarios* that must pass. Coverage becomes exhaustive by construction rather than by enumeration.

---

## Developer Experience

**Problem:** "How should we document our internal API for other teams?"

**Conventional search space:** OpenAPI/Swagger docs, README files, Confluence pages, auto-generated reference docs — all variations of "write documentation that developers read."

**Hidden assumption:** "Documentation is a text artifact that humans consume."

**Frame-break:** What if the documentation is a running environment, not a document? A shared development sandbox with pre-configured API calls, seeded test data, and live responses — developers learn the API by *using* it in a real environment, not by reading about it. The "documentation" is an interactive playground that cannot go stale because it runs against the actual service.

---

## UI Design

**Problem:** "How should we organize the settings page? There are 40+ options across 6 categories."

**Conventional search space:** Tabbed interface vs. sidebar navigation vs. accordion sections vs. single scrollable page — all variations of "organize all settings into a browsable structure."

**Hidden assumption:** "Users need to see and access all settings."

**Frame-break:** What if most settings don't need a page at all? A command palette (Cmd+K) that surfaces settings contextually — users type what they want to change and get taken directly there. The "settings page" becomes a minimal page with only the 5 most-changed options, and everything else is accessed through search. The organizational problem disappears because you stopped organizing.

---

## Frontend Architecture

**Problem:** "Should we use Redux, Zustand, or Pinia for global state management?"

**Conventional search space:** Redux vs. Zustand vs. Pinia vs. Jotai vs. Valtio — all variations of "client-side global state store."

**Hidden assumption:** "This data needs to be in global state."

**Frame-break:** What if the data lives in the URL? Route params + query strings as the single source of truth, with components reading from the URL directly. State is shareable (copy the URL), persistent (survives refresh), and debuggable (visible in the address bar). No store library needed. The "state management problem" was actually a "the wrong data was being globalized" problem.

---

## Pattern Recognition Guide

Use these signals to distinguish genuine frame-breaks from surface variation:

| Surface Variation (same frame) | Genuine Frame-Break (new frame) |
|---|---|
| Different tool for the same job | Eliminating the job entirely |
| Different database vendor | No database at all |
| Different API protocol | No API at all |
| Different test framework | Different testing paradigm |
| Different state library | Different location for the state |
| Different notification transport | No notification system |
| Different organizational scheme | No organization needed |

The quickest test: if you can describe both options using the same sentence structure with only the noun changed ("use X instead of Y"), it's surface variation. If describing the alternative requires a fundamentally different sentence, it's a frame-break.