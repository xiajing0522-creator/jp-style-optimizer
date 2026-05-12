# moomoo JP 实操日文案例对照组(Control Group)

为 boost 后的 jp-style-optimizer 效果测试提供对照组样本。每条样本来自飞书 wiki「内容生产场景盘点」(`OGQQwEmmhi0FFJkGwSYcasNCnyh`),按 jp-style-optimizer 的 Tier 1 (`--style`) 分组。

**测试方法**: 把每条「原文」分别给 boost 前 / boost 后的 skill 优化(同 `--style` × `--scene` × `--segment`),对比:
- 字数限制达成率(RL-4)
- 红线违反次数(RL-1 ~ RL-12)
- 验收 AC-1 ~ AC-16 通过比例
- 与 moomoo 品牌口吻 benchmark 的吻合度(参考 case-library.md 的 moomoo 条目)

样本不做任何编辑,保留原文完整内容,以便复测可重现。

---

## Tier 1: `campaign` — 营销活动类

### C-1 EDM(转仓活动)

**来源**: sheet2 R2 / @crystaldu / `--scene launch` (edm 频道)
**RL-4 限制**: 件名 ≤40 / プリヘッダー ≤80 / CTA ≤15

```
moomooへ株式移管で、米国株手数料2年間０円+出庫手数料全額還元で最大130万円相当の特典!
出庫手数料を全額負担!さらに、限定プレミアムサービスで取引体験をアップグレードしよう

いつもmoomoo証券をご利用いただきありがとうございます。

下記のようなお悩みはありませんか?

💸 取引手数料の負担:売買のたびに手数料が利益を削り、長期的に見ると大きな負担とな…
```

### C-2 Push(转仓活动)

**来源**: sheet2 R3 / @crystaldu / `--scene launch` (push 频道)
**RL-4 限制**: タイトル ≤20 / 本文 ≤60

```
title: 株式移管で最大130万円相当の特典!専用VIP特典を今すぐゲット
content: moomooなら、1つのアプリで米国株・日本株・ETF・オプション取引が可能。資産の損益が一目瞭然、手数料は業界最安。
今すぐ移管で、最長2年間の手数料無料+出庫手数料の還元、さらにVIP専用サービスをアンロック!
詳細をクリックして、特典を手に入れよう。
```

### C-3 站内弹窗(转仓活动)

**来源**: sheet2 R5 / @crystaldu / `--scene launch` (banner 频道, 810×1110)
**RL-4 限制**: メイン ≤15 / サブ ≤25 / CTA ≤8

```
株式入庫で
最大130万円相当が必ずもらえる!

最大2年間の米国株取引手数料無料
出庫手数料全額還元
限定プレミアムサービス利用

CTA: 今すぐ参加
```

### C-4 SNS(地政学风险/贵金属)

**来源**: sheet2 R52 / @panchohou / `--scene referral` (sns 频道)
**RL-4 限制**: 全文 ≤140

```
地政学リスクで貴金属急騰中🔥
関連株・ETFをチェック✨

初回入金で $NVDA などの買付代金プレゼント!

累計200万DL突破のmoomooアプリでチェック▼
{inviteLink}

#moomoo証券 #米国株
```

### C-5 SNS(注文機能宣传)

**来源**: sheet2 R60 / @panchohou / `--scene referral` (sns 频道)
**RL-4 限制**: 全文 ≤140

```
＼夜更かしせず米国株／
トレールストップ注文で利益を自動確保

これが賢い投資家の新常識です!
初回入金で $NVDA などの人気株が無料でもらえる

【すでに200万人が利用中】
moomoo証券でワンランク上の取引を始めよう↓↓
{appInviteLink}

#moomoo証券 #米国株
```

---

## Tier 1: `trade-ideas` — 赚效内容类

### T-1 气泡文案(高 CTR 集合)

