# 韩网 N5 作品集反读分析报告

> 样本：`<韩网N5语料目录>`
> 935 张图（PNG 156 / WebP 779），**391 张成功反读出完整生成参数**（余 544 张元数据已被上传流程剥离）
> 分析日期：2026-10-09 · 分析方式：本地二进制解析（未依赖 spell.novelai.dev）
> 标注规则：本报告全部结论为**本地实测统计**，非官方文档

---

## 一、元数据承载结构（技术发现，可复用）

### 1.1 NovelAI V5 出图的两种容器

| 容器 | 承载位置 | 备注 |
|---|---|---|
| **PNG** | `tEXt` 块：`Title` / `Description`(正面词) / `Comment`(参数 JSON) / `Software` / `Source` | 早期导出格式 |
| **WebP** | RIFF **`EXIF` chunk** | V5 主流格式，占本样本 83% |

### 1.2 WebP EXIF 的三个坑（PIL 默认读不到）

1. **必须剥离 `Exif\0\0` 前缀**：RIFF EXIF chunk 内容是 `45 78 69 66 00 00` + TIFF 头，不是裸 TIFF
2. **大小端都有**：TIFF 头既可能是 `II`（小端，PIL 常见）也可能是 **`MM`（大端）**——本样本两种混杂
3. **`UserComment` 位置不固定**：tag `0x9286` 可能挂在**根 IFD**（多数），也可能在 **Exif SubIFD**（tag `0x8769` 指向）里。稳健做法是把根 IFD、ExifOffset 指向的 SubIFD、以及 `next IFD` 链**全部遍历**

### 1.3 字段映射

```
EXIF 0x010D DocumentName     = "NovelAI generated image"
EXIF 0x010E ImageDescription = 正面 prompt（少数文件此处是 JSON 包装）
EXIF 0x0131 Software         = "NovelAI Diffusion V5 0ADF9AB7"
EXIF 0x9286 UserComment      = {"Comment": "<完整参数 JSON 字符串>"}
                                └─ 内含 prompt / uc / steps / scale / seed /
                                   sampler / noise_schedule / width / height /
                                   cfg_rescale / v4_prompt.caption.char_captions
                                   （含角色框正文与 centers 坐标）
```

### 1.4 工程注意

- `PIL.Image.open(p).info` **不含 WebP EXIF**，`getexif()` 对部分布局也会漏；大批量扫描建议直接 `struct` 解析 RIFF
- WebP 的图像数据（`VP8 ` / `VP8L` chunk）可能上 MB，**用 `f.seek()` 跳过**，只读 `EXIF` chunk，935 张全扫 < 3 秒
- 本样本 544 张无元数据 = 上传/图床重新编码导致，无隐藏残留（已做尾部字节 + ASCII run 穷尽扫描验证，`IEND` 后无附加数据）

---

## 二、提示词结构规律

### 2.1 总体形态

| 指标 | 数值 |
|---|---|
| 正面 prompt 长度 | 中位 **578** 字符（p90 = 1030，最长 4226） |
| UC 长度 | 中位 **1112** 字符（最长 1847） |
| 使用 `::权重::` 语法 | **391 / 391（100%）** |
| 分段（空行分块） | 72 / 391（18.4%） |
| 平均权重块数 | 正面 8.7 个 + 负强调 1.8 个 |

> ⚠️ **关键结论**：这批作者的 **UC 长度普遍是正面 prompt 的 2 倍**。他们不靠正面词堆砌，而是用极长的负面清单锁死画面上限。这是与「短负面 + 长正面」习惯完全相反的路线。

### 2.2 首块角色分布

| 首块类型 | 数量 |
|---|---|
| 画师串开头 | 190 |
| 质量词开头 | 176 |
| 主体词开头（`1girl, ...`） | 19 |
| 场景词开头 | 4 |

### 2.3 两种主流骨架

**骨架 A · 质量头优先（175 张）**
```
[年份词 + 负强调] → [质量词块] → [画师串] → [主体/构图/场景]
```

**骨架 B · 画师串优先（145 张）**
```
[主体词 1girl/1boy] → [画师串] → [年份] → [场景] → [质量词]
```

**骨架 C · 双头式（17 张）**：画师头 + 质量头分列前后

### 2.4 逐行范本（真实语料）

