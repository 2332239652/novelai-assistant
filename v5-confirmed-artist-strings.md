# V5 已确认画师串登记册

> 记录用户**亲自验收过**的 NAI5（V5 Full）画师串。
> 入册规则：成图须用户本人过目认可；配方逐字冻结，复现时不要增删改。
> 使用时机：用户说「用我确认过的串」「第X串」「社区A」等表述时，直接取用对应配方。

---

## 社区A ✅

**配方**：
```
1.1::artist:ningen_mame::, 0.7::artist:karameru::, 0.6::artist:mery::
```

| 项 | 内容 |
|---|---|
| 来源 | 5ch Wiki「アーティスト」页 V5 实测名单组合（ningen_mame 主导，karameru/mery 辅助；三人均为社区标注 V5 Full 可用） |
| 首验 | 2026-08-25 · 茉子白底站桩立绘（832×1216 · steps 28 · CFG 5 · k_euler_ancestral · quality_toggle off） |
| 风格倾向 | 日系现代赛璐璐、线条清晰（ningen_mame 底色为主） |
| 搭配注意 | 按「画师串表达铁律」使用：base 不放风格脚手架词、质量头只留一层 |

---

## 清新日常 ✅

**配方**：
```
0.9::artist:shiromanta::, 0.7::artist:karameru::, 0.6::artist:mignon::
```

| 项 | 内容 |
|---|---|
| 来源 | V5 安全池自研组合（shiromanta 主导的明亮简洁系，三人均为 5ch Wiki V5 实测确认） |
| 首验 | 2026-08-25 · 街道骑车晨光场景插图（832×1216 · steps 28 · CFG 5）· 用户验收"还可以" |
| 风格倾向 | 明亮干净、线稿清晰、日常轻场景向 |

---

## 厚涂质感 ✅

**配方**：
```
1.3::chen bin::, 0.8::rella::, 0.6::artist:mx2j::
```

| 项 | 内容 |
|---|---|
| 来源 | V5 安全池自研组合（chen bin 厚涂光影主导 + rella 氛围辅助） |
| 首验 | 2026-08-25 · 烛光城堡肖像（同参数）· 用户验收通过 |
| 风格倾向 | 暖调光影厚重、油画感 |

---

## 水墨黑白 ✅

**配方**：
```
greyscale, monochrome, ink (medium), sumi-e, traditional media, brush stroke, 0.5::tsukushi akihito::
```

| 项 | 内容 |
|---|---|
| 来源 | 特色媒介标签驱动 + tsukushi akihito 低权重笔触辅助（铁律「用户点名媒介」例外条款适用） |
| 首验 | 2026-08-25 · 云雾山峦汉服水墨（同参数）· 用户验收通过 |
| 风格倾向 | 黑白水墨、传统手绘质感 |
| ⚠️ 注意 | 本串以媒介标签为主体、画师仅低权重辅助——与纯画师串用法不同 |

---

## Q版贴纸 ✅

**配方**：
```
chibi, 0.9::kedama_milk::, 0.6::artist:karameru::
```

| 项 | 内容 |
|---|---|
| 来源 | chibi 标签驱动 + kedama_milk 软萌主导 + karameru 辅助 |
| 首验 | 2026-08-25 · 兔耳吃胡萝卜贴纸（同参数）· 用户验收通过 |
| 风格倾向 | 软萌Q版大头、贴纸素材向 |

---

## 人体1 ✅（原 NSFW人体 · ask + mignon 版）
**命名**：用户 2026-09-14 指定名称「人体1」——日系人体向首选串。

**配方**：
```
1.2::artist:ask::, 0.7::artist:mignon::
```

| 项 | 内容 |
|---|---|
| 来源 | ask 词条 V5 可用性实测确认（完整名 `artist:ask (askzy)` 与简名 `artist:ask` 均识别）+ mignon 安全池辅助 |
| 首验 | 2026-08-25 · explicit 裸体全身躺卧（832×1216 · steps 28 · CFG 5）· 用户验收「人体细节丰富」 |
| 复验 | 2026-09-14 · NSFW 立绘协议（裸体全身站姿 · 832×1216 · steps 28 · CFG 5 · k_euler_ancestral · quality_toggle off · seed 20260912）· 用户复核「还可以」——比例正常、手脚无畸变；**特点：皮肤哑光平滑、结构暗示少（偏玩偶感），胜在稳定不崩** |
| 风格倾向 | ask 的细腻线稿与人物张力 + mignon 柔和上色，人体细节丰富 |
| ⚠️ 单画师副作用 | ask 单画师高权重（1.3+）会连带画师角色习惯（如眼影），不适合通用配置——配 mignon 后已中和 |

