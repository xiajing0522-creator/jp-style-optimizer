---
id: ADR-006
title: TI-7 disclaimer threshold for trade-ideas content
date: 2026-04-30
status: accepted
deciders: jp-style-optimizer v6.0.0 redesign — Phase 1.8 synthesis (team abc2)
affects: references/trade-ideas-guide.md (TI-7), SKILL.md Step 5 verification (trade-ideas — theme/morning/community ≥500字), diagnosis/domain-research-trade-ideas.md (OQ-1)
references:
  - diagnosis/domain-research-trade-ideas.md — Sources 1, 2, 9, 10; Red Line Candidate RLC-6; Open Question OQ-1
  - 金融商品取引法 第37条（広告等の規制）
  - CFA Institute "Standards of Practice Handbook" 11th ed. — Standard V(B) Communication with Clients
---

# ADR-006: TI-7 Disclaimer Threshold for trade-ideas Content

## Context

TI-7 は trade-ideas 出力に**標準免責文言**（JSDA 雛形準拠の「本情報は投資助言を目的としたものではありません」等）を末尾に付記することを要求する制約である。`references/trade-ideas-guide.md` は現行「**500字超コンテンツ**に末尾免責文言必須」と規定し、SKILL.md Step 5 の「trade-ideas — theme/morning (≥500字)」で機械検証される。

### なぜ「閾値」が必要か

trade-ideas の配信単位は字数帯が大きく異なる：
- **flash / picks**: 80–200 字（Push 通知、アプリ内カード）
- **earnings**: 200–500 字（決算速報）
- **morning**: 300–800 字（朝刊ブリーフ）
- **theme**: 500–1500 字（テーマ分析）
- **community**: 400–800 字（コミュニティ投稿）

**免責文言（JSDA 雛形）の最短形は 60–80 字**。短尺 Push（20 + 60 字）に 60 字の免責を足すと、**本文が免責より短くなる**可能性がある。業界実務（Source 8: moomoo/楽天/みんかぶ 等）でも、Push や picks カードには定型免責が付かず、**アプリ共通 footer / 規約ページ**で包括的に担保するパターンが支配的。

一方、**長尺分析コンテンツ**（theme/morning の末尾）では、コンテンツ単体で受け手に届く際の「広告性」が強く、**個別コンテンツ内の免責が金商法第37条の形式要件として必要**。この境界線が閾値の本質である。

### なぜ「500」なのか — 候補値の比較

domain-research-trade-ideas.md の Source 1/2/10 および Open Question OQ-1 で検討した候補値：

| 候補閾値 | 意味 | Pros | Cons |
|---|---|---|---|
| **0 字（全件必須）** | 全 trade-ideas コンテンツに免責必須 | 法的に最大安全 | flash ≤140字 と picks ≤200字 が**文字数オーバー**で配信不能。業界実務と乖離 |
| **300 字** | earnings (200–500) の上位半分、morning と theme をカバー | earnings 長尺側にも免責 | earnings 短尺側（200 字台）が不安定。境界で**同一 scene 内で免責有無が割れる**ノイズ |
| **500 字** | theme / morning 長尺 / community 長尺をカバー | scene 単位できれいに分離（flash/picks/earnings 免除、theme/morning/community 必須）。JSDA 実務（長尺レポート免責必須）と整合 | earnings 最長（500字ちょうど）で境界ぶれ |
| **1000 字** | theme の中位以上のみ | theme 短尺も免除され免責範囲狭い | morning 全件が免除され法的リスク増 |
| **全件 Short-disclaimer** | 閾値なし、短尺は短免責（30 字程度）、長尺は長免責 | 法的安全 + 配信実務両立 | short-disclaimer の業界標準が未成熟、短免責の十分性に法的不確実性 |