**范本 1 · 10 画师厚涂（组内 13 张复用）**
```
1.5::mo_(kireinamo) , 0.6::artist:rusellunt::,0.5::artist:kunaboto::, 0.3::artist:mikozin ::,
0.8::artist:wagashi (dagashiya) ::, 0.7::artist:michiking,::, 0.9::artist:manglife ::,
0.5::artist:typehatena ::, 1.1::artist:healthyman ::,0.7::artist:tianliang duohe fangdongye::,
year 2026, year 2025, masterpiece, best quality, amazing quality, very aesthetic,
best illustration, newest, incredibly absurdres, hyper detail, hogwarts, 2koma, 2panels,
doujinshi, very aesthetic, masterpiece, no text
```
→ steps 28 / CFG 7.2 / cfg_rescale 0 / 832×1216 / k_euler_ancestral / karras

**范本 2 · 9 画师「专业漫画感」（组内 17 张复用）**
```
1.2::masterpiece, very aesthetic, best quality, amazing quality, absurdres, highres,
best illustration::, -1::artist collaboration, mosaic::,
1.3::artist:doppel (bonnypir)::, acolored, vibrant colors,
0.8::draw body like artist:henriiku (ahemaru) ::
0.9::artist:yoneyama mai, c.cu, artist:iuui::,
0.4::artist:freng::, 2people, 1girl, 1boy, standing side by side, front view,
wide shot, tatami, dojo set, studio lights, film camera, boom microphone
```
→ steps 23 / CFG 5.0 / 832×1216

**范本 3 · 12 画师光影立绘（组内 11 张复用）**
```
1girl,

0.05::artist:shexyo::, 0.5::artist:inoue_kiyoshirou::, 0.75::artist:anteiru::,
1::artist:gogalking::, 1.15::artist:haze_(7h4ze)::, 1.2::artist:mx2j::,
1.5::artist:yoneyama mai::, 0.75:: artist:pigeon666 ::, 0.5::artist:yesman_(cvbnyesman)::,
0.5::artist:hintobento::, 0.3::artist:takeda hiromitsu::, 0.15::artist:nyantcha::,

year 2024, year 2025, year 2026,

indoors, grand holy cathedral, marble pillars, giant stained glass windows,
golden sunlight beams, floating dust particles, sacred sanctuary,

best quality, amazing quality, very aesthetic, 1::very aesthetic::, 1.5::abusdres::,
1.5:: best illustration ::, 3::masterpiece::, 0.2::high complexity::,
1.5::background with high complexity ::,

1::Digital illustration::, 0.8::cel shading::, 0.3::low saturation ::, 1::soft colors::,
1koma, single frame, full page, nsfw,

-1::simple illustration, artist collaboration, door, doorway, speech bubble,
speech balloon, dialogue bubble, text::, -1.7::thick border::,
```
→ steps 21 / CFG 6.0 / 832×1216
> 💡 注意 `1.5::abusdres::`（拼写错误）仍生效，`3::masterpiece::` 与 `1::very aesthetic::` 单独加权重加强

---

## 三、画师串（核心资产）

### 3.1 高频画师 TOP 20（按出现张数）

| 排名 | 画师 | 出现 | 典型权重 |
|---|---|---|---|
| 1 | `freng` | 235 | 0.4 |
| 2 | `yoneyama mai` | 207 | 0.9 |
| 3 | `henriiku (ahemaru)` | 175 | 0.8（`draw body like` 专用） |
| 4 | `doppel (bonnypir)` | 174 | 1.3 |
| 5 | `iuui` | 174 | 0.9 |
| 6 | `c.cu` | 174 | 0.9 |
| 7 | `hwansang` | 61 | 0.5 |
| 8 | `wanke` | 61 | 0.6 |
| 9 | `murata yuusuke` | 60 | 0.5 |
| 10 | `supernew` | 60 | — |
| 11 | `deadflow` | 60 | 0.8 |
| 12 | `pottsness` | 60 | 0.7 |
| 13 | `yd (orange maru)` | 60 | 0.8 |
| 14 | `uchikaze` | 60 | **2.0** |
| 15 | `ciloranko` | 60 | 0.9 |
| 16 | `pija (pianiishimo)` | 26 | 1.5 |
| 17 | `himemura saki` | 23 | 1.0 |
| 18 | `queasy s` | 22 | 0.8 |
| 19 | `inoue kiyoshirou` | 22 | 0.9 |
| 20 | `meion` / `hizuki akira` / `jonpei` | 22 | 0.9–1.1 |

### 3.2 🔑 关键技法：`draw body like artist:X`

**44.5%（174/391）的作品使用此语法**，是本批语料最有价值的手法：

```
0.8::draw body like artist:henriiku (ahemaru) ::
```

