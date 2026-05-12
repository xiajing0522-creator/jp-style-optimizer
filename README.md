# jp-style-optimizer

**日语金融文案风格优化器** — Claude Code 自定义技能 (Custom Skill)

对现有日语金融文本进行文体转换和风格润色。不翻译、不添加信息、不生成新论断。

> 当前版本: **v6.6.0** (2026-05-12)

> **平台 footer 前提 (ADR-006)**: trade-ideas 的短尺场景 (flash / picks / earnings / morning短尺 / community短尺) 不生成个别免责声明，前提是分发平台 (app push / 券商 dashboard / SNS feed) 已配置全局免责 footer。Skill 本身不验证该前提，由运营方负责保障平台级覆盖。长尺场景 (theme / morning长尺 ≥ 500字) 仍需内嵌免责文 (AC-10)。

---

## 功能概述

jp-style-optimizer 是一个运行在 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 上的自定义技能，专为日语金融文案的风格调整而设计。它能够：

- 在 **5 种文案风格类 (Tier 1)** × **29 种应用场景 (Tier 2)** 之间进行文体转换
- 自动锁定金融术语，确保转换过程中专业词汇零变形
- 内置 **12 条红线 (Red Lines)** + **16 条验收标准 (Acceptance Criteria)**，防止信息注入、文体混杂、字数超限等问题
- 支持品牌特定语音匹配（野村证券、乐天证券、SBI证券、moomoo证券）；moomoo 已扩展为渠道级路由表 (ADR-011)
- 支持 **6 种用户分群策略**，根据用户画像调整文案角度和 CTA 温度
- 每次输出包含完整的验证块，逐项确认约束合规

---

## 风格路由

两参数路由：`--style` 决定 Tier 1 语体；`--scene` 决定 Tier 2 结构模板和句长目标。

### Tier 1 — 文案风格类 (`--style`)

| `--style` | 文案风格类 | 主导证明 | 共通语体约束 |
|-----------|----------|---------|------------|
| `campaign` | 营销活动类 | Pathos | です/ます体; CTA 必须 (Hot/Warm/Cold 阶段); 期限明示必须 |
| `trade-ideas` | 赚效内容类 | Logos + 行动桥 | 双语体 (分析: だ/である + 读者: です/ます); 行动示唆必须 |
| `news` | 新闻事件类 | Logos | だ/である体; CTA 禁止; 分析 ≤ 30%; 时点明示必须 |
| `product` | 产品运营类 | Logos | です/ます体; Feature → Benefit 必须配对; 低承诺 CTA 任意 |
| `compliance` | 合规服务类 | Ethos | scene 别语体 (disclosure=だ/である; 其他=です/ます+谦让语 II); 宣传性零 |

### Tier 2 — 应用场面 (`--scene`，共 29 个)

#### campaign (7 场景)
| `--scene` | 应用场面 | 句长目标 |
|-----------|---------|---------|
| `launch` | キャンペーン开始告知 | LP:20–35; Push:≤20/≤60 |
| `remind` | 中间提醒 | Push:≤80; EDM:200–400 |
| `lastday` | 最终日/Last Chance | Push:≤80; SNS:≤140 |
| `result` | 结果通知 | Push:≤80; アプリ内 100–200 |
| `seasonal` | 季节/活动联动 | LP:400–1000 |
| `referral` | 介绍/邀请 | SNS/EDM:200–400 |

#### trade-ideas (6 场景)
| `--scene` | 应用场面 | 句长目标 |
|-----------|---------|---------|
| `flash` | 市场速报 | ≤140 |
| `theme` | 主题分析/投资主张 | 500–1500 |
| `earnings` | 决算亮点 | 200–500 |
| `morning` | 早盘 brief | 300–800 |
| `picks` | 注目个股卡片 | 80–200/股 |
| `community` | 社区话题 | 400–800+ 参与模块 |

