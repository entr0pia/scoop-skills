## Why

The `scoop-shims` block in AGENTS.md is a flat list of tool names with minimal descriptions. Agents see the list but lack the context to proactively use these tools — they don't know when to use each tool, what built-in command it replaces, or how to invoke it. The discover-shims skill generates this block with a thin format template (`- cmd: short description (from package)`), so even after re-running the skill the output remains too sparse for autonomous tool selection.

## What Changes

- Update the `discover-shims` skill's output format template to produce categorized, scenario-driven tool listings with replacement targets and usage examples
- Add few-shot examples to the skill showing the agent how to infer "replaces X" from `scoop info` Description and `--help` output
- Enrich the AGENTS.md block header from passive description to an actionable instruction that tells the agent to prefer these tools over PowerShell cmdlets
- Update the AGENTS.md `scoop-shims` block to the new enriched format

## Capabilities

### New Capabilities

- `shims-format-template`: The enriched output format for the discover-shims skill, including categorization rules, replacement inference, and example extraction

### Modified Capabilities

_(none)_

## Impact

- `C:\Users\Peyton\.agents\skills\discover-shims\SKILL.md` — format template, few-shot examples, analysis step
- `C:\Users\Peyton\.config\opencode\AGENTS.md` — scoop-shims block rewrite
