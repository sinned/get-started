# Clean Project Shipping Loop Guide

This guide bootstraps a new application repository from an empty or early-stage repo into a loop that can ship quickly:

```text
plan -> code -> tests -> visible version bump -> install to iPhone -> user validates -> TestFlight -> App Store
```

The workflow still starts with **Stub -> Artifacts -> Code**, but it also sets up the repeatable iOS build, device-validation, TestFlight, and App Store paths that keep a project moving after the first commit.

Use this guide in the repository that should become the new app. If you are editing the `get-started` instruction repository itself, update the guide and skill files only; do not run this workflow in place.

## Usage

Pass this file to your AI assistant and ask:

```text
Follow the instructions in GET-STARTED.md to initialize this app repository.
```

Alternatively, reference the guide directly:

```text
Follow the instructions at https://raw.githubusercontent.com/sinned/get-started/refs/heads/main/GET-STARTED.md to initialize this app repository.
```

## Phase 1: Repo Skeleton

**Goal:** Create the repository shape and project contracts before implementing product logic.

### Initialize Repository

- Run `git init` if the repository is not already initialized.
- Create `.gitignore`.
- Never commit signing secrets, private keys, certificates, profiles, or local build outputs.

Recommended `.gitignore`:

```text
node_modules
dist
.env
.DS_Store
*.log

.asc/artifacts/
.asc/signing/
*.xcresult
DerivedData/
build/
*.ipa
*.xcarchive
*.p8
*.p12
*.key
```

### Create Directory Structure

Create the directories that apply to the project. For iOS-first projects, use this baseline:

```text
repo/
├── app/
│   └── ios/
│       ├── project.yml
│       └── AppName/
├── artifacts/
├── scripts/
├── metadata/
├── .asc/
│   └── artifacts/
├── AGENTS.md
├── CHANGELOG.md
├── HUMANS.md
├── README.md
└── VERSION
```

Use `.gitkeep` only when you need Git to track an otherwise-empty directory. Do not force-track ignored build or signing directories.

### Create `AGENTS.md`

Create `AGENTS.md` in the root. This file is the primary operating contract for AI assistants working in the generated app repository.

Use this template and adjust it during Phase 2:

````markdown
# AGENTS.md - AI Assistant Guide

**Last Updated:** [Date]
**Repository:** [Project Name]

---

## Directory Structure

```text
repo/
├── app/
│   └── ios/
│       ├── project.yml
│       └── AppName/
├── artifacts/
├── scripts/
├── metadata/
├── .asc/
│   └── artifacts/
├── AGENTS.md
├── CHANGELOG.md
├── HUMANS.md
├── README.md
└── VERSION
```

## Product And Architecture

*To be defined in Phase 2 from `artifacts/prd.md` and `artifacts/tdd.md`.*

## Code Conventions

*To be defined in Phase 2 from `artifacts/tdd.md`.*

## iOS Tooling Contract

- Use XcodeGen as the source of truth for the Xcode project.
- Edit `app/ios/project.yml`, then run `xcodegen generate` from `app/ios/` before building, installing, archiving, or uploading.
- Commit meaningful `project.yml` changes and the generated `.xcodeproj` together unless the team explicitly chooses not to commit generated project files.
- Every user-facing device, TestFlight, or App Store build must have a unique marketing version/build combination.
- Keep `VERSION`, `app/ios/project.yml`, generated `.xcodeproj`, `CHANGELOG.md`, startup UI, and Settings UI in sync.
- Show the app version/build visibly in the app, at minimum on startup and Settings/About.
- Prefer command-line build, test, install, and validation loops before sending the human to Xcode.
- Store Apple Team ID, bundle root, primary bundle ID, App Store Connect app ID, SKU, app group IDs, and public URLs in `HUMANS.md`.
- Document capabilities and entitlements, especially App Groups, widgets, notifications, Sign in with Apple, iCloud, and HealthKit.
- Never commit signing secrets, `.p8`, `.p12`, `.key`, provisioning profiles, or local signing caches.

