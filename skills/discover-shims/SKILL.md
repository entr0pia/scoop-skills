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

### 1. Scan Available Shims

Run `scoop shim list` to get all available shims:

```powershell
scoop shim list
```

### 2. Analyze Each Shim

For each shim, gather information using both methods:

```powershell
# Get help information
<cmd> --help

# Get Scoop package info
scoop info <cmd>
```

### 3. Determine Tool Value

Based on the help info and Scoop info, determine if each shim is:
- ✓ A valuable command-line tool (record it)
- ✗ A TUI program (skip - not suitable for Agent sessions)
- ✗ A GUI program (skip)
- ✗ An interactive editor (skip)

### 4. Write to Global Memory

Write discovered tools to your global memory file in a comment block:

```markdown
<!-- scoop-shims start -->
lsd: modern ls with icons and colors
bat: cat with syntax highlighting
fd: faster find alternative
<!-- scoop-shims end -->
```

**Format rules:**
- One tool per line
- Format: `cmd: short description`
- Keep descriptions concise (one line)
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
