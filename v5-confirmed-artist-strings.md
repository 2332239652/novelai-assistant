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
