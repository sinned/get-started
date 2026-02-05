# Get Started - Project Bootstrap Template

**Version:** 1.0.0

This repository is a **template and starter guide** for bootstrapping new coding projects with AI assistants. It provides a structured workflow to help you and your AI coding agent (Cursor, Claude, Windsurf, etc.) initialize new projects from scratch.

## Purpose

This project contains a comprehensive guide (`GET-STARTED.md`) that outlines a proven "Stub → Artifacts → Code" workflow for starting new projects. Instead of jumping straight into code, this approach ensures proper planning and documentation before implementation.

## How to Use

1. **Read the Guide**: Open `GET-STARTED.md` to understand the three-phase workflow
2. **Start Your New Project**: Create a new repository (or use an existing empty one)
3. **Run with Your AI Assistant**: Use one of the options below (Cursor, or any assistant)
4. **Let the Workflow Guide You**: The AI will follow the structured phases to set up the skeleton, create planning documents (PRD, TDD, task lists), and implement the code

### Using in Cursor

Cursor can use the **get-started** skill so the agent knows the workflow without you pasting the whole guide.

- **In this repo:** The skill is already available. Open this repo in Cursor and say e.g. *"Follow the get-started workflow to bootstrap a new project"* or *"Use the get-started skill to initialize this repo."*
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
- **Three-Phase Workflow**:
  - **Phase 1**: Create project structure and directories
  - **Phase 2**: Build planning artifacts (PRD, TDD, task lists)
  - **Phase 3**: Implement the code based on the plan

## Workflow Overview

The guide follows a structured approach:

1. **Stub Project Structure** - Create directories and basic files without logic
2. **Build Artifacts** - Document requirements and technical design before coding
3. **Implementation** - Execute the plan with proper setup and development

This ensures your project starts with a solid foundation, clear documentation, and a well-thought-out architecture.

## Getting Started

Simply read `GET-STARTED.md` and follow its instructions with your AI coding assistant to bootstrap your next project!

---

**Note**: This repository is a template. Clone it, fork it, or use it as a reference when starting new projects with AI coding assistants.

