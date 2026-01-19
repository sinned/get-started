# Clean Project Restart Guide

This guide contains instructions to bootstrap a new application project from scratch. It follows a "Stub -> Artifacts -> Code" workflow to ensure the project is well-planned before implementation.

**Usage:**
Pass this file to your AI assistant (Antigravity/Claude/Cursor/Windsurf) and ask it to: "Follow the instructions in GET-STARTED.md to initialize the repository."

Alternatively, you can reference this guide directly via URL:
- Share this URL with your AI assistant: `https://raw.githubusercontent.com/sinned/get-started/refs/heads/main/GET-STARTED.md`
- Ask it to: "Follow the instructions in the document at that URL to initialize the repository."

---

## Phase 1: Stub Project Structure

**Goal:** Create the skeleton of the project without implementing specific logic.

1. **Initialize Repository**
   - Run `git init` (if not already initialized).
   - Create `.gitignore`:
     ```text
     node_modules
     dist
     .env
     .DS_Store
     *.log
     ```

2. **Create `AGENTS.md`**
   - Create `AGENTS.md` in the root. This file serves as the primary context for AI assistants to understand the project.
   - Use this generic template:
     ```markdown
     # AGENTS.md - AI Assistant Guide

     **Last Updated:** [Date]
     **Repository:** [Project Name]

     ---

     ## Directory Structure

     ```
     [project-root]/
     ├── app/                     # Main Application Code
     │   ├── ios/                 # iOS Application (if applicable)
     │   ├── android/             # Android Application (if applicable)
     │   └── web/                 # Web Application (if applicable)
     ├── server/                  # Backend Server (Optional)
     ├── artifacts/               # Project Documentation (PRDs, TDDs, Logs)
     ├── README.md                # Project README (keep updated)
     ├── CHANGELOG.md             # Changelog (Keep a Changelog format)
     ├── VERSION                  # Current version number
     ├── HUMANS.md                # Human principals and team information
     └── AGENTS.md                # This file
     ```

     **Note:** See `HUMANS.md` for information about the human principals directing and operating this project (e.g., names, Apple Team ID, Bundle Root, etc.).

     ## Architecture
     *To be defined in Phase 2.*

     ## Code Conventions
     *To be defined in Phase 2.*

     ## Tooling
     - iOS projects should use `xcodegen` to generate and maintain the Xcode project file in `app/ios/`.
     ```

3. **Create `README.md`**
   - Create a `README.md` at the root level with basic project information.
   - Keep this file updated throughout all phases as the project evolves.

4. **Create `HUMANS.md`**
   - Create a `HUMANS.md` at the root level to document information about the human principals directing and operating the project.
   - Include information such as:
     - Names of principals
     - Apple Team ID (for iOS development)
     - Bundle Root (for iOS development)
     - Any other relevant human/team identifiers needed for development

5. **Create `CHANGELOG.md`**
   - Create a `CHANGELOG.md` at the root level to track all notable changes to the project.
   - Follow the format specified in [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
   - Use [Semantic Versioning](https://semver.org/spec/v2.0.0.html) for version numbers (MAJOR.MINOR.PATCH).
   - Start with an "Unreleased" section for changes that haven't been released yet.
   - Keep this file updated throughout all phases as changes are made.

6. **Create `VERSION`**
   - Create a `VERSION` file at the root level containing the current version number (e.g., `1.0.0`).
   - Update this file whenever you release a new version following Semantic Versioning.
   - This provides a single source of truth for the project version.

7. **Stub Directories**
   - Create the following empty directories:
     - `app/` (and subdirectories as needed: `app/ios/`, `app/android/`, `app/web/`)
     - `server/`
     - `artifacts/`

## Phase 2: Build Artifacts

**Goal:** Understand the product idea and plan the technical implementation *before* writing code.

**STOP AND ASK THE USER:**
> "The project skeleton is ready. What is the product idea you want to build? Please describe the features and goals."

**Once the user responds:**

1.  **Create `artifacts/prd.md`**: Document the Product Requirements based on user input.
2.  **Create `artifacts/tdd.md`**: Create a Technical Design Document outlining the architecture (e.g., Tech stack for `app/`, backend requirements, database choices).
3.  **Update `AGENTS.md`**: Fill in the "Architecture" and "Code Conventions" sections based on the TDD.
4.  **Update `README.md`**: Add project description, features, and setup instructions based on the PRD and TDD.
5.  **Create `artifacts/task.md`**: Create a checklist of tasks to implement the MVP. (Note: If the assistant has their own task management system, they can use that instead of creating this file.)

## Phase 3: Implementation

**Goal:** Execute the plan defined in Phase 2.

1.  **Setup Development Environment**:
    - Initialize `server` (e.g., `npm init`) if required by TDD.
    - Initialize `app` project:
      - iOS: Use `xcodegen` to generate and maintain the Xcode project file in `app/ios/`
      - Android: Create Android project in `app/android/`
      - Web: Initialize web project in `app/web/` (e.g., `npx create-react-app app/web`)
      - Cross-platform: Use framework-specific commands (e.g., `flutter create` in `app/`)

2.  **Execute Tasks**:
    - Follow `artifacts/task.md` to build the features.
    - Create `artifacts/implementation_plan.md` for complex steps.
    - **Keep `README.md` updated** as you implement features, add setup instructions, and document the current state of the project.
    - **Keep `CHANGELOG.md` updated** following [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format and [Semantic Versioning](https://semver.org/spec/v2.0.0.html) as you make changes and release versions.

---

**End of Guide**
