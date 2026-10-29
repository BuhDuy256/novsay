# Research

Technical research for Novsay. Each file covers a topic area with questions linked
to the UC-001 research checklist (`plans/UC-001/research-checklist.md`).

## Topics

- [Web content fetching](web-content.md) — RQ-1, RQ-2, RQ-3, RQ-4 + prior Q-001–Q-004
- [Audio generation](audio-generation.md) — RQ-6 (chunking)
- [Audio playback](audio-playback.md) — RQ-7 (format), RQ-13 (background)
- [Data storage](data-storage.md) — RQ-11 (audio compatibility logic)
- [Listening progress](listening-progress.md) — RQ-8 (checkpoint mechanism)
- [Preparation and recovery](preparation-and-recovery.md) — RQ-12 (request state)
- [Authentication](authentication.md) — RQ-14 (API key protection)

## Decision records

Questions that require a technology/architecture choice produce a decision record
in `docs/decisions/` instead of (or in addition to) a research answer here:

- RQ-5 → [DEC-001 TTS provider](../decisions/DEC-001-tts-provider.md)
- RQ-9 → [DEC-002 Execution model](../decisions/DEC-002-execution-model.md)
- RQ-10 → [DEC-003 Storage](../decisions/DEC-003-storage.md)
- RQ-15 → [DEC-004 Stack choice](../decisions/DEC-004-stack.md)
- RQ-16 → [DEC-005 Hosting](../decisions/DEC-005-hosting.md)

## Question status

Each question in these files carries a status:

- `open` — not started
- `researching` — in progress
- `answered` — answer written in this file
- `decided → DEC-NNN` — answer led to a decision record in `docs/decisions/`
