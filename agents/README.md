# Agents

This directory contains domain-specific AI agent configurations organized by expertise area.

## Structure

```text
agents/
├── backend/           # Backend architecture and development agents
├── core/              # Core functionality agents (code review, documentation)
├── data/              # Data management and optimization agents
├── devops/            # DevOps, infrastructure, and operations agents
├── web/               # Frontend and web development agents
└── template-agent/    # Template for creating new agents
```

## Agent Structure

Each agent should include:

- **`agent.yml`**: Configuration file with agent definition, capabilities, and behavior settings
- **`instructions.md`**: Detailed usage guide, examples, and best practices
- **`metadata.json`**: Metadata including version, ratings, and tags
- **`examples/`**: Directory with at least one usage example

## Agent Metadata

Each agent configuration includes metadata for tracking effectiveness:

```json
{
  "name": "agent-name",
  "version": "1.0.0",
  "description": "Brief description",
  "confidence_rating": 0.0,
  "effectiveness_score": 0.0,
  "context_compatibility": ["context-type-1", "context-type-2"],
  "tags": ["tag1", "tag2"]
}
```

## Usage

Refer to the main [README](../README.md) for detailed usage instructions.

For creating new agents, see [Creating Agents Guide](../docs/creating-agents.md).
