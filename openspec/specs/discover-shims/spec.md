## ADDED Requirements

### Requirement: Scan available shims
The system SHALL scan all available Scoop shims using `scoop shim list`.

#### Scenario: User requests available tools
- **WHEN** user asks "what tools are available" or "what commands can I use"
- **THEN** system runs `scoop shim list` to get all shims

### Requirement: Analyze each shim
The system SHALL analyze each shim using `--help` and `scoop info` to understand its purpose.

#### Scenario: Analyze shim value
- **WHEN** system has list of shims
- **THEN** system runs `<cmd> --help` and `scoop info <cmd>` for each shim
- **AND** system determines if shim is a valuable command-line tool (not TUI/GUI)

### Requirement: Write to global memory
The system SHALL write discovered tools to global AGENTS.md in a comment block.

#### Scenario: Update global memory
- **WHEN** system has identified valuable command-line tools
- **THEN** system writes to `~/.config/opencode/AGENTS.md` in format:
```
<!-- scoop-shims 开始 -->
cmd1：简短说明
cmd2：简短说明
<!-- scoop-shims 结束 -->
```

### Requirement: One line per tool
Each tool SHALL be documented in a single line format: `cmd：简短说明`.

#### Scenario: Compact format
- **WHEN** writing tool to global memory
- **THEN** each tool uses exactly one line
- **AND** format is `cmd：简短说明` (colon with space)
