# NovelAI 提示词模板库

## 通用提示词框架

### 推荐标签顺序
```
[画师tags], [画质tags], [角色数量/独唱], [角色名称], [发型], [发色], [眼睛], [表情], [服装], [姿势动作], [构图], [背景], [光影], [色彩/氛围], [额外细节]
```

### V4.5 Curated 最佳实践模板

**开启 Add Quality Tags 时的基础结构：**
```
[artist tags], 1girl, solo, [hair], [eyes], [expression], [clothing], [pose], [background], [lighting], [atmosphere]
```
> 系统会自动追加 `, very aesthetic, location, masterpiece, no text, -0.8::feet::, rating:general`

**关闭 Add Quality Tags 时手动控制：**
```
[artist tags], {{{{masterpiece}}}}, {{{best quality}}}, very aesthetic, absurdres, 1girl, solo, [detailed description...]
```

---

### V5 推荐模板

V5 官方明确支持更强的自然语言、多人角色、透明度和文字渲染。实用默认写法是：base 描述场景/布局/光线/氛围，角色框分别描述角色；用角色名、关键外观、视角和特殊能力标签做少量锚定。画师串和权重属于经验调参，先保留简单基线。

```
[optional artist tags], 1girl, solo, high complexity,
A girl with long silver hair stands beneath cherry blossoms in a quiet park;
soft morning light filters through the branches, with a cinematic medium shot.
```

**V5 多角色 + 角色框：**
```
base: 2girls, indoors, a warm classroom after sunset; the first girl stands on the left,
the second girl sits on the right, both facing each other in a calm conversation.
character 1: girl, blue hair, school uniform, left side, attentive expression
character 2: girl, red hair, casual clothes, right side, seated, gentle smile
```

官方建议人数标签放 base，角色框只写 `girl`/`boy`/`other`，不要在角色框重复数字。位置可用界面自定义定位；当前 MCP 的 `center_x/center_y` 和 `aic` 是实现映射，不能当作所有客户端都相同的语法。

**V5 多角色大合照（学校合照式）：**
```
14girls, school group photo, class photo; the students stand in three neat rows,
with the back row elevated on steps, the middle row standing, and the front row seated,
natural smiles, looking at the viewer.
```

**V5 文字渲染：**
```
1girl, solo, holding a sign, text, english text, bright outdoor light.
Text: HELLO WORLD
```

**V5 中文文字：**
```
1girl, solo, holding a sign, text, chinese text, classroom, daytime.
Text: 你好世界
```

官方长度上限：V5 Full 的 Text ≤750 字符，V5 Curated ≤374 字符，包含空格和换行；`Text:` 必须位于整个 base prompt 最末。

**V5 透明背景：**
```
1girl, solo, transparent background, has alpha
```

V5 官方确认支持 alpha transparency；当前 API/客户端若有透明开关，输出应选 PNG 以保留 alpha。`fake transparency` 是绘制假棋盘格效果的经验标签，不等于真正透明。

---

## 场景模板

### 1. 角色立绘/设定图

**V4.5**:
```
1girl, solo, full body, standing, center, [hair], [eyes], [clothing details], [accessories], simple background, white background, {{{masterpiece}}}, {best quality}
```

**UC**:
```
worst quality, low quality, blurry, text, watermark, extra fingers, bad anatomy, bad proportions
```

### 2. 肖像/特写

```
1girl, solo, portrait, close-up, [hair], [eyes], [facial expression], detailed face, [lighting], {masterpiece}, {best quality}, very aesthetic
```

### 3. 动态战斗场景

```
1girl, solo, action pose, dynamic angle, [weapon], battle outfit, battlefield, fire, explosion, debris, speed lines, {cinematic lighting}, {{masterpiece}}, high contrast
```

### 4. 浪漫氛围

```
1girl, solo, [dress/clothing], sunset, beach, wind, flowing hair, smile, looking at viewer, {cinematic lighting}, bloom, bokeh, romantic atmosphere, {{{masterpiece}}}
```

### 5. 黑暗奇幻

