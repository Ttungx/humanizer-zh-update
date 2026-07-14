# AGENTS.md

Guidance for AI coding agents (Claude Code, Codex, Warp, etc.) working in this repository.

## What this repo is

一个以纯 Markdown 实现的便携型 Agent 技能，面向中文用户。运行时的核心产物是 `SKILL.md`：Agent 读取其 YAML frontmatter（元数据 + 允许的工具列表）后执行编辑器提示。无构建步骤、无可执行代码，仓库应避免将支持范围限定在某一种或两种 Agent 框架上。

本项目基于 [blader/humanizer](https://github.com/blader/humanizer) v2.8.2 完整翻译，并参考了 [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) 和 [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop) 的中文适配经验。

## Key files

- `SKILL.md` — 技能本体。YAML frontmatter（`name`、`version`、`description`、`compatibility`、`allowed-tools`）之后是规范的编号模式列表，每条附有改写前/改写后示例。**这是唯一的真相来源。**
- `README.md` — 面向人类读者：安装方法、使用方式、模式汇总表和版本历史。
- `.claude-plugin/plugin.json` — 可选的 Claude Code 插件清单。
- `.claude-plugin/marketplace.json` — 可选的单仓库市场入口，使 `/plugin marketplace add Ttungx/humanizer-zh-update` 可用。

## The maintenance contract

`SKILL.md` 和 `README.md` 必须保持同步。当你修改行为或内容时：

- **模式：** 技能当前定义了 **33 个编号模式**。如果你新增、删除或重新编号任何一个，在同一次提交中更新 README 的模式汇总表、"N 种 AI 写作模式"标题以及所有交叉引用。除非刻意重新编号，否则保持编号稳定。
- **版本：** `SKILL.md` frontmatter 有 `version:` 字段，`README.md` 有版本历史章节，`.claude-plugin/plugin.json` 有 `version` 字段。三者需一起更新，使包元数据与技能保持一致。（`marketplace.json` 故意省略版本号，以 `plugin.json` 作为包的真相来源。）
- **兼容性：** 安装和使用说明保持框架中立。技能应能在任何支持加载 Markdown 技能指令的 Agent 框架中工作；Claude Code、OpenCode、Codex 等是示例，不是限制。
- **非显而易见的修复：** 如果你修改提示以处理棘手的失败模式（反复误改、意外的语气偏移等），在 README 版本历史中添加简短说明，解释修复了什么以及为什么。

## Editing SKILL.md

- 保留有效的 YAML frontmatter（格式和缩进）。
- frontmatter 之后的提示是产品本身。像编辑一份严谨的说明文档那样编辑它，而非像编辑代码。
- 翻译注意事项：示例文本中"改写前"展示的是典型的 AI 生成中文表达，"改写后"展示的是更自然的人类表达。修改示例时请确保"改写前"确实包含该模式的问题，"改写后"确实解决了该问题。
- 中文语境标注：对于在中文中不太适用或表现不同的模式（如标题大小写、连字符词对、弯引号），保留"注"说明。新增模式时考虑是否需要类似的中文适配说明。
