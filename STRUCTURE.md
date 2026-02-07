# Repository Structure Guide

This document outlines the organization of the `vidocs-agents` repository. Maintain this structure to ensure agents are discoverable and automatable.

## 📂 Top Level Directories

### `agents/`

The core AI agent configurations organized by domain expertise.

- **`backend/`**: Backend architecture and development agents
- **`core/`**: Core functionality agents (code review, documentation, etc.)
- **`data/`**: Data management and optimization agents
- **`devops/`**: DevOps, infrastructure, and operations agents
- **`web/`**: Frontend and web development agents
- **`template-agent/`**: Template structure for creating new agents

### `instructions/`

Context and knowledge injection files.

- **`context-overlays/`**: Project-specific context to specialize agents (e.g., `vidoxlabs-studio.md`)

### `prompts/`

Reusable prompt library and templates.

- **`chains/`**: Multi-step reasoning prompts (Chain of Thought)
- **`system-prompts/`**: Base system instructions
- **`task-prompts/`**: Quick-fire prompts for specific tasks
- **`templates/`**: Reusable prompt templates

### `automation/`

Python scripts for validation and repository maintenance.

- **`scripts/`**: Utility scripts for analysis and processing
- **`validators/`**: Scripts to check JSON schemas and metadata validity

## 🏷️ Naming Conventions

- **Directories**: kebab-case (`frontend-architect`).
- **Files**: kebab-case (`agent.md`, `metadata.json`).
- **IDs**: specific-generic (`frontend-architect`, not `architect-frontend`).
