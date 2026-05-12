---
id: ADR-007
title: news 字数上限の緩和（wrap 700字／digest 1200字）＋ NC-7 引用体内部レジスタ例外の明示
date: 2026-04-30
accepted_date: 2026-05-11
status: accepted
deciders: jp-style-optimizer v6.0.0 redesign (team abc2 / Phase 1.8 synthesis) → v6.1.0 boost で正式採決
affects: references/news-guide.md, diagnosis/synthesis.md
related: ADR-002-news-report-split, ADR-003-trade-ideas-dual-register
---

# ADR-007: news 字数上限の緩和 + NC-7 引用体内部レジスタ例外の明示

本 ADR は 2 つの密接に関連する微修正を 1 件で扱う。両者ともに `references/news-guide.md` の既存制約の**精密化**であり、T1 / T2 設計そのものを変更しない。

- **(a) 字数緩和**：`news/wrap` の上限を 600 → 700字、`news/digest` の上限を 1000 → 1200字
- **(b) NC-7 注記**：直接引用「」内で被引話者の原発話文体を保持することを register 純度の例外として明示

---

## 1. Context

### 1.1 背景

`diagnosis/domain-research-news.md`（Task #2 / #6 成果）で、10 独立ソース（共同通信『記者ハンドブック』、日経スタイルブック、時事通信配信規範、Reuters JP、Bloomberg Japan、QUICK、株探、MINKABU PRESS、東洋経済、Yahoo!ファイナンス）を横断する業界規範研究を実施した。その結果、`news-guide.md` の 85% は業界規範と整合するが、2 点で**実務との軽微な乖離**が確認された。

### 1.2 (a) 字数に関する業界実測と現 guide の乖離

| Scene | 現 news-guide 規定 | 業界実測レンジ | 業界実測中央値 | 乖離 |
|---|---|---|---|---|
| `news/flash` | ≤140字 | 60–180字 | 110字 | ✓ 整合（上限に収束） |
| `news/wrap` | **300–600字** | **350–900字** | 550字 | △ 上限が業界実測の 1σ 帯より短い（業界の 70 パーセンタイル以上が 600字超） |
| `news/earnings` | 150–400字 | 180–500字 | 300字 | ✓ 整合 |
| `news/indicator` | 100–300字 | 120–350字 | 200字 | ✓ 整合 |
| `news/digest` | **500–1000字** | **600–1500字** | 850字 | △ 上限が業界実測の 1σ 帯より短い（東洋経済系・日経電子版特集ダイジェスト等が 1000-1200 字に分布） |
| `news/alert` | ≤100字 | 40–120字 | 70字 | ✓ 整合 |

`flash / earnings / indicator / alert` 4 scene は整合、**`wrap` と `digest` の 2 scene のみ上限が短い**。日経夕刊「マーケット」、東洋経済オンライン「マーケット・トピックス」、Reuters JP 「市場概況」が 600-900字（wrap）/ 1000-1500字（digest）で日常配信されているのに対し、現 guide は 600字 / 1000字 で打ち切りを要求してしまう。

### 1.3 (b) NC-7 の絶対性と実務の乖離

現 `references/news-guide.md` §T1:

> **NC-7 レジスタ純度** — だ/である体以外の文末禁止。RL-11 news 適用。「文末: だ/である ✓」
> **Register** — だ/である体統一。**例外なし**。

しかし共同通信『記者ハンドブック』第 13 版 "文末統一" 節・日経スタイルブック "引用体" 節・Reuters Handbook of Journalism "direct quotation" 節のいずれも、**直接引用「」内では被引話者の原発話文体を保持する**ことを前提としている。典型例：

```
〇〇社長は「今後も積極的に投資を続けていきます」と述べた。
（本文：常体／引用内：敬体 — 業界慣行では問題なし）

財務相は「デフレ脱却は既に達成されたと考えている」と発言した。
（本文：常体／引用内：敬体 — 業界慣行では問題なし）
```

現 guide の「例外なし」表現を機械的に適用すると、`news/earnings`（会社コメント必須）、`news/wrap`（当局者コメント挿入）、`news/digest`（インタビュー引用）で**業界慣行の直接引用を誤って register 違反扱い**する false positive が発生する。

### 1.4 なぜ今この ADR か

v6.0.0 boost では domain-research の synthesis を元に `references/news-guide.md` を更新する。両修正は：
- **(a)** は実測業界上限への定量的調整（20pt 規模）
- **(b)** は既存制約の例外条項追加（1 文）

いずれも constraint の廃止・新設ではなく精密化で、段階的 rollout（v6.0.0 で同時採用）が可能。

---

## 2. Decision

### 2.1 (a) 字数上限の緩和

| Scene | 現上限 | 新上限 | 根拠 |
|---|---|---|---|
| `news/wrap` | 600字 | **700字** | 業界実測の 60 パーセンタイル境界。日経市況「今日の東京株式市場」平均 580字、Reuters JP「市況」平均 620字、Bloomberg Japan 同 680字。700字で実測 90% をカバー |
| `news/digest` | 1000字 | **1200字** | 業界実測の 70 パーセンタイル境界。東洋経済オンライン「市場トピックス」平均 1050字、日経電子版「ウィークリーダイジェスト」平均 1150字。1200字で実測 85% をカバー |

下限値・他 scene の字数は**変更なし**。上限を超えた場合のルーティング：
- `wrap` が 700 字を超える → `digest` へ自動ルーティング提案
- `digest` が 1200 字を超える → 分析比率 ≤30% なら `news` 維持しつつ分割推奨、30% 超なら `trade-ideas/theme` に再ルーティング

### 2.2 (b) NC-7 引用体内部レジスタ例外の明示

`references/news-guide.md` の NC-7 を下記のとおり改訂する（追記のみ、既存文言は不変）：

#### 改訂後 NC-7

> **NC-7 レジスタ純度**
> だ/である体以外の文末禁止。RL-11 news 適用。同一記事内で常体／敬体の混在は原則不可。
>
> **例外**：直接引用「」内では被引話者の原発話文体を保持する。共同通信『記者ハンドブック』第 13 版 "文末統一" 節の業界慣行に従う。地の文（ナラタティブ）は依然としてだ/である体を維持しなければならない。
>
> | Context | Register 要求 |
> |---|---|
> | 地の文（本文・見出し・要約） | だ/である体、例外なし |
> | 直接引用「」内（発話引用） | 原発話を保持（です／ます／口語いずれも可） |
> | 間接引用（「〜と述べた」「〜と発表した」） | 地の文扱い — だ/である体 |
> | 注・補足括弧（）内 | 地の文扱い — だ/である体 |

#### 検証・verification 手続き

- `verify` 関数：地の文の文末スキャン時、「」内は検出対象外とする。
- `verify` 関数：間接引用タグ（と述べた／と発表した／との見方）で終わる文は地の文扱いで常体をチェック。
- false positive 防止：引用符が閉じていない（typo）で検出漏れしないよう、「」ペアリングチェックを前置。

---

## 3. Alternatives

### 3.1 (a) 字数緩和の代替案

| 案 | 内容 | 採否 | 理由 |
|---|---|---|---|
| **A-0 現状維持**（wrap 600 / digest 1000） | 20pt 乖離を許容 | ✗ | 業界実測の 70-90% 帯を不当に切断し、正規の業界記事を違反判定する false positive が恒常化 |
| **A-1 本 ADR 推奨**（wrap 700 / digest 1200） | 業界 60-70 パーセンタイルまでカバー | ✓ | false positive 大幅削減、true positive（trade-ideas への越境）判定は維持 |
| A-1b wrap **800** 案 | wrap 上限を 800 字に（実測 80 パーセンタイル） | ✗ | 日経夕刊「マーケット」平均 580字、Reuters JP「市況」平均 620字、Bloomberg Japan 680字 と比べて 800 は上に振れすぎ。800 字に達した記事は業界では既に digest カテゴリへ移動しており、wrap の Ethos（簡潔な市況要約）を保てない。700 は 90% カバー、800 は 96% カバーで差分 6pt に対し境界曖昧化リスクが見合わない |
| A-2 アグレッシブ緩和（wrap 900 / digest **1500**） | 業界実測最大値までカバー | ✗ | digest 1500 字は東洋経済系の "analytic news" 帯（ADR-002 の境界記述どおり trade-ideas/theme に属すべきレンジ）。digest 上限 1500 にすると分析比率 ≤30% のみが唯一の境界 gate となり、routing 誤判定のリスクが増大。1200 は業界中央値 +1σ に相当し safety buffer を残す |
| A-3 下限のみ調整（wrap 200-700 / digest 400-1200） | 短文 flash との境界弱化 | ✗ | flash (≤140) と wrap の境界が曖昧化。scene routing の推論精度が低下 |
| A-4 Scene 細分化（wrap を wrap_short / wrap_long に分離） | 2 つの新 scene を追加 | ✗ | v6.0.0 の「Tier 2 を 6 scene に維持」方針と矛盾。複雑度 vs 価値が見合わない |

### 3.2 (b) NC-7 例外の代替案

| 案 | 内容 | 採否 | 理由 |
|---|---|---|---|
| **B-0 現状維持**（例外なし） | 「例外なし」を厳守し、引用内も常体化を要求 | ✗ | 業界慣行を違反し、発話の**原音再現性**を破壊する。news の Logos 原則自体と矛盾（改変は事実の歪曲に等しい） |
| **B-1 本 ADR 推奨**（**引用符「」単位**の例外、間接引用と注釈は地の文扱い） | 粒度：引用符。業界規範と完全整合、verification 境界明確 | ✓ | 業界慣行とも乖離せず、機械的検証が可能。引用符は文字レベルで境界を引ける |
| B-1b **段落粒度**の例外（引用を含む段落全体を例外ゾーン扱い） | 粒度：段落。「引用含む段落」を register 検証から外す | ✗ | 段落内の地の文部分（「〇〇社長は〜と述べた」の「と述べた」地の文タグ）も検証外となり、間接引用タグが register 検証を逃れる **false negative** が発生。共同通信『記者ハンドブック』第 13 版 §引用規範も「」単位で境界を引いている |
| B-2 全面的な register 自由化 | 「」内外とも話者判定で自動切替 | ✗ | NC-7 の存在意義を破壊。地の文の register 混在は業界規範上 disqualifying |
| B-3 引用＋コラム両例外化 | 直接引用＋コラム・解説も例外 | ✗ | コラム・解説は `news` ではなく `trade-ideas` に属する。news T1 の scope 外で対応すべき |
| B-4 NC-8（新規）として独立制約化 | NC-7 を触らず新制約 NC-8 で定義 | ✗ | 既存 NC 体系との重複。NC-7 の「例外」として注記する方が体系的に整合 |

---

## 4. Consequences

### 4.1 (a) 字数緩和の影響

**Positive:**
- **業界実測の 90%（wrap）／ 85%（digest）をカバー** — false positive（正当な記事を違反扱い）を大幅削減
- 日経夕刊、Reuters JP 市況、東洋経済オンライン マーケット・トピックスなどの代表的配信を natural register として扱える
- `news/wrap → digest → trade-ideas/theme` の段階的再ルーティング境界が実務と整合

**Negative:**
- 既存テストスナップショット（`build/tests/news-wrap-*.snapshot.md`、`news-digest-*.snapshot.md`）のうち、600字・1000字近辺を基準に作成されたものは再生成が必要（推定 6-10 snapshot）
- `news` と `trade-ideas/theme` の上限帯が重なる領域が拡大（800-1200字）。routing 時は**分析比率 ≤30% の gate** が決定打となる。Craft 層強化（ADR-007 採用後の NC-8 新設と併用）で補う必要あり

**中立（Neutral）:**
- 下限値は変更なし。flash / earnings / indicator / alert の 4 scene は一切影響を受けない
- `news/wrap` の業界慣行の 3 指標セット（日経平均＋TOPIX＋為替）は 500-700字で自然収束するため、上限 700 字が制約として過剰に働くケースは稀

### 4.2 (b) NC-7 例外の影響

**Positive:**
- **業界慣行との 100% 整合** — `news/earnings`（会社コメント）、`news/wrap`（当局者発言）、`news/digest`（複数インタビュー引用）における誤判定を解消
- 発話の**原音再現性**を守り、news の Logos 原則（事実・原音・出典）と強く整合
- Reuters・Bloomberg の attribution rules（"quote the speaker's words exactly"）と整合

**Negative:**
- verification 実装が若干複雑化：「」ペアリング解析＋間接引用タグ検出の 2 段階が必要
- false negative リスク：引用符 typo（「だけ or 」だけ）で「引用ゾーン」が誤判定される可能性。対策として ペアリングチェックを前置

**中立（Neutral）:**
- RL-11（register 混在禁止）の news 適用は依然として有効。引用内は「常体→敬体」ではなく「原音保持」という別次元の扱い
- `trade-ideas` の section-level dual-register（ADR-003）とは**適用範囲が異なる**：trade-ideas は章単位で切替、news は引用符内のみ。混同しないよう `docs/adr/ADR-003` と相互参照を追加する

### 4.3 テスト・互換性

**必要な更新（v6.0.0 boost）:**
- `references/news-guide.md` — NC-7 注記追加、wrap 字数 600→700、digest 字数 1000→1200
- **RL-4 硬上限表**（SKILL.md 内の `Hard Length Cap` テーブル）— wrap / digest 行を同期更新。RL-4 は全 style 共通の "char-level hard cap" を定義しているため、news の緩和が SKILL 本体にも反映されなければ routing と enforcement が齟齬を起こす
- **AC-4（Acceptance Criterion #4、字数適合）への影響** — AC-4 は scene 別字数レンジ内であれば PASS 判定する。wrap 上限 700 / digest 上限 1200 に同期すれば、現行 false positive が FAIL としてカウントされていた 600-700（wrap）/ 1000-1200（digest）帯の正当な記事が本来の PASS 判定に戻る。つまり AC-4 の recall は向上、precision は不変
- `diagnosis/behavioral-eval-suite.md` — wrap / digest のサンプル期待値に引用体入りケースを追加
- `diagnosis/constraint-enforcement-audit.md` — NC-7 audit に「引用ゾーン除外」手順を追記
- `build/verify/` 内のスキャナロジック — 「」ペアリング前処理を追加

**互換性:**
- 既存の 400-600字 wrap テストは全て通過（上限緩和は下限・中央値に影響しない）
- 既存の 500-1000字 digest テストは全て通過（同上）
- NC-7 の引用体例外は「より寛容になる」方向の変更で、既存の合格サンプルは全て引き続き合格

### 4.4 将来への波及（本 ADR では未決定、留待後続）

NC-7 の引用体例外を `trade-ideas` T1 にも準用するかは**本 ADR の範囲外**。特に：

- **`trade-ideas/earnings`（決算ハイライト）** — 会社コメント引用が多いため NC-7 相当の例外が必要になる可能性大
- **`trade-ideas/morning`（朝の市場ブリーフ）** — 当局者・アナリスト発言引用を含むため同上
- **`trade-ideas/theme`（テーマ分析）** — 機関投資家コメント引用で同上

ただし `trade-ideas` は既に ADR-003 で **section-level dual-register** が認められており、register 混在の粒度が異なる。`trade-ideas` の "分析セクション:だ/である + 読者セクション:です/ます" と "引用符内:原音保持" の二層例外をどう整合させるかは、**別 ADR で扱うべき設計判断**。本 ADR は news の範囲で完結させる。

関連 open question は `diagnosis/domain-research-news.md` §Open Questions #4 に記録済み。

---

## 5. References

### 5.1 一次規範（業界編集規範）

1. **共同通信社『記者ハンドブック — 新聞用字用語集』第 13 版**（2020）ISBN 978-4-7641-0734-1
   - "文末統一" 節：常体／敬体の混在は原則不可、ただし直接引用「」内は話者の発話を保持
   - "引用と要約" 節：直接引用は「発話の正確な再現」、間接引用は地の文扱いで常体に統一
   - https://www.kyodo.co.jp/kikaku/handbook/

2. **日本経済新聞社『日経スタイルブック』／『日経の使い方』**
   - "市況記事" 項：wrap 標準は 3 指標サマリー + 個別イベント + 明日の注目点（500-700字が標準帯）
   - "決算速報" 項：実績・会社予想・前年同期比の 3 値必須、会社コメントは「」で原音再現
   - https://www.nikkei.com/ 編集綱領

3. **時事通信社『最新用字用語ブック』／フラッシュ配信原稿規範**（2019 改訂）
   - 4 段階配信（フラッシュ ≤50字 → 第1報 80-140字 → 補完 200-400字 → 詳報 400-600字）
   - https://www.jiji.com/ 配信サービスガイド

4. **Thomson Reuters『ロイター・ジャパン スタイルガイド』** / Reuters Handbook of Journalism
   - "Direct quotation" 項：被引話者の発話は改変せず「」で保持
   - "Attribution" 項：間接引用は "said" 相当の地の文タグで統一
   - https://handbook.reuters.com/

5. **Bloomberg News "The Bloomberg Way"**
   - "Quotes" 項：発話は正確に再現、地の文と引用は物理的に区別
   - "Body structure" 項：body 字数は 300-1200字の幅で scene 依存（breaking / wrap / in-depth）
   - https://www.bloomberg.com/company/stories/

### 5.2 業界実測データ（domain-research-news.md Finding 3）

- QUICK ファクトブリーフ：flash 中央値 110字、alert 中央値 70字
- 日経電子版「市況」／Reuters JP「市場概況」／Bloomberg Japan「市況」：wrap 平均 550-680字、最大 900字
- 東洋経済オンライン「マーケット・トピックス」／日経電子版「ウィークリーダイジェスト」：digest 平均 850-1150字、最大 1500字
- 株探 決算速報：earnings 平均 300字、最大 500字

### 5.3 既存 ADR との関係

- **ADR-002 news / report split** — 本 ADR の前提。news T1 の確立により wrap / digest の境界を扱える
- **ADR-003 trade-ideas dual-register** — 混同注意。trade-ideas は「章レベルの register 切替」、news NC-7 例外は「引用符内のみ」。両者は独立した適用範囲
- **ADR-004 compliance merger** — 影響なし

### 5.4 関連内部ドキュメント

- `diagnosis/domain-research-news.md` — 本 ADR の根拠研究（Finding 3、Cross-Reference 表、Synthesis Q3）
- `diagnosis/synthesis.md` — Phase 1.8 で両修正を反映予定
- `references/news-guide.md` — 本 ADR 採用後に改訂対象
