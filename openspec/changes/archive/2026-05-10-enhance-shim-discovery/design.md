## Context

The current `discover-shims` skill only uses `scoop shim list` to find available tools. However, some Scoop packages (like `ffmpeg-shared`) don't create shims but instead add executables directly to PATH. This limits the Agent's ability to discover all available tools.

## Goals / Non-Goals

**Goals:**
- Discover all Scoop-installed tools, including those in PATH but not in shims
- Track source package for each command (using `scoop shim info`)
- Deduplicate commands that appear in both shim and PATH
- Maintain compact recording format with source information

**Non-Goals:**
- Don't scan all PATH entries (only Scoop-related paths)
- Don't maintain hardcoded package lists
- Don't change the fundamental recording format (still one line per tool)

## Decisions

1. **Scan PATH alongside shim list**
   - Extract Scoop-related paths from `$env:PATH`
   - List executables in those directories
   - Combine with `scoop shim list` results

2. **Use `scoop shim info` for source tracking**
   - For each discovered command, run `scoop shim info <cmd>`
   - Extract the `Source` field to get the real package name
   - Record as: `- cmd: description (from package)`

3. **Deduplicate by command name**
   - If same command appears in both shim and PATH, record only once
   - Prefer shim info for source tracking (more reliable)
   - Use command name as unique key

4. **Filter PATH directories**
   - Only scan directories containing "scoop" in path
   - Skip directories that are already covered by shim list
   - Focus on `~\scoop\apps\*\current\` patterns

## Risks / Trade-offs

- **Performance**: PATH scanning adds overhead → Mitigation: Only scan Scoop-related directories
- **Accuracy**: Some PATH entries might not be Scoop-managed → Mitigation: Filter by "scoop" in path
- **Complexity**: Dedup logic adds complexity → Mitigation: Simple command-name-based dedup
