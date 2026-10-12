# 韩网 N5 高复用画师串清单（8 个风格族）

> **来源**：2026-10-09 韩网 N5 作品集反读（935 张，391 张完整参数），从 `kr_corpus.jsonl` 聚类得出。
> **去重后共 8 个风格族**，合计覆盖 391 张中的 **367 张**。
> **性质**：外部社区语料，**未经本机验收**。配方与参数逐字冻结，使用前建议先跑小样本。
> 完整报告见 `kr-n5-corpus-analysis.md`；原始语料见 `kr_corpus.jsonl`。

---

## 【1】漫画人体串 · 174 张 ⚡（语料第一主力）

**画师串**：
```
1.3::artist:doppel (bonnypir)::, 0.8::draw body like artist:henriiku (ahemaru) ::, 0.9::artist:yoneyama mai, c.cu, artist:iuui::, 0.4::artist:freng::
```

| 项 | 内容 |
|---|---|
| 规模 | **174 张**，跨 4 个目录（`2026-10-03_21-49-01` 38 · `2026-10-03_21-55-05` 38 · `2026-10-04_08-11-38` 26 · `2026-10-05_13-20-37` 72） |
| 参数 | steps 23 · CFG 5.0 · rescale 0 · 832×1216 · k_euler_ancestral · karras |
| 风格 | 专业漫画感、线条有力、色彩鲜明 |
| 结构 | ⭐ `draw body like artist:X` 四层范本：主导画风(1.3) → 人体借用(0.8) → 氛围配色(0.9) → 兜底(0.4) |

**该族质量头（逐字，可选）**：
```
1.1::year 2025, ::, 0.3::, black outlines::, 1.2::masterpiece, very aesthetic, best quality, amazing quality, absurdres, highres, best illustration::, -1::artist collaboration, mosaic::
```

---

## 【2】高饱和变形串 · 60 张（含 NSFW）

**画师串**：
```
0.5::artist:murata yuusuke ::, 0.5::artist:hwansang ::, 0.8::artist:deadflow, artist:freng::, 0.7::artist:pottsness::, 0.8::artist:yd (orange maru)::, 2::artist:uchikaze::, 0.9::artist:ciloranko::, -1.5::artist collaboration::
```

| 项 | 内容 |
|---|---|
| 规模 | **60 张**（`2026-10-01_13-38-36`） |
| 参数 | steps 23 · CFG 5.0 · rescale 0 · 832×1216 |
| 风格 | 高饱和、细长身形；`uchikaze` 以 **2.0 权重**主导 |
| 负强调 | ⭐ 教科书配置：`-2::wide shot::` + `-2::multiple views, speech bubble, text, background human::` + `-5::anatomical nonsense::` + `-1.5::artist collaboration::` |

**完整正面（逐字）**：
```
1girl, -2::wide shot::, -2::multiple views, speech bubble, text, background human::, 0.5::artist:murata yuusuke ::, 0.5::artist:hwansang ::, artist:supernew, artist:wanke, 0.8::artist:deadflow, artist:freng::, 0.7::artist:pottsness::, 0.8::artist:yd (orange maru)::, 2::artist:uchikaze::, 0.9::artist:ciloranko::, year 2026, year 2025, heating relationship, contemporary, random pose, masterpiece, very aesthetic, incredibly absurdres, absurdres, ultra high resolution, digital illustration, 2::slender::, -5::anatomical nonsense::, -1.5::artist collaboration::
```

---

## 【3】中世纪酒馆双人串 · 41 张（韩文混用典型）

**画师串**：
```
1.5::Artist:pija (pianiishimo)::, 1.2::alp, ::, 1.1::hews::, 1.5::muchi_maro, ::, 0.3::kz_oji::, 0.2:: zettai_yarumoni, ::, 0.4::collagen,atte_nanakusa::, 0.6::obui::, 0.6::ahemaru::, -3::artist collaboration ::
```

| 项 | 内容 |
|---|---|
| 规模 | **41 张**（`2026-10-05_23-13-06`，该目录内另有变体） |
| 参数 | steps **28** · CFG **4.5** · rescale **0.5** · 832×1216 |
| 风格 | 精细线稿 + 立体光影（`delicate lineart, soft shading, anime-style facial features with carefully modeled three-dimensional shading`） |
| 特色 | ⭐ **韩文混用典型**：`주점,술집,분홍색 불빛들 클럽 내부`（酒馆/酒吧/粉光夜店内部）、`쇼파에 앉아,위를 올려다 보고`（坐沙发抬头看） |
| 结构 | 双角色框 + `Speech bubble, English text: ...` 对白 |

---

## 【4】写实光影串 · 35 张（无画师串路线）

**关键块**：
```
-1::flat color::, 0.5::photorealistic::, 1.2::detailed skin, very sweaty::, shiny skin
```

| 项 | 内容 |
|---|---|
| 规模 | **35 张**（`2026-10-04_14-01-54`） |
| 参数 | steps 23 · CFG **6.0** · rescale **0.4** · **1024×1024** |
| 风格 | ⭐ **无画师串**，纯靠 `photorealistic` 0.5 权重 + `-1::flat color::` 反平涂 + 详细皮肤质 |
| 说明 | 该族是全语料唯一主力方形分辨率（1024×1024）的组，且 cfg_rescale 启用（0.4） |