## Agent Operating Loop

1. Read `AGENTS.md`, `README.md`, `HUMANS.md`, and relevant artifacts first.
2. Make the smallest coherent change.
3. Bump version/build before any human-device build, TestFlight upload, or App Store submission.
4. Regenerate the Xcode project from XcodeGen.
5. Run tests and build verification.
6. Install to the phone when requested.
7. If install succeeds but launch fails because the phone is locked, report install and launch separately.
8. Use TestFlight only when distribution, review, or external validation is needed.
9. Keep final status short: version/build, install/upload result, and verification commands.
````

### Create `HUMANS.md`

Create `HUMANS.md` to document human principals and team identifiers. Keep secrets out of this file.

```markdown
# HUMANS.md - Project Principals

## Principals

- Name:
- Role:
- Contact:

## Apple / iOS

- Apple Team ID:
- Bundle Root:
- Primary Bundle ID:
- App Store Connect App ID:
- SKU:
- App Group IDs:
- Support URL:
- Privacy Policy URL:
- Terms URL:
- Review Contact:
- TestFlight Internal Group:

## Devices

- Primary test iPhone:
- Minimum iOS version:
- Notes: phone must be unlocked for launch/install retries.

## Other Identifiers

- Analytics:
- Backend:
- Other:
```

### Create `README.md`

Create a basic project README and keep it current throughout all phases. Include:

- Project name and purpose.
- Supported platforms.
- Setup commands.
- Verification commands.
- Device validation commands.
- TestFlight/App Store release notes once those lanes exist.

### Create `CHANGELOG.md`

