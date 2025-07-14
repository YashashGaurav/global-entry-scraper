# global-entry-scraper

Scraper for [Global Entry](https://www.cbp.gov/travel/trusted-traveler-programs/global-entry) appointments so that you can find timeslots at hotly contested locations.

## Prerequisites

- Python 3.8+
- [UV](https://docs.astral.sh/uv/) - Fast Python package manager

## Installation

### 1. Install UV
```bash
# On macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Or with Homebrew (macOS)
brew install uv
```

### 2. Setup Project
```bash
# Clone the repo locally
git clone <your-repo-url>
cd global-entry-scraper

# UV will automatically create a virtual environment and install dependencies
uv sync
```

## Usage

1. ~~Clone the repo locally.~~ *(Already covered in Installation)*
2. Create a `config.py` file with a single line, defining a string `WEBHOOK_URL` with the value of the Discord webhook URL.
3. Run it from the command line using UV. It takes the following parameters:

- `--location-ids`, a space-separated list of location ids to check for appointments.
- `--before`, a YYYY-MM-DD formatted date to filter appointment lookups (only appointments before this date will be returned).
- `--limit`, the number of **open** appointments per location to retrieve.
- `--silent`, flag to suppress messages when there are no open timeslots.

Example usage:
```bash
uv run python main.py --location-ids 5140 5444 --before 2023-01-01 --limit 5 --silent
```

The script, of course, can be modified to provide notifications other than Discord messages.

## Development

```bash
# Add new dependencies
uv add <package-name>

# Add development dependencies  
uv add --dev <package-name>

# Run the scraper in development
uv run python main.py --location-ids 5446 --before 2025-08-21 --limit 5
```

## Security Note

⚠️ **Important**: Keep your `config.py` file out of version control. Consider using environment variables for production:

```python
import os
WEBHOOK_URL = os.getenv('DISCORD_WEBHOOK_URL', 'your-fallback-url')
```

## Location IDs

Each location has a unique numeric ID. They can be found at [this link](https://ttp.cbp.dhs.gov/schedulerapi/locations/?temporary=false&inviteOnly=false&operational=true&serviceName=Global%20Entry). A list is below: