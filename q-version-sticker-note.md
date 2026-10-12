# Q版贴纸风 · 反读记录（用户指定保留）

> **来源**：2026-10-11 用户提供 `0ef4f42a…42328.png` 的完整元数据（用户手动读取），并指定「这张很特别，暂时不用加入插件，记在本地即可」。
> **性质**：单张 O 级样本，与 391 语料对照后确认是**独立路线**（语料中几乎不存在）。
> **状态**：仅存档，未入 NovelAIPainter 插件、未入 `v5-confirmed-artist-strings.md` 登记册。

---

## 一、核心发现：这张图就是用户预设「9 Q版」的原图

元数据 `Description` 与该用户在插件里使用的**预设 9「Q版」472 字符逐字完全相同**。

→ 结论：不是外部配方，而是该用户自己那档串的实际产出。
→ 说明该预设**已被验证有效**（用户主观评价「很不错」），但用户表示暂不调整。

---

## 二、完整参数（元数据确证）

| 项 | 值 |
|---|---|
| 模型 | `NovelAI Diffusion V5`（model_hash `657484A5`） |
| **steps** | **28** |
| **CFG scale** | **7** |
| **cfg_rescale** | **0.36** |
| **分辨率** | **832 × 832** |
| sampler | `k_euler_ancestral` |
| noise_schedule | `karras` |
| 请求类型 | `NativeInfillingRequest`（原生局部重绘，非纯文生图） |
| `straight_alpha` | `true`（但实测 alpha 极值 254–255，**无实际透明区**） |
| `add_original_image` | `false` |
| `img2img` | `null` |
| `tag_hint_uc_preset` | `2`（官方 Heavy） |
| `tag_hint_qt` | `1`（Quality Tags 开） |
| `skip_cfg_below_sigma` | `0` |
| `prefer_brownian` | `true` |
| `deliberate_euler_ancestral_bug` | `false` |
| 生成耗时 | 1.78 秒 |
| seed | `2780230579` |

### 与 391 语料的对照（四个离群值）

| 参数 | 此图 | 语料 391 张 |
|---|---|---|
| steps | 28 | 28 仅占 11%（主流 23×199） |
| CFG | 7 | CFG 7 仅占 5.9%（主流 5.0×239） |
| **cfg_rescale** | **0.36** | **0/391 用过非 0 值**（315 张为 0） |
| **分辨率** | **832×832** | **0/391 用过**（339 张为 832×1216） |

> 🔑 **CFG 7 + cfg_rescale 0.36 是刻意搭配**：高 CFG 保证贴纸风所需的严格平涂+粗描边贴合度，`cfg_rescale` 抵消高 CFG 的过饱和/色偏。
> 该组合在插件当前固定值（CFG 5 / rescale 0 / 832×1216）下无法复现。

> 📐 832×832 = 692,224 px，仍在免费电量包络（≤1,048,576）内。

---

## 三、正面 prompt（逐字）

```
1girl, 1.0::artist:monyami, artist:channel (caststation):::, 0.9::artist:dorkdragoon::, 0.8::artist:waonaolmao, aida (aidia)::, year 2025, -1::simple illustration ::, best quality, great quality, amazing quality, aesthetic, very aesthetic, highres, super detail, hyper detail, intricate details, detailed incredibly absurdres, skindentation, ultra high resoultion, digital illustration, -1::multiple views ::, speed lines, low angle, , very aesthetic, masterpiece, no text
```

### 结构拆解

| 层 | 内容 |
|---|---|
| 计数 | `1girl` |
| 画师（4 位梯度） | `1.0::monyami, channel (caststation)::` · `0.9::dorkdragoon::` · `0.8::waonaolmao, aida (aidia)::` |
| 年代 | `year 2025` |
| 负强调 ×2 | `-1::simple illustration ::` · `-1::multiple views ::` |
| 质量/细节词 ×16 | 占全 prompt **42%** |
| 动态 | `speed lines` · `low angle` |

### 值得注意的质量词

- `super detail` / `hyper detail` / `intricate details` —— 三个「细节」同义词连打（常规不该堆，但对**平涂风格下仍要求细节**有效）
- `skindentation` —— 勒痕/凹陷质感
- `great quality` —— **非标准档位**（NovelAI 标准档无此项），刻意混入
- `ultra high resoultion` —— **原文拼写错误**（应为 resolution），但照样生效
- 另有 `very aesthetic` 重复出现两次