#### news (6 场景)
| `--scene` | 应用场面 | 句长目标 |
|-----------|---------|---------|
| `flash` | 市况速报 | ≤140 |
| `wrap` | 当日总结 | 300–600 |
| `earnings` | 决算速报 | 150–400 |
| `indicator` | 经济指标速报 | 100–300 |
| `digest` | 新闻摘要 | 500–1000 |
| `alert` | 行情警报 | ≤100 |

#### product (7 场景)
| `--scene` | 应用场面 | 句长目标 |
|-----------|---------|---------|
| `short` | USP 卡片 | 30–80 |
| `detail` | 产品详细说明 | 200–500/段 |
| `manual` | 操作手册 | 150–400 |
| `script` | 视频/音频脚本 | ≤30/句 |
| `release` | Release notes | 100–300 |
| `onboard` | 新手引导 | 200–500 |
| `compare` | 对比表 | 100–200+ 表 |

#### compliance (5 场景)
| `--scene` | 应用场面 | 句长目标 |
|-----------|---------|---------|
| `disclosure` | 开示文书/目论见书 | 30–50 |
| `terms` | 利用规约 | 40–60 |
| `disclaimer` | 免责事项 | 40–60 |
| `faq` | FAQ | 20–35 |
| `guide` | 客服 / 操作向导 | 20–40 |

### 用户分群 (`--segment`，可选)

| `--segment` | 标签 | 漏斗阶段 | 心理策略 | CTA 温度 |
|-------------|------|---------|---------|---------|
| `churn` | 流失召回 | 再激活 | 损失厌恶, 好奇心 | warm |
| `never_traded` | 未首交 | 激活 | 低门槛, 社会证明 | cold |
| `high_value` | 高资产/高潜在 | 扩展 | 独占感, 表现力 | hot |
| `jp_stock_only` | 仅日本股 | 交叉销售 | 机会, FOMO | warm |
| `us_stock_only` | 仅美国股 | 交叉销售 | 机会, FOMO | warm |
| `inactive` | 无效户 | 再激活 | 低门槛, 激励 | cold |

### 品牌路由 Overlay (ADR-011)

输入或 brief 含品牌名时，加载 `case-library.md` 的品牌语音条目；对于渠道清单复杂的品牌（≥5 渠道在任一 T1 或 ≥3 T1 有渠道级 RL-4 差异），同时加载渠道路由表：

| 品牌 trigger | 配套文件 | 加载条件 |
|--|--|--|
| `moomoo` / `moomoo証券` | `references/moomoo-jp-routing.md` | 输入或 brief 中出现 moomoo |

后续 Nomura / 乐天 / SBI 一旦渠道清单达到阈值，按相同模式抽取（详见 [ADR-011](docs/adr/ADR-011-brand-routing-extraction-pattern.md)）。

---

## 安全护栏 (Red Lines)

| 编号 | 规则 | 适用范围 |
|------|------|---------|
| RL-1 | 术语锁定 — 金融/技术术语禁止替换为同义词或缩写 | 全部 |
| RL-2 | 信息注入禁止 — 不添加原文中不存在的事实、数据或论断 | 全部 |
| RL-3 | 主观表达禁止 — 零「思います」「感じます」 | news + trade-ideas 分析 |
| RL-4 | 硬字数限制 — 各场景严格字数上限（共覆盖 14 个场景/字段组合） | 见 SKILL.md RL-4 表 |
| RL-5 | 敬体禁止 — 零「です」「ます」 | compliance/disclosure |
| RL-6 | 语言门控 — 非日语输入拒绝处理，引导使用翻译工具 | 全部 |
| RL-7 | 双重否定禁止 | 全部 |
| RL-8 | 名词堆叠禁止 — 4+ 连续名词必须拆分 | 全部 |
| RL-9 | 数据出典要求 — 具体数值必须标注来源 | news + trade-ideas 分析 |
| RL-10 | 被动连续禁止 — 单句不超过 2 个被动构造（含 PASSIVE_ALLOW_LIST 例外） | 全部 |
| RL-11 | 文体混用禁止 — 动词词尾、敬语等级、modality、tone marker 一致；含 news 直接引用例外 | 全部 |
| RL-12 | 营销 CTA 必须 — 至少一个行动动词，按 Cold/Warm/Hot 阶段区分 | campaign |

