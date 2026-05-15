# Changelog

All notable changes to the **dev-workflows** plugin are recorded here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow semver at the plugin level.

## [1.2.1] — 2026-05-15

### Breaking changes
- **`impl:` is now a dispatcher.** Bare `impl:` no longer runs the code-implementation
  workflow — it prints a help page with the command matrix. Use `impl:code:` explicitly.
  Aligns with Claude Code plugin behaviour since v1.1.0.

### Added
- **`impl-dispatcher` skill.** Help / dispatcher triggered by bare `impl:`. Lists all
  `impl:*` variants and related skills (`fix-vuln:`, `upgrade:`), then stops.

### Changed
- **`impl` skill trigger narrowed.** Now only activates on `impl:code:` and `implement:`.
- **Marketplace descriptions enriched.** `dev-workflows` and `dt-style-guide` descriptions
  in `.github/plugin/marketplace.json` now enumerate all skills, sub-agents, and hooks.

## [1.2.0] — 2026-05-12

Copilot CLI port of the Claude Code dev-workflows plugin (v1.1.0).

### Added
- **Namespaced skill layout.** `skills/impl/`, `skills/impl-docs/`, `skills/impl-jira/`
  become the natural-language prefixes `impl:`, `impl:docs:`, `impl:jira:docs:`,
  `impl:jira:epics:` via Copilot CLI's skill discovery.
- **`impl:code:` full workflow.** Structured code-implementation skill: classify →
  optional Opus planning → feature branch → test baseline → implement → test-writing →
  optional Opus review → maintenance → report.
- **`impl:docs:` full workflow.** One-shot doc-editing skill: classify → plan →
  implement → doc-reviewer gate → maintenance → report.
- **`impl:jira:docs:` and `impl:jira:epics:` workflows.** Jira-driven documentation
  and Epic-writing skills with parallel sub-agent invocation, style checking, and
  Opus review gates.
- **15 sub-agent skills.** test-baseliner, test-writer, risk-planner, code-review,
  review-fixer, impl-maintenance, jira-reader, diff-summarizer, code-scanner,
  doc-location-finder, doc-planner, docs-style-checker, doc-reviewer, doc-fixer,
  epic-reviewer.
- **`fix-vuln:` workflow.** Security vulnerability remediation with NVD lookup,
  minimal-version fix strategy, baseline tests, and per-CVE branches/PRs.
- **`upgrade:` workflow.** Component upgrade with before/after test verification.
- **Hooks.** `preload-context.sh` injects git context on skill activation;
  `post-tool-use.sh` tracks tool usage.
- **Shared references.** `_shared/model-routing.md` defines task classification,
  model routing, and the mandatory Opus code-review checklist.

### Changed (vs Claude Code v1.1.0)
- Skills use SKILL.md with YAML frontmatter (not `commands/*.md` / `agents/*.md`).
- Orchestrator skills declare `allowed-tools:` in frontmatter; sub-agent skills do not.
- Path references use `~/.copilot/installed-plugins/...` instead of `${CLAUDE_PLUGIN_ROOT}`.
- Hooks use `${PLUGIN_ROOT}` instead of `${CLAUDE_PLUGIN_ROOT}`.
