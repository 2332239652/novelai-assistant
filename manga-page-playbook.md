# NAI V5 整页漫画规范（2026-09-11 整理）

> **来源**：官方文档 [Models](https://docs.novelai.net/en/image/models) / [Text Rendering](https://docs.novelai.net/en/image/textrendering) / [Multi-Character Prompting](https://docs.novelai.net/en/image/multiplecharacters)；社区实测 skill [Miint-Sunny/nai5-prompting](https://github.com/Miint-Sunny/nai5-prompting)（数据基线 1844 条真提示词 + 4663 张反推）；本环境 2026-09-11 实测。
> **官方口径**：官方模型页确认「V5 甚至能在单张图里做 fully paneled 的漫画生成」——分格是官方能力，不是社区猜测。

---

## 0. 和单人插图最大的区别：逐格描述写在 base，不写在角色栏

常见错误（本环境踩过）是把每一格的角色、动作、对白分别塞进多个角色栏。正确分工是：

| 字段 | 整页漫画里装什么 |
|---|---|
| **base prompt** | 版式声明句 + **每一格一条自然语言描述**（含该格的动作/表情/机位/对白）+ 人数 + 画风/技法 + 质量尾 |
| **角色栏**（Character N） | **只放出场角色的外观**，一角色一格，跨格复用；动作/表情/镜头/场景/背景一律不进 |
| **UC** | 这张图明确不要的东西（两档，见 §7） |

角色栏的作用是「减少角色特征串色」。**同一个角色出现在四格也只开一个角色栏**。

---

## 1. 版式声明：第一句话，用句子写

**格数、排布、有没有边框，全部靠句子**。tag 只有粗粒度的几个，说不了格数和排布：

```
A four-panel manga-style scene …
The page reads top to bottom in four equal panels.
A 3x3 grid of nine headshot portraits …
two-panel comic, one large main illustration and one small rectangular inset
in the lower-right corner, white panel borders
```

可用的版式 tag 频次（danbooru）：`comic` 572k · `4koma` 102k · `2koma` 32k · `5koma` 18k · `multiple 4koma` 4.6k · `square 4koma` · `multiple views` · `reference sheet` 16k · `chibi` 183k · `chibi only` · `chibi inset` · `sticker` 29k · `inset`

漫画构件：`speech bubble` 305k · `thought bubble` 38k · `emphasis lines` 36k · `sound effects` · `halftone` · `screentone`

> 反过来的技巧（官方文字渲染页示例）：不想要气泡时写 `-1::speech bubble::` 负权重压掉。

---

## 2. 逐格一条，每条带方位锚

每格自己的内容自己一条（表情/动作/底色/机位/对白），**格与格不共享句子**：

```
Panel 1: she is asleep at the desk, cheek flattened against an open book.
Panel 2: the alarm goes off; she jolts upright, hair sticking out, eyes still shut.
Panel 3: close on her face as she registers the time, mouth open, sweat drop.
Panel 4: she is already gone — only the toppled chair and a slice of toast in mid-air remain.
```

方位锚用 `top-left` / `bottom-center` / `inset (lower-right)` 这类词写死，bullet 或编号均可。

**一个可偷的创意**：把版式做成画中实物（侦探线索板、相册页、桌上摊开的拍立得），格子变成钉在板上的照片，天然解释了「为什么一张图里有很多小图」。

---

## 3. 对白：绑在「哪一格」上，不是绑在「谁」上

文字渲染节解决的是「**谁**说哪句」（角色↔文字），分格要解决的是「**哪格**说哪句」（格子↔文字）——**两个绑定不能互相代替**。只写角色栏对白会图文错位。

三条要点：

1. **台词写在它所属那一格的句子里**，不要把所有台词攒在开头或结尾一起说——攒在一起模型无法判断归属，这正是错位成因。
2. **每句台词当场说清载体和样式**（气泡形状、颜色、字体粗细、在谁旁边）。只给引号不给载体，文字会飘到画面任意位置。
   ```
   Panel 1: … A small speech bubble above her head reads "zzz".
   Panel 2: … A large jagged bubble beside her reads "I'm late!" in bold black text.
   ```
3. **没有台词的格子明写 `No text in this panel`**。不写的话相邻格台词容易漫进来。

**引号 = 要画进图里的文字**：
- 用引号包住要渲染的文字，前端会自动生成 `Text:` 块；**手写 `Text:` 块会关闭这个自动功能**。
- 叙事句**整段包引号**会被当成要渲染的文字——叙事句直接写，不加引号。
- 引号必须配载体（气泡/纸条/招牌/屏幕），否则字会飘。
- 官方要求：prompt 里写 `text, english text`（或 `chinese text` / `japanese text`），并把 `Text:` **放在 base prompt 最末**；多段文字用空行分隔；`Text:` 之后出现的任何内容都可能被画进图里。
- 长度上限（含空白与换行）：V4/V4.5 **118 字符** · V5 Curated **374** · V5 Full **750**。
- 语言优先级：**英日最好，中文欠佳**，其他语言出不了。中文能出（本环境实测竖排中文约 30 字可读），但逼真度要求高时优先日文/英文。

---

## 4. 人数：按「单格里的人数」算

- 人数 tag 放 **base**，放最前，**只出现一次**：`1girl` `2girls` `1boy` `2other` `girls` `boys` `multiple girls` `solo` `multiple views`
- **分格图的人数按单格里有几个人写**：同一个角色出现在四格 = 每格 1 人 → `1girl`。**不写 `solo`**，也不按格数乘人数。
- `solo focus` ≠ `solo`：多人图聚焦一人时写 `2girls, solo focus`，两者并存合法。
- 角色栏里只写 `girl` / `boy` / `other`，**不带数字**。
- 推荐让「人数 tag 与角色栏格数一致」（`2girls` ↔ 恰好两格）；多格复用同一角色时不适用，按单格人数口径走。

---

## 5. 角色栏放多少：原创和版权是两套

| 角色类型 | 角色栏怎么填 | 最容易犯的错 |
|---|---|---|
| **原创角色**（用户给设定） | `girl/boy/other` 打头，后接**全部样貌锚点**：发色·发型·瞳色·体型·种族特征·耳朵·角·尾巴·翅膀·标志性饰品，**一个都不许精简**。衣服可按画面换 | **删**——砍掉锚点，角色就不是那个角色 |
| **版权角色**（danbooru 认得的） | `girl/boy/other, 角色名` **到此为止**。名字自带全套设定，NAI 靠名字触发。没换装**不要**再列发色/发型/眼睛/配饰 | **添**——逐条列外貌等于把这些特征权重翻倍，还容易跟名字打架 |

共同三条：
1. **性别词写最前**（实测 92% 这么做），跟着角色本身，别默认 girl。
2. **作品名可省**（实测 94% 只写角色名）；拿不准名字拼写时补上有帮助。
3. **动作·表情·镜头·场景·背景一律不进角色栏**，留在 base。

角色名只认 ASCII；拼写必须完全正确；皮肤/换装写在「角色名 (作品名)」之间的括号里，不自造下划线连写。

---

## 6. 笔法：姿势和机位必须用 tag

这是整页漫画里最容易翻车的一点——**长从句描述肢体关系会被"每个从句各画一遍"**：

| 判据 | 证据 |
|---|---|
| **姿势必须词组** | 句子 **3/3 失败**，词组 **3/3 成功**；换第二条画师串复测 1/1，合计 **4/4** |
| **机位高低必须词组** | 句子 3/3 未压低机位（全平视），`from below` 3/3 明确仰视 |

失败方式**不是画错姿势，是把姿势画糊**：多余出一条腿、接不上的胯、腿能数出三段结构、曲起的那条腿整个没画出来。跨两条画风差异很大的串，失败模式一模一样 → 是模型对「长从句描述肢体关系」的处理方式问题。

姿势 tag 表：`sitting` `standing` `lying` `kneeling` `squatting` `sitting sideways` `leg up` `knees up` `crossed legs` `arm support` `head rest` `hand on own cheek` `arms up` `legs up` `hugging own legs` `on side` `on back` `on stomach`

景别：`full body` `upper body` `close-up` `cowboy shot` `wide shot` `portrait`
机位高低：`from below` `from above`
机位水平：`from side` `from behind` `straight on`
朝向：`three-quarter view` `pov` `profile`

**台词/关系/空间/占画幅/光影叙事用句子**；离散事实（人数、体位、机位、景别、道具、种族体征）用 tag。

> 画风上做减法：多格塞的东西多，**单格越简越不糊**。参考作者做法 `minimalism` + `1.3::no lineart::` + `2::chibi, chibi only::`，或 `1.2::rough sketch::`。

---

## 7. 互斥组：这几类各只能挑一个

| 类别 | 只能选一个 | 说明 |
|---|---|---|
| **视线** | `looking at viewer` · `looking to the side` · `looking up` · `looking down` · `looking away` · `looking at another` · `looking back` | 写两个通常两个都不准 |
| **景别** | `close-up` · `portrait` · `upper body` · `cowboy shot` · `full body` · `wide shot` | |
| **背景形态** | `simple background` · `white background` · `detailed background` · `transparent background` · `dark background` · `blurry background` | 别叠 |
| **体位** | `sitting` · `standing` · `lying` · `kneeling` · `squatting` | 多角色例外：一人站一人蹲时两个都要写 |
| **水平机位** | `from side` · `from behind` · `straight on` | `from behind, from side` **不合法** |
| **垂直机位** | `from below` · `from above` | 两者互斥，但可跟水平机位组合（`from below, from side` 合法） |
| **版式** | `comic` · `4koma` · `multiple views` · `reference sheet` · `sticker` | 格数词也别叠 |
| **透明** | `transparent background` · `alpha transparency` · `has alpha` | 不稳定时用 `2.1::transparent background::` |

其他：`close up` 与 `close-up` 是同一个词，挑一个；`depth of field`/`bokeh` 是浅景深虚化，大场景别用（会压掉远景细节）。

---

## 8. UC 与质量词

**UC 只有两档，二选一**：
- 没有要排除的 → 写一行「用默认预设」，**到此为止**。
- 有要排除的 → **只写排除项本身**，不要把预设串再抄一遍拼在一起。

> 本环境 extension 的 `quality_toggle` 等价于前端预设。整页漫画时**必须关掉它**——它会注入 `no text`。若对白死活不出，再把「UC 去掉 `no text`」或正文 `-1::no text::` 当排查手段。另注：官方文字页说 `no text` 通常不碍事，实测也如此，所以先关 toggle 是稳妥但非唯一解。

**质量词是重复注入**：前端预设会自动附加 `very aesthetic` / `masterpiece` / `no text` 三个词，你再写一遍等于同一权重叠两遍。默认一个都不写；只有明确要更高完成度时才追加**预设没有的**那几个（`best quality` `amazing quality` `absurdres` `ultra detailed`），放整条**最末尾**。

`high/ultra complexity` **不是质量尾**，是功能开关，默认不加（有画面固化倾向）。

**多人图的 UC 里不能有 `extra characters`**（以及用户端预设里的那段「多余角色」）——权重 2 的「多余角色」和人数 tag 打架。同理，多人图 UC 里也别反写具体人数（如 `2girls`）去压自己。

---

## 9. 稳定边界与参数

> ⏱️ **连抽间隔硬性 ≥46 秒**（2026-09-11 实测：间隔不足 45 秒直接返回 **403**）。整页漫画一次抽不中就重抽，每次都要等满间隔；**严禁同轮并发**。注意区分 403（速率限制）与 401（令牌失效）。

- 格数越多、每格台词越长，串格概率越高。**四格以内 + 每格一句**是稳的；再多就分两次生成。
- 整页可渲染文字上限 **750 token**（V5 Full）。
- 参数（实测 1844 条）：Steps **28**（80%）· Sampler `k_euler_ancestral`（90%）· Noise `karras`（98%）· Guidance 5.0–7.0 · PGR(cfg_rescale) **0.0**（官方口径）
- 尺寸：竖 **832×1216**（最常用）· 1024×1536；方 1024×1024；横 1216×832

---

## 10. 漫画排查表

| 症状 | 处理 |
|---|---|
| 图文错位 / 台词跑到别的格 | 台词写进所属那一格的句子，说清载体；无台词格明写 `No text in this panel` |
| 台词不出 | 引号包住 + 句子写清载体和位置；仍不出再关 `quality_toggle` / UC 去 `no text`；别手写 `Text:` 块 |
| 文字飘在不该在的位置 | 只写了引号没写载体；补「在谁旁边、什么形状的气泡」 |
| 姿势画糊 / 多出一条腿 | **姿势那段写成句子了**，改 tag。最高频失败模式 |
| 机位压不低 | 句子推不动机位，加 `from below`；三个镜头 tag 别一起上（会盖掉姿势） |
| 格数不对 / 排布乱 | 版式声明句放第一句，用句子写死格数与排布；tag 只有 `comic`/`4koma` |
| 角色跨格漂移 | 角色栏只放一份外观、跨格复用（原创给全锚点 / 版权只写名字） |
| 多人图多出人 | 检查 UC 里没有 `extra characters` 类词；人数 tag 放 base 最前且只一次 |
| 整张糊成一片灰 | 画风做减法；别叠 `ultra detailed` / `complexity`；互斥组只挑一个 |

---

## 11. 三格模板（可直接套）

```
Prompt:
1girl, monochrome, greyscale, comic, screentone, halftone, speech bubble,
有画风词放这里（挂画师串时删掉风格脚手架词）
A black and white manga page laid out in two rows: the top row is split into a narrow
panel on the left and a wide panel on the right, the bottom row is one wide panel across
the page, thin black panel borders.
Panel 1 (top-left): <该格内容 + 该格对白与载体>.
Panel 2 (top-right): <该格内容 + 该格对白与载体…No text in this panel>.
Panel 3 (bottom): <该格内容 + 该格对白与载体>.
质量尾（可选，且只有预设没带的那几个）

Character 1:
girl, <原创：全部样貌锚点 / 版权：只写角色名>

UC:
<只写排除项；没有就写「用默认预设」>
```

---

## 12. 戏剧分镜：让一页「值得被截图转发」

### 12.1 本子的四拍结构

一页有戏的漫画，按**事件**排格，不按"展示人物"排格：

| 拍 | 作用 | 常用格 |
|---|---|---|
| **铺垫** | 交代场景与权力关系（谁在审判谁） | 通栏大格、establishing shot |
| **侵犯** | 第一个越界动作（手探进裙子 / 按住手腕） | 中景 + 手部动作、加拟声词 |
| **绝顶** | 情绪峰值：脸部特写 + 极端表情 | 窄高格、`face focus` |
| **反转** | **钩子**：关系翻转、或一句把全局重新定义的台词 | 通栏大格 |

**反转格是「会不会被转发」的分水岭**。没有反转，只是一页工口；有反转，才值得截图。

**对白承担剧情**：每格一句，写得像真的台词（「証拠は、あなたの身体に聞くわ」优于「気持ちいい？」）。最后一格那句要能**重新定义前几格**。

### 12.2 【重要限制】V5 做不了跨格的角色地位反转

实测（同一页连抽三版）：**每格是独立描述的，模型不继承前几格建立的支配关系**。写「她被夺走木槌、反手抓住对方手腕」，模型仍会把支配方画成原来那个角色。

**解法：把反转从"肢体地位"搬到"表情 + 台词 + 前景景别"**——
- 反转格用**主角的脸占满画面**（`face focus`, `confident smirk`, `half-lidded eyes`, `looking at viewer`）
- 把道具放进**她的手里**（`holding gavel`），而不是描写争抢动作
- 对手放**背景虚化**（`the other girl's shocked face blurred in the background`）
- 身份靠**最有辨识度的锚点**（发色/帽子）锚定，不要指望模型记住"长发的那个"

### 12.3 每格都要用外貌锚点重新指认角色

模型不会稳定跟踪「the long-haired girl」这类指代。**每格重复写发色/标志物**（`the black-haired girl` / `the white-haired girl with a beret`），否则会串人（实测：把举木槌的一方画成了另一人）。

### 12.4 极端表情要加权

`ahegao` 单独写只出到"半闭眼红面"。要真正的绝顶脸：

```
1.4::ahegao::, 1.3::rolling eyes::, 1.3::tongue out::, 1.2::heavy drooling::, tears, heavy blush, sweat, face focus
```

### 12.5 拟声词是真实感的关键

日式漫画的拟声词（`sound effects`）在格内单独成字，比任何画风条都更能"像真本子"：`くちゅ…`（水声）、`ガイ`（抓紧）、`びくっ`（颤抖）。写进该格描述里并列入 `Text:` 块。

### 12.6 尺度的取舍

`rating:explicit` 会让模型放开；但**真正好转发的是"反应特写"而非器官特写**——脸、腿、手、被掀起的裙摆、拉开的衣领，比直给的下体更有张力，也更像真本子。UC 里要**拿掉** `nsfw, nude, sex, explicit`（否则会被压回全年龄）。

---

## 13. 伪造「章节页切片」——伪装度最高的形态（2026-09-13 实测定型）

**目标不是"设计一个本子"，而是"伪造一页从中段撕下来的章节页"。**

### 13.1 切片原则：一页不讲完一个故事

| ❌ 错误做法 | ✅ 切片做法 |
|---|---|
| 铺陈→侵犯→绝顶→反转，一页走完起承转合 | **舍弃前因后果**，从最烫的那一瞬直接切入 |
| 第 1 格交代场景（空教室/空法庭） | **不要 establishing shot**，读者默认"事情已经在发生了" |
| 对白是完整的一句台词 | 对白是**半截话**（破折号开头「——」、省略号结尾），暗示上一页还有内容 |
| 干净整洁的构图 | 衣服半脱、领带松掉、床单攥皱、汗、被拉开的内裤 |
| 结尾给反转或收束 | 结尾**悬在半空**，制造"翻下一页"的冲动 |

### 13.2 伪装信号（按性价比排序）

1. **页码**——最强信号。自然语言写：`A small page number "23" is printed at the bottom right corner.`，并把数字列入 `Text:` 块。实测落位精准。
2. **半截话对白**——破折号开头即可，零成本
3. **"已在进行中"的状态描写**——`shirt unbuttoned, necktie loose, skirt pulled up, crumpled bedsheet, sweat`
4. **本子经典场地**——保健室 / 空教室 / 厕所 / 自室 / 图书室，读者会自行脑补前文
5. **拟声词**——`くちゅ…` / `ぷちっ` / `びくっ`，格内单独成字

### 13.3 已验证的四格切片版式

```
① 上通栏     中段状态：两人已经缠在一起（切入口）
② 中左小格   手部/道具特写 + 拟声（拉内裤、按手腕、道具）
③ 中右窄高格 脸部反应特写（咬手忍声/红面/泪/视线偏开）
④ 下通栏     耳语或下一步推进（低语、耳元、压上去）
                 └─ 页码印在右下角
```

实测配方（魔裁本 · 保健室切片，全部日文渲染成功）：
`infirmary, bed` · `rating:explicit` · 对白「——もう、逃げないよね？」「くちゅ…」「…っ、だめ…」「声、我慢してね」· 页码 23

### 13.4 「色情向意外」是另一类高价值切片

本子常有的意外桥段同样是绝佳的切片素材：**被人撞见 / 门被推开 / 电话响了 / 制服从拉链处崩开 / 摔倒压在一起 / 湿身**。这类页的钩子在**最后一格的「!?」**——门外站着第三者，或两人僵住。

### 13.5 与 §12 的关系

§12（四拍结构）适合**单页要独立成篇**的场合（如测试、单图）。要**伪装成本子内页**时，用本节 §13 的切片法——它才是骗得过人的形态。

### 13.6 纯黑白配方（2026-09-13 实测定型）

默认写法（`monochrome, greyscale` + 带颜色的角色锚点）会**漏色**——实测画出了粉发和红瞳，看起来像"半上色"，反而不像真本子。**三处一起改**才能压干净：

| 位置 | ❌ 漏色写法 | ✅ 纯黑白写法 |
|---|---|---|
| **角色栏** | `white hair, pink hair, pink eyes` / `red eyes, red flower` | 只留**形状与配饰**锚点：`short hair, gradient hair, black beret` / `long hair, hair ornament` |
| **正向** | `monochrome, greyscale` | 加权 `1.3::monochrome::, 1.3::greyscale::` |
| **UC** | 只有 `colored, full color` | 追加**具体色名**：`color, colored hair, colored eyes, pink, red, blue, green, yellow, orange, purple, brown, sepia` |

要点：**不要在正文里写"drawn entirely in black ink, white paper and grey screentone with no colour at all"这类长句**——实测它会被当成画面内容，导致某格画成一块网点/白纸。颜色靠加权 tag + UC 压即可。

### 13.7 首格的「气泡陷阱」

**首个大格如果放了该页最大的对白气泡，模型会把这一格当作"放大台词格"：只画气泡 + 集中线，不画人**（连续三版复现）。

**解法：首格不放气泡，明写 `No text in this panel`**，把台词挪到后面的动作格。撤掉气泡后首格立即恢复正常作画（v4 验证）。

同理可推：**想要某格一定画人，就别让它承担该页的主气泡**。

### 13.8 表情呆板的真正原因（A/B/C 对照实测，2026-09-13）

同一页、同一场景，只改表情层，三组对照：

| 组 | 变量 | 结果 |
|---|---|---|
| **A** | 精简提示词、**无画师串**、只有放在 base tag 区的**全局**表情簇 | 四张脸同一副表情 → **呆板** |
| **B** | A + 画师串 `0.6::tsukushi akihito::` | 线质、睫毛、眼型变细腻，**但表情仍统一** |
| **C** | B + **每格写不同的表情** | 明显生动：焦らし / 快感 / 忍耐 三张不同的脸 |

**结论（按重要性排序）**：

1. **主因是「全局表情簇」**——`heavy blush` / `half-closed eyes` 这类词放在 base 的 tag 区会**均匀作用到所有脸**，导致"全员同一张色气脸"。**表情必须写进各格，且每格不同**。这是"呆板"的头号成因，跟提示词长短无关。
2. **画师串是次要但有效的补充**——它改善的是**脸部画法**（线质、睫毛、眼型、面部阴影），不负责表情强度。黑白漫画可挂漫画家串：`0.6::tsukushi akihito::`（《来自深渊》作者，实测线质更细腻）。注意挂了串要减少风格脚手架词。
3. **提示词过长确实会稀释，但不是主因**——A 组已经把句子压到很短，脸照样呆板；反过来说，句子长但有差异化表情仍然生动。

**写法**：用 `the <发色> girl with <具体面部特征>, <具体面部特征>` 的句式，比单堆 tag 有效。可用的具体面部特征词：

| 情绪 | 面部特征词 |
|---|---|
| 焦らし（忍耐/挑逗） | `half-closed eyes`, `parted lips`, `heavy blush`, `torogao` |
| 快感（被碰） | `rolling eyes`, `tongue out`, `1.3::ahegao::`, `biting own hand` |
| 羞恥 / 我慢 | `eyes squeezed shut`, `gritted teeth`, `tears running down`, `sweat` |
| 身体反应（补充真实感） | `toes curling`, `thighs twitching`, `trembling`, `arched back` |

一句话：**全局表情 = 全员同脸；逐格表情 = 一页三张脸**。
