## 1. Update SKILL.md Format Template

- [x] 1.1 Replace the flat format template (lines 82-89) with categorized format showing category headers, replacement targets, and example commands
- [x] 1.2 Add few-shot examples block after the format rules, covering three inference cases: explicit replacement, implied replacement, and no direct replacement
- [x] 1.3 Update analysis step (步骤 3) to add: infer replacement target from `scoop info` Description, extract usage examples from `--help`

## 2. Regenerate AGENTS.md Block

- [x] 2.1 Rewrite the `scoop-shims` block header to actionable instruction: "本机已安装以下 Scoop 工具，用于补全Windows的命令行生态。执行搜索、查找、文件处理等任务时优先使用这些工具，而非复杂的PowerShell指令及脚本"
- [x] 2.2 Rewrite tool entries in categorized format with replacement targets and usage examples
