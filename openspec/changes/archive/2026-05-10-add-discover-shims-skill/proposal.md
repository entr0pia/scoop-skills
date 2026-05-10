## Why

当前 Scoop 技能只提供命令参考，Agent 无法主动感知用户已安装的命令行工具。用户通过 Scoop 安装了 `lsd`、`bat`、`fd` 等现代工具，但 Agent 仍使用默认命令（如 `Get-ChildItem` 而非 `lsd`）。需要一个机制让 Agent 自动发现并利用这些工具。

## What Changes

1. **新建 `discover-shims` 技能**：扫描可用 shim，通过 `--help` 和 `scoop info` 理解工具，将有价值的命令行工具写入全局记忆
2. **修改 `SKILL.md`**：在 `scoop install` 和 `scoop shim add` 操作后，追加新工具到全局记忆
3. **全局 AGENTS.md**：添加触发指令，引导 Agent 检查可用工具

## Capabilities

### New Capabilities
- `discover-shims`: 扫描 Scoop shims，识别有价值的命令行工具，写入全局记忆注释块

### Modified Capabilities
- `scoop-skills`: 在安装/创建工具后，追加到全局记忆

## Impact

- New skill file: `skills/discover-shims/SKILL.md`
- Moved file: `SKILL.md` → `skills/scoop-skills/SKILL.md`
- Global memory: Agent's global instructions file (comment block format for easy updates)