Create `CHANGELOG.md` using [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) and [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Start with:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on Keep a Changelog, and this project adheres to Semantic Versioning.

## [Unreleased]
```

### Create `VERSION`

Create `VERSION` with the marketing version only:

```text
0.1.0
```

Do not store the build number in `VERSION`; store the build number in the iOS project settings.

## Phase 2: Product + Technical Artifacts

**Goal:** Understand the product and plan the technical implementation before writing feature code.

Stop and ask the user:

> The project skeleton is ready. What is the product idea you want to build? Please describe the features, users, goals, and target platforms.

Once the user responds, create these artifacts:

- `artifacts/prd.md`: product requirements, users, core workflows, MVP scope, and non-goals.
- `artifacts/tdd.md`: architecture, app/server stack, data model, persistence, integrations, capabilities, entitlements, testing plan, and distribution plan.
- `artifacts/task.md`: MVP task checklist.
- `artifacts/implementation_plan.md`: only for complex work that benefits from a step-by-step plan.

Update:

- `AGENTS.md`: fill in architecture, code conventions, capabilities, and validation commands.
- `README.md`: add product description, setup, verification, and current status.
- `CHANGELOG.md`: keep user-impacting changes under `Unreleased`.

For iOS apps, the TDD must define:

- Minimum iOS version.
- Bundle root and primary bundle ID.
- App capabilities and entitlements.
- Version/build display locations.
- Smoke-test launch arguments.
- Device-validation loop.
- TestFlight and App Store path.

## Phase 3: Implementation

**Goal:** Execute the plan with repeatable local verification.

### Version/Build Discipline

Every build that reaches a human device must be uniquely identifiable in the UI.

Required rules:

- `VERSION` stores the marketing version only, such as `0.1.0`.
- `app/ios/project.yml` stores `MARKETING_VERSION` and `CURRENT_PROJECT_VERSION`.
- Swift reads `CFBundleShortVersionString` and `CFBundleVersion`.
- The app displays `Version x.y.z (n)` on startup and in Settings/About.
- Bump patch version and/or build number for every phone install, TestFlight upload, or App Store submission.
- Keep `VERSION`, `project.yml`, generated `.xcodeproj`, `CHANGELOG.md`, startup UI, and Settings UI in sync.

Swift helper:

```swift
enum AppVersion {
    static var displayText: String {
        let version = Bundle.main.infoDictionary?["CFBundleShortVersionString"] as? String ?? "Unknown"
        let build = Bundle.main.infoDictionary?["CFBundleVersion"] as? String ?? "Unknown"
        return "Version \(version) (\(build))"
    }
}
```

### Standard XcodeGen Template

For iOS apps, create `app/ios/project.yml` before generating the Xcode project.

If `project.yml` changes, run `xcodegen generate` before building, installing, archiving, or uploading.

Minimal template:

```yaml
name: AppName

options:
  bundleIdPrefix: com.example
  deploymentTarget:
    iOS: "17.0"

settings:
  base:
    DEVELOPMENT_TEAM: TEAMID
    MARKETING_VERSION: 0.1.0
    CURRENT_PROJECT_VERSION: 1
    SUPPORTED_PLATFORMS: iphoneos iphonesimulator
    TARGETED_DEVICE_FAMILY: "1,2"

targets:
  AppName:
    type: application
    platform: iOS
    deploymentTarget: "17.0"
    sources:
      - AppName
    settings:
      base:
        PRODUCT_BUNDLE_IDENTIFIER: com.example.appname
    info:
      path: AppName/Info.plist
      properties:
        CFBundleDisplayName: AppName
        CFBundleIdentifier: "$(PRODUCT_BUNDLE_IDENTIFIER)"
        CFBundleShortVersionString: "$(MARKETING_VERSION)"
        CFBundleVersion: "$(CURRENT_PROJECT_VERSION)"
        UILaunchScreen: {}

  AppNameTests:
    type: bundle.unit-test
    platform: iOS
    deploymentTarget: "17.0"
    sources:
      - AppNameTests
    dependencies:
      - target: AppName
    settings:
      base:
        PRODUCT_BUNDLE_IDENTIFIER: com.example.appname.tests

schemes:
  AppName:
    shared: true
    build:
      targets:
        AppName: all
        AppNameTests: [test]
    test:
      targets:
        - AppNameTests
```

Optional app extension or widget pattern:

```yaml
  # Add this dependency under the app target when embedding an extension.
  AppName:
    dependencies:
      - target: AppNameWidgetExtension
        embed: true

  AppNameWidgetExtension:
    type: app-extension
    platform: iOS
    deploymentTarget: "17.0"
    sources:
      - AppNameWidget
    settings:
      base:
        PRODUCT_BUNDLE_IDENTIFIER: com.example.appname.widget
```

If adding widgets, App Groups, push notifications, Sign in with Apple, iCloud, HealthKit, or other capabilities, update all of these together:

- Entitlements files.
- `app/ios/project.yml`.
- Apple Developer bundle ID capabilities.
- Provisioning profiles.
- `HUMANS.md` and `artifacts/tdd.md`.

If device signing suddenly fails after adding a capability, regenerate or download provisioning profiles before debugging application code.

### Verification Script

Create `scripts/verify-ios.sh` for iOS projects. This is the command agents should run before installing to a phone or uploading a build.

Acceptance command:

```sh
./scripts/verify-ios.sh
```

Template:

```sh
#!/usr/bin/env bash
set -euo pipefail

ROOT="$(cd "$(dirname "${BASH_SOURCE[0]}")/.." && pwd)"
IOS_DIR="$ROOT/app/ios"
SCHEME="${SCHEME:-AppName}"
DERIVED_DATA="${TMPDIR:-/tmp}/verify-ios-derived-data"

cd "$IOS_DIR"

echo "==> Generating Xcode project"
xcodegen generate

echo "==> Typechecking/building app for iphoneos"
xcodebuild \
  -scheme "$SCHEME" \
  -destination 'generic/platform=iOS' \
  -derivedDataPath "$DERIVED_DATA" \
  CODE_SIGNING_ALLOWED=NO \
  build

echo "==> Building tests for iphoneos"
xcodebuild \
  -scheme "$SCHEME" \
  -destination 'generic/platform=iOS' \
  -derivedDataPath "$DERIVED_DATA" \
  CODE_SIGNING_ALLOWED=NO \
  build-for-testing

echo "==> Building app for iphonesimulator"
xcodebuild \
  -scheme "$SCHEME" \
  -destination 'generic/platform=iOS Simulator' \
  -derivedDataPath "$DERIVED_DATA" \
  CODE_SIGNING_ALLOWED=NO \
  build

echo "==> Building tests for iphonesimulator"
xcodebuild \
  -scheme "$SCHEME" \
  -destination 'generic/platform=iOS Simulator' \
  -derivedDataPath "$DERIVED_DATA" \
  CODE_SIGNING_ALLOWED=NO \
  build-for-testing

echo "==> Verification complete"
```

Include extension targets in the scheme or add explicit build commands when the app has widgets, intents, notification extensions, or other extension targets.

### App-Specific Smoke Tests

Create launch arguments that let agents validate a workflow without making the human tap through setup repeatedly.

Example launch argument:

```text
--my-app-smoke-test
```

App behavior for smoke mode:

- Seed demo or test data.
- Open the screen under test.
- Print deterministic logs.
- Avoid destructive behavior unless the argument explicitly says so.
- Let the agent capture logs briefly after launch.

## Phase 4: Fast iOS Device Iteration

**Goal:** Build, install, launch, and validate on a real iPhone from the command line.

### Device Validation Script

Create `scripts/device-validate-ios.sh` for iOS projects.

The script should support:

```text
--list
--device <device-id-or-name>
--team <apple-team-id>
--no-launch
--launch-only
--console
--console-seconds <seconds>
--quick-test
```

It should:

- Print `xcrun devicectl list devices` when `--list` is passed.
- Build into `$TMPDIR`, not the repo.
- Run `xcodegen generate`.
- Use `xcodebuild` with `-allowProvisioningUpdates`.
- Accept `DEVELOPMENT_TEAM`.
- Install with `xcrun devicectl device install app`.
- Launch with `xcrun devicectl device process launch`.
- Handle locked-phone launch failure as non-catastrophic.
- Support launch-only retries after the user unlocks the phone.
- Optionally stream logs for 10-20 seconds.

Template:

```sh
#!/usr/bin/env bash
set -euo pipefail

ROOT="$(cd "$(dirname "${BASH_SOURCE[0]}")/.." && pwd)"
IOS_DIR="$ROOT/app/ios"
SCHEME="${SCHEME:-AppName}"
BUNDLE_ID="${BUNDLE_ID:-com.example.appname}"
DEVICE=""
TEAM=""
NO_LAUNCH=0
LAUNCH_ONLY=0
CONSOLE=0
CONSOLE_SECONDS=15
QUICK_TEST=0

usage() {
  cat <<'USAGE'
Usage: scripts/device-validate-ios.sh [options]

Options:
  --list                         List available devices.
  --device <device-id-or-name>   Device identifier or name.
  --team <apple-team-id>         Apple development team ID.
  --no-launch                    Install only.
  --launch-only                  Skip build/install and retry launch.
  --console                      Stream logs briefly after launch.
  --console-seconds <seconds>    Log stream duration, default 15.
  --quick-test                   Pass app smoke-test launch argument.
USAGE
}

while [[ $# -gt 0 ]]; do
  case "$1" in
    --list) xcrun devicectl list devices; exit 0 ;;
    --device) DEVICE="$2"; shift 2 ;;
    --team) TEAM="$2"; shift 2 ;;
    --no-launch) NO_LAUNCH=1; shift ;;
    --launch-only) LAUNCH_ONLY=1; shift ;;
    --console) CONSOLE=1; shift ;;
    --console-seconds) CONSOLE_SECONDS="$2"; shift 2 ;;
    --quick-test) QUICK_TEST=1; shift ;;
    -h|--help) usage; exit 0 ;;
    *) echo "Unknown argument: $1" >&2; usage; exit 2 ;;
  esac
