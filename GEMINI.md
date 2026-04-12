# Scoop Skill Project Overview

This repository contains a specialized skill for the **Gemini CLI** designed to empower the agent with expert-level capabilities for managing **Scoop**, the command-line installer for Windows.

## Project Structure

- **`SKILL.md`**: The heart of the project. It contains the metadata, triggers, and core procedural instructions that the Gemini CLI agent uses to perform Scoop operations.
- **`references/scoop-wiki/`**: A bundled mirror of the official Scoop documentation (Wiki). This provides the agent with offline access to deep technical details regarding manifests, autoupdates, and advanced configurations.
- **`README.md`**: General project information, features, and installation instructions for users.
- **`LICENSE`**: The project is licensed under **GPL-3.0**.

## Core Capabilities

The skill defined in this repository enables the agent to:
1.  **Manage Software**: Search, install, update, and uninstall Windows applications via Scoop.
2.  **Handle Shims**: Discover and manage Scoop "shims" to ensure command-line tools are correctly identified and executed.
3.  **Recover Environments**: Restore Scoop installations from manual backups or directory migrations using established community best practices.
4.  **Develop Manifests**: Create, test, and format Scoop JSON manifests using internal Scoop development scripts.

## Building and Usage

### For Users
To use this skill, add it to your Gemini CLI environment:
```bash
npx skills add <repository-url>
```

### For Developers
If you are modifying this skill:
- **Testing**: You can test the skill's instructions by triggering the "scoop" keyword in a Gemini CLI session and observing if the agent correctly follows the procedures in `SKILL.md`.
- **Updating Documentation**: The `references/scoop-wiki/` directory is a static snapshot. To update it, you can manually pull from the official Scoop Wiki repository.

## Development Conventions

- **Imperative Instructions**: `SKILL.md` uses clear, imperative language to guide the agent.
- **Local Documentation Preference**: The agent is instructed to prioritize reading files in `references/scoop-wiki/` over fetching online documentation to ensure speed and reliability.
- **Surgical Edits**: When the agent modifies manifests or configuration files, it should use targeted search and replace tools to maintain file integrity.
