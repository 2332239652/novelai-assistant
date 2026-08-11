# NovelAI 画师串配方库

社区验证的画师混合串，可直接用于 V4.5 Curated/Full 模型。

## 使用说明

- 画师串放在提示词最前面，权重最高
- `1.2::artist:xxx::` 表示精确加权，`{artist:xxx}` 表示花括号加权
- 多画师混合时建议 CFG 3.5-5
- 每个串标注了适用模型版本

---

## V4.5 Curated 画师串

### 麦厨画风
- **特点**: 画麦哲伦无敌，一般只能画上半身
- **适用**: V4.5c
```
magallan (elite ii) (arknights),artist:piromizu,artist:fajyobore,artist:QUASARCAKE,artist:ebifurya,artist:neisan,0.4::artist:tab head::, 0.3::artist:yamamoto_souichirou::,1.72::artist:sigm@::
```

### 山含画风
- **特点**: 画出来的都是小孩，稳定，部分角色易出现"展示内裤"需反向词抑制
- **适用**: V4.5c
```
artist:piromizu,artist:fajyobore,artist:QUASARCAKE,artist:ebifurya,artist:neisan,0.4::artist:tab head::, 1.5::artist:mountain_han::
```

### ningen mame 简约人物风
- **特点**: 入门级，人物简约，适合配合 Vibe Transfer
- **适用**: V4.5c
```
year 2025,[[binggong_asylum,egami]],[[[a20_(atsumaru)]]],[[hanecha1220,hagi_(ame_hagi)]],[[houraku,houraku]],[[abpart,rucaco]],0.7::artist:na_tarapisu153 ::, 0.6::artist:ningen mame::, 0.4::artist:betabeet::, 0.6::artist:yuji (fantasia)::,1.1::umou_(umouawa),{{mikkun_04,realistic}}::
```

### 风景人物精致风格
- **特点**: 画背景不错，适合横屏规格
- **适用**: V4.5c
```
artist:piromizu,artist:fajyobore,artist:QUASARCAKE,artist:ebifurya,artist:neisan,0.4::artist:tab head::, 0.5::artist:yamamoto_souichirou::,1.72::artist:sigm@::,1.0::artist:spicy_moo::, artist:min_(120716),artist:rella
```

---

## 社区大佬画师串合集

### 灵佑佬系列

**串1 - sanbonzakura 主导**:
```
1.2::artist:rei_(sanbonzakura)::,1.0::artist:marushin_(denwa0214)::,0.8::artist:ciloranko::,0.9::artist:tekito_midori::,year_2025
```

**串2 - 多画师混合**:
```
{{{artist:konya_karasue}}},{{amagai_tarou}},{yoggi_(stretchmen)},[artist:rella],kedama_Milk,[[[miyu_(miy_u1308)]]],[[[[[ask_(askzy)]]]]],[[[[[ciloranko]]]]],[[[[lobelia_(saclia)]]]]
```

**串3 - 高权重 sanbonzakura**:
```
2.1::artist:rei_(sanbonzakura), 1.6::artist:repi, 1.2::artist:Tsunako, 0.6::artist:REDUM, 0.5::artist:Hiten, ::,year_2025
```

**串4 - soraneko 系**:
```
artist:soraneko_hino,0.95::artist:rei_(sanbonzakura)::,artist:repi,year 2025
```

### 普瑞塞斯大佬系列

**串1 - 角色向**:
```
1girl,year2025,artist:ikuchan kaoru,artist:kinosuke \(sositeimanoga\),0.7::artist:fajyobore::,1.1::artist:wangxiii.1.2::aetist:mizuharayuki,artist:minami::,solo,sitting, white background
```

**串2 - ebifurya 主导**:
```
artist:asanagi,0.5::artist:tab head::,1.3::artist:ebifurya,artist:neisan::,artist:modare,artist:yoneyama_mai,artist:piromizu
```

**串3 - 多人混合**:
```
artist:shion(mirudakemann),artist:tsurui,artist:yd orange maru,artist:misaka_12003-gou, [artist:sincos], [artist:rella], [artist:konya_karasue], ,artist:huanxiang_heitu,artist:ebifurya,artist:neisan
```

**串4 - 官方画风**:
```
muted_color, official_art, official_style, anime_coloring,artist:asanagi,artist:tab head, artist:wanke,artist:ebifurya,artist:laserflip,artist:modare, artist:ogipote, artist:muchi_maro
```

**串5 - piromizu 系**:
```
year2025,artist:piromizu,artist:fajyobore,artist:QUASARCAKE,0.8::artist:ebifurya,artist:neisan,::0.7:::artist:tab head::,0.4::artist:asanagi::
```

### v佬系列

**串1 - dino 系**:
```
artist:dino_(dinoartforame),artist:min_(120716),artist:john_kafka,artist:konya_karasue
```