## 验收标准 (Acceptance Criteria)

16 条 AC 覆盖：术语保留 (AC-1)、主观表达 (AC-2)、字数验证块格式 (AC-3, AC-4)、disclosure 验证 (AC-5)、出典标注 (AC-6)、营销具体性 + CTA (AC-7)、news/flash 完整性 (AC-8)、deadline 明示 (AC-9)、长尺免责 (AC-10)、news CTA 不在 (AC-11)、compliance 宣传性零 (AC-12)、news 字数上限 (AC-13)、引用配对 (AC-14)、picks 数值指标 (AC-15)、campaign 禁止词彙 (AC-16)。详见 SKILL.md。

---

## 使用方法

### 前提条件

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI / Desktop / Web
- Claude Pro / Max / Team / Enterprise 订阅

### 安装

将本仓库克隆到 Claude Code 的技能目录：

```bash
# macOS / Linux
git clone https://github.com/xiajing0522-creator/jp-style-optimizer.git ~/.claude/skills/jp-style-optimizer

# Windows (CMD)
git clone https://github.com/xiajing0522-creator/jp-style-optimizer.git %USERPROFILE%\.claude\skills\jp-style-optimizer

# Windows (PowerShell)
git clone https://github.com/xiajing0522-creator/jp-style-optimizer.git "$env:USERPROFILE\.claude\skills\jp-style-optimizer"
```

或者直接复制文件（无需 git）：

```bash
# 1. 下载并解压
curl -L https://github.com/xiajing0522-creator/jp-style-optimizer/archive/refs/heads/master.zip -o jp-style-optimizer.zip
unzip jp-style-optimizer.zip

# 2. 移动到技能目录
# macOS / Linux
mkdir -p ~/.claude/skills && mv jp-style-optimizer-master ~/.claude/skills/jp-style-optimizer

# Windows (PowerShell)
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills" | Out-Null
Move-Item jp-style-optimizer-master "$env:USERPROFILE\.claude\skills\jp-style-optimizer"
```

> **技能目录说明**：Claude Code 会自动扫描 `~/.claude/skills/` 下的子目录，读取其中的 `SKILL.md` 作为技能定义。安装后无需额外配置，重启 Claude Code 即可使用。

### 调用方式

在 Claude Code 对话中直接使用触发短语：

```
# 中文触发
润色日语文案 --style campaign --scene launch
改成投资分析 --style trade-ideas --scene theme
改成客观速报 --style news --scene flash

# 日语触发
キャンペーン告知文に
朝の市場ブリーフに
FAQ形式に

# 英语触发
rewrite as campaign copy
make SNS-friendly
```

也可以直接粘贴日语文本并附带风格关键词，技能会自动识别并激活。

### 输出格式

每次优化输出包含：

```
術語ロック: [锁定的术语列表]
スタイル: <style> / シーン: <scene>
セグメント: <分群> or なし

原文：<原始文本>
润色：<优化后文本>

検証:
  [逐项验证结果 — RL-1 ~ RL-12 适用项 + AC-1 ~ AC-16 适用项 + 字数计数]
  平均X字/文: ✓
  場面適合: X/N ✓
  自然さ: 問題なし

改動：[change1] [change2] ...
```

---

## 处理流程

1. **语言门控 (RL-6)** — 检测输入语言，非日语则拒绝并引导使用翻译工具
2. **术语锁定 + 源文分析** — 提取金融术语、识别信息结构和主导论证维度 (Logos/Ethos/Pathos)
3. **风格路由** — 确定 Tier 1 风格 + Tier 2 场景（可自动推断；加载对应 `references/{style}-guide.md`）
3.5. **品牌匹配**（可选）— 加载品牌语音条目 + 渠道路由表
3.6. **分群策略**（可选）— 注入用户分群心理策略，CTA 温度覆盖
4. **三层变换** — 结构层 (Layer 1) → 语言层 (Layer 2) → 论证框架层 (Layer 3)
5. **内联验证** — 逐条检查所有适用的 RL 和 AC，状态化输出在验证块中
6. **自然度检查** — 跨语体词汇泄漏、句长分布、参考对比、品牌语音吻合度

