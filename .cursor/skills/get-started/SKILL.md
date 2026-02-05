---
name: get-started
description: Bootstraps a new application project using the Stub → Artifacts → Code workflow. Creates project skeleton (AGENTS.md, README.md, HUMANS.md, CHANGELOG.md, VERSION, directories), planning artifacts (PRD, TDD, task list), and guides implementation. Use when the user wants to start a new project from scratch, initialize a repository with the get-started workflow, or follow GET-STARTED.md.
---

# Get-Started Workflow

Follow the three-phase workflow to bootstrap a new application project. For full templates and exact content, read **GET-STARTED.md** at the repository root (or fetch `https://raw.githubusercontent.com/sinned/get-started/refs/heads/main/GET-STARTED.md` when working in another repo).

## Phase 1: Stub Project Structure

**Goal:** Create the skeleton without implementing logic.

1. **Initialize repository**: `git init` if needed; create `.gitignore` (e.g. `node_modules`, `dist`, `.env`, `.DS_Store`, `*.log`).
2. **Create AGENTS.md** at root using the template in GET-STARTED.md (directory structure, Architecture and Code Conventions placeholders, note to see HUMANS.md).
3. **Create README.md** at root; keep it updated in all phases.
4. **Create HUMANS.md** at root for human principals (names, Apple Team ID, Bundle Root, other team identifiers).
5. **Create CHANGELOG.md** at root: [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), [Semantic Versioning](https://semver.org/spec/v2.0.0.html). Start with an "Unreleased" section.
6. **Create VERSION** at root with current version (e.g. `1.0.0`).
7. **Stub directories**: `app/` (and `app/ios/`, `app/android/`, `app/web/` as needed), `server/`, `artifacts/`.

## Phase 2: Build Artifacts

**Goal:** Plan the product and technical design before coding.

1. **Ask the user:** "The project skeleton is ready. What is the product idea you want to build? Please describe the features and goals."
2. **Once the user responds:**
   - Create `artifacts/prd.md` from their input.
   - Create `artifacts/tdd.md` (architecture, tech stack for app/server, database, etc.).
   - Update `AGENTS.md` Architecture and Code Conventions from the TDD.
   - Update `README.md` with description, features, setup from PRD/TDD.
   - Create `artifacts/task.md` for MVP tasks (or use the assistant’s own task system instead).

## Phase 3: Implementation

**Goal:** Execute the plan from Phase 2.

1. **Setup development environment:**
   - Server: e.g. `npm init` if in TDD.
   - App:
     - **iOS:** Use `xcodegen` to generate and maintain the Xcode project in `app/ios/`.
     - Android: Create project in `app/android/`.
     - Web: e.g. `npx create-react-app app/web` in `app/web/`.
     - Cross-platform: e.g. `flutter create` in `app/` as per TDD.
2. **Execute tasks:** Work from `artifacts/task.md`; use `artifacts/implementation_plan.md` for complex steps.
3. **Ongoing:** Keep `README.md` and `CHANGELOG.md` (and `VERSION` on release) updated.

## Quick reference

| Phase   | Outputs |
|---------|--------|
| 1 Stub  | `.gitignore`, AGENTS.md, README.md, HUMANS.md, CHANGELOG.md, VERSION, app/server/artifacts dirs |
| 2 Artifacts | artifacts/prd.md, artifacts/tdd.md, artifacts/task.md, updated AGENTS.md and README.md |
| 3 Implementation | Initialized app/server, features per task list, updated README and CHANGELOG |

For exact wording and templates, always refer to GET-STARTED.md.