```
1girl, solo, dark fantasy, [dark outfit], castle interior, candlelight, mysterious atmosphere, dramatic shadows, {{{{masterpiece}}}}, {best quality}, very aesthetic, [[simple background]]
```

### 6. 赛博朋克/都市

```
1girl, solo, city night, neon lights, rain, wet street, reflection, cyberpunk, glowing eyes, from side, {cinematic lighting}, vibrant colors, high contrast
```

### 7. 可爱/治愈风

```
1girl, solo, smile, gentle smile, soft lighting, pastel colors, [cute outfit], flower field, bloom, {masterpiece}, very aesthetic, dreamlike atmosphere
```

### 8. 泳装/夏日

```
1girl, solo, swimsuit, beach, ocean, blue sky, sunny, smile, {masterpiece}, {best quality}, very aesthetic, [sunlight], [wind]
```

---

## 画师混合模板

### 单一画师主导
```
{artist_name}, 1girl, solo, [描述...], {masterpiece}, best quality
```

### 两个画师混合 (各50%影响)
```
{artist1}, {artist2}, 1girl, solo, [描述...], {masterpiece}, best quality
```
> 建议 CFG 3.5 左右

### 主画师 + 辅助风格
```
1.2::artist_main::, 0.7::artist_secondary::, 1girl, solo, [描述...]
```

---

## 常见题材模板

### 古风/汉服
```
1girl, solo, hanfu, traditional Chinese clothing, [hair accessories], [dress details], ancient Chinese architecture, cherry blossoms, {masterpiece}, {best quality}, very aesthetic
```

### 和服/日式
```
1girl, solo, kimono, [kimono pattern/details], traditional Japanese, temple, garden, sunset, {{{{masterpiece}}}}, very aesthetic
```

### 女仆装
```
1girl, solo, maid outfit, [apron], [headpiece], [stockings], indoors, cafe, smile, {masterpiece}, best quality, very aesthetic
```

### 睡衣/居家
```
1girl, solo, pajamas, [loungewear], bedroom, messy hair, sleepy, morning, soft lighting, {masterpiece}
```

### 婚纱/礼服
```
1girl, solo, wedding dress, veil, bouquet, church / garden, sunlight, {{{{masterpiece}}}}, {best quality}, very aesthetic, bloom
```

---

## 权重调节实战模板

### 强调面部特征
```
1girl, solo, {face}, detailed face, [hair], {eyes}, {expression}, close-up, portrait
```

### 弱化背景
```
1girl, solo, [simple background], detailed character, portrait, urban, blurry background
```

### 强调画师风格
```
1.5::artist_name::, 1girl, solo, [描述]
```

### 精确控制 - 混合权重
```
1.2::masterpiece::, 1.1::best quality::, 1girl, solo, long hair, 0.8::bangs::, {{blue eyes}}, smile, dress, standing, garden, [simple background]
```

---

## V4.5 Curated 默认 Quality Tags 解析

当开启 "Add Quality Tags" 时，系统自动追加：
```
, very aesthetic, location, masterpiece, no text, -0.8::feet::, rating:general
```

| 标签 | 作用 |
|------|------|
| `very aesthetic` | 美学优化 |
| `location` | 引导模型生成场景背景 |
| `masterpiece` | 画质提升 |
| `no text` | 避免生成文字 |
| `-0.8::feet::` | 削弱足部出现概率 |
| `rating:general` | 普通/全年龄评级 |

---

## V4.5 Full vs Curated

| 方面 | Curated | Full |
|------|---------|------|
| 默认 Quality Tags | 开启并自动追加 | 需手动添加 |
| 风格稳定性 | 较高，画师追随性好 | 自由度更高 |
| 适合场景 | 常规创作、画师风格模仿 | 创意探索、实验性作品 |

---

## 元素魔法速查

来自社区《元素法典》的特定效果配方：

| 效果 | 关键标签 |
|------|---------|
| 水面反射 | `water reflection`, `lake`, `mirror image` |
| 水晶/透明 | `crystal`, `gemstone`, `transparent`, `sparkle` |
| 火焰特效 | `fire`, `flame`, `burning`, `explosion` |
| 光影氛围 | `volumetric lighting`, `god rays`, `sun rays` |
| 星空/宇宙 | `starry sky`, `galaxy`, `nebula`, `cosmos` |
| 雨中 | `rain`, `umbrella`, `wet`, `puddle` |
| 花瓣飘落 | `cherry blossoms`, `petals`, `floating petals` |

