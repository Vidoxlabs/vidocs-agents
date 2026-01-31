# vidocs-agents

The centralized agent-align configuration documents for Vidoxlabs. Unified intelligence repository housing Copilot agents, generalized agents, system prompts, and architectural context for current working and prior ecosystem(s).

## 📋 Overview

This repository serves as a central hub for:

- **GitHub Copilot Configurations**: Custom agents, prompts, and instructions
- **Generalized Agents**: Platform-agnostic agent configurations
- **System Prompts**: Reusable prompt templates and chains
- **Instructions**: Task-specific workflow documentation
- **Automation**: Tools for cross-referencing and effectiveness tracking

## 🗂️ Repository Structure

```text
vidocs-agents/
├── agents/                     # Generalized agent configurations
│   ├── general-purpose/        # Multi-purpose agents
│   ├── specialized/            # Domain-specific agents
│   └── experimental/           # Agents under development
├── copilot/                    # GitHub Copilot specific
│   ├── agents/                 # Copilot custom agents
│   ├── prompts/                # Copilot prompts
│   ├── instructions/           # Copilot instructions
│   └── examples/               # Example configurations
├── prompts/                    # Prompt library
│   ├── system-prompts/         # Base system prompts
│   ├── task-prompts/           # Task-specific prompts
│   ├── templates/              # Reusable templates
│   └── chains/                 # Multi-step prompt chains
├── instructions/               # General instructions
│   ├── development/            # Development workflows
│   ├── deployment/             # Deployment procedures
│   ├── testing/                # Testing strategies
│   └── maintenance/            # Maintenance procedures
├── schemas/                    # JSON schemas for validation
├── automation/                 # Automation tools
│   ├── scripts/                # Utility scripts
│   └── validators/             # Validation tools
└── docs/                       # Generated documentation
```

## 🚀 Quick Start

### Using an Agent

1. Browse the available agents in `agents/` or `copilot/agents/`
2. Review the agent's `instructions.md` for usage details
3. Check the `metadata.json` for confidence and effectiveness ratings
4. Use the agent configuration in your workflow

### Creating a New Agent

1. Copy the template from `copilot/examples/template-agent/`
2. Customize the `agent.yml` configuration
3. Write detailed instructions in `instructions.md`
4. Add initial `metadata.json` with baseline ratings
5. Test and iterate, updating effectiveness scores

### Running Automation

```bash
# Validate all metadata files
python3 automation/validators/validate_metadata.py

# Analyze agent cross-references
REPO_ROOT=. python3 automation/scripts/analyze_agents.py

# Calculate and update confidence ratings
REPO_ROOT=. python3 automation/scripts/calculate_confidence.py
```

## 📊 Metadata and Ratings

Each agent includes metadata for tracking:

- **Confidence Rating** (0.0-1.0): Overall confidence in agent performance
- **Effectiveness Score** (0.0-1.0): Measured effectiveness
- **Success Rate** (%): Historical success percentage
- **Usage Count**: Number of times used
- **Context Compatibility**: Compatible contexts/environments

### Rating Formula

```python
confidence = (success_rate * 0.4) +
             (min(usage_count/100, 1.0) * 0.3) +
             (effectiveness_score * 0.3)
```

## 🔄 Automation Features

### Cross-Reference Analysis

Identifies overlapping capabilities, complementary agents, and optimization opportunities.

### Confidence Calculation

Automatically updates confidence ratings based on usage data and effectiveness scores.

### Metadata Validation

Ensures all agent metadata conforms to the defined schema.

## 📖 Documentation

- [Agent Creation Guide](docs/creating-agents.md)
- [Metadata Schema](schemas/agent-metadata.schema.json)
- [Automation Guide](docs/automation-guide.md)
- [Contributing Guidelines](CONTRIBUTING.md)

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Contribution Workflow

1. Create a new branch for your agent/prompt
2. Follow the template structure
3. Include comprehensive metadata
4. Validate with automation tools
5. Submit a pull request with examples

## 📈 Reporting and Analytics

Generated reports include:

- Cross-reference analysis
- Confidence ratings
- Effectiveness trends
- Usage statistics

Reports are automatically generated in the `docs/` directory.

## 🔒 Best Practices

1. **Keep metadata updated**: Regularly update effectiveness and confidence scores
2. **Document thoroughly**: Include clear instructions and examples
3. **Test extensively**: Validate agents in multiple contexts
4. **Version carefully**: Use semantic versioning for agent updates
5. **Cross-reference**: Link related agents and complementary configurations

## 📝 License

[Specify your license here]

## 🙋 Support

For questions or issues, please open an issue in this repository.

---

**Vidoxlabs** - Building intelligent agent ecosystems
