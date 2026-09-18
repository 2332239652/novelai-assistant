# V5 实测校正（2026-09-11 · 与旧口径冲突处以本文为准）

> **来源**：官方 docs（models / textrendering / multiplecharacters）+ 社区实测 skill [Miint-Sunny/nai5-prompting](https://github.com/Miint-Sunny/nai5-prompting)（1844 条真提示词统计 + 4663 张反推 + 锁种子对照实验）+ 本环境实测。
> 本文修正 SKILL.md 里的旧口径。冲突时以官方 → 实测 → 本文 → 旧章节的顺序为准。

---

## 1. 【最重要】姿势和机位必须用 tag，不能写成句子

**旧口径**（SKILL.md §1.7 NL 优先范式）说「构图用 NL 句子，元素用 tag」——**这条对姿势和机位是错的**。

**实测证据**（锁 3 个 seed，只换被测块）：

| 判据 | 结果 | 强度 |
|---|---|---|
| 姿势必须词组 | 句子 **3/3 失败**，词组 **3/3 成功**；换第二条画师串再测 1/1，合计 **4/4** | 强（跨画师串复现） |
| 机位高低必须词组 | 句子 3/3 未压低机位（全平视），`from below` 3/3 明确仰视 | 强 |

**失败方式**：不是画错姿势，是把姿势**画糊**——多余一条腿、接不上的胯、腿能数出三段结构、曲起的那条腿整个消失。**长从句描述肢体关系时，模型会把每个从句各画一遍**。跨两条画风差异极大的串，失败模式完全一致 → 是模型机制问题，不是画师串副作用。

**落地规则**：
- **姿势 / 体位 / 机位 / 景别 / 朝向 → tag**（离散事实）
- **关系 / 空间 / 归属 / 占画幅 / 光影叙事 / 进行中的动作状态 → 句子**
- 判断口诀：**能查到 tag 的离散事实就 tag；说不准的"关系"就句子**

姿势 tag 表：`sitting` `standing` `lying` `kneeling` `squatting` `sitting sideways` `leg up` `knees up` `crossed legs` `arm support` `head rest` `hand on own cheek` `arms up` `legs up` `hugging own legs` `on side` `on back` `on stomach`

> 本环境对号入座：之前做「腋下托举悬空」「三条腿」那几张，姿势全是用长句写的（"he lifts her whole body up by sliding both arms under her armpits…"），正好命中这个最高频失败模式。改成 tag 组合才是正解。

---

## 2. 【重要】版权角色的角色栏只写名字，不要列外貌

| 角色类型 | 角色栏怎么填 | 易犯错 |
|---|---|---|
| **原创角色** | `girl/boy/other` + **全部样貌锚点**（发色·发型·瞳色·体型·种族特征·耳朵·角·尾巴·翅膀·标志性饰品），一个不许删 | 删锚点 → 角色崩 |
| **版权角色**（danbooru 认得的） | `girl/boy/other, 角色名` **到此为止**（作品名可省） | **添**外貌 → 特征权重翻倍、与名字打架 |

实测：写了版权角色名的 197 个格子里只有 **6%** 连作品名一起写；五人图五格**全部**多写了发色发型（用户报的 bug）。

> 本环境对号入座：给阿米娅写 `{{short hair}}, {{brown hair}}, {{blue eyes}}`、给辉夜写 `{{long hair}}, {{black hair}}, {{red eyes}}` —— 都属于「添」，是错的。正确写法就是 `girl, amiya (arknights)`。

角色名只认 ASCII、拼写必须完全正确；皮肤/换装写在「角色名 (作品名)」之间的括号里。

---

## 3. 【重要】画师名以数字结尾紧跟 `::` 会被解析成权重数值

**这是「画师串崩坏」的真凶之一。**

`na_tarapisu153::` 会被解析成**权重 153**，整条提示词被炸掉（画面融化/噪音/平块）。数字权重**不写闭合 `::` 时还会作用到之后所有 tag 直到结尾**。

- ✅ 安全写法：`na_tarapisu153, ::`（**加逗号比加空格安全**）
- ✅ 更安全：`2::artist:na_tarapisu153, ::`
- ❌ 危险：`0.7::artist:na_tarapisu153::`

> 本环境对号入座：`v5-confirmed-artist-strings.md` 里「NSFW 人体串淘汰记录」记载 `asanagi + chen bin + na_tarapisu153` 和 `rella 1.3 + na_tarapisu153 0.7` 两次"红色噪点崩坏"——**极可能就是这条**，不是画师兼容性问题。以后要复测这两位组合，先用逗号写法。

同理，任何**以数字结尾**的画师名（`na_tarapisu153`、`mx2j`、`ke-ta` 等）在权重语法里都要留意。

---

## 4. 权重语法要点

- `1.2::tag::` 增强，作用到 `::` 闭合为止
- `-2::tag::` 定向移除 / 概念反转
- **权重值不必整数**；V5 在 **1.0–2.0 区间非线性变化明显**，**1.3–1.8** 是调 tag 最值得关注的区间（1.5 在 V5 有负权重效果）
- **默认不加权**。只在实测某层效果不足时才对该层加权
- 实测高频增强值：2 / 1.2 / 1.1 / 1.3 / 1.5；负权重 -1 ~ -5 都有人用，**-2 最多**
- `::` 可自动闭合任何未配平的 `{` `[`
- `{tag}` / `[tag]` 是旧语法，读老串时理解即可

---

## 5. 互斥组（每类只能挑一个）

| 类别 | 只能选一个 |
|---|---|
| 视线 | `looking at viewer` · `looking to the side` · `looking up` · `looking down` · `looking away` · `looking at another` · `looking back` |
| 景别 | `close-up` · `portrait` · `upper body` · `cowboy shot` · `full body` · `wide shot` |
| 背景形态 | `simple background` · `white background` · `detailed background` · `transparent background` · `dark background` · `blurry background` |
| 体位 | `sitting` · `standing` · `lying` · `kneeling` · `squatting`（多角色例外） |
| 水平机位 | `from side` · `from behind` · `straight on` |
| 垂直机位 | `from below` · `from above`（可与水平机位组合） |
| 版式 | `comic` · `4koma` · `multiple views` · `reference sheet` · `sticker` |
| 透明 | `transparent background` · `alpha transparency` · `has alpha` |

`close up` 与 `close-up` 同一个词，挑一个。`depth of field`/`bokeh` 是浅景深，大场景别用。

---

## 6. 字段分工与顺序

**分工**：base 管「画师串 · 人数 · 动作 · 表情 · 镜头 · 场景 · 背景 · 光影 · 氛围色彩 · 技法 · 质量尾」；角色栏**只放外貌**；UC 放排除项。

**主提示词顺序**（实测两两先后比例）：

```
人数 → 外貌 → 服装 → 表情 → 镜头 → 动作
                场景·背景 在镜头之前
                              质量尾 → 最后
```
- 人数放最前、质量尾放最后这两条最硬（人数领先各类 80–97%）
- 表情留在**主提示词**（例外：配 `source#`/`target#` 前缀标施受气质时可进角色栏）
- **关键独立物件仍要拎出来单独做 tag 放前部**，别埋进句子（`transparent umbrella, wooden bench` 优于 "holding a transparent umbrella on a wooden bench"）

**多人交互**：用 `Character 1 / 2 / 3` 写归属（跟角色栏同名）；交互动作句用**外观短语**指认（"the girl in the beige coat hands the cup to the girl with headphones"）；不用角色真名当主语。每个接触点都要说清**是谁的手、碰到谁的哪里**。

**施受前缀**（写在角色栏，非 base）：`source#{动作}` 发起 · `target#{动作}` 承受 · `mutual#{动作}` 互相。前缀管归属，表情/动作 tag 管气质，两层互不干涉。

---

## 7. UC 与质量词

- **UC 两档，二选一**：没排除项就「用默认预设」；有排除项就**只写排除项本身**，别把预设串拼进去。
- **多人图 UC 不能有 `extra characters`**（权重 2 的「多余角色」与人数 tag 打架；压测 39/103 栽在这）。
- 画面里明确不要的具体元素，**直接负权重写进正文更准**，比堆进 UC 有效。
- **质量词重复注入**：前端预设自动附加 `very aesthetic`/`masterpiece`/`no text`，手写等于叠两遍。默认不写；只在要更高完成度时追加**预设没有的**（`best quality` `amazing quality` `absurdres` `ultra detailed`），放最末尾。
  - 本环境对应：`quality_toggle: true` = 预设开 → 别再手写质量词；`quality_toggle: false` = 预设关 → 手写一层质量头。（与 SKILL.md「单层原则」一致，本文给出机制解释）
- `high/ultra complexity` 是功能开关，不是质量尾，默认不加（有画面固化倾向，实测有加了负权重后画面反而变好的例子）。

---

## 8. 引号 = 要画进图里的文字

- 用**引号**包住要渲染的文字（前端自动生成 `Text:` 块）；**手写 `Text:` 块会关闭这个自动功能**。
- **叙事句不要整段包引号**——那是「要画进图里的文字」的既定语义。1844 条真提示词里包长段引号的只有 2%。
- 引号必须配**载体**（气泡/纸条/招牌/屏幕）并写清位置，否则字会飘。
- 官方：prompt 里要有 `text, english text`（或 chinese/japanese text），`Text:` 放 base **最末**，多段用空行分隔。
- 长度上限（含空白换行）：V4/V4.5 118 · V5 Curated 374 · V5 Full **750**。
- **语言优先级：英日最好，中文欠佳**，其他语言出不了。

---

## 9. 服装状态词的语义陷阱（选错会静默换衣服）

| tag | 真实语义 | 常被误当成 |
|---|---|---|
| `loose socks` | **堆堆袜**（一种粗针棉袜） | ❌「丝袜堆下来」 |
| `single thighhigh` | **只穿了一只**，另一腿光着 | ❌「一只滑下来了」 |
| `uneven legwear` | 两腿袜子**不一样**（语义对但单独写推不动 0/3） | ✅ |
| `asymmetrical legwear` | 同上，更高频 | ✅ |
| `thighhighs pull` | 拉扯丝袜的**动作**（太弱） | ❌ |

**规则：服装状态词用之前查中文释义，别按英文字面推。** 不对称/位置这类状态**用句子写**（实测：含句子 6/6 出不对称，纯词组 0/3）。

---

## 10. 容量、参数、额度

- **1471 token 是软阈值不是硬上限**（超了照样出图，只是更费额度）。实测主提示词+角色栏：中位 **374**、均值 430、p90 742；UC 另计中位 226。画面内文字上限 **750 token**。
- 参数实测（1844 条）：Steps **28**（80%）· Sampler `k_euler_ancestral`（90%）· Noise `karras`（98%）· Guidance 5.0–7.0 无共识 · **PGR(cfg_rescale) 0.0**（官方口径，41%）
- 尺寸：竖 832×1216（最常用）· 1024×1536；方 1024×1024；横 1216×832
- 额度：25 刀档约充 **1600–1700 张**，约 11%/天恢复；**免不免费看分辨率和步数，跟提示词长度无关**；steps 28 是免费临界，29 步起收费
- V5 发布后暂缺三项：**Vibe Transfer · Precise Reference · Curated 局部重绘**（V5 Full 局部重绘已支持）

---

## 11. XML 块不是 NAI 语法

`<artist>` / `<style>` 是某社群的人工分隔符，NAI **不解析**，官方 12 条示例一条都没用。别自造 `<content>` / `<scene>`（语料里出现 0 次）。质量词直接写末尾，不要包块。

---

## 12. 排查表（跨场景）

| 症状 | 处理 |
|---|---|
| 姿势画糊 / 多出一条腿 | 姿势那段写成句子了 → 改 tag（最高频） |
| 机位压不低 | 加 `from below`；三个镜头 tag 别一起上 |
| 整张图变成一片纹理／泥浆 | 画师名以数字结尾紧跟 `::` → 改 `name, ::` 写法 |
| tag 被忽略 | 提权重 / 前移 / 拆独立 tag / 改用整句 |
| 多角色串味 | 句子写死归属 + 编号对应定位 + 检查人数 tag 位置；角色 UC 排除对方特征 |
| 多人图多出人 | UC 里拿掉 `extra characters` 类词 |
| 角色白背景虚空 | `-1::simple background::` + 明确写场景 |
| 逆光面部过暗 | `-2::backlighting::` 或补 `front lighting` / `face lighting` |
| 色调不符 | 加主题色或 `limited palette`；色彩词前移 |
| 想强调腿但出不来 | 别堆 `thighhighs, bare legs`，别用 `leg focus`（太弱）；`from below` 压机位 + 句子写占画幅；要到脚就 `foot focus` |
| 固定物体始终画不对 | 模型知识盲区，换构图思路，别堆 tag |