done

if [[ -z "$DEVICE" ]]; then
  echo "Missing --device. Run with --list to see available devices." >&2
  exit 2
fi

BUILD_ROOT="${TMPDIR:-/tmp}/device-validate-ios"
DERIVED_DATA="$BUILD_ROOT/DerivedData"
PRODUCTS="$DERIVED_DATA/Build/Products/Debug-iphoneos"
APP_PATH="$PRODUCTS/$SCHEME.app"
LAUNCH_ARGS=()
BUILD_SETTINGS=()

if [[ "$QUICK_TEST" -eq 1 ]]; then
  LAUNCH_ARGS+=(--my-app-smoke-test)
fi

if [[ -n "$TEAM" ]]; then
  BUILD_SETTINGS+=(DEVELOPMENT_TEAM="$TEAM")
fi

cd "$IOS_DIR"

if [[ "$LAUNCH_ONLY" -eq 0 ]]; then
  echo "==> Generating Xcode project"
  xcodegen generate

  echo "==> Building for device into $BUILD_ROOT"
  xcodebuild \
    -scheme "$SCHEME" \
    -destination 'generic/platform=iOS' \
    -derivedDataPath "$DERIVED_DATA" \
    -allowProvisioningUpdates \
    "${BUILD_SETTINGS[@]}" \
    build

  if [[ ! -d "$APP_PATH" ]]; then
    echo "App bundle not found at $APP_PATH" >&2
    exit 1
  fi

  echo "==> Installing $APP_PATH"
  xcrun devicectl device install app --device "$DEVICE" "$APP_PATH"
