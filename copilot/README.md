# GitHub Copilot Configurations

This directory houses GitHub Copilot-specific configurations, including custom agents, prompts, and instructions.

## Directory Structure

```
copilot/
├── agents/             # GitHub Copilot custom agents
├── prompts/            # System prompts and prompt templates
├── instructions/       # Task-specific instructions
└── examples/           # Example configurations and use cases
```

## GitHub Copilot Agent Structure

Each agent should follow this structure:

```
agent-name/
├── agent.yml           # Agent definition and configuration
├── instructions.md     # Detailed instructions for the agent
├── metadata.json       # Tracking and rating metadata
└── examples/           # Example inputs/outputs
```

## Creating a New Agent

1. Copy the template from `examples/template-agent/`
2. Update the agent.yml with your configuration
3. Write clear instructions in instructions.md
4. Add metadata.json with initial ratings
5. Test the agent and update effectiveness scores

## Metadata Schema

See [../schemas/agent-metadata.schema.json](../schemas/agent-metadata.schema.json) for the complete metadata schema.