**来源**: sheet1 R5 / @sarahshi / `--scene flash`
**RL-4 限制**: 标题 ≤30 / CTA ≤4(气泡内置规格)

```
1. 半導体株に買い戻しが殺到!底打ちは本物か?
2. 中東緊張で米市場は再び警戒モード!今週は押し目買いか?
3. スペースX IPO加速、宇宙関連株に再点火?恩恵を受けそうな関連銘柄は?
4. 【マイクロン決算予想】EPS 5倍予想でもなお足りない?
5. 逆風下で輝くメモリー株!オプションでチャンスをつかもう
```

### T-2 木头姐 Trade Idea

**来源**: sheet4 R17 / `--scene picks`
**字数目标**: 80-200/銘柄、≥2 数字指标(AC-15)

```
キャシー・ウッド氏の投資動向:次世代原子力企業X-Energyを大量買い増し!逆張りでAMD売却——高値からの撤退
```

### T-3 当周展望(地政学+原油+XLE)

**来源**: sheet4 R10 / `--scene theme`
**字数目标**: 500-1500、需 disclaimer(AC-10)

```
【今週の展望&戦略】地政学で相場の風向き一変、原油急騰がリスク資産を圧迫!XLEで守るべきか?
```

### T-4 异动合集(米株プレマーケット)

**来源**: sheet4 R13 / `--scene wrap` (或 trade-ideas/morning)

```
【米株プレマーケット】量子コンピューティング関連銘柄は続伸、LAESは10%超上昇、QBTSは8%近く上昇、IONQ、QUBT、RGTIは4%超上昇 ブロードコムは3%近く上昇、Metaとの協力関係拡大を発表 原子力関連銘柄も続伸、OKLO、SMR、NNEはいずれも約3%上昇
```

### T-5 社区贴(AI 蓄電所 7 銘柄)

**来源**: sheet4 R21 / `--scene community`

```
AI"電力爆食"支える「蓄電所」7銘柄!年初来3バガーも!国策化で市場規模は5年後に5倍超か
```

---

## Tier 1: `news` — 新聞事件类

### N-1 速報(地政学)

**来源**: sheet4 R3 / `--scene flash`
**RL-4 限制**: 全文 ≤140 / 見出し ≤15

```
【速報】イラン外相アラグチ、ホルムズ海峡の商業船舶の航行は開放された
```

### N-2 朝刊(米国株先物急落)

**来源**: sheet4 R4 / `--scene morning`(news/wrap 边界)

```
【朝イチ報】米国株先物が急落、戦争終結期待ほぼ消滅 グーグル、新AI半導体開発でマーベルと交渉か
```

### N-3 米国市場展望(纯客观)

**来源**: sheet4 R5 / `--scene wrap`
**RL-4 限制**: 全文 ≤700 / 見出し ≤32

```
米国市場の展望:トランプ氏、イラン衝突下の米株反発に「驚き」、2割下落を予想 J.P.モルガン、アマゾン・アンソロピック提携でマーベルなど上昇 ドル高で銀鉱山が下落、投資家は米・イラン協議に注目
```

### N-4 決算速報(TSMC)

**来源**: sheet4 R3 / `--scene earnings`
**RL-4 限制**: 全文 150-400 / 見出し ≤32

```
更新-【TSMC決算速報】TSMC、時間外で2%超上昇 Q1は増収増益、AI需要追い風に純利益58%増
```

### N-5 经济指标 / 一周前瞻

**来源**: sheet4 R6 / `--scene digest` 或 indicator
**RL-4 限制**: digest ≤1200

```
今週の決算・経済カレンダー(4/27~5/1)注目要素満載!米M7・ストレージ・半導体決算、個別物色に全力投球!日米中銀会合、米PCE・GDP、バークシャー・ハサウェイ株主総会にも注目
```

### N-6 PR 稿(产品发布)

**来源**: sheet5 R22 / `--scene flash`(corporate news)