---

## NSFW 模板专题

### NSFW 通用框架

**关闭 Add Quality Tags，手动控制 Quality + 添加 rating:explicit**

```
[artist tags], {{{{masterpiece}}}}, {{{best quality}}}, very aesthetic, absurdres, 1girl, solo, [hair], [eyes], [expression], [nude/clothing], [pose], [sex act tags], [background], rating:explicit
```

**UC (NSFW) 推荐**:
```
worst quality, low quality, blurry, text, watermark, bad anatomy, extra fingers, ugly, fused face, cropped, jpeg artifacts, lowres, bad proportions
```
> 不要加 `censored`, `mosaic`, `censor`, `blur` 等会导致不必要的画面遮挡的标签到 UC

### NSFW 场景模板

#### 1. 单人自慰
```
1girl, solo, nude, on bed, lying on back, legs spread, masturbation, fingering, ahegao, sweat, blush, drooling, open mouth, {masterpiece}, rating:explicit
```

#### 2. 口交
```
1girl, 1boy, blowjob, fellatio, kneeling, looking at viewer, penis, open mouth, tongue out, drooling, eye contact, {masterpiece}, rating:explicit
```

#### 3. 后入式
```
1girl, 1boy, doggy style, from behind, vaginal, penetration, on bed, ass focus, arching back, {masterpiece}, rating:explicit
```

#### 4. 女上位
```
1girl, 1boy, cowgirl position, reverse cowgirl, vaginal, breasts, sweat, ahegao, bouncing, {masterpiece}, rating:explicit
```

#### 5. 扶她 (futanari)
```
1girl, futanari, futanari on female, vaginal, doggy style, penetration, large penis, sweat, ahegao, {masterpiece}, rating:explicit
```

#### 6. 乳交
```
1girl, 1boy, paizuri, titfuck, large breasts, cum on body, lying down, semen, {masterpiece}, rating:explicit
```

#### 7. 颜射/口爆
```
1girl, 1boy, facial, cum on face, semen, closed eyes, open mouth, tongue out, {masterpiece}, rating:explicit
```

#### 8. 绳索/捆绑
```
1girl, solo, bondage, shibari, rope, suspended, nude, harness, restrained, gag, ball gag, {masterpiece}, dark room, rating:explicit
```

#### 9. 触手
```
1girl, solo, tentacle, tentacle sex, bondage, nude, penetration, vaginal, anal, bound, floating, {masterpiece}, rating:explicit
```

#### 10. 露出/公共场所
```
1girl, solo, exhibitionism, outdoor, nude, public, hiding, covering face, embarrassed, blush, looking at viewer, {masterpiece}, rating:explicit
```

#### 11. 阿黑颜 (Ahegao)
```
1girl, solo, ahegao, drooling, tongue out, rolling eyes, sweat, blush, nude, on bed, masturbation, sex toy, {masterpiece}, rating:explicit
```

#### 12. 浴室湿身
```
1girl, solo, shower, bathroom, water, wet, wet body, wet hair, water droplets, steam, nude, looking at viewer, {masterpiece}, rating:explicit
```

### NSFW UC 注意事项

**SFW 转 NSFW 时需要移出 UC 的标签**:
- `rating:general` → 改为 `rating:explicit`
- `no text` → 可选保留
- `-0.8::feet::` → 可选保留（与 NSFW 题材无关时保留）

**不建议放入 NSFW UC 的标签**:
- `censored`, `censor` — 会导致画面出现马赛克遮挡
- `mosaic`, `blur` — 同样会非预期遮挡
- `modesty`, `modesty censor` — 会导致自带的遮挡物出现

**推荐保留的 UC 标签**:
```
worst quality, low quality, blurry, text, watermark, bad anatomy, extra fingers, ugly, fused face, jpeg artifacts, bad proportions
```