### NSFW 人体串淘汰记录（防止未来重蹈）

| 候选 | 结果 | 结论 |
|---|---|---|
| `1.4::asanagi::` 单画师 | 干净但**画风老旧**，用户不满意 | asanagi 可用但审美过时，弃用 |
| `asanagi + chen bin + na_tarapisu153`（0.9/0.7/0.6） | ❌ 红色噪点崩坏 | 组合冲突 |
| `rella 1.3 + na_tarapisu153 0.7` | ❌ 直接崩坏 | **na_tarapisu153 在多画师组合中兼容性差**（两次崩坏均含它；但朋友六人串中它 0.55 低权重时正常）——建议组合时该画师权重 ≤0.55 或不与其两人以上混搭 |
| `ask 完整名单画师 1.3` | 干净但带角色习惯（眼影） | 不适合通用配置 |
| `1.2::artist:ask::, 0.7::artist:as109::` | ❌ 满屏粉红 QR 状噪点 | **已定位真凶：`as109` 以数字结尾，紧贴 `::` 会被权重解析器误读**（与 `na_tarapisu153::` 被解析成权重 153 同源）。2026-09-14 首测崩坏；2026-09-15 三组对照定案 |
| `0.55::artist:ask::, 0.45::artist:as109, ::`（逗号断开） | ✅ **干净正常** | **as109 可用，但必须写成 `...as109, ::`（逗号断开数字与 `::`）**；或用括号链 `[[artist:as109]]`。注：「权重合计≈1」并非崩坏原因（合计 1.0 未加逗号时同样崩坏），该传闻尚未证实 |

> 🔑 **通用规则（2026-09-15 实测）**：**任何以数字结尾的画师名/标签，在 `N::xxx::` 数值权重写法里必须写成 `N::xxx, ::`**（逗号断开），否则数字紧贴 `::` 会被当作权重值、整条提示词崩坏。已知踩坑画师：`as109`、`na_tarapisu153`。

---

## 厚涂1 ✅

**配方**：
```
[artist:cogecha],{{artist:ciloranko}},artist:rella,[ask (askzy)],mignon,artist:kawacy,artist:minaba hideo,[artist:pigeon666]
```

| 项 | 内容 |
|---|---|
| 命名 | 用户 2026-09-14 指定「厚涂1」 |
| 来源 | nai4.top「所长常规NovalAI个人法典」作者自用基准串（源串中 `artist: kawacy` 的多余空格已归一化） |
| 首验 | 2026-09-14 · 窗边坐姿场景（1216×832 · 28 步 · CFG 5 · k_euler_ancestral · quality_toggle off · seed 784291504）对照社区A —— **细节密度最高**：云层体积光与层次、制服徽章/扣子/领巾、发丝分层、木窗铰链均有刻画 |
| 风格倾向 | 厚涂绘制感 + 光影体积强（ciloranko/rella 打底 + ask/mignon 撑人体 + kawacy/minaba hideo 提完成度） |
| ⚠️ 注意 | ①**8 画师组合实测未崩**（打破"多画师必崩"印象，但仍属高危区，改权重或加串前先小图验证）②括号链是 V4.5 时代语法，V5 可考虑转数值权重梯度（未测）③画师多、吃 token，场景描述要留预算 |

---

## 质感1 ✅

**配方**：
```
[artist:misyune],artist:karory
```

| 项 | 内容 |
|---|---|
| 命名 | 用户 2026-09-14 指定「质感1」 |
| 来源 | nai4.top「所长常规NovalAI个人法典」中频次最高的双人串（出现 4 次） |
| 首验 | 2026-09-14 · 窗边坐姿场景（同参数·同 seed）对照 —— 清爽 eroge 风、暖调夕阳、**保留原水手服设定不改**；细节中等，人体干净 |
| 风格倾向 | 双人轻量串，不抢设定；定位介于「社区A 极简」与「厚涂1 极繁」之间 |
| ⚠️ 注意 | token 占用小，适合搭配长场景描述；细节上限低于厚涂1 |

