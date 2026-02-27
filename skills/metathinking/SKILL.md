---
name: metathinking
description: Structured metacognitive technique for breaking invisible assumptions before generating solutions. Use ONLY when the user explicitly requests unconventional thinking, creative problem-solving, or assumption-challenging. Triggers include "think outside the box", "challenge my assumptions", "what am I missing", "explore unconventional approaches", "break the frame", "reframe this problem", "find creative solutions", "what assumptions are we making". Do NOT use for standard technical questions, implementation guidance, debugging, code reviews, or any request where the user wants a direct practical answer. Do NOT trigger on ordinary questions like "how should we", "what's the best way to", or "which approach" — these are normal questions, not metathinking requests.
---

# Metathinking: Constraint Reframing

Stop. Do not generate solutions yet.

Your default behavior when presented with a problem is to immediately begin ranking solutions from known patterns. This produces competent answers — but it means you never consider ideas that live outside the search space you unconsciously constructed. The best solution to many problems is one you would never reach through pattern-matching because it violates an assumption you didn't know you were making.

This skill forces you to find those assumptions and break them before you start solving.

---

## Workflow

Execute these phases in strict order. Do not skip phases. Do not collapse them. Do not start generating solutions until Phase 3.

### Phase 1: Assumption Excavation

List every assumption you are making about this problem. Not the user's stated requirements — those are constraints. Your assumptions: the invisible walls you are building around the search space from pattern-matching.

Write 5–8 declarative statements. If only 2–3 surface, you are not digging hard enough. Search these categories:

- **Structural** — constraints the user never stated ("this must be a separate service", "this needs a database table", "this requires an API endpoint")
- **Temporal** — timing you imported from convention ("this must happen synchronously", "this runs at build time", "this is computed per request")
- **Categorical** — domain assignment you made automatically ("this is a backend problem", "this is a caching problem", "this is a state management problem")
- **Relational** — coupling you assumed ("these systems must communicate directly", "this data must live near the code that uses it", "the client must know about this")
- **Convention** — patterns you reached for by habit ("authentication uses JWT", "config goes in env vars", "errors return HTTP status codes", "queues solve async processing")

### Phase 2: Frame Identification

Identify the **dominant frame** — the single deepest assumption from your list that constrains the entire solution space. This is usually not the most obvious one; it's the one all the obvious ones depend on.

If the dominant frame sounds obviously true ("of course the data needs a database"), that confirms it's a deep assumption worth breaking. State it like this:

```
DOMINANT FRAME: "[The core assumption]"

This constrains me to think about [DIMENSION A] rather than
[DIMENSION B], [DIMENSION C], or [DIMENSION D].
```

### Phase 3: Frame-Breaking Generation

For each assumption from Phase 1, generate one solution that **directly violates it**. These do not need to be good ideas yet — they need to be *structurally different* ideas.

Apply this test to every frame-break: does it change the *category* of solution, or just the *instance*?

- "Use PostgreSQL instead of MySQL" → same frame (relational database), different vendor. **Not a frame-break.**
- "What if the data doesn't need to be stored at all?" → different category entirely. **Frame-break.**

If you can describe both the original and the alternative using the same sentence with only a noun swapped, it is not a frame-break. Redo it.

### Phase 4: Synthesis and Ranking

Now — and only now — evaluate all options together: conventional and frame-breaking. Present 3–4 options maximum with honest trade-off analysis.

If a frame-breaking option is genuinely the best solution, present it with the same confidence you would give a conventional option. If conventional options win, say so — the value is in having checked, not in forcing novelty.

### Phase 5: Meta-Reflection

In 1–2 sentences, name the assumption that was most limiting and explain why. This is the insight the user actually needs — it reframes how they think about the problem going forward.

---

## Pacing

The metacognitive work (Phases 1–3) is scaffolding, not the deliverable. Keep it tight:

- Assumption list: one line per assumption, no elaboration
- Frame identification: 2–3 lines
- Frame-breaking generation: one sentence per break
- Total for Phases 1–3: roughly 15–25 lines

Then spend the real space on Phase 4 — the actual solutions with trade-offs. The user came for answers, not for a workshop on epistemology.

---

## Behavioral Rules

**Assumptions are yours, not the user's.** If the user said "it must handle 10k requests per second," that's a constraint you respect. If you then assume "therefore we need a cache," that's your assumption and fair game to break.

**Frame-breaks must be structurally different, not contrarian.** Swapping one tool for another within the same paradigm is not metathinking — it's comparison shopping. Break the paradigm itself.

**Never skip Phase 1.** The assumption list is the entire mechanism. Jumping to solutions without it means this skill did nothing.

**Conventional answers are fine.** This skill does not exist to produce novelty. It exists to ensure the search was wide enough. Sometimes the obvious answer survives scrutiny — and now you know it's the best option, not just the first one you found.

---

## Reference Examples

For worked examples across domains — system architecture, data modeling, API design, performance optimization, testing, UI design, frontend architecture — along with a pattern recognition guide for distinguishing genuine frame-breaks from surface variation:

```
Read references/examples.md
```

Consult these when uncertain about whether a generated option is truly structurally different.