---

## 四、真正的风格控制力在 UC（核心资产）

UC 头 = 官方 Heavy 预设原样，**后接 600+ 字符自定义尾**。这才是 Q 版的风格来源：

```
bunny ears,                          ← 防误出兔耳（此角色是精灵耳，易混）
anime coloring, anime screencap,      ← 防赛璐璐/动画截图感（要平涂贴纸）
doll,                                 ← 防人偶感
multiple girls, two girls,
extra heads, cloned face, fused bodies, ← 防分身/融体
tall, long body, long neck,           ← ★ 防比例漂移（Q版必须矮小）
multiple panels, comic strip,
manga style, split screen,            ← 防分格/漫画版式
glasses, sweat, shiny hair,
monochrome, greyscale, playboy bunny,
breast ptosis, nostrils, abstract, glowing,  ← 清理不需要的元素
bad hands, missing fingers, six fingers,
bad pupils, bad eyes, another hand,   ← 手部/五官崩坏
worst quality, low quality, bad quality,
normal quality, unfinished, displeasing,     ← 质量兜底
...
2::doll                               ← 末位 2 倍权重再压一次
```

### 三条可复用技法

1. **★ `tall, long body, long neck`** —— Q 版最易翻车点是比例被拉回普通人形，用负面词硬压「变高/变长」是精准解法。
2. **同概念多处压制** —— `doll` 在开头出现一次，末尾再用 `2::doll` 加权重压一次。
3. **风格定位型负面** —— `anime coloring, anime screencap` 不是「坏东西」，而是**排除掉你不想走的画风**（要平涂贴纸而非赛璐璐）。

> ⚠️ 瑕疵：该 UC 的 `::` 只出现 **1 次（奇数）**，`2::doll` 未闭合。影响有限（末尾截断），但严格说是语法瑕疵。

---

## 五、画师池（语料中几乎绝迹 → 独立路线证据）

| 画师 | 权重 | 391 语料出现次数 |
|---|---|---|
| `monyami` | 1.0 | **0** |
| `channel (caststation)` | 1.0 | 2 |
| `dorkdragoon` | 0.9 | **0** |
| `waonaolmao` | 0.8 | **0** |
| `aida (aidia)` | 0.8 | **0** |

→ 这套 Q 版画风是用户**独立于语料**找出来的，不在那批韩网数据里。

---

## 六、两张图的对应关系

| 文件 | 格式 | 元数据 | 说明 |
|---|---|---|---|
| `0ef4f42a…42328.png` | PNG 832×832 | ✅ 完整 | 本笔记主体（捧脸开心 + 摸头） |
| `dacd746e…dfe1.webp` | WebP 1216×832 | ❌ **无**（chunk 仅 `VP8X/ALPH/VP8`，无 EXIF/tEXt） | 吃汉堡那张，无法反读 |

**画风特征比对**（用于判断两者同源）：
- 同一角色：白发精灵耳 + 侧边麻花辫 + 灰色连帽衫（黑色抽绳）+ 黑色蝴蝶结
- 同一风格：粗黑描边 + 平涂色块 + 橙/粉暖底 + 白色雪花状点缀
- 同款表情语言：`> <` 或 `^ ^` 闭合眼 + 大张三角嘴 + 圆形腮红

→ 推断同批产出，但第一张配方**无法确证**（元数据已被剥离）。

---

## 七、如果要复现（备忘，未执行）

```
① 参数：steps 28 · CFG 7 · cfg_rescale 0.36 · 832×832 · k_euler_ancestral · karras
   ⚠️ 插件当前固定 CFG 5 / rescale 0 / 832×1216，需手工调参或改代码

② 正面：预设 9 原文（见 §三）

③ UC：官方 Heavy + §四 的自定义尾（补上 `::` 闭合）

④ 注意：原图是 NativeInfillingRequest（局部重绘），
   若需完全复现还需确认原始底图 —— 当前元数据看不到
```

---

## 附：本笔记的检查来源

- 参数与 prompt：用户提供的 PNG 元数据（`Description` / `Comment` / `v4_prompt` / `v4_negative_prompt` 全部字段）
- 文件结构核验：本地直接解析 PNG chunk 与 WebP RIFF chunk
- 语料对照：`kr_corpus.jsonl`（391 张带完整参数的韩网 V5 成图）
- 图像判读：两张样本已导出并逐张查看
