# Changelog

## [Unreleased]

### Changed
- Product vision: Novsay is now a web novel listening platform, not a generic TTS tool
  - VIS-001: identity updated to "nền tảng nghe truyện web", added B-2 boundary
  - BR-001 V-1: changed from closed set (Novel543 only) to open set (any supported
    novel site, with per-site config); Novel543 is the first supported source
  - UC-001, _STYLE.md: replaced hardcoded Novel543 references with "website nguồn"
- Research questions RQ-1, RQ-3, RQ-4 reframed from Novel543-specific to multi-site
- GitHub issues #1, #2, #4, #5 updated to match multi-site scope

### Fixed
- `.claude/skills` was a plain file (path reference) instead of a directory — replaced
  with synced skill mirrors so Claude Code CLI discovers all 15 skills via `/` commands
- Added "Known mistakes" section to `CLAUDE.md` to prevent recurring errors
  - Condensed to one-line-per-rule format

### Added
- Synced skill mirrors to `.claude/skills/` and `.codex/skills/` (15 skills each)
- Build workflow (`WORKFLOW.md`): 6-phase process from spec to working code
  (research, testing plan, implementation plan, tickets, execution, verification)
- `AGENTS.md`: project overview, workflow reference, skill routing, ticket rules
- `docs/decisions/` folder with README and decision record template
- `plans/` folder with README and templates (research checklist, testing plan,
  implementation plan, flow tracker)
- `.github/ISSUE_TEMPLATE/` with 5 templates (flow tracker, research ticket,
  test stub ticket, implementation ticket, post-impl test ticket)
- New skills: `research-questions`, `testing-plan`, `ticket-writer`,
  `flow-tracker-update`
- Workflow triggers in `CLAUDE.md` (build/continue/status UC-XXX)
- Flow model section in the research checklist template: per-step runtime trace
  that every research question maps back to
- Mermaid sequence diagram section in the research ticket template, highlighting
  the flow step each question comes from

### Changed
- `research-questions` skill builds an end-to-end flow model first, then derives
  questions from it; each question now carries a flow-step reference
- `ticket-writer` skill documents how research tickets reuse one base flow diagram
  with only the highlight moving per question
- Flatten `docs/research/technical-foundations/` to `docs/research/` and drop
  number prefixes from filenames
- Update `docs/research/README.md` as topic index with question status legend
- Add proposal status headers to `docs/development/coding-conventions.md`,
  `docs/development/code-review-criteria.md`, and
  `docs/development/repository-structure.md`
- Update `.agents/skill-manifest.json` with new skills and supersede deferred
  `research` skill

## [Previous]

### Changed
- Reorganize skills from `.claude/skills/` to `.agents/skills/` for cleaner agent-based structure
- Expand web content research (TF-001) with detailed Q&A on HTTP fetching, CORS, request anatomy, site variation, and anti-scraping

### Added
- New `commit-push` skill for one-step conventional commit and push workflow
- CHANGELOG.md to track project changes

### Removed
- Legacy `.claude/hooks/use-case-flowchart-reminder.sh` hook
- Old `.claude/settings.json` configuration
