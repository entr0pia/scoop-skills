## Context

The `discover-shims` skill scans Scoop shims and writes a tool list to AGENTS.md. Currently the output format is a flat alphabetical list:

```
- cmd: short description (from package)
```

This gives the agent awareness that tools exist, but not enough context to autonomously choose them over built-in alternatives. The agent needs three things to proactively use a tool:

1. **Trigger awareness** — "this is a text search task, I should use rg"
2. **Replacement mapping** — "rg replaces grep"  
3. **Invocation syntax** — `rg "pattern" --glob "*.ts"`

The skill already runs `scoop info` (which provides Description and Website) and `--help` (which provides syntax), but currently only uses these to judge tool value — not to enrich the output.

## Goals / Non-Goals

**Goals:**
- Agent automatically prefers Scoop tools over PowerShell cmdlets for relevant tasks
- Output format provides enough context for autonomous tool selection
- Few-shot examples teach the agent the inference pattern for new tools
- Header line acts as an actionable instruction, not just a description

**Non-Goals:**
- Changing the skill's scanning/discovery logic
- Adding a separate reference file (keep everything in AGENTS.md)
- Forcing the agent to visit tool websites during execution
- Supporting non-Scoop tool sources

## Decisions

### 1. Enrich output inline, not in a separate reference file

**Decision**: Keep all tool info in the AGENTS.md block rather than splitting into a separate file.

**Rationale**: AGENTS.md is always loaded. A separate file requires the agent to know to look for it. The enriched format adds ~100 lines — acceptable for modern context windows.

**Alternative considered**: Separate `shims-reference.md` with AGENTS.md as index. Rejected because the agent may not know to follow the pointer.

### 2. Categorize by function, not alphabetically

**Decision**: Group tools under functional categories (文本搜索, 文件查找, 文件操作, etc.).

**Rationale**: When the agent has a task, it thinks "I need to search text" — not "I need something starting with r". Category headers create natural scan paths.

**Alternative considered**: Alphabetical with "replaces X" tags. Rejected because the agent still has to scan the full list.

### 3. Use scoop info Description as primary source for replacement inference

**Decision**: The skill SHALL infer "replaces X" primarily from `scoop info` Description, falling back to `--help` output.

**Rationale**: `scoop info` Description is concise and often explicitly states the replacement (e.g., "A cat(1) clone", "alternative to 'find'"). `--help` output is verbose and format varies per tool.

**Alternative considered**: Hardcoded replacement mapping table. Rejected because it doesn't scale to new tools.

### 4. Website URL available but not required

**Decision**: `scoop info` Website URL is available for cases where Description and `--help` are insufficient, but the skill SHALL NOT require visiting it.

**Rationale**: Website visits add latency and may fail. Description + `--help` cover 90% of cases. Website is a safety net.

### 5. Few-shot examples in SKILL.md, not AGENTS.md

**Decision**: Place few-shot examples in SKILL.md to guide the agent's inference pattern. AGENTS.md contains only the final output.

**Rationale**: Few-shot examples are meta-instructions about how to format output — they belong in the skill definition, not in the user-facing context file.

### 6. Header as actionable instruction

**Decision**: Change the block header from passive description to instruction with trigger condition.

**Rationale**: Passive headers ("This block contains...") don't attract model attention. Instructional headers with trigger conditions ("执行搜索、查找、文件处理等任务时优先使用...") create behavioral hooks.

## Risks / Trade-offs

**[Risk] Agent may miscategorize a tool** → Mitigation: Use broad categories; "系统工具" as catch-all. Misclassification is low-impact — the tool is still discoverable.

**[Risk] Agent may infer wrong replacement** → Mitigation: Few-shot examples establish the pattern. "Replaces X" is guidance, not a hard rule — the agent can still choose alternatives.

**[Risk] Enriched format may be overwritten by skill re-run before skill is updated** → Mitigation: Update SKILL.md first, then regenerate AGENTS.md block.