---

## 魔裁画风（梅まろ）✅

**配方**：
```
1.1::artist:umemaro_(siona0908)::, 0.5::artist:anmi::
```

| 项 | 内容 |
|---|---|
| 来源 | 画师词条核实：gelbooru `umemaro_(siona0908)`（354 张，official artist extra 标签证实）＝《魔法少女的魔女审判》角色设计师「梅まろ」；anmi 低权重补人体结构（梅老师手指/下巴固有瑕疵） |
| 首验 | 2026-08-31 · 神官修女立绘/哥特场景插图/NSFW 裸体立绘多轮测试（V5 Full · steps 23 · CFG 5 · k_euler_ancestral · quality_toggle off）· 用户验收通过，定为魔裁画风主串 |
| 质量头 | `very aesthetic, masterpiece, absurdres, best quality, high complexity`（关 Add Quality Tags）⚠️ **勿过度堆叠**——ultra complexity 等高强度质量词反而拉出草稿感/混乱 |
| 风格倾向 | 魔女审判 galgame 立绘风：细长眼+浓眼妆、冷色调、长发白皮、修女/哥特洛丽塔题材强 |
| 搭配注意 | ① 纯梅串 `1.2::artist:umemaro_(siona0908)::` 备用（纯度最高但完成度下限浮动）② 长发角色加 `hair behind shoulders` 防挡脸/挡脚 ③ NSFW 用英文标签、UC 不加 censored ④ **连抽间隔 ≥46 秒**（2026-09-11 实测：间隔不足 45 秒直接 403） |

---

## 茉子串 V5（ningsen_mame 单画师版）✅

**配方**：
```
0.85::ningen mame::, anime style illustration, anime coloring, soft shading, year 2024, masterpiece
```

| 项 | 内容 |
|---|---|
| 来源 | 原 V4.5 茉子串（五画师）V5 迁移失败后的简化终版；经 14 轮定位实验定案 |
| 首验 | 2026-09-02 · 茉子夕阳街道场景（832×1216 · steps 28 · CFG 5 · k_euler_ancestral · quality_toggle off · 种子 9845102736）· 用户以 0.75 浓度验收"还原度标杆"，终版定 0.85 |
| 风格倾向 | ningen_mame 简洁日系底子 + 画风词兜底，还原茉子串主要风味 |
| ⚠️ 注意 | **禁用任何形式的 year 权重写法**（`1.15::year 2024::` 会崩），只用裸 `year 2024`；**五画师全组合在其他画师加入时必崩**（见下方坑记录），只能单画师或与已验证安全画师池搭配 |

### 茉子串 V5 排查坑记录（2026-09-02 十四轮实验定案，勿重蹈）

| 配方尝试 | 结果 | 教训 |
|---|---|---|
| 五画师权重梯度（0.9/0.75/0.8/0.9/0.7，ningsen_mame 主导）+ 任何 year/画风词组合 | ❌ 全崩（噪点溶解） | **五画师组合在 V5 上直接崩**，与画风词、质量头、正负强调写法无关（F1/F2 裸 year 也崩） |
| 单 onineko + 裸 year + 画风词 | ✅ 不崩但还原度不足 | onineko 清白的（E5d） |
| 单 onineko + 加权 year | ❌ 崩 | **`1.15::year 2024::` 权重写法本身有毒**（E5b vs E5d 唯一变量铁证） |
| 均衡画风六画师（ningsen_mame 0.7 低权重） | ✅ 正常 | ningsen_mame 低权重（≤0.75）在他人组合中安全 |

**安全边界结论**：
- ningen_mame 权重 **≤0.75 在组合中安全，单画师可到 0.85**；1.0+ 未验证（④ 实验掺杂 year 加权无法归因）
- **year 标签永远用裸写法**（`year 2024`），不要加 `1.x::` 权重
- 旧茉子串（五画师 + `-5::artist collaboration::` + 加权 year）在 V5 完全不可用，勿迁移
- 官方直连（NOVELAI_USE_PROXY=false）不改变上述结论——官方直连同样崩