---

## 项目结构

```
jp-style-optimizer/
├── SKILL.md                                    # 技能主定义文件（Claude Code 入口，~3,232 词）
├── CHANGELOG.md                                # 版本变更日志（混合叙事 + Keep a Changelog）
├── README.md                                   # 本文件
├── references/
│   ├── style-guide.md                          # 路由推断 + 品牌 overlay（始终加载，~751 词）
│   ├── campaign-guide.md                       # campaign T1+T2 约束（条件加载）
│   ├── trade-ideas-guide.md                    # trade-ideas T1+T2 约束
│   ├── news-guide.md                           # news T1+T2 约束
│   ├── product-guide.md                        # product T1+T2 约束
│   ├── compliance-guide.md                     # compliance T1+T2 约束
│   ├── case-library.md                         # 4 家券商语音基准 + 反模式
│   └── moomoo-jp-routing.md                    # moomoo JP 渠道 ↔ scene ↔ RL-4 路由表（ADR-011 抽取）
├── build/                                      # 构建过程文档
│   ├── domain-research.md
│   ├── examples.md
│   ├── red-lines-and-criteria.md
│   ├── constraint-enforcement-plan.md
│   ├── token-architecture.md
│   ├── validation-checklist.md
│   └── boost-report-moomoo-jp-routing.md       # v6.6.0 boost 周期发布报告
├── diagnosis/                                  # 诊断与评估
│   ├── structural-audit.md                     # 9 项结构检查
│   ├── token-audit.md                          # Token 预算审计
│   ├── platform-check.md                       # 平台兼容性
│   ├── synthesis.md                            # boost 周期综合分析
│   ├── cross-style-quality-rubric.md           # 跨风格质量评分（D1-D9）
│   ├── behavioral-eval-suite.md                # 行为测试套件
│   ├── moomoo-jp-control-group.md              # moomoo 31 样本 A/B 对照组
│   └── ...
└── docs/
    └── adr/
        ├── ADR-001-llm-native-execution.md     # LLM 原生执行
        ├── ADR-006-platform-footer-assumption.md  # 平台 footer 前提
        ├── ADR-007-news-direct-quote-carveout.md  # news 直接引用例外
        ├── ADR-008-trade-ideas-institutional-segment.md
        └── ADR-011-brand-routing-extraction-pattern.md  # 品牌路由抽取模式
```

---

## 设计理念

- **LLM 原生执行** — 所有风格转换直接由 LLM 推理完成，无需外部脚本或 API（见 [ADR-001](docs/adr/ADR-001-llm-native-execution.md)）
- **编辑纪律优先** — 只改风格，不改内容；只调整表达方式，不注入新信息
- **可验证的输出** — 每次输出都附带完整验证块，用户可逐项审核合规性
- **Token 预算管理** — SKILL.md 3,232 词（≤3,500）；始终加载总量 3,983 词（≤5,000）；条件加载文件按需进入上下文

---

## 版本历史

详见 [CHANGELOG.md](CHANGELOG.md)。

主要里程碑：
- **v6.6.0** (2026-05-12) — moomoo JP 品牌路由抽取 + ADR-011 模式 + 31 样本对照组
- **v6.0.0** (2026-04-29) — 架构重设计：5 T1 × 29 T2 + 12 RL + 16 AC + 6 segment + 双语体 trade-ideas
- **v5.2.0** (2026-04-28) — 跨风格优化：全 5 种 T1 风格的 D9 评分维度 + 20 个场景的 Business Goal
- **v5.1.0** (2026-04-28) — 营销深度优化：质量评分标准 + 真实样本对比评估
- **v5.0.0** (2026-04-28) — 品牌语音匹配 + 13 项行为测试套件
- **v4.6.0** (2026-04-28) — 场景扩展至 20 个 + topic 双变体结构
- **v3.0.0** (2026-04-24) — LLM 原生执行架构（移除 Python 脚本）

---

## 许可

本项目供个人学习和参考使用。