**500 字が選ばれる理由**:
1. **Scene 単位でクリーン**: flash (≤140) / picks (≤200) / earnings (200–500) は全域で閾値未満、theme (500–1500) / morning (300–800 の長尺側) / community (400–800 の長尺側) は閾値以上に落ちる。scene 別に「免責あり/なし」が予測可能。
2. **JSDA 実務との整合**: 野村 Investment Monthly / SBI テーマレポート等のリテール向けセルサイド資料は 500〜1500 字レンジで末尾 JSDA 雛形免責を付す標準運用（Source 6）。500 字は**このレンジの下限**。
3. **「広告性」の境界として合理的**: 500 字は「本文主体で独立流通する分析コンテンツ」の下限。これ未満は「通知・速報」として扱い、プラットフォーム共通 footer に委譲するのが業界慣行（Source 8）。
4. **境界ぶれの実害が小さい**: earnings の 500字ちょうど境界は、scene 字数レンジ (200–500) の**上限ちょうど**に位置するため、レアケース。かつ earnings は決算ハイライトとして数値予想を含み、**境界超過時は免責が付く方向にぶれる**（安全側）。

## Decision

### TI-7 閾値を **500 字** に維持する。

**TI-7 完全形（v6.0.0）**:

> **TI-7 免責文言の必須付記**:
> - **500 字超**のコンテンツ（theme / morning 長尺 / community 長尺）には末尾に**標準免責文言**（JSDA 雛形準拠、80–200 字）を必須付記する。
> - **500 字以下** のコンテンツ（flash / picks / earnings / morning 短尺 / community 短尺）は、個別コンテンツ内の免責を**免除**する。ただし配信プラットフォーム側で**共通 footer / 規約ページ**に相当する包括的免責が存在することを前提とする（skill の責任範囲外 — 人間レビューで確認）。
> - **境界ルール**: コンテンツ字数が 500 字ちょうどの場合は「500 字以下」に含め、免責任意とする。字数計算は skill 出力の本文（メタデータ・免責文言自体を除く）を対象とする。

**Verification**:
- Step 5 で本文字数を計算し、≥501 字なら「免責文言: ✓ / ✗」を判定。
- theme scene は字数帯 500–1500 のため**事実上常に必須**、実装上「theme は無条件必須」として扱う。
- morning/community は字数依存、scene checkpoint で個別判定。

## Alternatives Considered

### 候補 A: 0 字（全件必須）
- **却下**: flash ≤140 字に 60 字以上の免責を足すと本文が免責より短くなり、Push 通知の情報価値が毀損される。業界実務（moomoo/楽天/みんかぶ の Push）と完全に乖離。

### 候補 B: 300 字
- **却下**: earnings (200–500 字) が境界で割れ、同一 scene 内で免責有無が確率的に決まるため出力の予測可能性が低下。さらに 300 字帯は速報性の高い**短尺分析**（朝の短評、決算ヘッドライン）が集中する帯で、免責で字数を圧迫する実務的問題がある。

### 候補 C: 1000 字
- **却下**: theme の短尺側（500–999 字）と morning 全域が免除され、法的リスクが増大する。金商法第37条が要求する「コンテンツ単位の広告性担保」の観点から、1000 字は**過度に寛容**。

### 候補 D: 全件 short-disclaimer（閾値なし）
- **却下（ただし将来再評価）**: 短免責（30–40 字、例: 「投資判断はご自身の責任でお願いします」）は JSDA 雛形にも業界実務にも**確立された標準形が未成熟**。skill が独自に生成すると法的十分性が不明確。v6.0.0 では**閾値 500** を採用し、将来 JSDA 側で short-form disclaimer の標準化が進んだ段階で ADR-xxx として再検討する。

### 候補 E: scene 別固定（scene-driven）
- **準採用**: TI-7 の運用上、実質的にこれと同等。theme は常に必須、flash/picks/earnings は常に免除、morning/community は字数依存。ただし ADR としては**閾値 500 字ベース**を採用し、scene 別の振る舞いは TI-7 の適用結果として導出される位置づけとする（RL と scene 仕様の重複記述を回避）。

## Consequences

### Positive

