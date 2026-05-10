# Scoop Skills 仓库指南

## 仓库概述

这是一个 **Scoop 技能仓库**，为 AI Agent 提供 Windows 包管理能力。核心是 `SKILL.md` 文件，包含所有 Scoop 操作指令。

## 关键文件

- `SKILL.md` - 技能核心文件，包含元数据、触发条件和完整指令
- `references/scoop-wiki/` - Scoop 官方文档本地镜像（36 个 Markdown 文件）
- `.opencode/` - OpenCode 插件和技能配置
- `openspec/` - OpenSpec 工作流配置（spec-driven 模式）

## 架构特点

**无代码仓库**：这是纯文档/配置项目，没有源代码、构建系统或测试。

**技能触发**：当用户提到 "install"、"scoop"、"package"、"shim" 等关键词时触发。

**文档优先**：代理应优先读取 `references/scoop-wiki/` 而非在线文档。

## 开发工作流

### 修改技能
1. 编辑 `SKILL.md`（核心指令文件）
2. 测试：在 Gemini CLI 中触发 "scoop" 关键词验证行为
3. 更新文档：手动从 Scoop Wiki 仓库拉取更新到 `references/scoop-wiki/`

### OpenSpec 工作流
- 使用 `openspec` CLI 管理变更
- 命令：`openspec list --json`、`openspec status --change "<name>" --json`
- 技能目录：`.opencode/skills/openspec-*`

## 重要约束

- **GPL-3.0 许可证**：修改需遵守许可条款
- **本地文档优先**：代理必须优先使用 `references/scoop-wiki/` 中的文档
- **无自动测试**：没有测试套件，验证依赖手动触发
- **静态快照**：`references/scoop-wiki/` 是静态副本，不会自动更新

## 常见任务

### 添加新功能
1. 在 `SKILL.md` 中添加指令
2. 确保指令清晰、可操作
3. 测试触发条件

### 更新文档
1. 从 Scoop Wiki 仓库获取最新内容
2. 替换 `references/scoop-wiki/` 中的对应文件
3. 确保文件名和路径一致

### 调试技能
1. 检查 `SKILL.md` 中的触发条件
2. 验证关键词匹配
3. 测试指令执行结果