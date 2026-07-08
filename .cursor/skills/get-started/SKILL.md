---
name: get-started
description: Bootstraps a new application project into a shipping loop: repo skeleton, product and technical artifacts, implementation, iOS device iteration, TestFlight, and App Store submission prep. Use when the user wants to start a new project from scratch, initialize an app repository with the get-started workflow, or follow GET-STARTED.md.
---

# Get-Started Workflow

Follow the six-phase workflow to bootstrap a new application repository. For exact templates and operational details, read **GET-STARTED.md** at the repository root, or fetch `https://raw.githubusercontent.com/sinned/get-started/refs/heads/main/GET-STARTED.md` when working in another repo.

Do not run the bootstrap workflow inside the `get-started` instruction repository itself unless the user explicitly asks for a disposable test fixture or separate target directory.

## Phase 1: Repo Skeleton

Create the baseline repository contract without product logic:

- `.gitignore` with general, Xcode, ASC artifact, and signing-secret exclusions.
- `AGENTS.md` with the project structure, XcodeGen contract, version/build discipline, capability rules, and agent operating loop.
- `HUMANS.md` with principals, Apple Team ID, bundle root, App Store Connect IDs, URLs, TestFlight group, and device notes.
- `README.md`, `CHANGELOG.md`, and `VERSION`.
- `app/ios/`, `artifacts/`, `scripts/`, `metadata/`, and `.asc/artifacts/` as appropriate.

## Phase 2: Product + Technical Artifacts

Ask the user:

> The project skeleton is ready. What is the product idea you want to build? Please describe the features, users, goals, and target platforms.

Then create:

- `artifacts/prd.md`
- `artifacts/tdd.md`
- `artifacts/task.md`
- `artifacts/implementation_plan.md` when the work is complex

Update `AGENTS.md`, `README.md`, and `CHANGELOG.md` from the artifacts.

## Phase 3: Implementation

Execute the plan with repeatable verification:

- Use XcodeGen for iOS projects.
- Store marketing version in `VERSION`.
- Store `MARKETING_VERSION` and `CURRENT_PROJECT_VERSION` in `app/ios/project.yml`.
- Display `Version x.y.z (n)` in the app.
- Create `scripts/verify-ios.sh` and make it the default pre-install/pre-upload check.
- Add app-specific smoke-test launch arguments for deterministic validation.

## Phase 4: Fast iOS Device Iteration

Create `scripts/device-validate-ios.sh` to build into `$TMPDIR`, install with `xcrun devicectl`, launch from the command line, support `--launch-only`, and optionally stream logs.

If install succeeds but launch fails because the phone is locked, report that distinction clearly and ask the user to unlock the phone, then rerun with `--launch-only`.

For UI work, capture simulator screenshots with `xcrun simctl io` using absolute paths.

## Phase 5: TestFlight Distribution

Treat TestFlight as a distribution lane, not the tight local iteration loop.

Before upload, ensure the app record exists, bundle ID matches, icon and `CFBundleIconName` are valid, version/build is unique, XcodeGen is fresh, `scripts/verify-ios.sh` passes, archives go to `.asc/artifacts/`, and build processing completes before saying the build is ready.

Prefer `asc` when installed. Include the API-key recovery path for machines without usable Xcode account state.

## Phase 6: App Store Submission Prep

Prepare metadata, compliance, screenshots, selected build, release notes, pricing, availability, review contact, review notes, demo account details, privacy answers, export compliance, age rating, and icon validation.

Store canonical metadata in `metadata/` where possible and sync via `asc` or App Store Connect.

## Quick Reference

| Phase | Outputs |
| --- | --- |
| 1 Repo Skeleton | `.gitignore`, `AGENTS.md`, `HUMANS.md`, `README.md`, `CHANGELOG.md`, `VERSION`, `app/ios`, `artifacts`, `scripts`, `metadata`, `.asc/artifacts` |
| 2 Artifacts | `artifacts/prd.md`, `artifacts/tdd.md`, `artifacts/task.md`, updated docs |
| 3 Implementation | XcodeGen project, visible version/build, app code, `scripts/verify-ios.sh`, smoke args |
| 4 Device Iteration | `scripts/device-validate-ios.sh`, device install/launch loop, simulator screenshots |
| 5 TestFlight | archive/export/upload path, ASC auth recovery, group assignment, test notes |
| 6 App Store | metadata, compliance, screenshots, selected build, submission checklist |

For exact wording and templates, always refer to GET-STARTED.md.
