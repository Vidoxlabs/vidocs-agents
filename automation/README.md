# Automation

This directory contains automation tools for managing and analyzing agents in the vidocs-agents repository.

## Structure

```
automation/
├── scripts/            # Utility scripts
│   ├── analyze_agents.py
│   └── calculate_confidence.py
└── validators/         # Validation tools
    └── validate_metadata.py
```

## Installation

Install required dependencies:

```bash
pip install -r requirements.txt
```

Or install individually:
```bash
pip install jsonschema pyyaml
```

## Available Tools

### Validators

#### validate_metadata.py
Validates all metadata files against the JSON schema.

```bash
python3 automation/validators/validate_metadata.py
```

**Exit codes:**
- `0`: All files valid
- `1`: One or more files invalid

### Scripts

#### analyze_agents.py
Analyzes agent configurations for overlaps and relationships.

```bash
REPO_ROOT=. python3 automation/scripts/analyze_agents.py
```

**Outputs:**
- Console report
- `docs/cross-reference-analysis.md`

#### calculate_confidence.py
Calculates and updates confidence ratings based on usage data.

```bash
REPO_ROOT=. python3 automation/scripts/calculate_confidence.py
```

**Outputs:**
- Console updates
- `docs/confidence-ratings.md`
- Updated metadata files

## CI/CD Integration

These tools are integrated into GitHub Actions workflows:
- `.github/workflows/validate-agents.yml` - Runs on PR/push
- `.github/workflows/weekly-update.yml` - Runs weekly

## Development

### Adding New Validators

1. Create a new Python file in `validators/`
2. Implement validation logic
3. Return exit code 0 for success, 1 for failure
4. Add to CI workflow if needed

### Adding New Scripts

1. Create a new Python file in `scripts/`
2. Use the repository root pattern:
   ```python
   repo_root = os.getenv('REPO_ROOT', '.')
   ```
3. Document usage in this README
4. Consider CI/CD integration

## Documentation

See [docs/automation-guide.md](../docs/automation-guide.md) for detailed documentation.
