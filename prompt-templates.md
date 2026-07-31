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
