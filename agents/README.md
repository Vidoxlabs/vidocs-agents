# Agents

This directory contains generalized agent configurations that can be used across various platforms and contexts.

## Structure

```text
agents/
├── general-purpose/    # Generic multi-purpose agents
├── specialized/        # Domain-specific agents (code, docs, data, etc.)
└── experimental/       # Agents under development or testing
```

## Agent Metadata

Each agent configuration should include metadata for tracking effectiveness:

```yaml
metadata:
  name: "Agent Name"
  version: "1.0.0"
  description: "Brief description"
  confidence_rating: 0.0-1.0
  effectiveness_score: 0.0-1.0
  last_updated: "YYYY-MM-DD"
  context_compatibility:
    - "context-type-1"
    - "context-type-2"
```

## Usage

Refer to the main [README](../README.md) for detailed usage instructions.
