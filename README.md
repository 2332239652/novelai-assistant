# NovelAI Assistant

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![NovelAI](https://img.shields.io/badge/NovelAI-V5-purple.svg)](https://novelai.net/)

**一个面向 AI Agent 的 NovelAI 提示词工程 Skill —— 让 AI 用自然语言帮你写 Danbooru 风格提示词**

</div>

---

## ✨ 特性

- 🗣️ **自然语言 → Danbooru 标签** - 将口语化描述自动转换为符合 NovelAI 标准的标签提示词
- 🎨 **全版本模型支持** - NAI3/SDXL、V4、V4.5、**V5** 的参数策略与版本差异
- 🎬 **V5 导演式提示词法** - 自然语言场景描述 + 角色框分工 + 少量锚点标签（官方口径最多 22 个 distinct characters）
- ⚖️ **标签权重体系** - `{}` `[]` `1.5::tag::` 数值加权梯度、负强调、画师串主次混合
- 🧵 **整页漫画直出** - V5 fully paneled comic 版式规范与逐格描述法
- 🔤 **文字渲染** - 英 / 日 / 中文 `Text:` 语法、长度上限与排版注意点
- 🫥 **透明背景** - V5 原生 alpha 立绘配方与崩坏排查
- 🎭 **评分与 NSFW 标签** - rating:general / sensitive / questionable / explicit 完整体系
- 🧩 **Danbooru 标签数据库** - 内置 Top Tags、Tag Aliases、中英对照、全角色表四个查询表
- 📋 **场景化模板库** - 通用场景模板、NSFW 模板、职业/服装/民族服饰模板、419+ 画师混合串
- 🚦 **API 并发保护** - 内置 429 封禁风险警告，指导 AI 逐张排队生成

## 🚀 安装

将本仓库克隆到你的 Agent Skill 目录（如 OpenCode / Claude Code 的 skills 目录）：

```bash
git clone https://github.com/2332239652/novelai-assistant.git
```

或直接复制 `SKILL.md` 及配套资源文件到你的技能目录。

## 📚 内容结构

| 文件 | 说明 |
|------|------|
| `SKILL.md` | 核心技能定义：标签语法、权重规则、模型参数、NSFW 体系、工作流 |
| `manga-page-playbook.md` | V5 整页漫画规范：版式声明句 / 逐格方位锚 / 台词载体 / 无台词格标注 |
| `v5-field-corrections.md` | V5 实测校正（与旧口径冲突时以此为准）：姿势机位必须用 tag、角色栏写法、权重解析坑 |
| `v5-confirmed-artist-strings.md` | V5 已确认画师串登记册：逐字冻结的可复现配方 |
| `tag-reference.md` | 中文 → 英文标签速查表（772 行） |
| `game-character-tags.md` | 二游角色标签参考（碧蓝航线 / 蔚蓝档案等） |
| `danbooru-characters-full.txt` | D站全角色表（1106 行）：冷门角色与皮肤变体（碧蓝航线_(皮肤名) 格式） |
| `prompt-templates.md` | 通用场景提示词模板（Fumo 风、手办风、原画稿风、NSFW 模板等） |
| `artist-strings.md` | 社区画师串合集 |
| `artist-300-styles.txt` | 300画风法典·融合类（NAI3）：wlop 系 / 老五样系 / H 特攻等 419 个画师混合串 |
| `nai31-artists-full.txt` | NAI3.1 画师 tag 大全（118033 行，每行一个，grep 速查） |
| `nai3-template-codex.md` | Nai3 提词法典精华：日语服饰释义表 / 质量词 / 负面词 / 视角光线 |
| `community-recipes.md` | 社区配方（元素魔法 / 解构原典等） |
| `danbooru-dict.md` | Danbooru 标签对照表说明 |
| `Danbooru-Top-Tags.xlsx` | 高频标签数据库 |
| `Danbooru-Tag-Aliases.xlsx` | 标签别名数据库 |
| `danbooru-cn-reference.xlsx` | 5481 条中英标签对照 |

## 🤖 与 MCP Server 搭配使用

本 Skill 负责「提示词工程」层，配合 [NovelAI MCP Server](https://github.com/2332239652/NovelAI_MCP)（API 桥接层）可构成完整方案：

```
用户描述 → [本 Skill] → Danbooru 提示词 → [NovelAI MCP] → NovelAI API → 图片
```

## 👤 作者

- **歌靡Abyss** - 项目创建者与维护者（本 Skill 由作者创建，并借助 AI 辅助制作）
- 社区画师与配方贡献者（见下方致谢）

## 📄 许可证

[MIT](./LICENSE)

## 🙏 致谢

- [Danbooru](https://danbooru.donmai.us/) - 标签系统与数据来源
- [NovelAI](https://novelai.net/) - AI 绘画服务
- 社区画师与配方贡献者
