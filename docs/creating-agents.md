# Creating Agents Guide

This guide walks you through creating effective agents for the vidocs-agents repository.

## Overview

An agent is a configured AI assistant designed for specific tasks or contexts. Each agent consists of:
- Configuration defining behavior and capabilities
- Instructions explaining usage
- Metadata tracking effectiveness
- Examples demonstrating usage

## Step-by-Step Process

### 1. Choose Agent Type

**GitHub Copilot Agent**
- Location: `copilot/agents/`
- Best for: GitHub-specific tasks, code generation, PR reviews
- Template: `copilot/examples/template-agent/`

**Generalized Agent**
- Location: `agents/`
- Best for: Platform-agnostic tasks, general purpose
- Subdirectories: `general-purpose/`, `specialized/`, `experimental/`

### 2. Create Directory Structure

```bash
mkdir -p copilot/agents/my-new-agent/examples
cd copilot/agents/my-new-agent
```

### 3. Create Configuration File

**agent.yml** example:

```yaml
name: code-review-security
description: Security-focused code review agent
version: 1.0.0

agent:
  type: copilot
  model: gpt-4
  temperature: 0.3  # Lower for more consistent security checks
  max_tokens: 2000

capabilities:
  - security_analysis
  - code_review
  - vulnerability_detection

context:
  max_files: 5
  max_tokens: 8000

behavior:
  verbose: true
  include_reasoning: true
  suggest_alternatives: true
  focus_areas:
    - injection_attacks
    - authentication
    - data_validation
```

### 4. Write Instructions

**instructions.md** template:

```markdown
# [Agent Name] Instructions

## Purpose
[Clear statement of what this agent does]

## When to Use
- Scenario 1
- Scenario 2
- Scenario 3

## Capabilities
- Capability 1: [Description]
- Capability 2: [Description]

## Usage

### Basic Example
\```
[Show basic usage]
\```

### Advanced Example
\```
[Show advanced usage]
\```

## Best Practices
1. [Practice 1]
2. [Practice 2]

## Limitations
- [Limitation 1]
- [Limitation 2]

## Related Agents
- [Other Agent](../other-agent/)

## Feedback
Please report effectiveness at [link to issue template]
```

### 5. Create Metadata

**metadata.json**:

```json
{
  "name": "code-review-security",
  "version": "1.0.0",
  "description": "Security-focused code review agent",
  "created": "2026-01-31T18:00:00Z",
  "updated": "2026-01-31T18:00:00Z",
  "confidence_rating": 0.0,
  "effectiveness_score": 0.0,
  "success_rate": 0,
  "usage_count": 0,
  "context_compatibility": [
    "pull_requests",
    "code_review",
    "security_audit"
  ],
  "tags": [
    "security",
    "code-review",
    "vulnerability"
  ],
  "author": "Your Name",
  "related_agents": [
    "general-code-review",
    "security-scanner"
  ],
  "dependencies": [
    "static-analysis-tools"
  ]
}
```

### 6. Add Examples

**examples/example-1.md**:

```markdown
# Security Review Example

## Input
\```python
def login(username, password):
    query = f"SELECT * FROM users WHERE username='{username}' AND password='{password}'"
    return db.execute(query)
\```

## Agent Response
\```
⚠️ SQL Injection Vulnerability Detected

The code is vulnerable to SQL injection attacks because it uses string 
interpolation to construct SQL queries.

Recommendation:
- Use parameterized queries
- Implement input validation
- Use ORM framework

Fixed Code:
\```python
def login(username, password):
    query = "SELECT * FROM users WHERE username=? AND password=?"
    return db.execute(query, (username, password))
\```
\```

## Effectiveness
- ✓ Correctly identified vulnerability
- ✓ Provided accurate fix
- ✓ Explained security implications
```

### 7. Validate

```bash
# Validate metadata schema
python3 automation/validators/validate_metadata.py

# Check for issues
python3 automation/scripts/analyze_agents.py
```

### 8. Test the Agent

1. Use the agent in real scenarios
2. Document results in examples
3. Update effectiveness scores based on performance
4. Iterate on configuration

## Configuration Best Practices

### Temperature Settings
- **0.0-0.3**: Consistent, deterministic (security, validation)
- **0.4-0.7**: Balanced (general purpose)
- **0.8-1.0**: Creative (ideation, brainstorming)

### Context Windows
- Keep reasonable limits to avoid token exhaustion
- Balance between context and responsiveness

### Capabilities
- Be specific about what the agent can do
- Don't over-promise capabilities
- Focus on 3-5 core capabilities

## Metadata Guidelines

### Confidence Rating
- Start at 0.0 for new agents
- Let the automation calculate based on usage
- Update after significant testing

### Context Compatibility
Use standardized context tags:
- `code_review`
- `security_audit`
- `documentation`
- `testing`
- `deployment`
- `debugging`

### Tags
- Use lowercase, hyphenated tags
- Include domain tags (language, framework)
- Include task tags (refactoring, analysis)

## Iterating on Agents

### Collecting Feedback
1. Create GitHub issues for feedback
2. Track success/failure cases
3. Monitor effectiveness scores

### Updating Agents
1. Increment version number (semantic versioning)
2. Update `updated` timestamp
3. Document changes in examples
4. Re-validate with automation

### Deprecating Agents
1. Mark as deprecated in metadata
2. Suggest replacement agents
3. Keep for historical reference

## Common Pitfalls

❌ **Too Generic**
- Agent tries to do everything
- Better to have focused, specialized agents

❌ **Insufficient Examples**
- Users don't understand how to use the agent
- Provide diverse examples

❌ **Outdated Metadata**
- Confidence ratings not updated
- Run automation regularly

❌ **Missing Context Tags**
- Agent hard to discover
- Add comprehensive compatibility tags

## Advanced Topics

### Multi-Agent Workflows
- Design agents that complement each other
- Use `related_agents` field
- Document workflow in instructions

### Prompt Chaining
- Break complex tasks into steps
- Reference prompts from `prompts/chains/`
- Document the chain in agent instructions

### Custom Validators
- Add custom validation in `automation/validators/`
- Hook into CI/CD pipeline
- Document validation requirements

## Resources

- [Metadata Schema](../schemas/agent-metadata.schema.json)
- [Template Agent](../copilot/examples/template-agent/)
- [Contributing Guide](../CONTRIBUTING.md)

## Support

Questions? Open an issue with the `question` tag.

Happy agent building! 🤖