fi

if [[ "$NO_LAUNCH" -eq 1 ]]; then
  echo "Install complete; launch skipped."
  exit 0
fi

echo "==> Launching $BUNDLE_ID"
set +e
xcrun devicectl device process launch --device "$DEVICE" "$BUNDLE_ID" -- "${LAUNCH_ARGS[@]}"
LAUNCH_STATUS=$?
set -e

if [[ "$LAUNCH_STATUS" -ne 0 ]]; then
  echo "Install may have succeeded, but launch failed. If the phone is locked, unlock it and rerun with --launch-only." >&2
  exit "$LAUNCH_STATUS"
fi

if [[ "$CONSOLE" -eq 1 ]]; then
  echo "==> Streaming device logs for ${CONSOLE_SECONDS}s"
  xcrun devicectl device log stream --device "$DEVICE" &
  LOG_PID=$!
  sleep "$CONSOLE_SECONDS"
  kill "$LOG_PID" 2>/dev/null || true
  wait "$LOG_PID" 2>/dev/null || true
fi
```

Operational rule:

> If install succeeds but launch fails because the phone is locked, say that clearly and ask the user to unlock the phone, then rerun with `--launch-only`.

### Simulator Screenshots

For UI work, require screenshots before calling a view done.

Useful commands:

```sh
xcrun simctl list devices available
xcrun simctl launch <simulator-udid> com.example.app
xcrun simctl io <simulator-udid> screenshot /absolute/path/screenshot.png
```

Gotchas:

- Use absolute paths for screenshots.
- Delete throwaway screenshots when they are no longer useful.
- If simulator runtime and SDK mismatch, copy the exact destination from `xcodebuild` output.
- Prefer deterministic launch arguments for screenshot states.

## Phase 5: TestFlight Distribution

**Goal:** Produce a uniquely identifiable build, upload it, wait for processing, and assign it to testers when needed.

TestFlight is a distribution lane, not the tight local iteration loop.

### TestFlight Checklist

- App record exists in App Store Connect.
- Bundle ID matches the app record.
- App icon is included.
- `CFBundleIconName` exists if the app uses a custom `Info.plist`.
- Version/build is unique.
- `VERSION`, `project.yml`, generated `.xcodeproj`, `CHANGELOG.md`, startup UI, and Settings UI are in sync.
- XcodeGen project is freshly generated.
- `./scripts/verify-ios.sh` passes.
- Archive artifacts go to `.asc/artifacts/`.
- Build processing is complete before saying the build is ready.

### Preferred `asc` Path

If the `asc` CLI is installed and configured, prefer it for App Store Connect operations:

```sh
asc auth status
asc apps list --paginate
asc builds list --app APP_ID --paginate
```

Use the repo's current `asc` workflow if one exists under `.asc/`.

### Raw Xcodebuild Path

Archive:

```sh
# Run from the repo root.
mkdir -p .asc/artifacts
(cd app/ios && xcodegen generate)
xcodebuild archive \
  -project app/ios/AppName.xcodeproj \
  -scheme AppName \
  -destination 'generic/platform=iOS' \
  -archivePath .asc/artifacts/AppName.xcarchive \
  -allowProvisioningUpdates
