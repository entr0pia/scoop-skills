# Scoop Skills 项目概述

本仓库是一个**公开发布的 Scoop 技能仓库**，通过 `npx skills add` 安装到代理环境，为代理提供管理 **Scoop**（Windows 命令行安装器）的专家级能力。

## 项目结构

```
scoop-skills/
├── skills/
│   ├── scoop-skills/          # 核心 Scoop 管理技能
│   │   ├── SKILL.md           # 技能定义文件
│   │   └── references/        # Scoop 官方文档本地镜像
│   │       └── scoop-wiki/
│   └── discover-shims/        # Shim 发现技能
│       └── SKILL.md           # 技能定义文件
├── openspec/                  # OpenSpec 工作流配置
└── .opencode/                 # OpenCode 插件配置
```

## 技能说明

### scoop-skills（核心技能）
- **包管理**：搜索、安装、更新、卸载 Windows 应用
- **Shim 管理**：发现和管理 Scoop "shims"，确保命令行工具正确识别和执行
- **环境恢复**：从手动备份或目录迁移中恢复 Scoop 安装
- **Manifest 开发**：使用内部脚本创建、测试和格式化 Scoop JSON manifests

### discover-shims（工具发现技能）
- **Shim 扫描**：扫描所有可用的 Scoop shims
- **工具分析**：通过 `--help` 和 `scoop info` 理解每个工具
- **全局记忆**：将有价值的命令行工具写入代理的全局记忆

## 使用方法

### 用户安装
```bash
npx skills add <repository-url>
```

### 开发者指南
- **测试**：在 Gemini CLI 中触发 "scoop" 关键词，观察代理是否正确遵循 `SKILL.md` 中的流程
- **更新文档**：`skills/scoop-skills/references/scoop-wiki/` 目录是静态快照，需手动从 Scoop Wiki 仓库拉取更新

## 开发规范

- **祈使语气**：`SKILL.md` 使用清晰的祈使语气指导代理
- **本地文档优先**：代理应优先读取本地文档，而非在线获取
- **精准编辑**：修改 manifests 或配置文件时，使用精准的搜索和替换工具
- **英文编写**：技能文件使用英文编写，确保跨平台兼容性
