## 1. 创建 discover-shims 技能

- [x] 1.1 创建技能文件 `skills/discover-shims/SKILL.md`
- [x] 1.2 定义触发条件（"available tools"、"what commands"、"shim"、"discover tools"）
- [x] 1.3 实现扫描逻辑：运行 `scoop shim list`
- [x] 1.4 实现分析逻辑：对每个 shim 运行 `--help` 和 `scoop info`
- [x] 1.5 实现写入逻辑：将有价值的工具写入全局记忆注释块
- [x] 1.6 确保格式为 `cmd：简短说明`，一行一个工具

## 2. 修改 SKILL.md

- [x] 2.1 移动现有 `SKILL.md` 到 `skills/scoop-skills/SKILL.md`
- [x] 2.2 在 `scoop install` 命令说明后添加追加到全局记忆的指令
- [x] 2.3 在 `scoop shim add` 命令说明后添加追加到全局记忆的指令
- [x] 2.4 明确追加格式和位置（`<!-- scoop-shims -->` 注释块内）


