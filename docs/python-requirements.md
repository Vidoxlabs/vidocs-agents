# Python Version Requirements

The automation tools in this repository require **Python 3.9 or higher**.

## Why Python 3.9+?

- Uses `datetime.timezone.utc` for timezone-aware timestamps
- Modern type hints with `Dict`, `List` from `typing`
- Improved pathlib features
- Better performance

## Checking Your Python Version

```bash
python3 --version
```

## Installation

If you need to upgrade Python, visit [python.org](https://www.python.org/downloads/) or use your system's package manager:

### macOS (Homebrew)
```bash
brew install python@3.11
```

### Ubuntu/Debian
```bash
sudo apt update
sudo apt install python3.11
```

### Windows
Download from [python.org](https://www.python.org/downloads/windows/)

## Virtual Environment (Recommended)

```bash
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
```