**串2 - kieed 系**:
```
artist:kieed,0.3::artist:Rolua::,0.6::artist:konya_karasue::,0.3::artist:wlop::,0.4::artist:dino_(dinoartforame)::,artist:rella,0.6::artist:wanke::
```

**串3 - wanke+dino 混合**:
```
0.6::artist:wanke::,0.4::artist:dino_(dinoartforame)::,artist:min_(120716) ,1.1::artist:fujiwara_ryo_(wsise47)::,0.4::artist:nakddidi::,0.6::artist:ugonba_(howatoro)::,0.4::artist:nakamura_hinata::,artist:yoneyama_mai,artist:rella
```

**串4 - quasarcake 系**:
```
artist:min_(120716),0.6::artist:quasarcake::,0.8::artist:kim_eb::,0.8::artist:love_cacao::,0.5::artist:nababa,::0.8::artist:cuboon::,0.4::artist:kuzuvine::,0.6::artist:yd_(orange_maru)::,0.3::artist:rella::,0.3::artist:rhasta::,artist:ciloranko
```

### 猫南北大佬系列

**串1 - 厚涂写实风**:
```
{{photo (medium), 3d}}, [artist: ask (askzy)], {{wanke}}, [mika pikazo], {cowboy shot}, pale color, realistic background,
{{year 2024, best quality, amazing quality, very aesthetic, highres, incredibly absurdres, masterpiece, ultra-detailed, 4K, 8K, 16K, high quality, hyper detailed, cinematic composition, detailed beautiful face and eyes}}
```

**串2 - mel 系**:
```
0.8::artist:mel (melty pot)::, 0.9::artist:d jirooo::, 0.7::artist:deadflow::, 1.1::artist:channel (caststation)::, {year 2025, year 2024}, best quality, amazing quality, very aesthetic, highres, absurdres
```

**串3 - blue gk 系**:
```
[[[[artist:blue gk, artist:mamimi (mamamimi)]]]], [[[[artist:quasarcake]]]], [[[artist:freng]]], [[[artist:nompang]]], [[artist:kawacy]], [[artist:ciloranko]], [[artist:modare]], year 2024
```

### 清梦大佬 - 水墨淡彩风
```
{{limited palette}},{animation paper,color trace},{colored},fujiyama,nardack,tekito_midori,shuri_(84k),mion,{{{artist:yoneyama_mai}}},[[artist:rella]],ink wash painting,{lineart},[monochrome],[[colorful]],stunning composition
```

### 古川大佬
```
{artist:miv4t},{{artist:konya karasue}},artist:rella,[[[artist:quasarcake]]],artist:fajyobore,[[[[[artist:skyrick9413]]]]]
```

### 萤火大佬 - 精细化混合
```
0.4::artist:ask_(askzy)::,1.01::artist:mochizuki_kei::,1.12::artist:ekina_(1217)::,1.014::aritist:akakura::,1.03::artist:motimoti067,::1.01::artist:tokkyu::,artist:icomochi,1.2::artist:kouyafu::,masterpiece, {best quality},{{amazing quality}},very aesthetic,ultra-detailed,year 2024,year2025
```

### 石头大佬 - 精确小数权重
```
(artist:reoen:0.826446), artist:machi, (artist:ningen mame:0.9), (artist:sho (sho lwlw):0.9), (artist:rhasta:0.9), (artist:wlop:0.7), (artist:ke-ta:0.6), (fkey:0.5), (tianliang duohe fangdongye:0.5), (hiten \(hitenkei\):0.6), best quality, amazing quality, (artist:onineko:0.826446)
```

### 夕方忻大佬 - dishwasher 系
```
artist:freng, [[artist:starshadowmagician]],[[[[artist:dishwasher1910, artist:ask_(askzy)]]]], [[artist:nekometaru]],[[artist:sheya,artist:ciloranko]],{artist:yukiko_(tesseract)}, [[artist:u35]],{{{artist:takeshima_eku}}}
```

### 休闲大佬 - 简约六画师
```
artist:tianliang_duohe_fangdongye,artist:wlop,artist:ask_(askzy),artist:ciloranko,artist:sho_(sho_lwlw),artist:ningen_mame
```

### 空想家大佬系列

**串1 - FynnF 系**:
```
artist:FynnF, artist:shion(mirudakemann), artist:tsurui, artist:yd orange maru, artist:misaka_12003-gou
```

**串2 - 全画师大混合**:
```
artist:nonoko, artist:muromaki, artist:torino, artist:aban_donranka, artist:scottie, artist:FynnF, artist:shion(mirudakemann), artist:tsurui, artist:yd orange maru, artist:misaka_12003-gou, artist:sincos, artist:rella, artist:konya_karasue, artist:huanxiang_heitu, artist:ebifurya, artist:neisan, artist:clearite, artist:modare, artist:happoubi_jin
```

