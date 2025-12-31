# Clean Project Restart Guide

This guide contains instructions to bootstrap a new application project from scratch. It follows a "Stub -> Artifacts -> Code" workflow to ensure the project is well-planned before implementation.

**Usage:**
Pass this file to your AI assistant (Antigravity/Claude/Cursor/Windsurf) and ask it to: "Follow the instructions in INITIALIZE_CLEAN_PROJECT.md to initialize the repository."

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
     └── AGENTS.md                # This file
     ```

     ## Architecture
     *To be defined in Phase 2.*

     ## Code Conventions
     *To be defined in Phase 2.*
     ```

3. **Stub Directories**
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
4.  **Create `artifacts/task.md`**: Create a checklist of tasks to implement the MVP. (Note: If the assistant has their own task management system, they can use that instead of creating this file.)

## Phase 3: Implementation

**Goal:** Execute the plan defined in Phase 2.

1.  **Setup Development Environment**:
    - Initialize `server` (e.g., `npm init`) if required by TDD.
    - Initialize `app` project:
      - iOS: Create Xcode project in `app/ios/`
      - Android: Create Android project in `app/android/`
      - Web: Initialize web project in `app/web/` (e.g., `npx create-react-app app/web`)
      - Cross-platform: Use framework-specific commands (e.g., `flutter create` in `app/`)

2.  **Execute Tasks**:
    - Follow `artifacts/task.md` to build the features.
    - Create `artifacts/implementation_plan.md` for complex steps.

---

**End of Guide**
