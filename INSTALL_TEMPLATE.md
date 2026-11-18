# Install Intent-Driven Template: Grill Docs

This file is for AI coding agents. Follow these instructions when a user asks you to add this template to an existing project.

## Goal

Install the intent-driven OpenSpec assets and the grill-with-docs proposal flow into the user's current project without overwriting project-specific work blindly.

This guide covers first-time installation. It does not track template versions; upgrades are a separate change.

## Source Template

Use a local checkout of this repository. If the user does not have one, clone it outside the target project:

```bash
git clone <this-repository-url> ~/Projects/intent-driven-template-grill-docs
```

Check the source's branch and status before copying.

## Target Project Review

Before copying anything, inspect the target project:

- `README.md`, `AGENTS.md`, `opencode.json`, `.opencode/`, `.agents/`, `.cursor/`, `openspec/`
- Any existing OpenSpec schema, config, skills, or rules
- Existing `glossary/`, `adr/`, and documentation conventions

Preserve user-specific instructions and project conventions. Do not delete or replace existing files without explaining the conflict and getting approval.

## Files To Install

Copy these when they do not already exist:

- `openspec/` (keep the target's `config.yaml` and specs if it already uses OpenSpec)
- `.opencode/`
- `.agents/`
- `.cursor/`
- `opencode.json`

Merge these when they already exist:

- `AGENTS.md`: add the OpenSpec git-discipline and glossary/ADR lines without removing existing instructions.
- `.gitignore`: add `openspec/.cache/` and `.opencode/node_modules/`.
- `openspec/config.yaml`: keep the target's `context` and `rules`; adopt the template's `operations` guidance where compatible.

Do not copy this repository's `README.md`, `INSTALL_TEMPLATE.md`, or `LICENSE.md` over the target's own files.

## Install Steps

1. Locate or clone the source template.
2. Inspect the target project for existing configuration and documentation.
3. Copy missing directories and files.
4. Merge `AGENTS.md` and `.gitignore`.
5. If `openspec/config.yaml` exists, compare schemas and rules. Ask before replacing a different schema. Do not silently switch a project off its current workflow.
6. If the target has hand-written specs in bullet style and `spec-as-source` is requested, stop: enabling it makes an unfenced scenario a hard error, so the migration needs its own change.
7. Keep the target's product code, package files, application docs, and tests unchanged.

## Verify

```bash
git status --short
openspec schema validate intent-driven
openspec update --dry-run
```

Then check that the proposal rule resolves:

```bash
openspec instructions proposal --change <any-change> --json
```

The returned `rules` array must name `grill-with-docs`. If it does not, the config was not merged correctly.

If the OpenSpec CLI is unavailable, report that and leave the files in place for the user to verify.

## Notes

- The generated lifecycle skills under `.opencode/skills/` and `.agents/skills/` are CLI-owned. Refresh them with `openspec update` instead of editing them.
- `.agents/skills/.openspec-target` records the Codex target. Leave it in place when Codex is one of the tools.
- The template vendors `grilling`, `domain-modeling`, and `grill-with-docs` under `.agents/skills/`. If the user already has global copies, the repo-local copies win; state that in the summary.
