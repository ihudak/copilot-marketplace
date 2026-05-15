# Changelog

All notable changes to the **obsidian-llm-wiki** plugin are recorded here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow semver at the plugin level.

## [0.3.0]

### Added
- **wiki-task** skill — create individual tasks from natural language with
  effort estimation, tagging, and Jira linking in Obsidian Tasks format.
- **wiki-tasks-extract** skill — batch-extract tasks from wiki content
  after ingest.

## [0.2.0]

### Changed
- Ported from Claude Code plugin to GitHub Copilot CLI plugin format.
- Skills use SKILL.md with YAML frontmatter.
- Orchestrator skills declare `allowed-tools:` in frontmatter.
- Path references use `~/.copilot/installed-plugins/...`.

## [0.1.0]

### Added
- Initial release with nine skills: wiki-init, wiki-ingest, wiki-scan,
  wiki-query, wiki-save, wiki-lint, wiki-hot, wiki-tags-refresh, wiki-schema.
- Hooks: `SessionStart` and `Stop` via `hooks.json`.
- AGENTS.md for Claude Code compatibility.
