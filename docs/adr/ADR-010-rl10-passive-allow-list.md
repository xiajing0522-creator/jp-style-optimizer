---
id: ADR-010
title: RL-10 受け身連続スキャンに news / trade-ideas 限定の allow-list を導入
date: 2026-05-11
accepted_date: 2026-05-11
status: accepted
deciders: jp-style-optimizer v6.1.0 boost (team abc2 / Phase 2 prescription)
affects: SKILL.md (RL-10 文言), references/news-guide.md (NC-9), references/trade-ideas-guide.md (TI-9), Step 5 verification ロジック
related: OQ-TI-9, ADR-007-news-length-and-quote-exception
---

# ADR-010: RL-10 Passive Allow-List for news / trade-ideas

## Context

現 RL-10 は「同一文中の受け身 (〜される/〜られる) を 2 つ以上含む文」を一律違反とするスキャン規則である。これは campaign / product / compliance では妥当だが、**news と trade-ideas 分析セクション**では業界規範と衝突する。

`diagnosis/domain-research-news.md` および `domain-research-trade-ideas.md` の横断観測では、報道・市場分析の客観表現として以下の受け身が**語彙化された定型句**として支配的に使用される（実測 60-90% の wrap / earnings / theme 記事に少なくとも 1 つが含まれる）：

| 定型受け身 | 用途 | 業界実例 |
|---|---|---|
| 〜とみられる / 〜と見られる | 観測者中立の見立て | Reuters JP「〜利上げに踏み切るとみられる」 |
| 〜と発表された | 一次出典付きの発表事実 | 日経電子版「〜が発表された」 |
| 〜と報じられた | 二次伝聞 (出典タグ付き) | Bloomberg Japan「〜と報じられた」 |
| 〜と見込まれる / 〜と見込み | 数値推計の attribution | 株探「業績は前年比増となる見込み」 |
| 〜と指摘される | アナリスト見解の attribution | QUICK「〜と指摘される」 |
| 〜と位置付けられる | 構造的解説 | 東洋経済「〜と位置付けられる」 |

これら 6 語彙は CFA Standards V(B) の「fact / opinion separation + attribution」を日本語で実現する**事実上唯一の自然な構文**であり、能動形に書き換えると：

- 主語が消える（「市場は〜とみられる」→「市場は〜だ」では断定化、attribution 喪失）
- 主体を補うと事実の歪曲（「アナリストは〜と見る」では出典限定が必要、業界慣行と乖離）

OQ-TI-9 (`domain-research-trade-ideas.md` L615) はこの矛盾を提起し、(a) RL-10 全廃 / (b) allow-list 化 / (c) news/trade-ideas で RL-10 自体を不適用 の 3 案を保留した。

### 候補比較

| 案 | Pros | Cons |
|---|---|---|
| (a) RL-10 全廃 | 検証ロジック簡素 | campaign の冗長受け身連続「ご利用いただかれることが推奨されます」が再発、Pathos 主導文体の質低下 |
| (b) allow-list 化 (本 ADR) | 業界定型句のみ除外、過検出/過漏れの双方を抑制 | 6 語彙のメンテナンスコスト、辞書化が必要 |
| (c) news/trade-ideas で RL-10 不適用 | 実装単純 | 報道/分析でも非定型な受け身連続 (例:「〜が指示され、変更されることが想定される」) は質低下、検出すべき真の違反を逃す |

## Decision

**RL-10 受け身連続スキャンに 6 語彙の allow-list を導入し、news 全 scene + trade-ideas 分析セクション (デュアルレジスタ前半) のみに適用する**。campaign / product / compliance では allow-list を適用せず、現 RL-10 を維持する。

### Allow-list (固定 6 項目)

```
PASSIVE_ALLOW_LIST = [
  "とみられる", "と見られる",
  "と発表された",
  "と報じられた",
  "と見込まれる", "と見込み",
  "と指摘される",
  "と位置付けられる", "と位置づけられる"
]
```

表記揺れ (見られる/みられる/位置付け/位置づけ) は同一項目として扱う。実装上は正規化後マッチ。

### RL-10 改訂文言（追記のみ、既存文言は不変）

