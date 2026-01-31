# Automation Guide

This guide explains the automation tools available in the vidocs-agents repository.

## Overview

The automation system provides tools for:

- **Validation**: Ensuring metadata compliance
- **Analysis**: Cross-referencing agents and identifying relationships
- **Rating**: Calculating confidence and effectiveness scores
- **Reporting**: Generating insights and analytics

## Available Tools

### 1. Metadata Validator

**Purpose**: Validate all metadata files against the JSON schema

**Location**: `automation/validators/validate_metadata.py`

**Usage**:

```bash
python3 automation/validators/validate_metadata.py
```

**What it checks**:

- Schema compliance
- Required fields present
- Data type correctness
- Value constraints (e.g., ratings between 0-1)

**Output**:

```text
Validating 5 metadata files...

✓ template-agent.json is valid
✓ code-reviewer.json is valid
✓ security-scanner.json is valid
✗ broken-agent.json is invalid:
  'version' does not match pattern '^\\d+\\.\\d+\\.\\d+$'
✗ incomplete-agent.json is invalid:
  'created' is a required property

3/5 metadata files are valid
```

**Exit codes**:

- `0`: All files valid
- `1`: One or more files invalid

### 2. Agent Analyzer

**Purpose**: Analyze agent configurations for overlaps and relationships

**Location**: `automation/scripts/analyze_agents.py`

**Usage**:

```bash
REPO_ROOT=. python3 automation/scripts/analyze_agents.py
```

**Features**:

- Identifies capability overlaps
- Finds context overlaps
- Calculates agent similarity
- Suggests related agents

**Output**:

```markdown
# Agent Cross-Reference Analysis Report

Total agents analyzed: 8

## Capability Overlaps
- **code_review**: general-reviewer, security-reviewer, performance-reviewer
- **security_analysis**: security-reviewer, vulnerability-scanner

## Context Overlaps
- **pull_requests**: general-reviewer, security-reviewer, docs-reviewer
- **code_review**: general-reviewer, security-reviewer

## Related Agents
- security-reviewer ↔ vulnerability-scanner (similarity: 0.75)
- general-reviewer ↔ code-analyzer (similarity: 0.62)
- docs-generator ↔ docs-reviewer (similarity: 0.58)
```

**Use cases**:

- Finding complementary agents
- Identifying redundancy
- Discovering optimization opportunities
- Planning agent improvements

### 3. Confidence Calculator

**Purpose**: Calculate and update confidence ratings based on usage data

**Location**: `automation/scripts/calculate_confidence.py`

**Usage**:

```bash
REPO_ROOT=. python3 automation/scripts/calculate_confidence.py
```

**Algorithm**:

```python
confidence = (success_rate * 0.4) +
             (min(usage_count/100, 1.0) * 0.3) +
             (effectiveness_score * 0.3)
```

**Factors**:

- **Success Rate** (40%): Historical success percentage
- **Usage Count** (30%): Number of uses (capped at 100)
- **Effectiveness Score** (30%): Manual effectiveness rating

**Output**:

```text
Found 5 metadata files
Updated template-agent.json: 0.00 → 0.00
Updated code-reviewer.json: 0.65 → 0.72
Updated security-scanner.json: 0.45 → 0.58
Updated docs-generator.json: 0.80 → 0.85
Updated test-helper.json: 0.55 → 0.60

Confidence rating update complete!
Report saved to: docs/confidence-ratings.md
```

**Generated Report**:

```markdown
# Agent Confidence Ratings Report

| Agent            | Confidence | Effectiveness | Usage Count |
| ---------------- | ---------- | ------------- | ----------- |
| docs-generator   | 0.85       | 0.90          | 120         |
| code-reviewer    | 0.72       | 0.75          | 95          |
| test-helper      | 0.60       | 0.65          | 48          |
| security-scanner | 0.58       | 0.60          | 35          |
| template-agent   | 0.00       | 0.00          | 0           |
```

## Integration with CI/CD

### GitHub Actions Workflow

Create `.github/workflows/validate-agents.yml`:

```yaml
name: Validate Agents

on:
  pull_request:
    paths:
      - "agents/**"
      - "copilot/**"
      - "schemas/**"
  push:
    branches:
      - main

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: "3.x"

      - name: Install dependencies
        run: |
          pip install jsonschema pyyaml

      - name: Validate metadata
        run: |
          python3 automation/validators/validate_metadata.py

      - name: Analyze agents
        run: |
          REPO_ROOT=. python3 automation/scripts/analyze_agents.py

      - name: Calculate confidence
        run: |
          REPO_ROOT=. python3 automation/scripts/calculate_confidence.py

      - name: Upload reports
        uses: actions/upload-artifact@v3
        with:
          name: agent-reports
          path: docs/*.md
```

