# Changelog

## [Unreleased]

### Added
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

### Changed
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