> **RL-10 No passive stacking** — No sentence with 2+ passive constructions (〜される/〜られる). Rewrite to reduce passive load.
> **Exception (news + trade-ideas analysis sections only)**: Passive forms in `PASSIVE_ALLOW_LIST` (とみられる / と発表された / と報じられた / と見込まれる / と指摘される / と位置付けられる) are excluded from the 2+受け身 count. Other passive constructions in the same sentence still count toward the limit. Allow-list does NOT apply to campaign / product / compliance.

### Verification 手続き変更（Step 5）

`news` または `trade-ideas` 分析セクションの場合：

1. 文単位で受け身候補をすべて検出 (〜される/〜られる/〜られた/〜された 全形)。
2. 検出された各候補が `PASSIVE_ALLOW_LIST` のいずれかと一致するかを照合。一致した候補は count から除外。
3. 残った受け身が 2 個以上の文を違反とする。
4. 状態申告:「受け身連続なし: ✓ (allow-list 適用)」または違反文を列挙。

trade-ideas 読者呼びかけセクション (デュアルレジスタ後半、です/ます体) には allow-list を適用しない (campaign 同等扱い)。これは読者向けの行動橋渡しでは定型受け身の出現頻度が低く、誤検出リスクより冗長性検出を優先する判断による。

### NC-9 / TI-9 への配置

- `references/news-guide.md` に **NC-9 (受け身 allow-list)** を新設し、本 ADR の allow-list を転記する。
- `references/trade-ideas-guide.md` に **TI-9 (受け身 allow-list、分析セクション限定)** を新設し、デュアルレジスタの section 境界判定ロジックと併記する。

## Alternatives Considered

### 候補 (a): RL-10 全廃
- **却下**: campaign 系で「〜いただかれる」「〜されることが推奨される」など意味の薄い受け身連続が再発する。`domain-research-campaign.md` Source 3 (LINE 公式アカウントガイド) で能動推奨が明示されており、業界規範に反する。

### 候補 (c): news/trade-ideas で RL-10 自体を不適用
- **却下**: news/trade-ideas でも非定型な受け身連続は質低下要因。例:「政府によって発表され、市場で受け止められた政策が…」の連続受け身は能動「政府が発表した政策を市場が受け止めた…」に書き換える方が読みやすい。allow-list 化は定型/非定型を分離できる。

### 候補 (b-1): Allow-list を 10 語彙以上に拡大 (〜される全般、〜と思われる、〜と推察される等)
- **却下**: 拡大すると campaign 流入時の境界が曖昧化。「〜と思われる」は modality marker でもあり、news の NC-3 (subjective expression) とも衝突。6 語彙は実測 95-pct カバーで安定境界。

### 候補 (b-2): Allow-list を scene 別に細分化 (flash 用 / wrap 用 / theme 用)
- **却下**: メンテナンスコスト過大。実測では 6 語彙の出現分布が scene 横断でほぼ均一 (各 scene で 4-5 語彙が出現)。scene 別管理の便益なし。

## Consequences

### Positive

1. **業界定型句との整合**: news/trade-ideas で attribution-bearing passives が natural register として扱える。CFA V(B) "fact/opinion separation" を日本語で表現する標準構文を skill が阻害しなくなる。
2. **誤検出削減**: ADR-007 採用後の wrap/digest 拡張字数 (700/1200) で受け身定型句の出現頻度が増えるため、本 ADR なしでは false positive が比例増加する。allow-list 導入で抑制。
3. **campaign 規範を保持**: campaign / product / compliance では現 RL-10 が無傷。冗長受け身連続の検出能力は維持。
4. **段階的拡張余地**: 将来 trade-ideas/community に投稿例の口語受け身が混入した場合、allow-list を section context 付きで拡張可能 (本 ADR では未着手)。

### Negative

1. **Allow-list 辞書のメンテナンスコスト**: 6 語彙は固定だが、業界用語の変遷で追加が必要になった場合は ADR 追補で対応。次回 boost (v6.2+) で実測を再確認する。 → 緩和策: ADR-010 References に「業界実例」リンクを残し、根拠を追跡可能にする。
2. **Section 境界判定の実装複雑化 (trade-ideas)**: デュアルレジスタの分析/読者呼びかけ境界を allow-list 適用範囲として識別する必要。 → 緩和策: 既に RL-11 (a) でも section 境界を判定しており、同じロジックを再利用可能。
3. **表記揺れ正規化の責務**: 「見られる/みられる」「位置付け/位置づけ」を同一視する正規化が verification 実装側に必要。 → 緩和策: 6 語彙それぞれの表記揺れを ADR で明示 (上記 PASSIVE_ALLOW_LIST 配列に列挙済み)。

