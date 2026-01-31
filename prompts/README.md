# Prompts Library

A curated collection of prompts for various AI models and contexts.

## Structure

```text
prompts/
├── system-prompts/     # Base system prompts
├── task-prompts/       # Task-specific prompts
├── templates/          # Reusable prompt templates
└── chains/             # Multi-step prompt chains
```

## Prompt Format

Each prompt should include:

1. **Context**: What the prompt is designed for
2. **Variables**: Template variables that can be customized
3. **Effectiveness Metrics**: Historical performance data
4. **Version History**: Changes and improvements over time

## Example

```markdown
# Prompt: Code Review Assistant

## Context

Designed for reviewing pull requests with focus on security and best practices.

## Variables

- `{{language}}`: Programming language
- `{{context}}`: Additional context about the codebase

## Effectiveness

- Confidence: 0.85
- Success Rate: 92%
- Last Updated: 2026-01-31
```
