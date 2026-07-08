# Get Started - Project Bootstrap Template

**Version:** 1.0.0

This repository is a **template and starter guide** for bootstrapping new coding projects with AI assistants. It provides a structured workflow to help you and your AI coding agent (Cursor, Claude, Windsurf, etc.) initialize new app repositories and set up the loop from planning through iOS device validation, TestFlight, and App Store prep.

## Purpose

This project contains a comprehensive guide (`GET-STARTED.md`) that expands the proven "Stub → Artifacts → Code" workflow into a practical shipping loop. Instead of jumping straight into code, this approach ensures proper planning, documentation, verification, device iteration, and distribution prep.

## How to Use

1. **Read the Guide**: Open `GET-STARTED.md` to understand the full shipping-loop workflow
2. **Start Your New Project**: Create a new repository (or use an existing empty one)
3. **Run with Your AI Assistant**: Use one of the options below (Cursor, or any assistant)
4. **Let the Workflow Guide You**: The AI will follow the structured phases to set up the skeleton, create planning documents (PRD, TDD, task lists), implement the code, validate on device, and prepare distribution lanes

### Using in Cursor

Cursor can use the **get-started** skill so the agent knows the workflow without you pasting the whole guide.

- **In this repo:** The skill source is available for editing and packaging. This repository stores the instructions; do not initialize this repository as if it were the target app.
- **In any other project:** Install the skill globally so it’s available everywhere:
  1. Copy the skill folder to your global Cursor skills directory:
     ```bash
     mkdir -p ~/.cursor/skills
     cp -r .cursor/skills/get-started ~/.cursor/skills/
     ```
  2. In your new or empty project, ask Cursor to follow the get-started workflow. The agent will use the skill and fetch the full guide from the URL below when it needs the exact templates.
- **Without the skill:** Share the guide with the agent by reference. In any project, you can say: *"Follow the instructions in the document at this URL to initialize the repository: https://raw.githubusercontent.com/sinned/get-started/refs/heads/main/GET-STARTED.md"*

## What's Included

- **GET-STARTED.md**: A step-by-step guide that AI assistants can follow to bootstrap new projects
- **Six-Phase Workflow**:
  - **Phase 1**: Create the repo skeleton and operating contracts
  - **Phase 2**: Build product and technical artifacts (PRD, TDD, task lists)
  - **Phase 3**: Implement the code with repeatable verification
  - **Phase 4**: Iterate quickly on a real iOS device
  - **Phase 5**: Distribute through TestFlight
  - **Phase 6**: Prepare for App Store submission

## Workflow Overview

The guide follows a structured approach:

1. **Repo Skeleton** - Create directories, basic files, and agent contracts without product logic
2. **Product + Technical Artifacts** - Document requirements and technical design before coding
3. **Implementation** - Execute the plan with proper setup and verification
4. **Fast iOS Device Iteration** - Build, install, launch, and validate from the command line
5. **TestFlight Distribution** - Archive, upload, process, and assign builds
6. **App Store Submission Prep** - Prepare metadata, compliance, screenshots, and selected builds

This ensures your project starts with a solid foundation, clear documentation, repeatable verification, and a path to real-device validation and distribution.

## Getting Started

Simply read `GET-STARTED.md` and follow its instructions with your AI coding assistant to bootstrap your next project!

---

**Note**: This repository stores the template and skill source. Clone it, fork it, or use it as a reference when starting new projects with AI coding assistants, but run the bootstrap workflow in the target app repository.

