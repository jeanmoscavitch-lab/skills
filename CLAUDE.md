# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of agent skills (slash commands and behaviors) for Claude Code and other Agent-Skills-standard harnesses. There is no application code, build step, lint, or test suite — the deliverables are the markdown skill definitions under `skills/`. The collection ships as a Claude Code plugin (`.claude-plugin/plugin.json`) and via the skills.sh installer (`npx skills@latest add mattpocock/skills`).

## Commands

- `scripts/list-skills.sh` — list every `SKILL.md` in the repo.
- `scripts/link-skills.sh` — symlink every non-deprecated skill into `~/.claude/skills` and `~/.agents/skills` for local development (a `git pull` then updates installed skills in place).
- `npx changeset` — record a changeset for any user-facing skill change. Releases are automated: the `Release` workflow on `main` opens a "chore: version skills" PR via changesets and tags versions. Changeset summaries are written as rich release notes (bold skill names, behavior-level descriptions — see `CHANGELOG.md` for the house style).

## Repository structure

Each skill is a folder containing a `SKILL.md` with YAML frontmatter (`name`, `description`, and optionally `disable-model-invocation: true`). Supporting reference docs live as sibling files inside the same skill folder (e.g. `tdd/tests.md`, `tdd/mocking.md`) — never shared across skill folders.

Skills are organized into bucket folders under `skills/`:

- `engineering/` — daily code work
- `productivity/` — daily non-code workflow tools
- `misc/` — kept around but rarely used
- `personal/` — tied to my own setup, not promoted
- `in-progress/` — drafts not yet ready to ship
- `deprecated/` — no longer used

## Registration rules

Every skill in `engineering/`, `productivity/`, or `misc/` must have a reference in the top-level `README.md` and an entry in `.claude-plugin/plugin.json`. Skills in `personal/`, `in-progress/`, and `deprecated/` must not appear in either.

Each skill entry in the top-level `README.md` must link the skill name to its `SKILL.md`.

Each bucket folder has a `README.md` that lists every skill in the bucket with a one-line description, with the skill name linked to its `SKILL.md`. Bucket `README.md`s and the top-level `README.md` group entries into **User-invoked** and **Model-invoked**.

## Invocation model

Every `SKILL.md` is either user-invoked (`disable-model-invocation: true`, reachable only by the human; human-facing one-line description with no trigger phrases) or model-invoked (the default; model-facing description with rich "Use when…" trigger phrasing so auto-invocation fires). A user-invoked skill can invoke model-invoked skills but never another user-invoked one. Dependencies between skills are expressed as `/skill`-style prose invocation ("Run the `/grilling` skill"), not `../other-skill/FILE.md` cross-references. For the full definitions and rationale, see [docs/invocation.md](./docs/invocation.md).

## Domain language and decisions

`CONTEXT.md` is the project glossary — use its terms when writing or editing skills: **Issue tracker** (not "backlog manager" or "backlog backend"), **Issue** (not "ticket"), **Triage role**. Architecture decisions live in `docs/adr/`.

`.out-of-scope/` documents feature requests that have been deliberately rejected (e.g. niche issue-tracker backends, hard caps on grilling questions, a verify mode for setup). Check it before implementing a request in those areas, and add a new entry when rejecting a recurring class of request.
