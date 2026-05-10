## MODIFIED Requirements

### Requirement: Scan available shims
The system SHALL scan all available Scoop shims using `scoop shim list` AND scan PATH for additional tools.

#### Scenario: User requests available tools
- **WHEN** user asks "what tools are available" or "what commands can I use"
- **THEN** system runs `scoop shim list` to get all shims
- **AND** system scans PATH for Scoop-related directories
- **AND** system combines results and deduplicates

### Requirement: Analyze each shim
The system SHALL analyze each shim using `--help`, `scoop info`, AND `scoop shim info` to understand its purpose and source.

#### Scenario: Analyze shim value
- **WHEN** system has list of shims (from shim list and PATH)
- **THEN** system runs `<cmd> --help` and `scoop info <cmd>` for each command
- **AND** system runs `scoop shim info <cmd>` to get source package
- **AND** system determines if command is a valuable command-line tool (not TUI/GUI)

### Requirement: Write to global memory
The system SHALL write discovered tools to global memory in a comment block with source information.

#### Scenario: Update global memory
- **WHEN** system has identified valuable command-line tools
- **THEN** system writes to global memory file in format:
```
<!-- scoop-shims start -->
This block contains command-line tools discovered from Scoop:
- cmd1: short description (from package1)
- cmd2: short description (from package2)
<!-- scoop-shims end -->
```

### Requirement: One line per tool
Each tool SHALL be documented in a single line format with source information.

#### Scenario: Compact format with source
- **WHEN** writing tool to global memory
- **THEN** each tool uses exactly one line
- **AND** format is `- cmd: short description (from package)`
- **AND** source package is included in parentheses