作用：**让该画师只贡献人体结构与比例，不污染整体画风**。与普通 `artist:X` 相比，它把画师影响限制在「身体绘制方式」这一个维度，因此可以安全地叠加在另一个主导画师串之上。

配合方式（实测高频组合）：
```
[主导画风] 1.3::artist:doppel (bonnypir)::
[人体]     0.8::draw body like artist:henriiku (ahemaru)::
[氛围色]   0.9::artist:yoneyama mai, c.cu, artist:iuui::
[兜底]     0.4::artist:freng::
```

### 3.3 权重梯度规律

- 权重区间实测 **0.05 – 2.0**，中枢在 **0.3 – 0.9**
- **主导画师 1.1–1.5**，辅助 0.3–0.9，点缀 0.05–0.3
- **单张图最多 15 位画师**（实测分布）：

| 画师数 | 张数 |
|---|---|
| 0 位 | 84 |
| 1–2 位 | 27 |
| 5–9 位 | 184 |
| 10–15 位 | 96 |

### 3.4 画师数与参数的联动（实测）

| 画师数 | CFG 中位 | steps 中位 |
|---|---|---|
| 0 位 | **6.0** | 25 |
| 1–2 位 | **4.0** | 25 |
| 5–9 位 | **5.0** | 23 |
| 10+ 位 | **5.0** | 23 |

> 结论：**画师越多，CFG 与步数越要降**（多画师互相干扰时高 CFG 会放大冲突）。无画师时反而可以放心拉高 CFG。

### 3.5 同一系列内的画师串惯用「整段复用」

聚类显示 82 种组合中 29 种被复用 ≥3 次，最高单组复用 **173 张**。即：**作者一旦调好一组画师串就整季沿用，只改主体与场景词**。

---

## 四、负强调（写在正面词里的负权重）——最高频技法

**92.8% 的作品**在正面 prompt 内使用 `-N::...::`。幅度分布：

| 幅值 | 出现 |
|---|---|
| -1 | 233 |
| -2 | 179 |
| -3 | 104 |
| -1.5 | 78 |
| -5 | 63 |
| -6 | 24 |

### 4.1 负强调目标 TOP 榜

| 目标 | 次数 | 作用 |
|---|---|---|
| `artist collaboration` | **304** | 阻止多画师被画成「画师合作图 / 多人签名」 |
| `mosaic` | 174 | 解除马赛克 |
| `wide shot` | 60 | 压制自动拉远镜头 |
| `multiple views, speech bubble, text, background human` | 60 | 防分格 / 防气泡 / 防背景路人 |
| `anatomical nonsense` | 60 | 修解剖 |
| `simple illustration` | 44 | 防简化 |
| `flat color` | 32 | 防平涂 |
| `thick border` | 11 | 防粗黑边 |
| `thighs, shoulders, legs, arms` | 18 | 反向控制肢体不出现 |

### 4.2 可直接复用的两个句式

```
-1::artist collaboration, mosaic::
-6.0::artist collaboration::          ← 最强档，用于严防画师互串
-2::wide shot::
-2::multiple views, speech bubble, text, background human::
-5::anatomical nonsense::
-3::simple illustration::
```

> ⚠️ 本 skill 此前记录过「大倍数负强调曾致崩坏」，属**本环境特定路径**问题。本批语料中 `-5` / `-6` 大量稳定出图，说明该现象与镜像/通道相关，不是 V5 的普遍限制。

---

## 五、UC（负面词）规律

### 5.1 高复用模板

54 种不同 UC 字符串中，**前 3 种覆盖 190 张（48.6%）**。

### 5.2 核心 UC token（≥60% 作品共有，共 37 项）

```
very displeasing, lowres, worst quality, jpeg artifacts, artistic error,
bad quality, logo, film grain, multiple views, dithering, blank page,
scan artifacts, chromatic aberration, halftone, screentone, too many watermarks,
bad hands, unfinished, negative space, incomplete, nsfw, disfigured,
disorganized colors, cheesy, signature, extra legs, deformed, extra digits,
bad eyes, monochrome, bad hand structure, fewer digits, 1990s (style),
artist:milkpanda, fewer details, reference, chibi
```

### 5.3 标准 UC 头（可直接复用，本语料最通用）

```
nsfw, lowres, artistic error, film grain, scan artifacts, worst quality, bad quality,
jpeg artifacts, very displeasing, chromatic aberration, dithering, halftone, screentone,
multiple views, logo, too many watermarks, negative space, blank page,
```

### 5.4 画师黑名单（防止特定画风污染）

