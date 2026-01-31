# Contributing to vidocs-agents

Thank you for contributing to the vidocs-agents repository! This guide will help you contribute effectively.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Contribution Types](#contribution-types)
- [Agent Contribution Guidelines](#agent-contribution-guidelines)
- [Prompt Contribution Guidelines](#prompt-contribution-guidelines)
- [Documentation Guidelines](#documentation-guidelines)
- [Pull Request Process](#pull-request-process)

## Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Focus on what is best for the community
- Show empathy towards other community members

## Getting Started

1. Fork the repository
2. Clone your fork locally
3. Create a new branch for your contribution
4. Make your changes
5. Test your changes
6. Submit a pull request

## Contribution Types

### 1. New Agents

- Add new agent configurations
- Include complete metadata
- Provide usage examples
- Document capabilities and limitations

### 2. Agent Improvements

- Update existing agents
- Improve effectiveness scores
- Add new capabilities
- Fix bugs or issues

### 3. Prompts and Templates

- Add new prompt templates
- Improve existing prompts
- Document prompt effectiveness

### 4. Documentation

- Improve README files
- Add tutorials and guides
- Fix typos and clarifications

### 5. Automation

- Enhance automation scripts
- Add new validation rules
- Improve reporting capabilities

## Agent Contribution Guidelines

### Required Components

Every agent contribution must include:

1. **Configuration File** (`agent.yml` or similar)
   - Clear agent definition
   - Capability declarations
   - Behavior settings

2. **Instructions** (`instructions.md`)
   - Purpose and use cases
   - Usage examples
   - Best practices
   - Limitations

3. **Metadata** (`metadata.json`)
   - Schema-compliant metadata
   - Initial confidence rating (0.0 for new agents)
   - Context compatibility tags
   - Author information

4. **Examples** (in `examples/` directory)
   - At least one usage example
   - Input/output samples
   - Success/failure cases

### Naming Conventions

- Use kebab-case for directories: `my-agent-name`
- Use descriptive names that indicate purpose
- Avoid overly generic names

### Testing Requirements

Before submitting:

1. Validate metadata: `python3 automation/validators/validate_metadata.py`
2. Test the agent in intended contexts
3. Document test results in examples

## Prompt Contribution Guidelines

### Prompt Structure

```markdown
# Prompt: [Name]

## Context

[What this prompt is for]

## Variables

- `{{variable1}}`: Description
- `{{variable2}}`: Description

## Usage

[Usage instructions]

## Effectiveness

- Confidence: [0.0-1.0]
- Success Rate: [%]
- Last Updated: [Date]
```

### Prompt Categories

Place prompts in appropriate directories:

- `system-prompts/`: Base system prompts
- `task-prompts/`: Task-specific prompts
- `templates/`: Reusable templates
- `chains/`: Multi-step prompt sequences

## Documentation Guidelines

### Writing Style

- Use clear, concise language
- Include code examples where appropriate
- Add diagrams for complex concepts
- Keep formatting consistent

### Documentation Structure

- Start with a clear purpose statement
- Include a table of contents for longer documents
- Use headings hierarchically
- Add links to related documentation

## Pull Request Process

### Before Submitting

1. **Validate your changes**

   ```bash
   python3 automation/validators/validate_metadata.py
   ```

2. **Update documentation**
   - Update relevant README files
   - Add entries to CHANGELOG if applicable

3. **Test thoroughly**
   - Test in multiple contexts
   - Verify examples work correctly

4. **Run analysis**
   ```bash
   REPO_ROOT=. python3 automation/scripts/analyze_agents.py
   ```

### PR Description Template

```markdown
## Description

[Brief description of changes]

## Type of Change

- [ ] New agent
- [ ] Agent improvement
- [ ] New prompt/template
- [ ] Documentation
- [ ] Automation/tooling
- [ ] Bug fix

## Checklist

- [ ] Metadata validated
- [ ] Examples provided
- [ ] Documentation updated
- [ ] Tests passed
- [ ] Related agents cross-referenced

## Testing

[Describe how you tested these changes]

## Related Issues

[Link any related issues]
```

### Review Process

1. Automated validation checks run
2. Maintainer review
3. Community feedback (if applicable)
4. Approval and merge

### After Merge

- Your contribution will be included in the next release
- Metadata will be tracked for effectiveness
- Community feedback will help improve ratings

## Questions?

- Open an issue for questions
- Tag with `question` label
- Maintainers will respond promptly

## Recognition

Contributors will be recognized in:

- README contributor section
- Release notes
- Agent metadata (author field)

Thank you for helping improve vidocs-agents! 🚀