### Pre-commit Hook

Create `.git/hooks/pre-commit`:

```bash
#!/bin/bash

echo "Validating agent metadata..."
python3 automation/validators/validate_metadata.py

if [ $? -ne 0 ]; then
    echo "❌ Metadata validation failed"
    echo "Fix errors before committing"
    exit 1
fi

echo "✓ Metadata validation passed"
exit 0
```

Make executable:

```bash
chmod +x .git/hooks/pre-commit
```

## Scheduled Updates

### Weekly Confidence Updates

Run confidence calculator weekly to update ratings based on usage:

```yaml
name: Weekly Confidence Update

on:
  schedule:
    - cron: "0 0 * * 0" # Every Sunday at midnight

jobs:
  update-confidence:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: "3.x"

      - name: Install dependencies
        run: pip install jsonschema pyyaml

      - name: Update confidence ratings
        run: |
          REPO_ROOT=. python3 automation/scripts/calculate_confidence.py

      - name: Commit updates
        run: |
          git config user.name "GitHub Actions"
          git config user.email "actions@github.com"
          git add .
          git commit -m "chore: update confidence ratings" || exit 0
          git push
```

## Custom Automation

### Adding Custom Validators

Create a new validator in `automation/validators/`:

```python
#!/usr/bin/env python3
"""
Custom validator for checking agent naming conventions
"""

from pathlib import Path
import sys

def validate_naming(agent_dir: Path) -> bool:
    """Check if agent follows naming conventions"""
    name = agent_dir.name

    # Must be kebab-case
    if not all(c.islower() or c == '-' for c in name):
        print(f"✗ {name}: Must use kebab-case")
        return False

    # Must not start or end with hyphen
    if name.startswith('-') or name.endswith('-'):
        print(f"✗ {name}: Cannot start/end with hyphen")
        return False

    print(f"✓ {name}: Valid naming")
    return True

def main():
    repo_root = Path(__file__).parent.parent.parent
    agent_dirs = list(repo_root.glob("*/agents/*/"))

    valid_count = sum(1 for d in agent_dirs if validate_naming(d))

    print(f"\n{valid_count}/{len(agent_dirs)} agents have valid names")

    if valid_count < len(agent_dirs):
        sys.exit(1)

if __name__ == '__main__':
    main()
```

### Adding Custom Analysis

Extend `analyze_agents.py` with custom metrics:

```python
def analyze_effectiveness_trends(self) -> Dict:
    """Analyze effectiveness trends over time"""
    trends = []

    for agent in self.agents:
        # Compare current vs historical effectiveness
        current = agent.get('effectiveness_score', 0)
        # Could load historical data from git history
        trends.append({
            'name': agent.get('name'),
            'current_score': current,
            'trend': 'improving'  # Calculate based on history
        })

    return {'trends': trends}
```

## Troubleshooting

### Metadata Validation Fails

**Problem**: Schema validation errors

**Solution**:

1. Check the schema: `schemas/agent-metadata.schema.json`
2. Verify required fields are present
3. Check data types match schema
4. Ensure version follows semver (X.Y.Z)

### Confidence Calculation Issues

**Problem**: Confidence ratings not updating

**Solution**:

1. Verify metadata files are valid JSON
2. Check that success_rate, usage_count, and effectiveness_score are present
3. Ensure values are numeric
4. Run validator first to catch issues

### Analysis Script Errors

**Problem**: Cannot find agent files

**Solution**:

1. Set `REPO_ROOT` environment variable correctly
2. Check file extensions (.yml, .yaml, .json)
3. Ensure directory structure matches expected layout

## Best Practices

1. **Run validators before committing**
   - Catch issues early
   - Maintain data quality

2. **Update confidence regularly**
   - Weekly automated updates
   - Manual updates after significant testing

3. **Review analysis reports**
   - Look for optimization opportunities
   - Identify gaps in agent coverage

4. **Keep automation updated**
   - Update Python dependencies
   - Enhance validators as needs evolve

5. **Document custom automation**
   - Comment your scripts
   - Update this guide with new tools

## Dependencies

Required Python packages:

```bash
pip install jsonschema pyyaml
```

For development:

```bash
pip install pytest black pylint
```

## Additional Resources

- [JSON Schema Documentation](https://json-schema.org/)
- [PyYAML Documentation](https://pyyaml.org/)
- [Python jsonschema](https://python-jsonschema.readthedocs.io/)

## Support

Questions about automation? Open an issue with tag `automation`.
