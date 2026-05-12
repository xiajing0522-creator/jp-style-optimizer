---
id: ADR-005
title: campaign does NOT adopt dual-register
date: 2026-04-30
status: accepted
deciders: jp-style-optimizer v6.0.0 redesign (team abc2)
affects: SKILL.md (RL-11 campaign branch), references/campaign-guide.md
related: ADR-003, OQ-CAMP-1, OQ-CAMP-2
---

# ADR-005: campaign Register Boundary — No Dual-Register Exception

## Context

ADR-003 が `trade-ideas` に RL-11 section-level dual-register 例外（分析=だ/である、読者呼びかけ=です/ます）を入れたのを受け、同等例外を `campaign` にも導入すべきか（例「特典説明は だ/である、CTA は です/ます」）が v6.0.0 redesign で提起された。電通・博報堂 経由のブランディング短文（SMBC「いいかもしれない。」等）が 体言止め／だ 終止を多用し表層で dual-register に見えるため、現実味のある論点。本 ADR はこの疑問を一回で決着させる。

## Decision

**`campaign` は dual-register 例外を採用しない**。全 6 シーン（launch/remind/lastday/result/seasonal/referral）で **です/ます 単一レジスタ**を維持。体言止め（Push/Banner/SNS 見出し）は **省略**扱いでレジスタ切替に非該当。modality marker（〜と見られる等）は引き続き禁止。状態申告：`文体統一: ✓ / 体言止め=省略扱い ✓`。

## Alternatives Considered

- **(a) 完整 dual-register（trade-ideas 式を横展開）** — 棄却。campaign は Pathos 主導で分析セクションが本質的に存在せず、ADR-003 の根拠（分析+行動の二段構造）が適用できない。
- **(b) `seasonal` シーン限定で例外化** — 棄却。市場文脈は導入 ≤20% が既定で独立ブロックを支えられず、1 シーン例外化は CA-6 lifecycle 一貫性（4 フェーズ同一レジスタ前提）を seasonal 跨ぎで破綻させる。
- **(c) `branding-campaign` 新シーン専用例外（OQ-CAMP-2 連動）** — 棄却（射程外）。情緒駆動ブランディングの routing は OQ-CAMP-2 で裁決中で、暫定は **marketing スタイルに分離**（OQ-CAMP-2 recommended interim と整合）。

## Consequences

- RL-11 campaign 分支が単純化（verification は単一レジスタ scan 1 pass、`デュアルレジスタ` 状態行は非出力）。
- CA-6 lifecycle 一貫性が成立し、4 フェーズ横断の表記統一 check が機械化可能。
- ADR-003 の射程が hard-bound され、news/product/compliance への波及も本 ADR を根拠に拒絶可能。
- **副作用**: 体言止め主体のブランディング短文を `--style campaign` で入力するとレジスタ違反が頻発。`campaign-guide.md` 冒頭に「dual-register 例外なし、branding 色強い入力は `--style marketing` 検討」を暫定追記。
- OQ-CAMP-1（年間複数キャンペーン連結）とは非干渉。跨 campaign でも単一レジスタ前提が維持されるため設計自由度を狭めない。
- SKILL.md line 92 は変更不要（(a) 例外が trade-ideas 限定である旨すでに明示）。

## References

- **domain-research-campaign.md** L42–L58（L1 楽天 / L2 SBI）: 大手証券 LP/EDM は一貫 です/ます、dual-register 実践なし → Decision 実証根拠。
- **domain-research-campaign.md** L60–L68（L3 moomoo）/ L119–L127（A1 電通）/ L592・L614（OQ-CAMP-1/-2 由来節、博報堂 視点）: 情緒訴求は体言止め/省略美であって だ/である 断定ではない → 体言止め=省略扱いの根拠 + Alternative (a) 棄却根拠。
- **ADR-003** *RL-11 exception for trade-ideas*: 本 ADR と対称。例外根拠（分析+行動二段構造）が campaign に存在しない旨の相互参照。
- **case-library.md** campaign/launch 楽天・SBI 事例、branding SMBC・大和 事例: 実運用文案レジスタが一貫 です/ます である裏付け + branding 事例を marketing 側に分類する根拠。