```
moomoo証券、国内初となるTradingView上での米国株オプション取引に対応
【iOS】日本専用版moomooアプリ リリースのお知らせ-moomoo証券
moomoo証券、米国株信用取引の利便性を大幅向上
```

### N-7 行情通知(应用更新)

**来源**: sheet1 R6 / @jasperqiu / `--scene alert`
**RL-4 限制**: 全文 ≤100 / 見出し ≤15

```
標題: 新アプリダウンロードのお願い
正文: iOS向け「日本専用版」アプリをリリースしました。自動アップデートは新しい日本専用版アプリのみ対応のため、App Storeよりダウンロードをお願いします。
主按钮: 入手する
```

---

## Tier 1: `product` — 产品运营类

### P-1 新功能上线宣发(API Skills)

**来源**: sheet5 R2 / `--scene release` 或 detail
**字数目标**: 500-8000

```
Moomoo API Skills解禁!AIが"24時間眠らないトレーディングエージェント"に。チャットだけで自動売買が完結。プレミアム機能が今だけ無料!
```

### P-2 用户之声栏目

**来源**: sheet5 R5 / `--scene release`

```
「お客様の声」を実現しました!注文・約定履歴の管理機能を強化について
```

### P-3 赚效×产品力营销贴

**来源**: sheet5 R6 / `--scene detail` 或 trade-ideas/theme

```
決算シーズンを乗り切る必須アイテム!投資を加速させる「秘密の道具箱」大公開!
DeepSeekショックをチャンスに!moomooアプリの4大機能で相場の波に乗ろう
```

### P-4 节奏型专项(年末/新年)

**来源**: sheet5 R7 / `--scene release` 或 trade-ideas/theme

```
新年を迎える前に!moomooの人気機能で投資チャンスを掴もう!
【2025年振り返り】moomoo証券の4大機能で投資の一歩先へ!
```

### P-5 Auto PUSH(User Journey)

**来源**: sheet5 R21 / `--scene short` (push 频道)、需 `--segment` 配套
**RL-4 限制**: title 15-35 / subtitle 30-60

```
1. 業界初*投資に特化した対話型AI登場! 膨大なデータを瞬時に分析!
   投資家にとって重要な情報を効率よく抽出し、あなたの「知りたい」にすぐ答えます。詳しくはこちら>https://j.moomoo.com/0bEtLn

2. 業界最大級の銘柄取扱数! あなたにピッタリな銘柄を探そう!
   米国株、米国ETFの取扱数が業界最大級!中には年初来400%以上上した銘柄も! 圧倒的なパフォーマンスを狙える…
```

### P-6 PUSH(产品功能介绍)

**来源**: sheet5 R19 / `--scene short`
**字数目标**: title 15-35 / subtitle 15-45

```
title: 金・銀急落は押し目買いチャンス?大幅変動時に差がつく投資機能とは
subtitle: リスク管理しながらチャンスを掴む5大機能を徹底解説。今すぐ確認>>
```

### P-7 小号文(KOC 第一人称)

**来源**: sheet5 R10 / `--scene` 走 trade-ideas/community(允许タメ口)

```
【是銀が斬るシリーズ1回目】MoomooAPI Skillsを試しに使ってみたぞ
TSLAのバックテストやってみたので手順まとめます
米国株チャートの一目均衡表がアプリ内で確認できてターゲットバイイングが出来るのはmoomooだけ!?
決算プレーの勝率アップ!私が手放せない「機関投資家の持株比率」活用術
```

### P-8 小号评论(口语)

**来源**: sheet5 R11 / `--scene community`(タメ口允许、【投稿例】区段)

```
24時間監視してくれるのはいいけど、急落したときの損切り設定とかも細かくできるんですかね。使ってる方いたら教えてほしい。

Claudeコードの実行中画面をコピペでウェブのClaudeの方で聞きながら実装しました。たしかに導入とかは日本語チャットで出来るのはすごいですね、プログラム知識もいらないんですが、まだPCに慣れてないとハードル高いですね PG知識も合ったほうが有利な指示ができそうです。
```