```
artist:xinzoruo, artist:milkpanda
```
→ 出现率 62%（`milkpanda`）/ 53%（`xinzoruo`），是这批作者的共识黑名单

### 5.5 值得注意的 UC 写法

- `0::ai-generated::` —— 用 **0 权重**「提及但不激活」，作为占位式排除
- `1.2::worst quality::` —— 给负面词本身加权重强化
- `3::2koma::, 2::multiple views::` —— 用正权重压制分格
- `red bed, red sheet, red bedding` —— **场景级定向排除**（防止不该出现的红色床品串味）

---

## 六、NSFW 专用技法

| 技法 | 用法 | 出现率 |
|---|---|---|
| `faceless male` | 男方不画脸，降低崩坏率 | 18.9% |
| `uncensored` | 解除审查 | 19.7% |
| `background human` | 主动生成背景路人（营造场景感） | 15.3% |
| `multiple boys` | 多人场景 | 13.3% |
| `minigirl` | 透视缩小人物（用于体内/手中等极端镜头） | 7.2% |
| `species transformation` / `mid transformation` / `under transformation` | 变身过程分帧 | 11.3% |
| `speech bubble` + `English text, black text "..."` | 精确对白渲染 | 18.4% |

**复合镜头词串**（实测完整可用）：
```
pussy, penetration, large insertion, stomach bulge, onahole position,
grabbed by another's hand, squeezed by another hands, head back, head up,
fucked silly, onhand, arms, legs, thighs, shoulders, teardrop, turned pale, scared
```

**文字渲染放在独立角色框**（而非 base）：
```
角色框 2: Large text, title, Blue characters, English text:Arch Priest
角色框 3: Heart, Devil Tail, Large text, title, Pink characters, English text:and Succubus
```

---

## 七、🔑 韩文混用（36.1%）

**141 / 391 张在角色框或场景描述里直接使用韩语**，模型能正确理解：

| 韩文 | 含义 | 用途 |
|---|---|---|
| `대머리` | 秃头 | 角色特征 |
| `넘어져 쓰러짐` | 摔倒 | 动作 |
| `개가 옷을 잡아 물어 뜯음` | 狗咬住衣服撕扯 | 复合动作 |
| `앞치마를 묶음` | 系围裙 | 动作 |
| `화난 표시` / `아쿠아의 뺨을 양손으로 꼬집는다` | 生气表情 / 双手捏 Aqua 的脸颊 | 表情+动作 |
| `옆모습, 마주보고, 테이블을 사이에 두고` | 侧脸、面对面、隔桌 | 机位 |

> 💡 这印证了 V5 的多语言能力：**当英语标签难以精确表达复合动作时，直接用母语自然语言描述是有效策略**。本样本 0% 使用日文/中文，说明该能力并非日语专属。

---

## 八、角色框（Character Frames）

| 指标 | 数值 |
|---|---|
| 使用角色框的作品 | 318 / 391（81.3%） |
| 全部带 `centers` 坐标 | 318 / 318（100%） |
| 角色 caption 长度中位 | 171 字符 |

### 框数分布

| 框数 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| 张数 | 57 | 123 | 50 | 70 | 11 | 5 | 2 |

### 写法特征

- **全部坐标定位**：`centers` 使用 `x/y ∈ [0,1]` 连续值，不用 AI's Choice
- **2 框（男女互动）是最大宗**：女角写满细节，男角极简
  ```
  框1: girl, nagisa (swimsuit) (blue archive), wide hips, thick thighs, huge ass,
       spread legs, presenting pussy, pussy, labia, clitoris, spread own pussy,
       raised inner eyebrows, nervous smile, looking at own pussy, close-up,
       ass focus, pussy focus, nsfw, completely nude, open mouth, anus
  框2: boy, faceless male, large penis, testicles, thighs          ← 极简
  ```
- **坐标示例**：`{"x": 0.652, "y": 0.51}`（主角色偏右下）、`{"x": 0.18, "y": 0.183}`（男角左上角）
- **同一角色可开多框**（不同镜头/不同格）
- **变体角色用同框多细节**：`draco malfoy, genderswap (mtf), straight hair, slytherin, green eyes, ringed eyes, tsurime, ...`

---

## 九、参数实测分布

