# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Required ongoing PRD, TDD, and related artifact synchronization at meaningful checkpoints, including the generated agent operating contract and skill wrapper.
- Expanded the guide from a three-phase bootstrap into a six-phase iOS shipping loop covering device validation, TestFlight, and App Store prep.
- Added version/build discipline, XcodeGen templates, verification scripts, device-install scripts, ASC recovery guidance, and App Store metadata checklists.
- Added repository-specific `AGENTS.md` guidance to prevent agents from bootstrapping this instruction repository in place.
- Added a visible version footer to `GET-STARTED.md`.
- CHANGELOG.md creation step in Phase 1
- Instructions to follow Keep a Changelog format and Semantic Versioning
- Reminder to maintain CHANGELOG.md throughout project lifecycle

## [1.0.0] - 2025-01-27

### Added
- Initial project bootstrap guide (GET-STARTED.md) with three-phase workflow
- README.md explaining project purpose and usage
- AGENTS.md template for AI assistant context
- HUMANS.md creation step for documenting human principals and team information
- iOS/Android directory structure clarifications (app/ios/, app/android/)
- README.md maintenance instructions throughout all phases
- URL reference option for using the guide directly from GitHub
- xcodegen tip for iOS project setup
- Task management system flexibility note

### Changed
- Updated directory structure template to include README.md, HUMANS.md, and CHANGELOG.md
- Updated AGENTS.md template to reference HUMANS.md

[Unreleased]: https://github.com/sinned/get-started/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/sinned/get-started/releases/tag/v1.0.0

