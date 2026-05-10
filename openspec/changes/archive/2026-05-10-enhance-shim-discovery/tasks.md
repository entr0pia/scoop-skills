## 1. 增强扫描逻辑

- [x] 1.1 在 SKILL.md 中添加 PATH 扫描步骤
- [x] 1.2 实现提取 `$env:PATH` 中包含 "scoop" 的路径
- [x] 1.3 实现过滤逻辑：只保留 `~\scoop\apps\*\current\` 模式
- [x] 1.4 实现列出目录中的可执行文件（.exe, .cmd, .bat）

## 2. 添加来源跟踪

- [x] 2.1 在分析步骤中添加 `scoop shim info <cmd>` 调用
- [x] 2.2 提取 `Source` 字段获取真实包名
- [x] 2.3 更新记录格式为 `- cmd: description (from package)`

## 3. 实现去重逻辑

- [x] 3.1 实现按命令名去重
- [x] 3.2 处理同一命令同时出现在 shim 和 PATH 的情况
- [x] 3.3 处理同一包提供多个命令的情况

## 4. 更新技能文档

- [x] 4.1 更新 SKILL.md 中的格式规则
- [x] 4.2 更新示例中的注释块格式
- [x] 4.3 添加 PATH 扫描的说明