| 参数 | 分布 | 中位/主导 |
|---|---|---|
| **steps** | 23×199 · 25×105 · 28×43 · 24×22 · 21×12 · 20×6 · 18×2 · 26×1 | **23** |
| **CFG scale** | 5.0×239 · 6.0×42 · 7.2×38 · 7.0×23 · 4.0×20 · 4.5×18 · 4.2×6 | **5.0** |
| **cfg_rescale** | 0.0×316 · 0.4×35 · 0.3×14 · 0.1×11 · 0.2×10 · 0.5×4 | **0.0** |
| **sampler** | `k_euler_ancestral` 390 / `k_euler` 1 | **k_euler_ancestral** |
| **noise_schedule** | `karras` 391 / 391 | **karras** |
| **resolution** | 832×1216 ×339 · 1024×1024 ×32 · 1216×832 ×16 · 1280×1280 ×2 | **832×1216** |

> ✅ **重要交叉验证**：这批高阶作者的选择与本 skill 此前的推荐**高度吻合**——CFG 5.0 主导（本 skill 「V5 可从 5 起步」）、steps 23 主导（本 skill 「20-23 稳定带」）、832×1216 主导（免费包络内）。且 **100% 使用 `k_euler_ancestral` + `karras`**。

> 💡 **cfg_rescale 新发现**：316 张为 0（不启用），但有 **75 张启用 0.1–0.5**。启用者多集中在 CFG ≥6 或画师数 ≤2 的场景——说明它确实是「高 CFG 过饱和」的补偿手段，与本 skill 记录一致。

---

## 十、可直接吸收进 skill 的规则清单

### R1 · 画师串标准范式（新增）
```
[主导画风] 1.1~1.5::artist:A::
[人体结构] 0.6~0.9::draw body like artist:B::      ← 只借人体，不污染画风
[氛围配色] 0.8~1.0::artist:C, artist:D, artist:E::
[兜底统一] 0.3~0.5::artist:F::
```
配合负强调 `-1::artist collaboration, mosaic::`

### R2 · 负强调配置（新增/强化）
- `-1::artist collaboration, mosaic::` 作为**所有多画师图的默认项**
- 镜头失控时：`-2::wide shot::`
- 画面被切成多格时：`-2::multiple views, speech bubble, text, background human::`
- 解剖崩坏时：`-5::anatomical nonsense::`
- 画风被简化时：`-3::simple illustration::` / `-2::flat color::`

### R3 · UC 长度策略（修正认知）
本语料 **UC ≈ 2 × 正面 prompt 长度**。此前 skill 的 UC 五层模板方向正确，但**应当敢于拉到 800–1200 字符**。

### R4 · 参数联动（新增）
- 画师 0 位 → CFG 6.0；1–2 位 → CFG 4.0；**5 位以上 → CFG 5.0**
- 画师 5 位以上 → steps 23；0–2 位 → steps 25
- `cfg_rescale` 仅在 CFG ≥6 时考虑开 0.3–0.4

### R5 · 多语言混用（新增）
精确复合动作无法用 Danbooru tag 表达时，**直接用母语自然语言写进角色框**（本样本 36% 韩文验证有效）。

### R6 · NSFW 男方极简原则（强化）
`faceless male` + 只写性器官相关词，其余全留给女方框。

### R7 · 角色框坐标（强化）
**应使用显式 `centers` 坐标**而非 AI's Choice——318/318 实测。

### R8 · `0::tag::` 占位排除法（新增）
用 `0::ai-generated::` 把某个词「写进 UC 但不激活」，作为可随时调权的占位。

---

## 十一、逐图精读发现（2026-10-09 补 · 12 张全图人工通读）

> 方法：从 12 个风格族各抽 1 张（共 12 张），**导出图片实际观看 + 完整记录逐字通读**。
> 这一步纠正了纯统计得出的一些偏差——统计能看出「出现频率」，看不出「作者在想什么」。

### 🔴 重大纠正 1：`faceless male` **并不会让男方没脸**

**看图的直接证据**：
- 样本 04（道场对峙）：男框写了 `faceless male`，**画面里男方有完整的脸**（侧脸、微笑、秃头特征全部可见）
- 样本 05（三人场景）：男框写了 `faceless male`，**上方男方有明确的侧脸与笑容**
- 样本 07（献花场景）：男框写了 `faceless male`，**男方正脸完全画出来了**

**代码核实**：130 个含 `faceless male` 的框里，**66.9%（87 个）同时写了面部词汇**（`smile`/`grin`/`laugh`/`smirk` 等）。

