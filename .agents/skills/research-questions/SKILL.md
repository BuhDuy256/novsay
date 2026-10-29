---
name: research-questions
description: Generate a research checklist from a use case. Reads the UC, its FRs, NFRs, and BRs, then produces questions grouped by requirement. For technical questions, provides options with tradeoffs. Used at the start of Phase 1.
---

# Research questions

Generate the research checklist for a use case build.

## Input

The user names a UC (e.g., "UC-001"). Read these files:

1. The UC file: `docs/spec/02-use-cases/UC-XXX.md`
2. Every FR referenced in the UC's step table and alternative flows.
3. Every NFR and BR referenced by those FRs or by the UC.
4. Existing research in `docs/research/` — to avoid asking already-answered questions.
5. Existing decisions in `docs/decisions/` — to avoid asking already-decided questions.

## Process

For each FR/NFR/BR referenced by the UC:

1. Identify what the system must do (from the FR statement and ACs).
2. Ask: "What technical knowledge is needed to implement this?"
3. Ask: "What decisions must be made before implementation?"
4. Check if existing research already answers the question — if yes, reference it and
   mark as `answered` or `decided`.
5. For technology choices, provide an options table:

   | Option | Description | Fits requirements | Tradeoffs |
   |---|---|---|---|

6. Tag each question with why it matters: which FR/AC depends on the answer.

## Output

Create `plans/UC-XXX/research-checklist.md` from the template at
`plans/_TEMPLATES/research-checklist.md`.

Group questions by FR/NFR. Each question has:
- A unique ID: `RQ-N`
- The question text
- Why it matters (which FR/AC)
- Status: `open`, `answered`, or `decided`
- Options table (for technical choices)

## Rules

- Do not generate questions about product requirements — those are settled in the spec.
- Do not generate questions answerable by reading the spec — read it first.
- Do not generate questions about implementation details that can be decided during
  coding (variable names, internal function splits). Focus on decisions that affect
  the architecture, the test strategy, or the ticket structure.
- If a question spans multiple FRs, list it once under the most relevant FR and
  cross-reference.
- Existing answered questions in `docs/research/` are referenced, not duplicated.
