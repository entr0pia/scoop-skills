## Why

Some Scoop packages don't create shims but instead add their executables directly to PATH (e.g., `ffmpeg-shared`). The current `discover-shims` skill only uses `scoop shim list`, missing these tools. This limits the Agent's ability to discover all available command-line tools.

## What Changes

1. **Enhance scanning logic**: Add PATH scanning alongside `scoop shim list`
2. **Add source tracking**: Use `scoop shim info <cmd>` to identify the source package for each command
3. **Implement deduplication**: Ensure each command is recorded only once, even if it appears in both shim and PATH
4. **Update recording format**: Include source package info: `- cmd: description (from package)`

## Capabilities

### New Capabilities
- `path-scanning`: Scan PATH environment variable to discover Scoop-installed tools not exposed via shims

### Modified Capabilities
- `discover-shims`: Enhance with PATH scanning, source tracking, and deduplication logic

## Impact

- Modified skill file: `skills/discover-shims/SKILL.md`
- No breaking changes to existing functionality
- Improved tool discovery coverage for Agent
