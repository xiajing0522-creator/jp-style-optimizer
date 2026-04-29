# Step 1: Concrete Examples

## Example 1 — Casual description → report 体

**Input**: 「この文章をレポート風に直して：現在の株式市場は上昇傾向にあり、多くの投資家が利益を得ています。」
**Ideal output**: 株式市場は上昇基調にあると見られ、多くの投資家が利益を享受していると考えられる。
**Failure case**: 「投資家が儲かっています」（術語「投資家」を口語化）／「利益を得ていると思います」（主観表現が残留）

## Example 2 — Formal instruction → sns 体

**Input**: 「このLP文をSNS向けに短くして：口座開設をご希望のお客様は、所定の書類をご準備いただき、当社窓口にてお手続きください。」
**Ideal output**: 口座開設はカンタン3ステップ✨ 書類1枚で今すぐOK！詳しくはこちら▶
**Failure case**: 140字超 ／ 敬語ブロックがそのまま残る ／ CTAなし

## Example 3 — 口語 → formal 体

**Input**: 「formal風に直して：配当金がもらえてお得です」
**Ideal output**: 配当金収入を受領することが可能であり、投資効率の向上に資する。
**Failure case**: 「配当金がもらえてお得です。」（未変換）／「配当金を受け取れてお得です」（です混在）

## Example 4 — Failure: 術語保護なし（悪い出力の例）

**Input**: 「当期純利益が増加しました」を sns 体に変換
**Bad output**: 「もうかりました！」（「当期純利益」が消失 → 術語保護違反）
**Correct output**: 当期純利益が増加📈 詳細はこちら▶

## Example 5 — Style ambiguous → inference

**Input**: 「これを営業向けに使いたいんだけど：ROEが改善されました」
**Trigger inference**: 「営業向け」 → marketing 体
**Ideal output**: ROEが改善！収益力が着実にアップしています✨
**Failure case**: formal体のまま出力 ／ 「ROE」を「株主資本利益率」に変換（術語変更違反）

---

## Trigger Phrases

- 「〜をreport風に直して」「研報体にして」「レポート調に変換」
- 「〜をSNS向けに」「Twitter用に短く」「LINE配信に使いたい」
- 「formal風に」「正式な文体に」「書き言葉に直して」
- 「営業文案に」「marketing風に」「口語化して」
- 「文体を変えて」「〜のスタイルに直して」「润色して」（中文trigger）