---

## 特殊风格模板

### 贴纸/表情包风格

**社区验证的高质量贴纸模板**:

```
1girl, sticker, chibi, Q, white background,
```

- `sticker` — 指定风格为社交软件贴纸风格（必须）
- `chibi` — 大头小身 Q 版角色（不够 Q 可加权 `{chibi}`）
- `Q` — 强化 Q 版感
- `white background` — 干净白底
- `masterpiece, best quality` — 可选，质量不够时加入
- `lowres` — 可选，想要复古贴纸时加入

**推荐 UC**:
```
bad anatomy, bad hands, text, error, missing fingers, extra digit, fewer digits, cropped, worst quality, jpeg artifacts, signature, watermark, username, blurry, bad feet
```

**尺寸**: 正方形为主 (1024x1024 或 832x832)

**示例**: `:-)`, `Q`, `sticker`, `:-D`, `:-P` 等颜文字配合贴纸风格，产出质量极高。

### 颜文字表情包

```
1girl, solo, sticker, Q, white background, :-(, angry, annoyed, chibi
```

### 厚涂/无线条风格

```
no lineart, painterly, 1girl, solo, [描述], {masterpiece}
```
> 关闭 Add Quality Tags，避免 `anime screencap` 等默认标签影响厚涂效果

### 赛璐珞/动画原画风

```
color trace, production art, animation paper, 1girl, solo, [描述]
```
> 产生动画制作过程中的原画稿风格，带色彩标注和标注线

### Fumo 布偶风

```
photo (medium), photographic doll, fumo (doll), 1girl, solo, [角色描述]
```

### 手办/塑料人偶风

```
photo (medium), figure, 1girl, solo, [角色描述], display case, gradient background
```

---

## OC 角色：小银（银霜）

> 锚点标签完整定义见 `SKILL.md` > OC 角色库 > 小银。以下为各场景快捷模板。

### SFW 标准立绘

```
[artist:ask (askzy)], artist:wanke, artist:ciloranko, [[artist:rhasta]], {chiaroscuro}, wlop, [artist:ke-ta], masterpiece, best quality, very aesthetic, absurdres, white background, simple background

1girl, solo, young, teenage, petite, silver hair, medium hair, blunt bangs, hair between eyes, amber eyes, {heart-shaped pupils}, mole under eye, {{ahoge}}, pale skin, delicate features, narrow waist, small breasts, {half-closed eyes}, expressionless, sleepy, languid, messy hair, one strand out of place, oversize hoodie, light gray hoodie, hood down, loose fit, sleeves covering hands, black shorts, black thighhighs, slippers, standing, full body, arms at sides, slightly slouched, facing viewer
```

### SFW 动作场景（替换后半段即可）

```
[画师串], [画质标签], [场景], [光照]

[锚点不变]: silver hair, medium hair, blunt bangs, amber eyes, {heart-shaped pupils}, mole under eye, {{ahoge}}, pale skin, narrow waist, small breasts, {half-closed eyes}, expressionless
[服设不变]: oversize hoodie, light gray hoodie, black shorts, black thighhighs, slippers, messy hair
[动作]: [自由替换]
```

### R18 触手

```
[artist:ask (askzy)], artist:wanke, artist:ciloranko, [[artist:rhasta]], {chiaroscuro}, wlop, [artist:ke-ta], masterpiece, best quality, highres, rating:explicit, dark dungeon, stone floor, dim lighting, dramatic shadows

1girl, solo, silver hair, medium hair, blunt bangs, amber eyes, {heart-shaped pupils}, mole under eye, {{ahoge}}, pale skin, narrow waist, small breasts, {half-closed eyes}, expressionless, nude, all fours, from behind, looking back, tentacles, many tentacles, tentacle around legs, tentacle around arms, tentacle around waist, tentacle in pussy, creampie, absent look, dazed, drooling, sweaty, trembling, messy hair, cum drip
```

### R18 泳装

