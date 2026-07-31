# NovelAI Assistant

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![NovelAI](https://img.shields.io/badge/NovelAI-V4.5-purple.svg)](https://novelai.net/)

**一个面向 AI Agent 的 NovelAI 提示词工程 Skill —— 让 AI 用自然语言帮你写 Danbooru 风格提示词**

</div>

---

## ✨ 特性

- 🗣️ **自然语言 → Danbooru 标签** - 将口语化描述自动转换为符合 NovelAI 标准的标签提示词
- 🎨 **全版本模型支持** - NAI3/SDXL、V4、V4.5 Curated/Full 的参数策略与版本差异
- ⚖️ **标签权重体系** - `{}` `[]` `1.5::tag::` 数值加权等 V4/V4.5 语法
- 🎭 **评分与 NSFW 标签** - rating:general / sensitive / questionable / explicit 完整体系
- 🧩 **Danbooru 标签数据库** - 内置 Top Tags、Tag Aliases、中英对照三个查询表
- 📋 **场景化模板库** - 通用场景模板（Fumo 布偶风、手办风、动画原画稿风等）
- 🚦 **API 并发保护** - 内置 429 封禁风险警告，指导 AI 逐张排队生成

## 🚀 安装

将本仓库克隆到你的 Agent Skill 目录（如 OpenCode / Claude Code 的 skills 目录）：

```bash
git clone https://github.com/SGSxingchen/novelai-assistant.git
```

或直接复制 `SKILL.md` 及配套资源文件到你的技能目录。

## 📚 内容结构

| 文件 | 说明 |
|------|------|
| `SKILL.md` | 核心技能定义：标签语法、权重规则、模型参数、NSFW 体系、工作流 |
| `tag-reference.md` | 中文 → 英文标签速查表（772 行） |
| `game-character-tags.md` | 二游角色标签参考（碧蓝航线 / 蔚蓝档案等） |
| `prompt-templates.md` | 通用场景提示词模板（Fumo 风、手办风、原画稿风等） |
| `artist-strings.md` | 社区画师串合集 |
| `community-recipes.md` | 社区配方（元素魔法 / 解构原典等） |
| `danbooru-dict.md` | Danbooru 标签对照表说明 |
| `Danbooru-Top-Tags.xlsx` | 高频标签数据库 |
| `Danbooru-Tag-Aliases.xlsx` | 标签别名数据库 |
| `danbooru-cn-reference.xlsx` | 5481 条中英标签对照 |

## 🤖 与 MCP Server 搭配使用

本 Skill 负责「提示词工程」层，配合 [NovelAI MCP Server](https://github.com/SGSxingchen/NovelAI_MCP)（API 桥接层）可构成完整方案：

```
用户描述 → [本 Skill] → Danbooru 提示词 → [NovelAI MCP] → NovelAI API → 图片
```

## 📄 许可证

[MIT](./LICENSE)

## 🙏 致谢

- [Danbooru](https://danbooru.donmai.us/) - 标签系统与数据来源
- [NovelAI](https://novelai.net/) - AI 绘画服务
- 社区画师与配方贡献者