---

## 均衡画风 V5 ✅

**配方**：
```
1.1::tianliang_duohe_fangdongye::, 0.9::wlop::, 0.85::ask (askzy)::, 0.8::ciloranko::, 0.75::sho (sho lwlw)::, 0.7::ningen mame::, very aesthetic, best quality, masterpiece, absurdres
```

| 项 | 内容 |
|---|---|
| 来源 | 原 V4.5 休闲大佬"简约六画师"串 V5 改写（等权→权重梯度，ningsen_mame 收尾 0.7） |
| 首验 | 2026-09-02 · 夕阳街道/夜灯卧室普通+NSFW 双场景（832×1216 · steps 23/28 · CFG 5）· 用户验收"效果不错，和以前也像" |
| 风格倾向 | 均衡厚涂混搭，六画师递减梯度，tianliang 主导 |
| ⚠️ 注意 | 挂画师串时 base 不放画风脚手架词（画师串表达铁律）；quality 头只留一层 |

---

## 凉佬 V5 ✅

**配方**：
```
0.95::wanke::, 0.95::ask (askzy)::, 0.9::ciloranko::, 0.85::wlop::, 0.7::rhasta::, 0.65::tidsean::, 0.65::ke-ta::, 0.6::chiaroscuro::, very aesthetic, best quality, masterpiece, absurdres
```

| 项 | 内容 |
|---|---|
| 来源 | 原 V4.5 凉佬串（`[artist:ask (askzy)], artist:wanke, artist:ciloranko, [[artist:rhasta]], {chiaroscuro}, wlop, [artist:tidsean], [artist:ke-ta]`）V5 改写：`[ ]`/`{ }` 括号链全部换数值权重 |
| 首验 | 2026-09-02 · 同双场景横测 · 用户验收通过 |
| 风格倾向 | 凉佬明暗法底子，wanke/ask 双主位 0.95 |
| ⚠️ 注意 | chiaroscuro 保留为低权重 0.6 辅助画风词；其余同铁律 |

---

## 萝莉画风 ✅

**配方**：
```
artist: ciloranko, [artist: sho (sho lwlw)], [artist: baku-p]
```

| 项 | 内容 |
|---|---|
| 来源 | 中文 NovelAi-Bot 指南「绘画nai5模型」（nai-bot.pages.dev），标 `#绘画模型nai5方案` 的 V5 官方向单角色配方。原配方另带 `-2::artist collaboration::`、`-2::bikini::` 与 `Prompt_Guidance = 7.0`；**本条登记的是画师串本体，不含那两个负强调** |
| 首验 | 2026-10-02 · 茉子（mako）SFW/NSFW 双图对照（832×1216 · 28 步 · CFG 5 · k_euler_ancestral · seed 1255178144）· 用户验收并指定命名「萝莉画风」 |
| 风格倾向 | 亮面赛璐璐、线条干净、色彩明快；用户评语：**萝莉向**，和服类服装读起来会偏现代裙装 |
| 语法特征 | 用的是 **V4.5 式括号链**（`[...]` 降权）而非本 skill 主推的数值权重梯度——这是登记册里**唯一一条括号链配方**，别擅自改写成 `0.x::` 形式 |
| ⚠️ 注意 | ① 括号链与数值权重**不要混用**在同一串里；② 若要复现官方原意，可另加 `-2::artist collaboration::`（本登记版未含）；③ 官方原配方 CFG 是 7.0，本环境验收用的是 5，两者都正常出图 |

---

## 轻漫画 ✅

**配方**：
```
1.2::artist:icomochi::, 1.0::artist:oouso::, 0.8::artist:kaisen_chuui::, 0.7::artist:tomari_(veryberry00)::
```

