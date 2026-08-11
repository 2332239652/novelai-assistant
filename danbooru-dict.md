# Danbooru 中文标签对照表

## 文件说明
- 文件: `danbooru-cn-reference.xlsx`
- 来源: Editor阿巧的中文化 Danbooru Tag 对照表（词性对 AI 用优化版）
- 总计: **5481 条标签映射**

## 数据结构

| 列 | 内容 |
|----|------|
| A (id) | 编号 |
| B (url) | Danbooru 搜索链接 |
| C (tag) | **Danbooru 英文标签** |
| D (right_tag_cn) | **中文翻译** |
| E | 其他备注 |
| F | 验证/状态 |
| G | 验证/状态 |

## 使用方式

当用户提供的中文描述在本 skill 的 `tag-reference.md` 中找不到时，AI 应查询此对照表，找到准确的英文标签。例如：

- 用户说"我想看猫耳萝莉" → 查表得: `cat ears`, `loli`
- 用户说"她的发型是钻头卷" → 查表得: `drill hair`
- 用户说"制服姿势" → 查表得: `uniform`, `pose`

## 注意

- 表格中的 tag 列即为 Danbooru 可直接使用的英文标签
- 中文列 (right_tag_cn) 为对应中文翻译
- 标签涉及全年龄和成人内容两方面
