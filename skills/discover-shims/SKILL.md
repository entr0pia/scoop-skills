---
name: discover-shims
description: Discover available Scoop shims and identify valuable command-line tools. Use when the user asks about available tools, what commands they can use, or wants to explore their Scoop environment.
---

# Discover Shims Skill

This skill helps you discover and catalog available Scoop shims, identifying valuable command-line tools that can replace default Windows commands.

## When to Use

Trigger this skill when the user asks:
- "What tools are available?"
- "What commands can I use?"
- "What shims do I have?"
- "Explore my Scoop environment"

## Steps

### 1. Scan Available Tools

Run both `scoop shim list` and scan PATH for Scoop-related directories:

```powershell
# Get all shims
scoop shim list

# Get Scoop-related paths from PATH
$scoopPaths = $env:PATH -split ';' | Where-Object { $_ -match 'scoop' } | Where-Object { $_ -match '\\apps\\' }

# List executables in those directories
$scoopPaths | ForEach-Object {
    Get-ChildItem -Path $_ -Filter "*.exe" -ErrorAction SilentlyContinue
} | Select-Object -ExpandProperty Name
```

### 2. Analyze Each Command

For each command (from shim list and PATH), gather information:

```powershell
# Get help information (skip if obviously a GUI program)
<cmd> --help

# Get Scoop package info
scoop info <cmd>

# Get source package (for commands from PATH)
scoop shim info <cmd>
```

**IMPORTANT:** Do NOT run `--help` on obviously GUI programs (e.g., firefox, vscode, notepad++). Running them will launch the application and interrupt the user. Use `scoop info <cmd>` to check the description and homepage instead.

**Note:** `scoop shim info <cmd>` returns the source package name (e.g., `fchash` comes from `fastcopy`). Use the `Source` field for tracking.

### 3. Determine Tool Value and Deduplicate

Based on the help info and Scoop info, determine if each command is:
- ✓ A valuable third-party command-line tool (record it)
- ✗ A programming language itself (skip - e.g., python, node, go, rust)
- ✗ A language's built-in tool (skip - e.g., pip, npm, cargo)
- ✗ A TUI program (skip - not suitable for Agent sessions)
- ✗ A GUI program (skip)
- ✗ An interactive editor (skip)

**If tool is unknown:**
- Use `scoop info <cmd>` to get the homepage URL
- Visit the homepage to understand the tool's purpose
- Determine if it's a valuable third-party tool (not a language or built-in tool)

**Deduplication rules:**
- Use command name as unique key
- If same command appears in both shim list and PATH, record only once
- Prefer `scoop shim info` for source tracking (more reliable)
- If package provides multiple commands (e.g., ffmpeg, ffprobe), record each separately
- **IMPORTANT**: Do NOT use text processing tools (grep, awk, etc.) for deduplication. You already have all the information in the command outputs - analyze them directly.

### 4. Write to Global Memory

Write discovered tools to your global memory file in a comment block:

```markdown
<!-- scoop-shims start -->
This block contains command-line tools discovered from Scoop:
- lsd: modern ls with icons and colors (from lsd)
- bat: cat with syntax highlighting (from bat)
- ffmpeg: multimedia framework (from ffmpeg-shared)
- fchash: file hash tool (from fastcopy)
<!-- scoop-shims end -->
```

**Format rules:**
- First line: brief description of the block (e.g., "This block contains command-line tools discovered from Scoop:")
- One tool per line
- Format: `- cmd: short description (from package)`
- Keep descriptions concise (one line)
- Include source package in parentheses
- If comment block exists, replace entire block content

## Output

After scanning, inform the user:
- How many shims were scanned
- How many valuable tools were identified
- What was written to global memory

## Notes

- This skill does NOT maintain hardcoded lists - let the Agent judge based on help info
- TUI/GUI programs are skipped as they're not suitable for Agent sessions
- The global memory block can be updated anytime by re-running this skill