1. **Scene 単位の予測可能性**: flash / picks / earnings は免責不要、theme は常に必要、morning / community は字数で決まる。ユーザー・運用者とも挙動を予測できる。
2. **JSDA 実務との整合**: 野村/大和/SBI のリテール向けレポート（500–1500 字）が末尾 JSDA 雛形免責を付す運用と一致。skill 出力をそのままリテール配信フローに流せる。
3. **Push/SNS 実装と両立**: flash ≤140 字が免責で圧迫されず、業界 Push 配信と互換。
4. **法的安全性の確保**: 長尺コンテンツ（theme/morning/community）には必ず免責が付き、金商法第37条の形式要件を自動担保。
5. **CFA V(B) 整合**: 意見と事実を峻別し、forward-looking に不確実性を開示する原則は免責文言の中で明示される。

### Negative

1. **500 字境界のぶれ（earnings 最長域）**: earnings scene の字数レンジ上限（500 字）で境界が一致。境界超過時の挙動は「免責が付く」方向に振れる（=安全側）ため実害は小さいが、**earnings の免責有無がユーザー目線で「ブレる」**可能性がある。→ 緩和策: SKILL.md の earnings scene 仕様に「500 字を超える場合は免責付加」と明記する。
2. **短尺の法的安全は「プラットフォーム前提」に依存**: flash/picks/earnings では個別免責が付かないため、**配信プラットフォーム側の共通 footer / 規約** に包括的免責があることを前提とする。skill は**この前提の検証責任を負わない** — 人間レビューで確認する必要がある。SKILL.md の README で明記すべき。
3. **community の長尺側のみ免責必須**: 400–800 字レンジなので、境界 (500) を跨ぐ。運用で「community 短尺は免責なし、長尺は免責あり」の使い分けが生じる。
4. **将来変更のリスク**: JSDA が「投資情報資料には字数に関わらず免責表示を付すこと」の解釈強化を出した場合、閾値撤廃（候補 A）への移行が必要。→ 緩和策: 免責テンプレを skill 内で parameterize し、将来の全件適用に備える。

### Scene-by-Scene Impact

| Scene | 字数レンジ | TI-7 適用 | 理由 |
|---|---|---|---|
| **flash** | ≤140 | 免除 | プラットフォーム Push footer が担保 |
| **picks** | 80–200/銘柄 | 免除 | アプリ内カード UI、共通 footer が担保 |
| **earnings** | 200–500 | 免除（境界 500 で要付加） | 速報性優先、境界超過時は安全側に倒す |
| **morning** | 300–800 | 字数依存（≥501 で必須） | 短尺版は免除、長尺版は必須 |
| **theme** | 500–1500 | **常に必須** | レンジ下限が閾値と一致、事実上全件 |
| **community** | 400–800 | 字数依存（≥501 で必須） | 短尺版は免除、長尺版は必須 |

## References

- **Internal**:
  - `diagnosis/domain-research-trade-ideas.md` — Sources 1 (金商法), 2 (JSDA), 9 (CFA), 10 (Reg FD / EDINET)
  - `diagnosis/domain-research-trade-ideas.md` — Red Line Candidate **RLC-6** (TI-7 閾値再設計)
  - `diagnosis/domain-research-trade-ideas.md` — Open Question **OQ-1** (TI-7 500字 vs 数値予想含む短文にも短免責)
  - `references/trade-ideas-guide.md` — TI-7 現行規定
  - `docs/adr/ADR-003-trade-ideas-dual-register.md` — 関連 RL-11 例外
- **External**:
  - **金融商品取引法 第37条**（広告等の規制）https://www.fsa.go.jp/common/law/kinshouhou/ — コンテンツ単位の広告性担保義務
  - **日本証券業協会「広告等の表示及び景品類の提供に関する規則」+「会員における投資情報の提供等に関する指針」** https://www.jsda.or.jp/about/kisoku/ — 免責雛形の業界標準
  - **CFA Institute "Standards of Practice Handbook" 11th ed. — Standard V(B) Communication with Clients** https://www.cfainstitute.org/en/ethics-standards/codes/standards-of-practice-handbook — 事実と意見の峻別、不確実性開示義務
  - **SEC Rule 10b-5 / PSLRA 1995 forward-looking safe harbor** https://www.sec.gov/rules/final/33-7881.htm — forward-looking disclaimer の法的位置付け
