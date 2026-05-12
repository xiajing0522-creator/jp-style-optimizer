# moomoo JP 内容场景 → jp-style-optimizer 路由表

**Load when**: 输入或 brief 中出现 `moomoo` / `moomoo証券` 字样，或操作者明确要求 moomoo 品牌口吻（同时也会触发 Step 3.5 → `case-library.md` 中 moomoo 条目）。否则按 `style-guide.md` 通用推断走。

来源: 飞书 wiki「moomoo JP 内容生产场景盘点」(`OGQQwEmmhi0FFJkGwSYcasNCnyh`)。本表把 moomoo JP 实际投放场景按 `--style` × `--scene` 映射，并标注触发的 RL-4 字数限制和 `--segment` 配套建议。具体 31 条原文样本见 `diagnosis/moomoo-jp-control-group.md`（boost 效果测试对照组）。

---

## Tier 1: `campaign`（营销活动类）

| moomoo 场景 | 投放载体 | 推荐 `--scene` | RL-4 限制 |
|---|---|---|---|
| 活动 Push（转仓 / 口座開設&入金） | push | `launch` / `remind` | タイトル≤20 / 本文≤60 |
| 活动 EDM（官宣 / 中段 / 最终日） | edm | `launch` / `remind` / `lastday` | 件名≤40 / プリヘッダー≤80 / CTA≤15 |
| 落地页 LP（H5 / Web-PC） | LP | `launch` / `seasonal` | 主标题≤10 / 副标题≤15 |
| 站内闪屏 | banner 2000×2400 | `launch` | メイン≤15 / サブ≤25 / CTA≤8 |
| 站内一级 / 动效弹窗 | banner 810×1110 | `launch` | 同上 |
| 站内位（个股 / 交易 / 资讯 / 我的 / 活动中心 / 课堂 / 仿原生） | banner 各尺寸 | `launch` | RL-4 banner 限制 |
| 悬浮球 A 面 + B 面 | banner 异形 | `launch` | 各面文字≤8 字 |
| 宝箱任务详情页 | banner 1080×675 | `result` | RL-4 banner 限制 |
| 产品弹窗（活动视图） | banner | `launch` | 主≤10 / 副≤16 / CTA主≤5 |
| 站外（官网首页 / Newsroom / iframe / 侧边栏 / Top） | banner | `launch` | RL-4 banner 限制 |
| SNS 投稿（X/Twitter） | sns | `referral` / `seasonal` | 全文≤140 |
| 分享任务 | sns 入口 | `referral` | 1 句利益点 + 1 句动作 |
| SEM（品牌 / 竞品 / 通用 / 美股词） | banner 文本广告 | `launch` | 标题≤30 / 描述≤90 |
| 禀议書 / 调研问卷 | 内部审批 / 调研 | — 不走 skill | 排除 |

**`--segment` 配套**:

| moomoo 用户场景 | `--segment` |
|---|---|
| 流失召回 | `churn` |
| 拉新（未首交） | `never_traded` |
| 高资高潜 | `high_value` |
| 仅持日股 → 跨卖美股 | `jp_stock_only` |
| 仅持美股 → 跨卖日股 / NISA | `us_stock_only` |
| 无效户激活 | `inactive` |

**moomoo campaign 特有约束**（叠加在 T1+T2 之上，详见 case-library.md moomoo 条目）:
- 奖品名必带「相当」（最大5万円**相当**）
- 奖品全称: 株式キャッシュバック**券** / **MMF利回りアップ**券 / **取引手数料優待**カード
- 抽奖描述用「必ずもらえる」，禁用「100%当選」
- 市场语境用客观词（「変動の市場」），禁主观鼓动（「チャンス密集中」）
- セクター回帰用「資金回帰」，禁「資金流入が続く」
- Win-back EDM 开场固定「いつもmoomoo証券をご利用いただきありがとうございます」

---

## Tier 1: `trade-ideas`（赚效内容类）

| moomoo 场景 | 推荐 `--scene` | 字数 / 形态 |
|---|---|---|
| 气泡文案 | `flash` | ≤140 字 + 标题 + CTA |
| 行情通知（营销侧） | `flash` / `alert` | 标题≤15 / 主按钮≤5 |
| 资讯早报 | `morning` | 300–800 字 |
| 开盘速递 / 收盘点评（含投资视点） | `morning` / `wrap` | 纯事实改走 news；含分析+行动桥接走 trade-ideas |
| 异动合集 | `theme` | 500–1500 字 |
| 名人作业（木头姐 等） | `picks` | 80–200 字/銘柄、≥2 数字指标（AC-15） |
| 赚效×产品力营销贴 | `theme` | ≥500 字、必加 disclaimer（AC-10） |
| 节奏型专项（年末 / 新年盘点） | `theme` | 同上 |
| 社区话题 / 互动贴 | `community` | 400–800 字 + 参加模块 |
| 小号文（KOC 第一人称） | `community` | 50–800 字、【投稿例】允许タメ口（RL-11 例外） |
| 小号评论 | `community` | 30–250 字、同上 |
| PUGC 帖（编辑导语 + 用户语录） | `community` | 编辑层だ/である + 用户语录原貌保留 |
| 决算ハイライト（个股投资视点） | `earnings` | 200–500 字 |

