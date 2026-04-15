# Whiteboard

Scratch space for ideas, reframings, and open design questions *before* they land in `Spec.json`. Think of this as the working memory; the spec is the lockbox.

## Protocol

- **Proposed** — idea has been raised, not yet decided. Captures the thought and the tradeoff.
- **Accepted** — decided; ready to merge into `Spec.json` on the next revision bump.
- **Deferred** — considered, explicitly pushed out of current scope, with reason.
- **Rejected** — considered and turned down, with reason.

Every entry gets a date. When something moves from Proposed → Accepted, update the spec and optionally leave the entry here as a trail of *why*.

---

## Accepted (ready for next spec revision)

### 2026-04-15 — Output is a queryable research artifact, not a one-shot report
**From:** discussion on NotebookLM-style interaction
**Change:** Replace `must_have mh_4` ("Synthesis pass → 2-page summary") framing with: research run produces a *source-grounded artifact* you can interrogate after the fact. The 2-page summary remains the default view; underneath it, all sources and intermediate findings are queryable via chat.
**Why:** Big decisions are iterative ("what if the wedding is 6 months later?"). A one-shot report discards the richest artifact the overnight run produces — the sources themselves. This is a modest extension of the already-planned audit trail, not a new feature.
**Spec touch points:** `concept_v1.must_haves.mh_4`, `concept_v1.must_haves.mh_5`, `concept_v1.non_goals_v1` (clarify "daily-use chatbot framing" vs. "decision-artifact chat").

### 2026-04-15 — Refine the "daily-use chatbot" non-goal
**From:** tension between "no chatbot" and "where does personal info come from?"
**Change:** The non-goal is *general-purpose chatbot companionship* (Pi / Replika class). It is **not** "any interaction outside a single research request." Purposeful, event-driven interactions are in scope.
**Why:** Without some interaction loop, `context.md` goes stale and becomes a maintenance burden the user won't sustain. The original non-goal was too blunt and was hiding an assumption about manual upkeep.
**Spec touch points:** `concept_v1.non_goals_v1` (rewrite the chatbot line).

---

## Proposed (under discussion)

### 2026-04-15 — Interaction ladder for personal info capture
**From:** discussion on sources of personal context
**Options on the table:**
1. **Onboarding primer** — one-time structured interview to seed `context.md`. Walks through decision categories from the spec.
2. **In-run clarification** — agent logs questions to a file / emails / pings a local web UI when it hits a gap; user answers when convenient. Text-based, no mobile.
3. **Post-research capture** — after the report, short prompt: "anything here surprise you? anything I got wrong?"
4. **Chat-with-artifact revelations** — during chat with the research expert, user naturally reveals things; system captures back into `context.md`.
5. **Periodic check-in** — weekly/monthly: "what changed?"

**Current lean for v1:** (1) + (2) + (4). Skip (3) and (5) — additive, can come later.
**Open question:** What's the mechanism for (2)? File-based seems simplest (agent writes `clarifications_needed.md`, user fills in, agent resumes on next invocation). Email is overkill for v1.
**Spec touch points:** new `interaction_surfaces` section under `concept_v1`; update `must_haves` to include onboarding primer and clarification loop.

---

## Deferred

### 2026-04-15 — Mobile notifications for in-run clarification
**Why:** Mobile app + push + two-way sync is a massive infrastructure lift for a first project. Underlying need (agent asks when stuck) is real but solvable with text-file or local-web mechanisms at a fraction of the cost. Revisit post-v1, alongside the broader "mobile app" item already in `out_of_scope_for_now_revisit_later`.

---

## Rejected

*(none yet)*