> **结论修正**：`faceless male` 不是「把脸去掉」的指令，它更接近**「这是个不重要的男性配角」的语义标签**，或者理解为**「不需要刻画他的脸」= 不用给脸部细节，但该有脸还是有脸**。
> 之前统计推出的「不写面部词汇就能无脸」也**不成立**——样本 04/05/07 都没给男方写脸部细节词，但脸照样画出来了。
> ⚠️ 真正想彻底去掉男方脸，得用 **`head out of frame` / 构图裁切**（样本里 `head out of frame` 只占 0.8%，说明这批作者**根本不在意男方露脸**）。

### 🔴 重大纠正 2：base prompt 的尾部是**一整句自然语言动作描述**

精读样本 01/04/05/07 的 base prompt 尾部形态：
```
… massage room, massage bed with white sheet,
  the second masseur pours oil on her back, nude, explicit          ← 完整英文句子

… dojo, tatami,
  woman barely standing with trembling knees,
  fluid running down her thighs, man facing her, wide shot, full body, explicit

… dojo, tatami,
  woman on all fours sucking a man's penis and stroking another with
  one hand while a third man penetrates her pussy from behind,
  side view, full body, explicit
```

**42/391（10.7%）** 的 base 尾部有这种 ≥10 词带动词的完整句子，且**几乎全部集中在「道场」这一族**（2026-10-03/10-04/10-05 的 3 个目录）。

> 这族人手写的不是标签串，而是**一句先定动作、再用 3-4 个标签收尾构图（`side view, full body, dojo, tatami, explicit`）的「句子 + 标签」混合体**。
> 配合「全部框坐标 = (0.5,0.5)」的特点（见纠正 3），这一族本质上是**用自然语言当导演、放弃坐标控制**的流派。

### 🔴 重大纠正 3：「角色框」有近半不是人物，而是**道具/手/人群/文字槽位**

832 个角色框里，**378 个（45.4%）完全不含任何人物名词**。实际用途：

| 槽位类型 | 数量 | 逐字样本 |
|---|---|---|
| **手/肢体单独成框** | 294（35.3%） | `hand entering frame from the edge of the screen, thumbs up, director's hand` |
| **道具/物件** | 186（22.4%） | `puddle, wet tatami, urine puddle spreading on the floor`<br>`large wet stain on the white sheet`<br>`clapperboard, hand holding clapperboard, foreground` |
| **文字/标题框** | 51（6.1%） | `speech bubble, text: "Action!"`<br>`Large text, title, Blue characters, English text:Arch Priest` |
| **人群/背景** | 27（3.2%） | `faceless crew members applauding, clapping hands, smiling, in the background` |
| **视觉特效** | 11（1.3%） | `motion lines`、`sound effects`、`Heart, ~~, !!` |
| **动物** | — | `dog, 1.2::biting clothes, pulling down clothes with mouth::` |

> **这是最高价值的发现**：角色框不是「一个人一个框」，而是**「一个画面元素一个框」**。
> 手、道具、体液、文字、人群各自独立占框并**带自己的坐标**——这正是它们能做到精确构图（左手在左、右人在右）而不用自然语言描述方位的原因。
> 样本 07 用了 4 个框表达：`女方持花束` + `秃头男鼓掌` + `导演的手入镜` + `背景工作人员鼓掌`，**其中只有 2 个是「人」**。

### 4. 框尾的「氛围总结句」

108/832（13.0%）的角色框在标签后追加一句**氛围定性**，句式高度模板化：
```
…, {身份} {气质词}, wearing {装备细节} in {场景}
```
实例：
```
sacred paladin beauty, wearing gleaming white-gold plate armor with revealing
  cleavage cutout and highleg bodysuit in holy cathedral
intimidating dark knight presence, wearing cropped black steel cuirass revealing
  prominent underboob and sculpted abs in obsidian fortress
fierce dragon knight elegance, wearing metallic dragon scale bikini armor
  exposing cleavage and bare thighs on windy mountain peak
```
> 这是**「气质定位 + 服装复述 + 场景复述」三合一的收尾句**，同族内句式完全一致（同一作者批量生产时复用模板）。

### 5. 两套坐标策略并存（各占一半）

| 策略 | 占比 | 集中族 |
|---|---|---|
| **全部框 = (0.5, 0.5)** | **56.9%**（181/318） | 道场族（72+38+38+26 = 174 张） |
| **真实分布坐标** | 43.1%（137/318） | 其余各族 |

> `(0.5,0.5)` 不是「正方构图」，而是**放弃坐标、把摆位交给 prompt 描述**——这一族全靠 base 尾部的自然语言句 + 角色框的动作词来定位置。
> 反过来，采用真实坐标的族（如样本 01 的按摩场景）就用 4 个框 + 方位描述做精确调度。

