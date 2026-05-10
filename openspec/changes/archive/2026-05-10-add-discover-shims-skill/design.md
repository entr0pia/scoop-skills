## Context

Scoop uses shims to expose executables. User-installed tools are in `~\scoop\shims`. The current skill only provides command reference without awareness of the actual environment. The Agent needs to know which tools are available to prefer modern alternatives.

## Goals / Non-Goals

**Goals:**
- Agent automatically discovers available Scoop tools
- Tool info persists in global memory to avoid repeated scanning
- New tools are appended to memory after installation

**Non-Goals:**
- No hardcoded tool blacklist/mapping tables
- No TUI/GUI program filtering (Agent judges itself)
- No automatic scan trigger (passive, triggered by Agent or user)

## Decisions

1. **Agent inference, not hardcoding**: Use `--help` and `scoop info` to let Agent judge tool value
2. **Comment block format**: `<!-- scoop-shims start -->...<!-- scoop-shims end -->` for easy replacement
3. **One line per tool**: `cmd: short description` to minimize token usage
4. **Write to global memory**: Agent's global instructions file, shared across sessions

## Risks / Trade-offs

- **Slow scan with many shims**: Each shim requires `--help` and `scoop info`, first scan may be slow
- **Inconsistent Agent judgment**: Different sessions may judge the same tool differently
- **Global memory bloat**: If user installs many tools, comment block grows (but one line per tool, usually manageable)