**串3 - amonitto 系**:
```
0.2::artist:amonitto::,0.4::artist:taowu (20809)::,0.6::artist:stu dts::,artist:rei_(sanbonzakura),0.4::artist:buzzlyears::,artist:sak_(lemondisk),year 2025
```

### 茶叶大佬 - mochizuki_kei 系
```
0.7::artist:mochizuki_kei::,0.4::artist:akakura,,0.6::artist:aamond::,0.4::artist:criis-chan::,0.5::artist:channel_(caststation),0.7::artist:tsurumi_kazane::
```

### 鲍大人系列

**串1 - mika pikazo 系**:
```
[[artist:mika_pikazo]],{artist:mignon},{ask (askzy)},[artist:ciloranko],[artist:atdan],[artist:chen bin]
```

**串2 - chen bin 系**:
```
[[artist:chen_bin]], [artist:sho_(sho_lwlw)], [artist:ningen_mame], [artist:tianliang_duohe_fangdongye], [[artist:ciloranko]], [[artist:rella]], [[artist:konya_karasue]]
```

### 凉大佬
```
[artist:ask (askzy)],artist:wanke,artist:ciloranko,[[artist:rhasta]],{chiaroscuro},wlop,[artist:tidsean],[artist:ke-ta]
```

### 苦苦大佬
```
artist:fenrir (fenriluuu),artist:tsubasa tsubasa,artist:sho_(sho_lwlw)
```

---

## 特定风格串

### 水墨风
```
{{{{ink wash painting}}}},lineart,monochrome,gril
```

### 极简风格
```
minimalism,{faceless},(white skin),portrait,{no lineart},simple background,white background,blending,flat color,limited palette,high contrast
```

### 手绘风
```
graphite (medium),{{monochrome}},paper,art tools in frame,pencil,traditional media
```

### 3D 写实风
```
best quality, masterpiece, realistic, 1.4::void 0 ::1.2::liduke::, 1.3::tangerine_(dudu)::, 1.4::ryanreos::
```

### 柚子社 Galgame 风
```
cafe stella to shinigami no chou (game cg),{{senren banka (game cg)}},riddle joker (game cg),amairo islenauts (game cg),{{{ask (askzy),kobuichi,muririn}}},game cg
```

---

## V4.5 Full 单画师推荐

以下画师在 V4.5 Full 下效果优秀（光影系为主）：

| 画师 Tag | 备注 |
|----------|------|
| `artist:yao liao wang` | 光影出色 |
| `artist:meinoss` | |
| `artist:others (gogo-o)` | |
| `artist:xiaobanbei milk` | |
| `artist:matsuura kento` | |
| `artist:jl tan` | |
| `artist:betabeet` | |
| `artist:solipsist` | |
| `artist:kan liu (666k)` | |
| `artist:Zygocactus` | |
| `artist:wang-xi` | |
| `artist:ririko (fhnngririko)` | |
| `artist:simz` | |
| `artist:qingli ye` | |
| `artist:huade xiami` | |
| `artist:sydus` | |
| `artist:murata range` | |
| `artist:v.a. (vanilla)` | |
| `artist:spykeee` | |
| `artist:shexyo` | |
| `artist:akipeko` | |
| `artist:ria (baka-neearts)` | |
| `artist:soleil (soleilmtfbwy03)` | |
| `artist:some1else45` | |
| `artist:polilla` | |
| `artist:aoi sakura (seak5545)` | |
| `artist:jianjia` | |
| `artist:cutesexyrobutts` | 知名厚涂画师 |
| `artist:suzukasuraimu` | |
| `artist:misaka 12003-gou` | |
| `artist:miv4t` | |
| `artist:sweetonedollar` | |
| `artist:dana (ocana dana)` | |
| `artist:bayashiko` | |
| `artist:dingding (chongsangjun)` | |
| `artist:observerz` | |
| `artist:kyano (kyanora3141)` | |
| `artist:h.an (516635864)` | |
| `artist:bigrbear` | |
| `artist:kaede (sayappa)` | |
| `artist:kofi-mo` | |
| `artist:cherre` | |
| `artist:ragecndy` | |
| `artist:hani haya` | |
| `artist:kele mimi` | |
| `artist:neko blow` | |
| `artist:tianliang duohe fangdongye` | 社区高频使用 |
| `artist:qianyuu (senba)` | |
| `artist:emmmerald` | |

> 测试参数: V4.5f: CFG 4, Steps 28, dpm++2m sde, karras

---

## 画师串使用技巧

1. **权重调节**: 如果某画师风格过强，用 `0.5::artist:xxx::` 削弱
2. **CFG 配合**: 多画师混合建议 CFG 3.5，少画师建议 CFG 5
3. **年份标签**: `year 2024` / `year 2025` 可微调风格时效性
4. **混搭原则**: 2-3个主画师 + 3-5个辅助画师效果最佳
5. **关闭 Add Quality Tags**: 使用画师串时建议手动控制 quality tags