---

## 【5】rusellunt 厚涂串 · 25 张

**画师串**：
```
0.6::rusellunt::, 0.5::kunaboto::, 0.3::mikozin ::, 0.8::wagashi (dagashiya) ::, 0.7::michiking,::, 0.9::manglife ::, 0.5::typehatena ::, 1.1::healthyman ::, 0.7::tianliang duohe fangdongye::
```

| 项 | 内容 |
|---|---|
| 规模 | **25 张**（`2026-09-29_21-03-14`） |
| 参数 | steps **28** · CFG **7.2** · rescale 0 · 832×1216 |
| 风格 | 厚涂、细致线稿（`thick eyelashes, thick draw lines, hatching (texture)`） |

**质量头（逐字，可选）**：
```
year 2026, year 2025, masterpiece, best quality, amazing quality, very aesthetic, best illustration, newest, incredibly absurdres, hyper detail
```

---

## 【6】mo_(kireinamo) 主导厚涂串 · 24 张

**画师串**：
```
1.5::mo_(kireinamo) ::, 0.6::rusellunt::, 0.5::kunaboto::, 0.3::mikozin ::, 0.8::wagashi (dagashiya) ::, 0.7::michiking,::, 0.9::manglife ::, 0.5::typehatena ::, 1.1::healthyman ::, 0.7::tianliang duohe fangdongye::
```

| 项 | 内容 |
|---|---|
| 规模 | **24 张**（`2026-10-02_14-11-40` 11 张 + 根目录 13 张） |
| 参数 | steps **28** · CFG **7.2** · rescale 0 · 832×1216 / 1024×1024 |
| 与【5】的关系 | 同为 rusellunt 厚涂族，【6】把 `1.5::mo_(kireinamo)::` 提到主导位替换 rusellunt |
| 注意 | `mo_(kireinamo) , 0.6::rusellunt::` 这个写法里 `0.6` 属于 rusellunt，原文如此 |

---

## 【7】漫画描线串 · 22 张（最强负强调）

**画师串**：
```
-6.0::artist collaboration::, 1.1::artist:wanderjegson, artist:yoneyama mai::, 0.8::artist:queasy s::, 0.9::artist:inoue kiyoshirou::, 0.4::artist:hood (james x)::, 0.9::artist:meion::, 1.1::artist:hizuki akira::, 0.4::artist:ikuchan kaoru::, 0.3::artist:houtengeki ::, 1.1::artist:jonpei::
```

| 项 | 内容 |
|---|---|
| 规模 | **22 张**（`2026-09-30_21-06-25`） |
| 参数 | steps **24** · CFG **7.0** · rescale 0 · 832×1216 |
| 风格 | 漫画/贴纸感（`comic style, toon (style), bold outlines`） |
| 负强调 | ⭐ **`-6.0::artist collaboration::` 全语料最强档**，稳定出图 |
| 其他技法 | `1.25::redrawn::`（重绘感）、`1.4::detailed anatomy::` |

---

## 【8】Hogwarts 光影立绘串 · 10 张（12 画师）

**画师串**：
```
0.05::artist:shexyo::, 0.5::artist:inoue_kiyoshirou::, 0.75::artist:anteiru::, 1::artist:gogalking::, 1.15::artist:haze_(7h4ze)::, 1.2::artist:mx2j::, 1.5::artist:yoneyama mai::, 0.75::artist:pigeon666 ::, 0.5::artist:yesman_(cvbnyesman)::, 0.5::artist:hintobento::, 0.3::artist:takeda hiromitsu::, 0.15::artist:nyantcha::
```

| 项 | 内容 |
|---|---|
| 规模 | **10 张**（`2026-09-29_21-10-44`） |
| 参数 | steps **21** · CFG 6.0 · rescale 0 · 832×1216 |
| 风格 | 教堂/圣殿光影立绘；12 画师梯度，`yoneyama mai` 1.5 主导、`shexyo` 仅 0.05 |
| 质量头 | `best quality, amazing quality, very aesthetic, 1::very aesthetic::, 1.5::abusdres::, 1.5:: best illustration ::, 3::masterpiece::, 0.2::high complexity::, 1.5::background with high complexity ::` |
| 负强调 | `-1::simple illustration, artist collaboration, door, doorway, speech bubble, speech balloon, dialogue bubble, text::, -1.7::thick border::` |

---

## 附：跨族通用要素

**被多个族共用的画师**（可作组合基底）：

| 画师 | 出现族 | 权重带 |
|---|---|---|
| `freng` | 【1】【2】 | 0.4 / 0.8 |
| `yoneyama mai` | 【1】【7】【8】 | 0.9 / 1.1 / 1.5 |
| `kunaboto` | 【5】【6】 | 0.5 |
| `wagashi (dagashiya)` | 【5】【6】 | 0.8 |
| `healthyman` | 【5】【6】 | 1.1 |
| `mikozin` | 【5】【6】 | 0.3 |

**三个跨族负强调**（几乎所有族都在用）：
```
-1::artist collaboration, mosaic::          ← 【1】防合作签名图 + 解马赛克
-1.5::artist collaboration::                ← 【2】
-2::artist collaboration, :: / -3:: / -6.0::← 【5】【3】【7】逐级加强
```