```
year 2025, masterpiece, best quality, amazing quality, very aesthetic, highres, absurdres, rating:explicit, poolside, blue sky, sunlight, summer, soft lighting, cowboy shot

1girl, solo, silver hair, medium hair, blunt bangs, amber eyes, {heart-shaped pupils}, mole under eye, {{ahoge}}, pale skin, narrow waist, small breasts, {half-closed eyes}, expressionless, school swimsuit, swimsuit aside, pulling swimsuit aside, exposed pussy, spread legs, sitting, legs apart, looking at viewer, embarrassed, heavy blush, shy, sweating, petite
```

### R18 颜射

```
year 2025, masterpiece, best quality, amazing quality, very aesthetic, highres, absurdres, rating:explicit, bedroom, dim lighting, soft lighting

1girl, solo, silver hair, medium hair, blunt bangs, amber eyes, {heart-shaped pupils}, mole under eye, {{ahoge}}, pale skin, narrow waist, small breasts, {half-closed eyes}, expressionless, nude, bare shoulders, bukkake, excessive cum, cum on face, cum on hair, cum on body, cum on breasts, cum drip, thick cum, portrait, upper body, kneeling, messy hair, disheveled, looking at viewer, exhausted, spent, embarrassed, heavy blush, sweaty
```

### R18 后入

```
[artist:ask (askzy)], artist:wanke, artist:ciloranko, [[artist:rhasta]], {chiaroscuro}, wlop, [artist:ke-ta], masterpiece, best quality, highres, rating:explicit, bedroom, bed, silk sheets, moonlight, dim lighting, night, pov, from behind

1girl, silver hair, medium hair, blunt bangs, amber eyes, {heart-shaped pupils}, mole under eye, {{ahoge}}, pale skin, narrow waist, small breasts, {half-closed eyes}, expressionless, clothes on, partially clothed, oversize hoodie, hoodie lifted, no panties, panties pulled down, exposed pussy, doggystyle, on all fours, back arched, hips raised, belly bulge, pained expression, mind broken, dazed, open mouth, drooling, tears, messy hair, sweaty, trembling, hands gripping sheets, hickeys on neck, bruised hips, creampie, cum leaking, cum on thighs, cum on ass | 1boy, faceless, faceless male, no face, head out of frame, muscular, kneeling behind, large penis, vaginal, penetration, deep, grabbing hips, thrusting, rough sex, intense
```

---

## OC 角色：紫姬

### SFW 立绘
```
[artist:ask (askzy)], artist:wanke, artist:ciloranko, [[artist:rhasta]], {chiaroscuro}, wlop, [artist:tidsean], [artist:ke-ta], masterpiece, best quality, very aesthetic, absurdres, white background, simple background, 1girl, solo, silver hair, long hair, hime cut, blunt bangs, sidelocks, hair between eyes, purple eyes, downturned eyes, long eyelashes, pale skin, delicate features, petite, slim, narrow waist, small breasts, {short kimono}, white kimono, long sleeves, purple obi, {kimono skirt}, above knee, thighhighs, geta, camellia hair ornament, bare legs, standing, full body, facing viewer, shy, blush, looking away
```

### 泳装
```
artist:tianliang_duohe_fangdongye, artist:wlop, artist:ask_(askzy), artist:ciloranko, artist:sho_(sho_lwlw), artist:ningen_mame, masterpiece, best quality, very aesthetic, poolside, blue sky, sunlight, summer, soft lighting, rating:sensitive, 1girl, solo, silver hair, long hair, hime cut, blunt bangs, sidelocks, hair between eyes, purple eyes, downturned eyes, long eyelashes, pale skin, delicate features, petite, slim, narrow waist, small breasts, school swimsuit, standing, full body, collarbone, navel, bare shoulders, bare legs, looking at viewer, shy, blush, embarrassed
```

### R18 剥下胸口
```
[artist:ask (askzy)], artist:wanke, artist:ciloranko, [[artist:rhasta]], {chiaroscuro}, wlop, [artist:tidsean], [artist:ke-ta], masterpiece, best quality, highres, rating:explicit, bedroom, soft lighting, moonlight, mood lighting, 1girl, solo, silver hair, long hair, hime cut, blunt bangs, sidelocks, hair between eyes, purple eyes, downturned eyes, long eyelashes, pale skin, delicate features, petite, slim, narrow waist, small breasts, barefoot, bare shoulders, collarbone, white kimono, purple obi, camellia hair ornament, {kimono pulled down}, dress pull, exposed breasts, nipples, sitting on bed, looking at viewer, embarrassed, heavy blush, shy, biting lip, sweaty, messy hair
```

