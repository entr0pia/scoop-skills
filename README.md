# Scoop Skill for Gemini CLI

A specialized skill for the Gemini CLI agent to manage Windows packages using the [Scoop](https://scoop.sh/) command-line installer.

## Features

- **Automated Package Management**: Search, install, update, and uninstall Windows applications.
- **Shim Discovery & Management**: Deep visibility into Scoop's "shim" system, allowing the agent to find and execute installed CLI tools accurately.
- **Environment Recovery**: Built-in knowledge for restoring Scoop from manual backups or directory moves (based on GitHub Issue #2894).
- **Manifest Development**: Tools and references for creating, testing, and formatting Scoop application manifests.
- **Offline Documentation**: Bundled with a local mirror of the [Official Scoop Wiki](https://github.com/ScoopInstaller/Scoop/wiki) in the [`/references/scoop-wiki/`](/references/scoop-wiki/) directory.

## Installation

To add this skill to your Gemini CLI environment:

1. Run the following command:
   ```bash
   npx skills add https://github.com/entr0pia/scoop-skills -g
   ```
2. The agent will automatically recognize the `SKILL.md` and begin using it when Scoop-related tasks are requested.

## Usage

Once installed, the agent will trigger this skill when you ask to:
- "Install git using scoop"
- "How do I restore my scoop backup from C:\backup\scoop?"
- "What shims are currently available?"
- "Create a manifest for this new CLI tool"
- "Update all my scoop apps"

## Bundled Documentation

This repository includes a snapshot of the official Scoop documentation to ensure the agent has expert-level knowledge even without internet access:
- [`/references/scoop-wiki/App-Manifests.md`](/references/scoop-wiki/App-Manifests.md): Core manifest specification.
- [`/references/scoop-wiki/App-Manifest-Autoupdate.md`](/references/scoop-wiki/App-Manifest-Autoupdate.md): Automated update logic.

## License

GPL-3.0
