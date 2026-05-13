# Scoop Skills 项目概述

你是Skills开发者, 所有修改在仓库内完成, 不要修改已经安装的skills文件. 所有`SKILL.md`都必须是全英文的, `README.md`也是全英文的

## 仓库概述

这是一个**公开发布的 Scoop 技能仓库**，用于通过 `npx skills add` 安装到 AI Agent 环境。包含两个技能：

- `scoop-skills` - 核心 Scoop 包管理技能
- `discover-shims` - 发现可用命令行工具

## 项目结构

```
scoop-skills/
├── skills/
│   ├── scoop-skills/          # 核心 Scoop 管理技能
│   │   ├── SKILL.md           # 技能定义文件
│   │   └── references/        # Scoop 官方文档本地镜像
│   │       └── scoop-wiki/    # 36 个 Markdown 文档
│   └── discover-shims/        # Shim 发现技能
│       └── SKILL.md           # 技能定义文件
├── openspec/                  # OpenSpec 工作流配置
└── .opencode/                 # OpenCode 插件配置
```

## 技能说明

### scoop-skills
核心技能，当用户提到 "install"、"scoop"、"package"、"shim" 等关键词时触发。提供：
- 包管理命令（搜索、安装、更新、卸载）
- Shim 发现和管理
- 环境恢复
- Manifest 开发

### discover-shims
工具发现技能，当用户问 "what tools"、"available commands" 等时触发。提供：
- 扫描所有可用 shim
- 通过 `--help` 和 `scoop info` 分析工具
- 推断每个工具替代的内置命令（从 `scoop info` Description 提取）
- 按功能分类输出，附带使用示例
- 将有价值的命令行工具写入全局记忆

## 开发工作流

### 修改技能
1. 编辑对应的 `skills/<skill-name>/SKILL.md`
2. 测试：触发相关关键词验证行为
3. **不要在开发会话中更新全局记忆文件**。提示用户在新的会话中执行技能，完成全局记忆的更新
4. 更新文档：手动从 Scoop Wiki 仓库拉取更新到 `skills/scoop-skills/references/scoop-wiki/`

### OpenSpec 工作流
- 使用 `openspec` CLI 管理变更
- 命令：`openspec list --json`、`openspec status --change "<name>" --json`
- 归档：`openspec archive <name>`

## 重要约束

- **GPL-3.0 许可证**：修改需遵守许可条款
- **本地文档优先**：代理应优先使用 `skills/scoop-skills/references/scoop-wiki/` 中的文档
- **无自动测试**：没有测试套件，验证依赖手动触发
- **静态快照**：`references/scoop-wiki/` 是静态副本，不会自动更新

## 常见任务

### 添加新技能
1. 在 `skills/<skill-name>/` 目录创建 `SKILL.md`
2. 遵循 [agent-skills 规范](https://github.com/vercel-labs/agent-skills)
3. 使用英文编写技能内容

### 更新文档
1. 从 Scoop Wiki 仓库获取最新内容
2. 替换 `skills/scoop-skills/references/scoop-wiki/` 中的对应文件
3. 确保文件名和路径一致

### 调试技能
1. 检查 `SKILL.md` 中的触发条件
2. 验证关键词匹配
3. 测试指令执行结果