| 项 | 内容 |
|---|---|
| 来源 | 按 **ai-nante.com 的 NovelAI Diffusion V5 Full 逐一实测目录**（734 个 tag，每个都在 V5 Full 上以同一 prompt / seed 2874500165 / 832×1216 单独出过图，并带 S/A 评级 + 风格分组）现组。本串取该目录 **S 级「セミリアル・大人っぽい」组**的 4 位 |
| 首验 | 2026-10-02 · 七海千秋（nanami chiaki）SFW/NSFW 双图（832×1216 · 28 步 · CFG 5 · k_euler_ancestral · seed 1255178144 · 床上、NSFW 为坐姿 M 开腿比 Y）· 用户验收并指定命名「轻漫画」 |
| 风格倾向 | 皮肤有立体质感、光影偏写实、人体结构严谨；漫画感强但不过度厚涂——用户评语：**轻漫画** |
| 语法特征 | 标准 V5 数值权重梯度（与「萝莉画风」的括号链相反），四位画师全部来自 V5 实测 S 级，**无欧美画师** |
| ⚠️ 注意 | ① 这是登记册里**唯一一条由 V5 实测数据现组**（非社区流传成品串）的配方，改动前请先跑小样本；② 若要更强的漫画感，可加 `comic style, halftone`；③ 避免与括号链串混用 |

---

## 社区A1 ✅

**配方**：
```
1.1::artist:ningen_mame::, 0.7::artist:karameru::, 0.6::artist:ainy::
```

| 项 | 内容 |
|---|---|
| 命名 | 用户 2026-10-02 指定「社区A1」 |
| 与社区A 的关系 | **社区A 的单画师变体**——只把第 3 位 `mery` 换成 `ainy`，权重（0.6）与位置不变。第 1、2 位 `ningen_mame 1.1` / `karameru 0.7` 原样保留 |
| 来源 | 为解「社区A 足部细节差」而做的对照实验产物；`ainy`（あいに）出自 5ch Wiki「アーティスト」表，该表标注 `V5 Full。V4.5でも反応` |
| 首验 | 2026-10-02 · 七海千秋（nanami chiaki）SFW/NSFW 双图（832×1216 · 28 步 · CFG 5 · k_euler_ancestral · seed 1255178144 · 床上；NSFW 为坐姿 M 开腿比 Y + 社区足部配方） |
| 风格倾向 | 与社区A 同系（ningen_mame 主导的简洁日系赛璐璐），**画风最接近社区A 的一条**；足底、脚趾、手指结构明显优于社区A |
| 验证依据（关键） | 同批把**社区A 本体设为对照组**，同一提示词、同 seed、同一套足部配方。结果社区A 仍然**比 Y 的那只手糊成一团 + 下半身出现融化区**，而社区A1 手部五指正常、足底脚趾清晰 → 证明社区A 的手足崩坏是**串本身**的问题，非提示词问题 |
| ⚠️ 注意 | ① 这条是**实验产物**，只验过七海千秋一个角色 + 床上场景，换角色/场景前先跑小样本；② 足部收益有一部分来自配套的**足部配方**（`sole of foot, bare soles, clean soles, soles toward viewer, detailed toes, subtle wrinkles` + `low angle`），单靠换串未必复现；③ 若要微调，建议不要动第 1 位 `ningen_mame`（它是风格骨架） |

---

## 赛璐璐1 ✅

**配方**：
```
artist:sho (sho lwlw), artist:tianliang duohe fangdongye, artist:kappe, artist:fuzichoco, vibrant colors
```