```

Export:

```sh
xcodebuild -exportArchive \
  -archivePath .asc/artifacts/AppName.xcarchive \
  -exportPath .asc/artifacts/export \
  -exportOptionsPlist .asc/exportOptions.plist \
  -allowProvisioningUpdates
```

Upload:

```sh
xcrun altool --upload-app \
  --type ios \
  --file .asc/artifacts/export/AppName.ipa \
  --apiKey API_KEY_ID \
  --apiIssuer API_ISSUER_ID
```

If the repo has an `asc` upload command available, use that instead of `altool`.

### TestFlight Without Xcode Account State

Use this recovery path when export or upload fails with account-state errors such as:

```text
exportArchive Failed to Use Accounts
Failed to find an account with App Store Connect access
```

Recovery steps:

- Create an App Store Connect API Team Key.
- Store the `.p8` under `~/.asc/private_keys`.
- Run `asc auth login --network`.
- Verify with `asc auth status`.
- Create a distribution certificate if the local signing identity is missing.
- Create an App Store provisioning profile.
- Use manual export options.
- Upload with `xcodebuild -exportArchive` plus API-key flags when supported by the local Xcode version.
- Poll build processing with `asc`.
- Set export compliance.

Important gotcha:

> If using an Individual Key, do not invent an issuer ID. Use Team Keys for issuer-id based auth, or follow the CLI's individual-key mode exactly.

### TestFlight Groups And Notes

Useful commands:

```sh
asc testflight groups list --app APP_ID --paginate
asc builds add-groups --build-id BUILD_ID --group GROUP_ID
asc builds test-notes create --build-id BUILD_ID --locale en-US --whats-new "..."
```

If a group has access to all builds, do not manually assign the build; Apple may reject that operation even though distribution is fine.

## Phase 6: App Store Submission Prep

**Goal:** Prepare the app, metadata, compliance answers, and selected build for review.

Store canonical metadata in `metadata/` where possible, then sync through `asc` or App Store Connect.

Submission checklist:

- App name.
- Subtitle.
- Description.
- Keywords.
- Support URL.
- Privacy Policy URL.
- Terms URL.
- Pricing or free decision.
- Availability territories.
- Review contact name, phone, and email.
- Review notes and test information.
- Demo account if required.
- Screenshots for required device classes.
- Privacy manifest and data collection answers.
- Encryption/export compliance.
- Age rating.
- App icon validation.
- Build selected for submission.
- Release notes / What's New.

Before submission:

- Confirm the selected build's version/build is visible in the app.
- Confirm `CHANGELOG.md` and What's New agree.
- Confirm the latest uploaded build has finished processing.
- Confirm capability, entitlement, and provisioning profile changes are reflected in Apple Developer and App Store Connect.
- Run the app from a clean install if user data or onboarding matters.

## Acceptance Criteria

The improved bootstrap is complete when a fresh iOS repo initialized from this guide has:

- `AGENTS.md`, `HUMANS.md`, `README.md`, `CHANGELOG.md`, and `VERSION`.
- `app/ios/project.yml`.
- Visible app version/build.
- `scripts/verify-ios.sh`.
- `scripts/device-validate-ios.sh`.
- `.asc/artifacts/` ignored.
- Documented Team ID and bundle root.
- Command-line device install working.
- Launch-only retry working.
- TestFlight upload path documented.
- App Store prep checklist documented.

---

**GET-STARTED Version:** 1.0.0

**End of Guide**
