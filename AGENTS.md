# AGENTS.md - Repository Guidance

**Last Updated:** 2026-07-08
**Repository:** get-started

---

## Important Scope Note

This repository is the source of the `get-started` bootstrap instructions. It is not itself a target application repository to initialize.

Do not run the `GET-STARTED.md` workflow against this repository unless the user explicitly asks to test the workflow in a disposable fixture or separate target directory. In particular, do not create starter-project files or directories such as `.gitignore`, `HUMANS.md`, `app/`, `server/`, `artifacts/`, `scripts/`, `metadata/`, or `.asc/` here just because the workflow describes them.

When a user says to "init" or "initialize" this repository, treat that as a request to update, validate, or maintain the instruction/template repository, not to bootstrap a new app project in place.

## Repository Purpose

This repo stores:

- `GET-STARTED.md`: the canonical long-form bootstrap guide.
- `.cursor/skills/get-started/SKILL.md`: the Cursor skill wrapper for the guide.
- `README.md`: usage documentation for humans and AI assistants.
- `CHANGELOG.md` and `VERSION`: release tracking for this instruction repository.

## Editing Guidance

- Keep `GET-STARTED.md` and `.cursor/skills/get-started/SKILL.md` aligned when changing the workflow.
- Keep examples phrased so they clearly distinguish this instruction repository from a separate project being bootstrapped.
- Preserve this repository as a lightweight template/documentation source unless the user asks for broader repo changes.