| 项 | 内容 |
|---|---|
| 命名 | 用户 2026-10-05 指定「赛璐璐1」 |
| 来源 | 用户提供的配方（四位画师全等权 + 一个风格标签）；四位画师**均不以数字结尾**，不触发 `N::xxx::` 的权重解析崩坏坑 |
| 首验 | 2026-10-05 · 阿米娅（`amiya (arknights)`）SFW/NSFW 双图（832×1216 · 28 步 · CFG 5 · k_euler_ancestral · seed 1255178144 · 日式庭院 + 樱花 + 石径，站姿全身）· 用户验收并指定命名 |
| 风格倾向 | 明快高饱和：人物层线条干净、色块清晰（赛璐璐倾向），背景保留笔触感；`vibrant colors` 等权作用显著——石块/水面出虹彩反光、发丝带虹彩渐变 |
| 语法特征 | 纯等权写法（通篇无 `N::` 权重，与本册主流的权重梯度串用法不同）；末尾 `vibrant colors` 是**风格标签不是画师**；`tianliang duohe fangdongye` 用的是**空格版**——Danbooru 规范写法是下划线 `tianliang_duohe_fangdongye`（本册「均衡画风 V5」用的即下划线版），本次空格版出图正常、未见差异 |
| ⚠️ 注意 | ① 角色还原走「版权角色只写名字」：本次仅给 `amiya (arknights)`、**零外貌锚点**即准确还原（兔耳／棕发／蓝瞳／黑底青衬大衣），无需补发色瞳色；② 机位 tag `from side` 放在尾部未生效（与同日 rhasta-test 完全同因，不是本串的问题）——要压机位需前移或加权；③ `vibrant colors` 等权会带来彩边／虹彩反光，若要正常色温可降为 `0.6::vibrant colors::` 或删除 |
| 产物 | `<输出目录>\amiya-sho-test-20261005\`（`amiya-sho-test_SFW.png` / `amiya-sho-test_NSFW.png` / `_contact-sheet.png` / `manifest.json`） |

---

## 二游渲染 ✅

**配方**：
```
0.7::artist:poruserin::, 0.9::artist:rebun::, 0.8::artist:kurotsuki (luowei99)::, 0.8::honkai impact 3rd official art::, game cg, zenless zone zero official art, 2::year 2026 ::, 5::masterpiece, aesthetic, very aesthetic, best quality, absurdres, newest, highres::, 3::no text::, masterwork, 5::high-quality rendering ::, 2::cinematic composition ::, soft studio lighting::, -2::flat color, crudely drawn image::, -2::upscaled, blurry, dark background::
```

| 项 | 内容 |
|---|---|
| 命名 | 用户 2026-10-05 指定「二游渲染」（测试代号 P6） |
| 来源 | 融合配方：基础三画师梯度（poruserin 0.7 / rebun 0.9 / kurotsuki 0.8）+ 二游官方CG风（honkai impact 3rd 0.8 / ZZZ / game cg）+ 2026 电影渲染/光照质感与负强调（year 2026 / cinematic composition / soft studio lighting / -2::flat color... / -2::upscaled, blurry, dark background::）全开大合体 |
| 首验 | 2026-10-05 · 七海千秋（`nanami chiaki`）全身双图对照（832×1216 · 28 步 · CFG 5.0 · k_euler_ancestral · 学校夕阳倚桌环境交互 + 泳池全身比基尼人体解剖测试）· 用户满意并指定入册 |
| 风格倾向 | **二游商业级完成度 + 电影级布光**：既有二游官方立绘级别的严谨解剖比例、紧实肌肉线条与服饰层次，又有电影渲染底模带来的高动态范围光影（窗外夕阳轮廓光、地面光斑倒影、逆光发丝漫射） |
| 语法特征 | 混合数值权重体系：涵盖画师权重梯度、二游标签权重、多级质量/构图标签强加权（5:: / 2::），以及 `-2::` 负强调对糙画与死黑背景的强力压制 |
| ⚠️ 注意 | ① 自身已包含高强度质量词与负强调，使用时**不要在正向提示词中重复堆砌基础 quality tags**；② 场景与光影交互能力极强，在教室、室内或自然光下能自动生成极其高级的漫射光与地面倒影；③ 人体测试证明其全身头身比与骨骼体态极其稳定，极少出现多肢体或比例崩坏 |
| 产物 | `<输出目录>\chiaki-7strings-test\`（`P6_school.png` / `P6_swimsuit.png` / `_contact-sheet.png` / `manifest.json`） |

---

## 质感2 ✅

**配方**：
```
0.8::artist:iumu ::, 0.75::artist:ask (askzy) ::, 0.65::artist:ningen_mame ::, 0.6::artist:betabeet ::, 0.5::artist:kase_daiki ::, 0.5::artist:meion ::, 0.5::artist:kousaki_rui ::, 0.45::artist:jima ::, 0.45::artist:misaka_12003-gou ::, 0.45::artist:dino_(dinoartforame) ::
```

| 项 | 内容 |
|---|---|
| 命名 | 用户 2026-10-06 指定「质感2」 |
| 来源 | 「所长 NovelAI 个人法典」（nai4.top）**编纂者常用画师组 · 组4** 的 V5 语法转译版。原串为 `1.3::artist:iumu::,1::ask(askzy)::,ningen mame,,0.9::betabeet::,,0.5::kase_daiki,meion,kousaki rui::,0.6::jima::,0.5::misaka12003-gou ::,,artist:hagi (ame hagi),,dino(dinoartforame),year 2024,year 2025 ::,no text,best quality,very aesthetic,absurdres,0.1::shiny skin::,year 2025,-5.1::artist collaboration::` |
| 与法典原串的差异 | ① **整串权重 ×约 0.6 折算**（原 1.3/1.0 等 → 0.8/0.75 等），落入本册 V5 权重的 0.4–0.9 稳妥带；② **删去 `-5.1::artist collaboration::`** 与两处 `year 20xx`、`no text`、质量词、`0.1::shiny skin::`——这些属于当时的脚手架，本册按「base 不放风格脚手架、质量头只留一层」处理；③ 补 `hagi (ame hagi)` 下划线规范写法为未纳入（该画师在原串中无权重、且 `misaka12003-gou` 已由 0.5 权重位替代）；④ `misaka12003-gou` 规范化为 `misaka_12003-gou` |
| 首验 | 2026-10-06 · 七海千秋（`nanami chiaki`）SFW/NSFW 双图（832×1216 · 28 步 · CFG 5 · k_euler_ancestral · seed 1255178144 · SFW 为普通教室布景坐姿插图；NSFW 为教室课桌上、`spread pussy` + `sole of foot, soles toward viewer, detailed toes` 阴部与足底双细节展示）· 用户验收满意并指定命名 |
| 风格倾向 | **五官立体、体积感强**：面部明暗过渡层次最丰富，肌肤有实体厚度而非平涂；十个画师梯度把「美型」（iumu/ask）与「上色层级」（ningen_mame/betabeet）叠在一起，是本次 5 串里**质感最厚、最不扁平**的一条；用户评语定位为「质感」系 |
| 语法特征 | 标准 V5 数值权重梯度（`N::artist:name ::`），**权重末尾一律带一个空格再闭合 `::`**；十位画师全部不以数字结尾（`misaka_12003-gou` 以 `gou` 结尾、`dino_(dinoartforame)` 以 `)` 结尾），不触发数字紧贴 `::` 的解析崩坏坑 |
| ⚠️ 注意 | ① **画师数量达 10 位，吃 prompt token 明显**，场景描述预算要给足，复杂多人/文字渲染场景建议先裁到 5–6 位再试；② 本条只验过七海千秋一个角色 + 教室场景，换角色/换场景前先跑小样本；③ 第 1 位 `iumu` 与第 2 位 `ask (askzy)` 是风格骨架，微调时优先不动这两位；④ `ask (askzy)` 含空格与括号，逐字复制，勿改成 `ask` 或 `ask_askzy` |
| 产物 | `<输出目录>\chiaki-5v5strings-classroom-20261006\`（`2_iumu_ask_balance_SFW.png` / `2_iumu_ask_balance_NSFW.png` / `_contact-sheet.png` / `manifest.json`；同目录另有本轮对照的 ①③④⑤ 四条串，可作横向比对基线） |

---

## 🇰🇷 韩网社区串（外部语料反读 · 未经本机验收）

> ⚠️ **性质说明**：以下三条**不是**用户本人验收过的串，而是 2026-10-09 从韩网 N5 作品集（935 张，391 张反读成功）中提取的**高复用社区配方**。
> 每条在原始语料里被整组复用于 11–173 张成图，配方**逐字保留原始权重**。
> **使用前建议先跑小样本**（见 `kr-n5-corpus-analysis.md`），确认在本机通道下的表现。
> 与上文已验收串的区别：这些串未经本机出图验证，但样本量大、风格特征明确。

### 韩网·漫画人体串（173 张复用，语料第一主力）⚡

**配方**：
```
1.2::masterpiece, very aesthetic, best quality, amazing quality, absurdres, highres, best illustration::, -1::artist collaboration, mosaic::, 1.3::artist:doppel (bonnypir)::, acolored, vibrant colors, 0.8::draw body like artist:henriiku (ahemaru) ::, 0.9::artist:yoneyama mai, c.cu, artist:iuui::, 0.4::artist:freng::
```

| 项 | 内容 |
|---|---|
| 来源 | 韩网 N5 作品集 `2026-10-03_21-49-01` / `2026-10-03_21-55-05` / `2026-10-04_08-11-38` / `2026-10-05_13-20-37` 四个目录，同签名 **173/391 张**，是本语料最大单一画风族 |
| 推荐参数 | steps 23（部分目录 25）· **CFG 5.0** · cfg_rescale 0 · 832×1216 · k_euler_ancestral · karras |
| 风格倾向 | 专业漫画感、线条有力、色彩鲜明（`acolored, vibrant colors`）；人体结构由 henriiku 定向提供，比例紧实 |
| 语法特征 | ⭐ **教科书级 `draw body like artist:X` 四层结构**：主导画风(1.3) → 人体借用(0.8) → 氛围配色(0.9) → 兜底统一(0.4)；配 `-1::artist collaboration, mosaic::` |
| ⚠️ 注意 | ① 权重块内 `(ahemaru) ::` **闭合前留空格**，规避 `)` 紧贴 `::` 的解析风险；② 此串**自带质量头与负强调**，搭配时不要再叠一层 quality tags |

### 韩网·厚涂质感串（13 张复用）

**配方**：
```
1.5::mo_(kireinamo) , 0.6::rusellunt::, 0.5::kunaboto::, 0.3::mikozin ::, 0.8::artist:wagashi (dagashiya) ::, 0.7::artist:michiking,::, 0.9::artist:manglife ::, 0.5::artist:typehatena ::, 1.1::artist:healthyman ::, 0.7::tianliang duohe fangdongye::
```
> 质量头尾缀（原文照录）：`year 2026, year 2025, masterpiece, best quality, amazing quality, very aesthetic, best illustration, newest, incredibly absurdres, hyper detail`

| 项 | 内容 |
|---|---|
| 来源 | 韩网 `2026-10-02_14-11-40`（11 张）+ `2026-09-29_21-03-14`（rusellunt 换位版），10 画师厚涂系 |
| 推荐参数 | **steps 28 · CFG 7.2** · cfg_rescale 0 · 832×1216 · k_euler_ancestral · karras |
| 风格倾向 | 厚涂质感、繁复线稿（`thick eyelashes, thick draw lines, hatching (texture)`）、painterly |
| ⚠️ 注意 | ① 这是本语料中**少见的 CFG 7.2 高值**案例，配合 steps 28；② `michiking,::` 内部那个逗号是原文，非笔误；③ `tianliang duohe fangdongye` 含空格，勿改下划线 |

### 韩网·高饱和变形串（60 张复用，含 NSFW 场景）

**配方**：
```
1girl, -2::wide shot::, -2::multiple views, speech bubble, text, background human::, 0.5::artist:murata yuusuke ::, 0.5::artist:hwansang ::, artist:supernew, artist:wanke, 0.8::artist:deadflow, artist:freng::, 0.7::artist:pottsness::, 0.8::artist:yd (orange maru)::, 2::artist:uchikaze::, 0.9::artist:ciloranko::, year 2026, year 2025, heating relationship, contemporary, random pose, masterpiece, very aesthetic, incredibly absurdres, absurdres, ultra high resolution, digital illustration, 2::slender::, -5::anatomical nonsense::, -1.5::artist collaboration::
```

| 项 | 内容 |
|---|---|
| 来源 | 韩网 `2026-10-01_13-38-36`（60 张），9 画师高饱和族 |
| 推荐参数 | steps 23 · CFG 5.0 · cfg_rescale 0 · 832×1216 |
| 风格倾向 | 高饱和、细长身形（`2::slender::`）；`uchikaze` 以 **2.0 权重**主导 |
| 语法特征 | ⭐ **负强调教科书**：`-2::wide shot::`（防镜头拉远）+ `-2::multiple views, speech bubble, text, background human::`（防分格/气泡/路人）+ `-5::anatomical nonsense::`（修解剖）+ `-1.5::artist collaboration::` |
| ⚠️ 注意 | ① `-5::anatomical nonsense::` 是本语料中最强解剖负强调，**在正常通道下稳定**（此前"大倍数负强调崩坏"应归因旧镜像通道）；② 此族含大量 NSFW 变身/多男场景，`faceless male` + 女方框写满是其主要写法 |