### R18 触手（全身·验证模板）
```
[artist:ask (askzy)], artist:wanke, artist:ciloranko, [[artist:rhasta]], {chiaroscuro}, wlop, [artist:tidsean], [artist:ke-ta], masterpiece, best quality, highres, rating:explicit, wide shot, full body, {{tentacles}}, many tentacles, tentacle sex, smooth, round tentacles, flesh, inside, organic, meat, pulsating, grotesque, living cave, wet, slime, detailed background, 1girl, nude, silver hair, long hair, hime cut, blunt bangs, sidelocks, hair between eyes, purple eyes, downturned eyes, long eyelashes, pale skin, delicate features, petite, slim, narrow waist, flat chest, small breasts, all fours, doggy style, from behind, looking back, looking at viewer, open mouth, {{torn clothes}}, ripped clothing, torn pantyhose, torn stockings, thighhighs, tentacle around body, tentacle around arms, tentacle around torso, tentacle around waist, tentacle around legs, restrained, tentacle in pussy, tentacle penetration, creampie, {semen overflow}, {{excessive cum}}, cum covered, cum on body, cum on face, cum on hair, cum on back, cum drip, {heavy-lidded eyes}, empty eyes, dazed, limp, exhausted, {embarrassed}, shy, blush, tears, drooling, sweaty

---

## 工具人男角色 & POV 视角

> NSFW 双人/多人图中「不重要的男配角」归纳。原则:**不给他人设**——不写具体外貌/发型/表情/服装,只保留能构成体位的身体存在感,注意力锁死在女孩。

### 工具人男三层 tag 策略

| 层级 | 策略 | 标签 |
|------|------|------|
| 匿名词条 | 男完全不可辨认(最强) | `anonymous`, `anonymous male`, `faceless male`, `face obscured`, `face hidden`, `shadowed face`, `silhouette` |
| 局部词条 | 只露身体某部分 | `offscreen`, `male torso`, `waist down`, `penis`(配体位用), `hands`(掐脖/抓发时) |
| 注意力锁定 | 焦点钉在女孩 | `solo focus`(放女孩侧), `looking at viewer`, `eye contact`;男孩框全部 `[tag]` 或 `0.5::tag::` 降权 |

### POV vs 第三人称选择

| 诉求 | 方案 | 组合 |
|------|------|------|
| 女主体感/特写(嘴·手·射精) | **第一人称 POV**,男=观众不出场 | `pov, looking at viewer, eye contact, 1girl`;细节:`from below`(仰视)、`selfies`;缺点:无法表达男的身体压迫 |
| 体位展示/支配感(ryona·abuse) | **第三人称双人**,男入画但只留压迫存在 | `faceless male, face obscured, shadowed face, dark skin, tall male, muscular male, broad shoulders, nude, solo focus` |

强烈建议第三人称时**绝对不写**男的具体发型/发色/五官/表情/服装(抢戏);**保留**肤色+体格(身高差/力量差压迫感)+ nude。男孩框整体降权,女孩框正常/加权。

### 复用模板插槽

**插槽A · 第三人称工具人男通用块**(用于 ryona/abuse 体位场景):
```
1boy, faceless male, face obscured, shadowed face, dark skin, tall male, muscular male, broad shoulders, nude, dominant, sadistic, [体位动作]
```

**插槽B · 第一人称 POV(男隐藏)**:
```
1girl, pov, looking at viewer, eye contact, [体位动作], [女孩表情]
```

**插槽C · 双人 (通用结构)**:
```
[画师串], masterpiece, best quality, rating:explicit, [场景·光照],
1girl, [角色锚点], [表情], [体位·女孩侧], solo focus, looking at viewer |
1boy, faceless male, face obscured, [肤色·体格], nude, [体位·男孩侧]
```
```