**moomoo trade-ideas 特有约束**:
- デュアルレジスタ（RL-11 trade-ideas 例外）: 分析段だ/である / 读者参加段です/ます
- community 的【投稿例】区段允许タメ口（RL-11 例外 b）
- 行动桥接必须存在（不可纯客观，否则改走 news）
- ≥500 字必加 disclaimer 一行（AC-10）；短尺（flash/picks/earnings/morning短/community短）按 ADR-006 由平台 footer 兜底

---

## Tier 1: `news`（新闻事件类）

| moomoo 场景 | 推荐 `--scene` | 字数 |
|---|---|---|
| 自动化资讯（机器生成快讯） | `flash` | ≤140 |
| 资讯专栏 - 纯客观开 / 收盘 | `wrap` | ≤700（AC-13）；分析>30% 改走 trade-ideas |
| 决算速报（客观业绩） | `earnings` | 150–400 |
| 经济指标速报（CPI / 雇用統計 / GDP） | `indicator` | 100–300 |
| ニュースダイジェスト | `digest` | ≤1200（AC-13） |
| 行情アラート（閾値到達 / 閉市変動） | `alert` | ≤100 |
| PR 稿 / 公司新闻（产品发布 / 制度变更） | `flash` / `wrap` | 见闻发型 |
| 重要公告（アプリ更新 / 規制対応） | `alert` | ≤100 |

**moomoo news 特有约束**:
- CTA 禁止（AC-11） — PR 稿即使含「詳しくはこちら」也必须从 news 抽出改走 trade-ideas/community 或 product/release
- 主観表現禁止（RL-3） — 「思います」「感じます」全移除
- 分析比率 ≤30% — 超出门槛在 Step 5 自动 re-route 提示走 trade-ideas

---

## Tier 1: `product`（产品运营类）

| moomoo 场景 | 推荐 `--scene` | 字数 |
|---|---|---|
| 搜索暗纹 | `short` | 1 行≤12 字 |
| Tooltip / UI 微文案 | `short` | 30–80 字 |
| 产品说明书（Manual） | `manual` | 150–400 |
| Step by Step 一图 | `manual` | 3–7 步、每步 10–20 字 |
| What's New 栏目 | `release` | 100–300 |
| 用户之声栏目 | `release` | 100–300 |
| 新功能上线宣发帖 | `release` / `detail` | 500–8000 |
| 投教课程（USP 课程） | `onboard` / `manual` | 500–2000 |
| 直播预告（中 / 日文） | `short` / `release` | 50–200 |
| 动画 / 音声脚本 | `script` | ≤30 字/文（RL-4） |
| Auto PUSH（User Journey） | `short` | title 15–35 / subtitle 30–60、需配 `--segment` |
| Auto EDM 模块（USP 段） | `short` / `detail` | 模块标题 10–20 / 正文 50–150 |
| USP 文案库（跨场景复用） | `compare` / `short` | 短版 50–100 / 长版 150–300 |
| App 卡片页（User Journey） | `onboard` | 200–500 |

**moomoo product 特有约束**:
- F→B（Feature→Benefit）必须成对（product T1 强制）
- 功能名走 RL-1 锁词:「注目テーマ追跡」「機会リスト」「TradingView」「moomoo API Skills」原貌保留
- CTA 任意，但只允许低承诺（「詳しく見る」「使い方を見る」），禁 hot CTA（「今すぐ申し込む」）

---

## Tier 1: `compliance`（合規服務类）

| moomoo 场景 | 推荐 `--scene` | 字数 |
|---|---|---|
| 帮助中心文章 | `faq` / `guide` | Q&A 20–35 字 / 手順 20–40 字 |
| 利用規約 / T&C（LP 底部） | `terms` | 40–60 字/文 |
| 免責事項 / Disclaimer | `disclaimer` | 40–60 字/文。trade-ideas/theme・morning ≥500 字必加（AC-10） |
| 開示文書 / 目論見書 | `disclosure` | 30–50 字、だ/である体（RL-5） |
| 景表法 / 禀议書 T&C 段（内嵌） | `disclosure` / `terms` | 同上 |

**moomoo compliance 特有约束**:
- 全场景禁宣传词彙（AC-12, AC-16）: 必勝 / 絶対 / 確実 / 100% / 間違いなし / 今すぐ / ！
- disclosure 段绝对だ/である体（RL-5），LP 嵌入也不破例
- compliance/faq + guide 用谦譲語 II（承ります / ございます / おります）

---

## 路由排查清单（走 skill 前确认）

1. **语种**: 中文 / 英文素材 → 先走 `lark-cn2jp-finance` 翻译，再交本 skill。本 skill 不译（RL-6）。
2. **Tier 1 判定**:
  - 含「特典 / 期限 / CTA / 申し込む / プレゼント」→ `campaign`
  - 含个股 / 数据 / 投资视点 + 行动桥接 → `trade-ideas`
  - 客观事件、零 CTA、分析 ≤30% → `news`
  - 功能 / 操作 / 版本 / 教育 → `product`
  - 規約 / 免責 / 開示 / FAQ → `compliance`
3. **Tier 2 判定**: 看字数限制、信息结构（結論先行 / 並列型 / 手順型）、有无 CTA。
4. **Segment**: campaign 务必传 `--segment`，影响 CTA 温度（cold/warm/hot）和 Layer 3 心理触发。
5. **品牌口吻**: 触发 Step 3.5 → 加载 `case-library.md` moomoo 条目；对标 SBI / 楽天 / Nomura 时同样触发各自条目。