### P-9 帮助中心标题列表

**来源**: sheet5 R14 / `--scene faq` 或 manual

```
アプリ機能
Moomoo APIについて
Moomoo API開発者ガイド
銘柄スクリーナー
銘柄モニターについて
```

### P-10 直播预告(日文)

**来源**: sheet5 R9 / `--scene release` 或 short

```
神藤将男の実践マーケット 今の相場を徹底解剖×チャートの極意
ここが凄いぞTradingView「鬼に金棒!ファンダメンタルズさえ、TradingViewで究めることが出来る!」<第4回>
決算狙いで朝起きたら急騰も!?ゼロから始める 米国オプション実践セミナー
```

---

## Tier 1: `compliance` — 合規服務类

### CP-1 禀议書 标题(内部审批)

**来源**: sheet2 R15 / @crystaldu

```
【稟議書】株式移管プログラム(2026/4〜)
```

### CP-2 NUP 禀议書 + T&C 大纲

**来源**: sheet2 R17 / @elliechen / `--scene disclosure` 或 terms
**RL-5 要求**: です/ます 禁止

```
【稟議書】2026/03 口座開設&入金プログラム(NUP)
项目背景+概要(三问、活动目标)+コンプライアンスリスク対応等+プログラム整理+T&C(キャンペーン内容(ランディングページT&Cに以下内容を掲載) 、景表法整理、想定景品総額、特典の上限管理方法、事前確認)
```

### CP-3 Disclaimer(SNS 内嵌)

**来源**: sheet2 R19 / `--scene disclaimer`(SNS 内 disclaimer 段)

```
※特典の銘柄(買付代金)は抽選により異なる
```

### CP-4 SNS 期間限定 + 特典条件

**来源**: sheet2 R12 / `--scene terms`(LP/SNS 底部条款段)

```
株式入庫で最大130万円相当が必ずもらえる!
最大2年間の米国株取引手数料無料 & 限定プレミアムサービス利用
期間: 2026/04/17(金)〜
```

---

## 测试矩阵建议

| 维度 | Tier 1 × Tier 2 组合数 | 已收样本数 | 覆盖率 |
|---|---|---|---|
| campaign | 6 scene × 4 channel | 5 (C-1〜5) | launch+referral 已覆盖,缺 remind/lastday/result/seasonal |
| trade-ideas | 6 scene | 5 (T-1〜5) | flash+picks+theme+wrap+community 已覆盖,缺 earnings/morning |
| news | 6 scene | 7 (N-1〜7) | flash+morning+wrap+earnings+digest+alert 已覆盖,缺 indicator |
| product | 7 scene | 10 (P-1〜10) | release+short+faq+community 已覆盖 |
| compliance | 5 scene | 4 (CP-1〜4) | disclosure+terms+disclaimer 已覆盖,缺 faq/guide |

**覆盖缺口**: campaign/remind, campaign/lastday, campaign/result, campaign/seasonal, trade-ideas/earnings(个股), trade-ideas/morning(原创非速报型), news/indicator(经济指标单独), compliance/faq, compliance/guide。后续可在 boost 完成后,用 boost 后 skill 自动生成这些缺失场景的样本作为「实验组」。

## 使用方式

1. 选取一条 control sample(如 C-2 Push)。
2. 走 boost **前** skill,用相同 `--style campaign --scene launch --segment never_traded`,记录输出 + 验证块结果。
3. 走 boost **后** skill,同参数,记录输出 + 验证块结果。
4. 对比:
  - RL-4 字数 pass / fail
  - 红线违反次数(尤其 RL-2、RL-11、RL-12)
  - AC-7 / AC-9 / AC-12 / AC-16 通过率
  - 与 moomoo 品牌 benchmark 的吻合度
5. 多条样本汇总,得 boost 净收益曲线。