### 6. 逐字确认的特殊语法（都是小规模用法，别当通用规则）

| 语法 | 占比 | 实例 |
|---|---|---|
| `panel-N:` 分格前缀 | 1.8%（7 张） | `panel-1: girl, draco malfoy, …` |
| `style:` 前缀 | 2.3%（9 张） | `style:eiyuu densetsu::`、`{style:mabinogi}` |
| `\|` 分隔符 | 4.6%（18 张） | `very aesthetic, amazing quality, no text\| awa subaru, qudaraple amputee…` |
| 转义括号 `\(` `\)` | 0.5% | `sen no kiseki \(series\)` |
| `Scene N` 编号脚本 | 0.3%（1 张） | 样本 10 的整页漫画 |
| 字符表情 `:o` `;D` | 5.9% | `:o`、`;D` |

### 7. 精读暴露的一处「作者笔误」

样本 03 的角色框：
```
boy,  boy,satou_kazuma(konosuba),…        ← "boy," 重复了两次
```
样本 08：
```
solo,0.6::rusellunt::,…                   ← 前缀写了 solo 但后面是双人场景
```
> 说明**这批高阶作者也会写错**，且错字不影响出图（样本 03/08 都正常）——不必过度追求 prompt 完美。

---

## 十二、🔴 根目录外放图 vs 子目录批量图 —— 两条完全不同的审美路线

> **2026-10-09 用户指正**：「你挑的图都是一些韩国风格的，基本不是我喜欢的类型。直接在文件夹里找外放（没有二级文件夹）的图片，那些基本都是优秀精品。」
>
> 重新分析后确认：这个合集里存在**两个截然不同的批次**，我此前只看了子目录那批（占 96%），完全错过了用户真正欣赏的根目录那批。

### 12.1 样本划分

| 批次 | 数量 | 位置 | 性质 |
|---|---|---|---|
| **根目录外放** | 116 张（13 张带完整元数据） | 合集根目录，无子目录 | ⭐ **用户指定：优秀精品** |
| **子目录批量** | 819 张（378 张带完整元数据） | 31 个日期命名的子文件夹 | 批量产出（我此前误当作样本主体） |

### 12.2 特征对比（13 vs 378）

| 特征 | 根目录（精品） | 子目录（批量） | 差异 |
|---|---|---|---|
| **非标准分辨率** | **23.1%** | 0.3% | ⭐ 77× |
| **白底 / 简单背景** | **30.8%** | 2.4% | ⭐ 13× |
| **画风技法词**（`(medium)`/`pixel art`/`oekaki`/`hatching`/`hand-drawn`） | **30.8%** | 3.2% | ⭐ 10× |
| **`cfg_rescale` > 0** | **61.5%** | 18.0% | ⭐ 3.4× |
| **画师数 ≥ 8** | **53.8%** | 25.7% | 2.1× |
| **角色框 ≤ 1 个** | **61.5%** | 32.3% | 1.9× |
| **漫画结构**（koma/panel/manga） | **38.5%** | 16.9% | 2.3× |
| **非默认 steps**（非 23/25/28） | **38.5%** | 10.3% | 3.7× |
| NSFW 硬核占比 | 31%（更低） | 48%（更高） | 精品更含蓄 |

### 12.3 根目录精品的三条核心路线

**路线 A · 画师串调色板（最主流）**
大量堆画师（中位 8 位、最多 15 位），用**高 CFG + cfg_rescale 压过饱和**，追求画风独特性：
```
R01  steps 26 · CFG 7.5 · rescale 0.02 · 1024×1024
     1.5::artist:ask (askzy)::, 1.4::artist:liduke::, 1.3::artist:(mikel (1013mik))::,
     1.2::artist:rusellunt::, 1.2::artist:(hibi08)::, 1.1::artist:messikid::,
     1.0::artist:gogalking::, 0.9::artist:(as109)::, -1::artist collaboration::
     1girl, running, run, street, panicked expression, flustered, looking over shoulder,
     a floating penis is chasing her, flying, detailed penis and testicles,
     realistic (anatomy), mid-air, penis,, very aesthetic, masterpiece, no text
```
> 💡 注意：**画师列表本身几乎就是完整的 prompt**，场景描述极简（只有 1 句）。这跟子目录那批「长质量头 + 长负强调 + 长场景」的堆砌路线完全相反。