### Scene-by-Scene Impact

| Style / Scene | RL-10 適用 | Allow-list 適用 | 備考 |
|---|---|---|---|
| news/全 scene | ✓ | ✓ | wrap/earnings/digest で「とみられる」「と発表された」が自然頻出 |
| trade-ideas 分析セクション | ✓ | ✓ | theme/morning/earnings の analysis で attribution-bearing passive 多用 |
| trade-ideas 読者呼びかけセクション | ✓ | ✗ | です/ます体、CTA 文脈は能動推奨 |
| trade-ideas/community 投稿例 | ✗ (RL-11(b) 適用) | — | 口語/タメ口扱い |
| campaign 全 scene | ✓ | ✗ | 現 RL-10 維持 |
| product 全 scene | ✓ | ✗ | 現 RL-10 維持 |
| compliance 全 scene | ✓ | ✗ | 現 RL-10 維持 |

### テスト・互換性

- 新規追加: `build/tests/passive-allow-list-*.snapshot.md` を news 3 件 + trade-ideas 分析 3 件 + campaign 1 件 (誤検出回避確認) の計 7 件想定。
- 既存 news/trade-ideas snapshot で受け身定型句を含むものは pass 判定が変わる可能性あり (false positive → pass)。再生成不要、AC 合致のみ確認。
- AC への追加候補: AC-19「news 受け身 allow-list 対象は count から除外、非定型受け身 2 個以上は引き続き flag」(Phase 3 判断、Phase 1.8 synthesis では未含)。

### 既存制約との関係

- **NC-3 (news subjective expression)**: 「〜と思われる」は subjective expression として NC-3 で禁止のため、本 allow-list には**含めない**。NC-3 と RL-10 allow-list は直交。
- **NC-7 (news register purity)** と ADR-007 引用体例外: 「」内の受け身は地の文ではないため、RL-10 スキャン時に既に除外される (ADR-007 §2.2 verification 規則)。本 ADR は地の文の受け身に限定して適用。
- **TI-2 dual-register**: 分析セクション = だ/である体 = allow-list 適用、読者呼びかけセクション = です/ます体 = allow-list 不適用。section 境界は ADR-003 で確立済みの判定ロジックを使用。
- **ADR-008 institutional segment**: institutional segment 指定時は trade-ideas 全文がだ/である単一になるが、本 allow-list は分析セクションと同等に全文へ適用される (institutional の register 性質が分析セクションに最も近いため)。

## References

### Internal
- `diagnosis/domain-research-news.md` — Source 1 (共同通信)、Source 4 (Reuters JP)、Source 5 (Bloomberg Japan)、Source 7 (QUICK) — 受け身定型句の業界使用実例
- `diagnosis/domain-research-trade-ideas.md` — Source 9 (CFA V(B))、Source 5 (野村・大和)、Open Question OQ-TI-9
- `docs/adr/ADR-007-news-length-and-quote-exception.md` — 引用体例外と本 ADR の協調関係
- `docs/adr/ADR-003-trade-ideas-dual-register.md` — section 境界判定ロジック
- `docs/adr/ADR-008-trade-ideas-institutional-segment.md` — institutional segment 適用範囲との関係
- `references/news-guide.md` — NC-9 追加対象 (Phase 3)
- `references/trade-ideas-guide.md` — TI-9 追加対象 (Phase 3)

### External
- **CFA Institute "Standards of Practice Handbook" 11th ed. — Standard V(B)** — fact/opinion separation, attribution requirement
- **共同通信社『記者ハンドブック』第 13 版** §受け身・客観表現 — 報道での attribution-bearing passive 使用規範
- **Reuters Handbook of Journalism** §Attribution — "appears to / is seen as / is expected to" 構文の日本語定型対応
- **日本経済新聞社『日経スタイルブック』** §文末・客観表現 — wrap/earnings での「とみられる」「と発表された」標準頻度
