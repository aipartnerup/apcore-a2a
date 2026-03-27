# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.3.0] - 2026-03-27

### Added

- **Display overlay in `SkillMapper`** (§5.13) — both Python and TypeScript SDKs now read `metadata["display"]["a2a"]` for skill name, description, tags, and guidance.
  - Skill name: `a2a.alias` → `display.alias` → humanized `module_id`.
  - Description: `a2a.description` → `display.description` → `module.description`. Guidance appended if present.
  - Tags: `display.tags` → `module.tags`.

### Changed

- **Cross-language sync** — aligned Python and TypeScript SDKs on endpoint, env vars, CLI interface, and documentation.
- **Well-known endpoint** unified to `/.well-known/agent.json` across both SDKs (TypeScript was using `agent-card.json`).
- **Environment variables** renamed with `APCORE_` prefix: `JWT_SECRET` → `APCORE_JWT_SECRET`, `A2A_EXECUTION_TIMEOUT` → `APCORE_A2A_EXECUTION_TIMEOUT`.
- **CLI `--execution-timeout`** now accepts seconds in both SDKs (TypeScript was using milliseconds).
- **`apcore` dependency** bumped from `0.9.0+` to `0.14.0+` in both SDKs.
- Updated feature spec `docs/features/adapters.md` — SkillMapper field mapping table corrected (`id`→`module_id`, `name`→alias chain).

### Removed

- **`_build_extensions()` dead code** (Python) — `AgentSkill` has no `extensions` field in the A2A SDK; deleted along with 3 tests.

---

## [0.2.1] - 2026-03-22

### Changed
- Rebrand: aipartnerup → aiperceivable

## [0.2.0] - 2026-03-10

### Changed

- Updated Python requirement from 3.10+ to 3.11+ to match pyproject.toml.
- Updated apcore dependency requirement from 0.6.0+ to 0.9.0+.
- Delegated TaskStore and InMemoryTaskStore to a2a-sdk (replaces custom protocol).
- Replaced ExecutionRouter, TaskManager, and TransportManager with a2a-sdk components (ApCoreAgentExecutor, DefaultRequestHandler, A2AStarletteApplication).
- CLI `--host` default changed from `0.0.0.0` to `127.0.0.1` for safer defaults.
- Default agent name fallback changed from `"apcore-agent"` to `"Apcore Agent"`.
- Auth 401 response body now returns `{"error": "Unauthorized", "detail": "Missing or invalid Bearer token"}`.
- AgentCard `defaultOutputModes` now includes both `"text/plain"` and `"application/json"`.

### Added

- Expanded public API exports: auth classes, adapter classes, and server factory now re-exported from top-level `__init__.py`.
- Documented that SkillMapper `_build_extensions()` cannot wire annotations into AgentSkill (a2a-sdk lacks `extensions` field); annotations available via Explorer UI instead.
- ErrorMapper `_sanitize_message()` now strips traceback lines in addition to file paths.
- Explorer `create_explorer_mount()` accepts optional `registry` parameter to enrich agent card with input schemas.
- Path-based registry resolution: `serve()` and `async_serve()` accept `str`/`Path` for auto-discovery.

### Fixed

- Feature specs updated to match actual implementation (F-01 through F-11).
- Documentation version references corrected (Python 3.11+, apcore 0.9.0+).

## [0.1.0] - 2026-03-07

### Added

- Product Requirements Document (PRD), Software Requirements Specification (SRS), Technical Design Document, and Test Plan.
- 11 feature specifications: adapters, storage, server-core, streaming, push-notifications, auth, client, public-api, cli, explorer, ops.
- Getting Started guide with Python and TypeScript examples.
- README with project overview, quick start, and architecture summary.
- MkDocs Material documentation site with GitHub Pages deployment.
- Project logo (`apcore-a2a-logo.svg`).
