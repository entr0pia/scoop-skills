## ADDED Requirements

### Requirement: Append new tools to global memory
The system SHALL append newly installed or created tools to global memory after `scoop install` or `scoop shim add` operations.

#### Scenario: After scoop install
- **WHEN** user runs `scoop install <app>`
- **THEN** system analyzes the installed app
- **AND** system appends to `~/.config/opencode/AGENTS.md` if it's a valuable command-line tool

#### Scenario: After scoop shim add
- **WHEN** user runs `scoop shim add <name> <path>`
- **THEN** system analyzes the new shim
- **AND** system appends to `~/.config/opencode/AGENTS.md` if it's a valuable command-line tool

### Requirement: Use same format as discover-shims
New tools SHALL use the same format: `cmd：简短说明`.

#### Scenario: Consistent format
- **WHEN** appending new tool to global memory
- **THEN** format matches discover-shims: `cmd：简短说明`
- **AND** tool is added inside `<!-- scoop-shims -->` comment block
