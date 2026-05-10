# Scoop Skills for AI Agent

A collection of specialized skills for AI agents to manage Windows packages using [Scoop](https://scoop.sh/) command-line installer.

## Skills

### [scoop-skills](skills/scoop-skills/SKILL.md)
Core skill for Scoop package management:
- **Package Management**: Search, install, update, and uninstall Windows applications
- **Shim Management**: Discover and manage Scoop "shims" for CLI tools
- **Environment Recovery**: Restore Scoop from manual backups or directory moves
- **Manifest Development**: Create, test, and format Scoop application manifests
- **Offline Documentation**: Bundled mirror of [Official Scoop Wiki](skills/scoop-skills/references/scoop-wiki/)

### [discover-shims](skills/discover-shims/SKILL.md)
Discover available command-line tools:
- **Shim Scanning**: Scan all available Scoop shims
- **Tool Analysis**: Use `--help` and `scoop info` to understand each tool
- **Global Memory**: Write valuable tools to Agent's global memory for future reference

## Installation

```bash
npx skills add https://github.com/entr0pia/scoop-skills -g
```

The agent will automatically recognize the skills and use them when appropriate.

## Usage

The agent will trigger skills when you ask:
- "Install git using scoop"
- "What tools are available?"
- "How do I restore my scoop backup?"
- "Create a manifest for this new CLI tool"

## Project Structure

```
scoop-skills/
├── skills/
│   ├── scoop-skills/          # Core Scoop management skill
│   │   ├── SKILL.md
│   │   └── references/        # Offline Scoop documentation
│   │       └── scoop-wiki/
│   └── discover-shims/        # Shim discovery skill
│       └── SKILL.md
├── openspec/                  # OpenSpec workflow configuration
└── .opencode/                 # OpenCode plugin configuration
```

## License

GPL-3.0