**路线 B · 特殊媒介风（子目录完全没有的）**
用 `(medium)` 系列标签定义**画风媒介**，走非主流美术路线：
```
R08  steps 28 · CFG 7.0 · rescale 0.28 · 1216×832
     2::color ink (medium)::, 0.6::millipen (medium), hatching shading, hand-drawn::
     -1::flat color::, -2.0::art program in frame::, -2.0::art tools in frame::

R09  steps 22 · CFG 4.0 · rescale 0.2 · 832×1216
     4.0::aliasing::, pixel art, 2.0::microsoft paint (medium)::, 2.0::oekaki::
```
> `color ink (medium)` + `millipen (medium)` + `hatching shading` + `hand-drawn` = **钢笔手绘墨水画风**
> `pixel art` + `microsoft paint (medium)` + `4.0::aliasing::` = **刻意保留像素锯齿的低像素画风**（用超高权重 aliasing **制造**锯齿，常规做法是消除它）

**路线 C · 整页漫画 / 分格叙事**
```
R04  steps 28 · CFG 6.0 · rescale 0.4 · 1280×1856（非标准尺寸）
     2::manga, comic, monochrome, best quality, amazing quality, very aesthetic,
     incredibly absurdres, multiple views, comic::
     teXt: 제발 일생의 부탁이야!        ← 韩文对白直接写进 teXt:
     5 个角色框，每框一个 panel
```
> 与子目录那批的漫画页不同：**根目录的漫画是「一图多格 + 完整对白」的成稿**，子目录的是草图式分镜。

### 12.4 根目录独有的画师（子目录没有的 57 位）

根目录 77 位画师中，**57 位（74%）在子目录里从未出现**——两条路线几乎不共享画师池：

```
ask (askzy) · liduke · (mikel (1013mik)) · (hibi08) · messikid · (as109)
mamerakkkkko · onono imoko · memekko · kotoyama · azz0422 · letdie1414
horikoshi kouhei · dsmile · nonddu · billbung · cocoballking · teshima nari
kat (bu-kunn) · hechima (issindotai) · taaru (taru) · kubo tite · kuroboshi kouhaku
ankoman · abara heiki · zyugoya · ssambatea · michibata 65 · crain1art
hamada yoshikazu · arikanrobo · petosu (sunoco) · rehu (astd5787) · kaisen chuui
aoi sakura (seak5545) · creamyghost · riko-m · u u ki u u · hyde (tabakko)
tostantan · yamamoto souichirou · inoino · j@ck · atelier bono · kagto (alterna)
mochizuki kei · mi 398 · fungi542 · songchuan li · tuda6 · kimtoxic · nishi yasuaki …
```
共用画师仅 20 位：`rusellunt` · `gogalking` · `mx2j` · `healthyman` · `meme50` · `shexyo` · `inoue_kiyoshirou` · `anteiru` · `haze_(7h4ze)` · `yoneyama mai` · `pigeon666` · `yesman_(cvbnyesman)` · `hintobento` · `takeda hiromitsu` · `nyantcha` · `wagashi (dagashiya)` · `henriiku (ahemaru)` · `himemura saki` · `ie (raarami)` · `channel (caststation)`

### 12.5 ⚠️ 方法教训

统计分析的**样本选择本身会决定结论**。我按目录分层抽样，正好全落在占 96% 的子目录批里，于是把「韩式批量产出风格」当成了整个合集的代表。
**正确做法**：抽样前先确认**文件夹结构本身是否携带语义**——本例中「根目录 vs 子目录」就是用户自己做的质量分级。

### 12.6 完整配方

13 张的逐字配方（含画师串、完整 prompt、角色框）已单独存档：见 `root-curated-recipes.md`。

---

## 十三、数据资产位置

| 文件 | 内容 |
|---|---|
| `kr_corpus.jsonl` | 935 条完整反读记录（含 prompt / uc / params / characters / centers） |
| `kr_analysis.json` | 标签频次、画师频次与权重、UC token 统计 |
| `kr_clusters.json` | 画师串聚类结果 |
| `kr_deep.json` | 结构角色序列、UC 模板核心、负强调目标榜 |
| `_sample_view/01-12.jpg` | 精读用 12 张**子目录**样本（人工通读素材） |
| `_root_view/R01-12.jpg` | 精读用 12 张**根目录精品**样本 |
| `kr_sample_contact_sheet.jpg` | 子目录 12 张拼图 |
| `kr_root_all_contact.jpg` | 根目录全部 116 张拼图（看整体口味用） |

路径：`<工作目录>\`

**skill 内配套文件**：[root-curated-recipes.md](<skill目录>\root-curated-recipes.md)（13 张根目录精品的逐字配方 + 题材索引）
