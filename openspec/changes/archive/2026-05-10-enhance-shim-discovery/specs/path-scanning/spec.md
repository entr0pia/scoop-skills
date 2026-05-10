## ADDED Requirements

### Requirement: Scan PATH for Scoop tools
The system SHALL scan PATH environment variable to discover Scoop-installed tools not exposed via shims.

#### Scenario: Extract Scoop-related paths
- **WHEN** scanning for available tools
- **THEN** system extracts paths from `$env:PATH` containing "scoop"
- **AND** filters to include only `~\scoop\apps\*\current\` patterns

### Requirement: List executables in PATH directories
The system SHALL list executable files in Scoop-related PATH directories.

#### Scenario: Find executables in PATH
- **WHEN** system has identified Scoop-related PATH directories
- **THEN** system lists `.exe`, `.cmd`, `.bat` files in those directories
- **AND** excludes known non-tool files (uninstallers, etc.)

### Requirement: Track source package
The system SHALL identify the source package for each discovered command.

#### Scenario: Get source from shim info
- **WHEN** system discovers a command (from shim or PATH)
- **THEN** system runs `scoop shim info <cmd>` to get source package
- **AND** records source as `(from <package>)` in description

### Requirement: Deduplicate commands
The system SHALL ensure each command is recorded only once.

#### Scenario: Command in both shim and PATH
- **WHEN** same command appears in both shim list and PATH scan
- **THEN** system records command only once
- **AND** uses shim info for source tracking (more reliable)

#### Scenario: Multiple executables from same package
- **WHEN** package provides multiple commands (e.g., ffmpeg, ffprobe)
- **THEN** system records each command separately
- **AND** all share same source package reference
