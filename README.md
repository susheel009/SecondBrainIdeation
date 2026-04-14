# Second Brain — Personal Decision-Support Agent

> *"The pain comes from not one single area but the fact I have to think of such critical ideas/decisions in parallel."*

A narrow, personal-context overnight research agent that decomposes high-stakes life decisions into answerable sub-questions, researches each thread against your actual situation, and hands you back a two-page synthesized answer with a full audit trail.

---

## The Problem

Big life decisions don't arrive one at a time. Immigration paperwork, marriage savings, career pivots, and a cracked car bumper all sit in your head simultaneously — each one a parent question that fans out into a dozen sub-questions the moment you look directly at it.

Take something as simple as *"How do I save for my wedding next year?"* It immediately becomes:

- How much do I need to save?
- What are my current expenses?
- What are typical Indian wedding costs?
- What are my parents' expectations?
- How much gold do I need to buy?
- When can her brother and sister take vacation?
- How do all of these constraints interact?

You can ask Claude this question. You'll get a good generic answer. But it doesn't know your income, your immigration status, your family's expectations, or that you're also juggling a PR application right now. So you're left doing the synthesis yourself — chasing threads across tabs, stitching notes together in your head, losing threads, procrastinating.

That's the gap this project fills.

---

## The Concept (v1)

**Narrow personal-context overnight research agent.**

You submit a big question. The system:

1. Reads your hand-curated personal context file (`context.md`)
2. Calls a frontier model to decompose the question into a tree of sub-questions with a reasoning plan
3. Works through each sub-question in an agent loop — using web search where needed, grounded in your actual situation throughout
4. Preserves all intermediate findings in a timestamped folder
5. Synthesizes everything into a 2-page summary you can act on

You wake up to a report. The audit trail is there if you want to dig.

### What makes this different

| Tool | What it does well | What it misses |
|---|---|---|
| Claude Projects / Custom GPTs | Holds static context | Doesn't decompose or run multi-step research autonomously |
| OpenAI / Gemini / Claude Deep Research | Decomposes and researches well | Stateless about you — doesn't know your income, family, timeline |
| Mem / Rewind / Personal.ai | Knows you | Doesn't reason deeply or run research agents |
| **This** | Personal context + autonomous decomposition + research | — |

---

## v1 Scope

### Must-haves
- **Hand-curated context file** — Markdown, 2-3 pages, user-maintained. No RAG, no vector DB, no extraction pipeline. You write it; the model reads it.
- **Question decomposition** — Frontier model takes your question + context, emits a sub-question tree with a reasoning plan.
- **Overnight research loop** — Agent works through sub-questions, calls web search, preserves intermediate findings.
- **Synthesis pass** — One final model call reads all findings + context, produces the 2-page summary.
- **Audit trail** — Intermediate answers live in a folder you can open later.
- **Cost-aware model routing** — Cheap model (Haiku/mini class) for simple sub-queries; frontier for decomposition and synthesis. Keeps runs under $4 and monthly spend under $50.
- **Text interface only** — Terminal, CLI, or dead-simple local web UI.

### Explicitly not v1
Multi-model critique, automatic memory extraction, vector RAG, voice interface, mobile app, tool suite (finance/health/calendar), beta to friends, short/conversational mode, autonomous world actions.

---

## Decisions Made

| Question | Decision | Rationale |
|---|---|---|
| Language | Python | Velocity over familiarity; learning value is a stated success criterion |
| Agent framework | Hand-rolled loop | Learning value; revisit if pain emerges |
| Memory approach | Curated markdown | Gets 70-80% of personalization at 5% of RAG complexity |
| Storage | Local (SQLite / flat file) | Zero cost, no PIPEDA/GDPR surface, simpler |
| Latency | Overnight only | Short mode dropped; quick questions go to Claude.ai directly |
| Multi-model council | Deferred indefinitely | Evidence says single strong model + self-critique matches; real value came from human iteration, not models judging each other |

---

## Validation Plan

Before shipping anything, one week inside Claude Projects with a hand-written `context.md` — running the same questions the system will be evaluated on:

1. Marriage savings strategy
2. Canadian PR: CEC vs PNP
3. One more TBD high-stakes question

These establish the baseline the custom build must beat. Without this, there's no way to know if building is worth it over what's already paid for.

**Validation test:** *Did the reports help me think better about these decisions, even if I didn't fully act on them?* Yes = validated. No = stop and learn from why.

---

## Success Criteria

**v1 succeeds if:** I am more technically hireable in the AI age AND the app solves a real problem for me.

**v1 fails if:** It doesn't grow my skills and doesn't solve a real problem.

The learning value (agent patterns, cost-aware routing, structured prompting, context engineering) is locked in from day one of building — independent of whether the product works.

---

## Spec

The canonical source of truth for this project lives in [`Spec.json`](./Spec.json). It contains the full problem framing, assumptions and their verdicts, open questions, constraints, and the phase-by-phase reasoning that produced the v1 design. All future design and build conversations should be grounded in it.

---

*Codename: `second-brain` — v0.1.0*
