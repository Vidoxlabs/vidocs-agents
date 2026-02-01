# Repository Structure Guide

This document outlines the organization of the `vidocs-agents` repository. Maintain this structure to ensure agents are discoverable and automatable.

## 📂 Top Level Directories

### `agents/`

The core logic definitions for AI agents.

- **`general-purpose/`**: Agents that can work on any project (e.g., Doc Sentinel).
- **`specialized/`**: Agents with deep domain expertise (e.g., Frontend Architect, Security Guardian).
- **`experimental/`**: Agents in testing/beta.

### `instructions/`

Knowledge injection files.

- **`context-overlays/`**: Project-specific context (e.g., `vidoxlabs-studio.md`) to specialize general agents.
- **`tech-stacks/`**: Reusable guides for specific technologies (React, Python, Docker).

### `prompts/`

Ready-to-use prompts for users.

- **`chains/`**: Multi-step reasoning prompts (Chain of Thought).
- **`system-prompts/`**: Raw system instructions for copying into LLMs.
- **`task-prompts/`**: Quick-fire prompts for specific tasks (e.g., "Debug this").

### `copilot/`

Configurations for GitHub Copilot.

- **`collections/`**: Groups of related prompts/instructions.
- **`examples/`**: Demo files.

### `automation/`

Python scripts for validating and maintaining the repo.

- **`validators/`**: Scripts to check JSON schemas and link validity.

## 🏷️ Naming Conventions

- **Directories**: kebab-case (`frontend-architect`).
- **Files**: kebab-case (`agent.md`, `metadata.json`).
- **IDs**: specific-generic (`frontend-architect`, not `architect-frontend`).
