## ADDED Requirements

### Requirement: Tool listing SHALL be organized by functional category
The discover-shims skill output SHALL group tools under functional category headers (e.g., 文本搜索, 文件查找, 文件操作, JSON处理, 压缩解压, GitHub操作, 数据库, 网络, 多媒体, 系统工具). Tools that do not fit existing categories SHALL be placed under a catch-all category.

#### Scenario: Agent categorizes rg under 文本搜索
- **WHEN** the skill processes `rg` (ripgrep) and its `scoop info` Description says "Recursively searches directories for a regex pattern"
- **THEN** the output SHALL place `rg` under a `## 文本搜索` category header

#### Scenario: Agent creates new category for uncategorized tool
- **WHEN** the skill processes a tool that does not fit any existing category
- **THEN** the skill SHALL create a new category or place it under `## 系统工具`

### Requirement: Each tool entry SHALL include replacement target
Each tool entry SHALL include a "replaces X" clause indicating which built-in command or PowerShell cmdlet the tool replaces. The replacement target SHALL be inferred primarily from the `scoop info` Description field, falling back to `--help` output.

#### Scenario: Description explicitly states replacement
- **WHEN** `scoop info fd` Description says "A simple, fast and user-friendly alternative to 'find'"
- **THEN** the entry SHALL say "替代 find"

#### Scenario: Description implies replacement
- **WHEN** `scoop info bat` Description says "A cat(1) clone with syntax highlighting"
- **THEN** the entry SHALL say "替代 cat"

#### Scenario: No direct replacement exists
- **WHEN** `scoop info jq` Description says "lightweight command-line JSON processor" with no built-in equivalent
- **THEN** the entry SHALL describe capability without "替代 X" (e.g., "JSON 处理器")

### Requirement: Each tool entry SHALL include usage examples
Each tool entry SHALL include one or two example commands extracted from `--help` output, showing the most common invocation patterns.

#### Scenario: Typical single-file usage
- **WHEN** processing `rg` and `--help` shows common patterns
- **THEN** the entry SHALL include examples like `rg "TODO" --glob "*.ts"`

#### Scenario: Two examples for versatile tools
- **WHEN** a tool has multiple common usage patterns (e.g., rg with glob and type filters)
- **THEN** the entry SHALL include up to two examples showing different patterns

### Requirement: Block header SHALL be an actionable instruction
The first line of the `scoop-shims` comment block in AGENTS.md SHALL be an actionable instruction that tells the agent to prefer these tools over PowerShell cmdlets, with a trigger condition describing when to use them.

#### Scenario: Header reads as instruction
- **WHEN** the agent loads AGENTS.md
- **THEN** the scoop-shims block header SHALL say "本机已安装以下 Scoop 工具，用于补全Windows的命令行生态。执行搜索、查找、文件处理等任务时优先使用这些工具，而非复杂的PowerShell指令及脚本"

### Requirement: Few-shot examples SHALL guide inference pattern
The SKILL.md SHALL contain few-shot examples demonstrating how to infer replacement targets from `scoop info` Description and `--help` output. Examples SHALL cover three cases: explicit replacement in Description, implied replacement, and no direct replacement.

#### Scenario: Few-shot covers explicit replacement
- **WHEN** the agent reads the skill's few-shot examples
- **THEN** there SHALL be an example where `scoop info` Description directly states "alternative to X"

#### Scenario: Few-shot covers implied replacement
- **WHEN** the agent reads the skill's few-shot examples
- **THEN** there SHALL be an example where the Description says "X clone" and the agent infers "replaces X"

#### Scenario: Few-shot covers no replacement
- **WHEN** the agent reads the skill's few-shot examples
- **THEN** there SHALL be an example where the tool has no built-in equivalent and the entry describes capability only
