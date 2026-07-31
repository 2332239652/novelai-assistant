# NovelAI 社区魔法配方库

来自《元素法典》《解构原典》等社区合集的经典配方。配方中的 `{tag}` 语法为旧版加权方式，在 V4.5 中可改用 `1.05::tag::` 数值语法。

---

## 通用起手式

### 正向起手
```
((masterpiece)), (((best quality))), ((ultra-detailed)), ((illustration)), ((disheveled hair))
```

### 通用负面 (UC)
```
longbody, lowres, bad anatomy, bad hands, missing fingers, pubic hair, extra digit, fewer digits, cropped, worst quality, low quality
```

---

## 元素魔法 (NAI V1/V2 时代经典)

### 水魔法
营造水面漂浮、湿润衣物的梦幻效果。

**正向**:
```
((masterpiece)), (((best quality))), ((ultra-detailed)), ((illustration)), ((disheveled hair)), ((frills)), (1 girl), (solo), dynamic angle, big top sleeves, floating, beautiful detailed sky, on beautiful detailed water, beautiful detailed eyes, overexposure, (fist), expressionless, side blunt bangs, hairs between eyes, ribbons, bowties, buttons, bare shoulders, (((small breast))), detailed wet clothes, blank stare, pleated skirt, flowers
```

**反向**:
```
nsfw, lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, fewer digits, cropped, worst quality, low quality, normal quality, jpeg artifacts, signature, watermark, username, blurry, missing fingers, bad hands, missing arms, long neck, Humpbacked
```

**参数**: CFG 5.5, Euler a, Steps 30

---

### 空间法
以最少的 tag 呈现最强视觉冲击力，宽画幅效果极佳。

**正向**:
```
((illustration)), ((floating hair)), ((chromatic aberration)), ((caustic)), lens flare, dynamic angle, ((portrait)), (1 girl), ((solo)), cute face, ((hidden hands)), asymmetrical bangs, (beautiful detailed eyes), eye shadow, ((huge clocks)), ((glass strips)), (floating glass fragments), ((colorful refraction)), (beautiful detailed sky), ((dark intense shadows)), ((cinematic lighting)), ((overexposure)), (expressionless), blank stare, big top sleeves, ((frills)), hair_ornament, ribbons, bowties, buttons, (((small breast))), pleated skirt, ((sharp focus)), ((masterpiece)), (((best quality))), ((extremely detailed)), colorful, hdr
```

**参数**: CFG 4.5, Euler a, Steps 28

---

### 冰魔法
冰晶宫殿、天蓝色调的氛围效果。

**正向**:
```
(((masterpiece))),best quality, illustration,(beautiful detailed girl),beautiful detailed glow,detailed ice,beautiful detailed water,(beautiful detailed eyes),expressionless,(floating palaces),azure hair,disheveled hair,long bangs, hairs between eyes,(skyblue dress),black ribbon,white bowties,midriff,{{{half closed eyes}}},big forhead,blank stare,flower,large top sleeves
```

**参数**: Steps 27, Euler a, CFG 7

---

### 核爆法
战争火焰与核爆背景的强烈视觉。

**正向**:
```
(((masterpiece))),best quality, illustration,(beautiful detailed girl),beautiful detailed glow,((flames of war)),(((nuclear explosion behind))),rain,detailed lighting,detailed water,(beautiful detailed eyes),expressionless,palace,azure hair,disheveled hair,long bangs,hairs between eyes,(whitegrey dress),black ribbon,white bowties,midriff,big forhead,blank stare,flower,long sleeves
```

**参数**: Steps 28, Euler a, CFG 7

---

## NAI V3.0 进阶魔法 (解构原典)

### 角色还原法
> NAI3 可以还原 50 图以上的二次元角色特征，2023年6月前出现的角色效果最佳。

**正向**:
```
{{texas the omertosa (arknights)}}1girl,solo white background,dymanic pose, cute,smile,floating,floating hair,hand on own chest, best quality, amazing quality, very aesthetic, absurdres
```

**要点**:
- 使用 `角色名 (作品名)` 格式
- 特征出不全时用 `{}` 加权或加特征tag
- 不知道角色tag可用立绘反推

---

### 单手倒立法
> NAI3 构图能力极强，可处理复杂姿势。

**正向**:
```
very aesthetic,1girl, {one arm handstand}, outdoors, upside-down,armpits, asymmetrical legwear, black footwear, black jacket, black shorts, black socks, black thighhighs, blue sky, boots, breasts, pink hair, ribbon, short shorts, shorts, sky, smile, socks, solo, best quality, amazing quality, very aesthetic, absurdres
```

**参数**: Steps 28, Euler a, CFG 6.0, Size 832x1216

**核心**: `one arm handstand` + `upside-down` 是构图关键

---

### 情绪流
> NAI3 对情绪展现有很大提高，加入情绪词有惊喜。

**正向**:
```
{{texas the omertosa (arknights)}}1girl,white background,sitting, grass, from side,head down,sad,solo
```

**反面需排除**: `tear, artistname, weapon, earphones`

---

## V4.5 实用技巧配方

### 模拟 V4 风格
在 V4.5 中如果想获得接近 V4 的效果：
```
{{monochrome}}, inoitoh
```
或用低强度 `ai-assisted` tag（效果因画师串而异）

### 电影感写实
```
fine art, realistic, {cinematic lighting}, 2::contrasting shadows::
```
配合 Euler 采样器效果最佳。

### 角色设定参考图
```
1girl, solo, multiple views, reference sheet, expressions, white background, simple background, character design, turnaround
```
加入 `no text` 避免 AI 写设计注释。

### 消除精灵耳
添加: `human only` 或 UC 中加入 `elf ears, pointy ears`

### 抑制白化肤色
不要额外添加 `white` 或 `pale skin`（如果模型已默认白皙），改用 `light skin` 或直接不加肤色标签。

---

## 元素魔法速查

| 效果 | 关键标签组合 |
|------|-------------|
| 水面倒影 | `water reflection`, `lake`, `mirror image`, `on beautiful detailed water` |
| 水晶透明感 | `crystal`, `gemstone`, `transparent`, `sparkle`, `colorful refraction` |
| 火焰特效 | `fire`, `flame`, `burning`, `explosion`, `flames of war` |
| 体积光 | `volumetric lighting`, `god rays`, `sun rays`, `cinematic lighting` |
| 星空宇宙 | `starry sky`, `galaxy`, `nebula`, `cosmos`, `beautiful detailed sky` |
| 雨中意境 | `rain`, `umbrella`, `wet`, `puddle`, `reflection`, `detailed wet clothes` |
| 花瓣飘落 | `cherry blossoms`, `petals`, `floating petals`, `flowers` |
| 玻璃碎裂 | `glass strips`, `floating glass fragments`, `colorful refraction` |
| 时钟机械 | `huge clocks`, `gears`, `clockwork`, `steampunk` |
| 色差特效 | `chromatic aberration`, `caustic`, `lens flare` |
