# Contributing to pyResearch-ReadingSkill

感谢你对本项目的关注！我们欢迎各种形式的贡献。

## 如何贡献

### 报告问题 (Bug Reports)

如果你在使用中发现任何问题，请提交 Issue 并包含以下信息：

1. **问题描述** - 清晰描述遇到的问题
2. **复现步骤** - 如何触发该问题
   - 测试文件链接（如有）
   - 触发词（你使用的指令）
   - 错误输出片段
3. **环境信息** - Claude Code 版本、操作系统

### 功能建议 (Feature Requests)

如果你有新的功能想法，请提交 Issue 并描述：

1. **功能描述** - 你希望添加什么功能
2. **使用场景** - 这个功能如何帮助你
3. **实现建议**（可选）- 你认为如何实现

### 提交代码 (Pull Requests)

如果你想直接贡献代码，请遵循以下流程：

1. **Fork 本仓库**
2. **创建功能分支** - `git checkout -b feature/AmazingFeature`
3. **提交更改** - `git commit -m 'Add some AmazingFeature'`
4. **推送到分支** - `git push origin feature/AmazingFeature`
5. **提交 Pull Request**

## 代码规范

- **保持一致性** - 遵循现有代码风格
- **添加文档** - 更新相关的 README 或注释
- **测试用例** - 为新功能添加测试用例（如适用）
- **反幻觉机制** - 确保所有输出都有原文引用和标签

## 开发流程

### 测试新技能

1. 将测试数据放入 `test_data/` 目录
2. 在 `skills/[skill-name]/evals/` 中添加测试用例
3. 使用 skill 测试功能验证效果

### 文档更新

- 更新相关技能的 README
- 如有新可视化类型，更新可视化类型说明
- 更新示例

## 许可证

通过提交 PR，你同意你的贡献将采用 MIT 许可证进行许可。