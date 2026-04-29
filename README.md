# jp-style-optimizer

**日语金融文案风格优化器** — Claude Code 自定义技能 (Custom Skill)

对现有日语金融文本进行文体转换和风格润色。不翻译、不添加信息、不生成新论断。

> 当前版本: **v5.2.0**

---

## 功能概述

jp-style-optimizer 是一个运行在 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 上的自定义技能，专为日语金融文案的风格调整而设计。它能够：

- 在 **5 种文案风格** 和 **20 种应用场景** 之间进行文体转换
- 自动锁定金融术语，确保转换过程中专业词汇零变形
- 内置 12 条安全护栏（Red Lines），防止信息注入、文体混乱等问题
- 支持品牌特定语音匹配（野村证券、乐天证券、SBI证券、moomoo证券）
- 支持 6 种用户分群策略，根据用户画像调整文案角度和 CTA 语气
- 每次输出包含完整的验证块，逐项确认约束合规

---

## 风格路由

### Tier 1 — 文案风格 (`--style`)

| 风格 | 日语名称 | 语体特征 |
|------|---------|---------|
| `marketing` | 営業推広 | です/ます体; CTA 必须; 利益先行; 能动态 |
| `product` | 産品説明 | です/ます体; 功能→利益结构; 术语首次解释 |
| `report` | 情報分析 | 第三人称客观体; 推测表达必须; 零主观 |
| `legal` | 法律合規 | 免责条款; 风险警告必须; 零推广 |
| `support` | 客服支援 | 谦让语 II; お/ご前缀全覆盖; 功能性 CTA |

### Tier 2 — 应用场景 (`--scene`)

| 场景 | 名称 | 所属风格 | 字数目标 |
|------|------|---------|---------|
| `lp` | LP/落地页 | marketing | 20-35字/句 |
| `sns` | SNS/社交媒体 | marketing | 10-25字/句, 总计 ≤140字 |
| `event` | 活动告知/Campaign | marketing | 15-25字/句 |
| `push` | Push 通知 | marketing | 标题 ≤20字; 正文 ≤60字 |
| `edm` | EDM/邮件营销 | marketing | 件名 ≤40字; 预览 ≤80字 |
| `banner` | 应用内横幅 | marketing | 主文 ≤15字; 副文 ≤25字 |
| `short` | 短产品文案/卖点 | product | 15-25字/句 |
| `detail` | 产品详细说明 | product | 20-35字/句 |
| `manual` | 使用说明/手册 | product | 20-40字/句 |
| `script` | 视频/音频脚本 | product | ≤30字/句 |
| `report` | 研报/周报 | report | 20-35字/句 |
| `press` | 新闻稿 | report | 20-40字/句 |
| `deck` | 幻灯片/PPT | report | ≤25字/bullet |
| `hottopic` | 市况速报 | report | 15-25字/句, 总计 ≤140字 |
| `topic` | 话题文章/社区投稿 | report | 25-50字/句 |
| `disclosure` | 开示文书/目论见书 | legal | 30-50字/句 |
| `terms` | 利用规约 | legal | 40-60字/句 |
| `disclaimer` | 免责事项 | legal | 40-60字/句 |
| `faq` | FAQ/常见问题 | support | 20-35字/句 |
| `guide` | 手续说明 | support | 20-40字/句 |

### 用户分群 (`--segment`)

| 分群 | 标签 | 漏斗阶段 | 心理策略 | CTA 温度 |
|------|------|---------|---------|---------|
| `churn` | 流失召回 | 再激活 | 损失厌恶, 好奇心 | warm |
| `never_traded` | 未首交 | 激活 | 低门槛, 社会证明 | cold |
| `high_value` | 高资产/高潜在 | 扩展 | 独占感, 表现力 | hot |
| `jp_stock_only` | 仅日本股 | 交叉销售 | 机会, FOMO | warm |
| `us_stock_only` | 仅美国股 | 交叉销售 | 机会, FOMO | warm |
| `inactive` | 无效户 | 再激活 | 低门槛, 激励 | cold |

---

## 安全护栏 (Red Lines)

| 编号 | 规则 | 适用范围 |
|------|------|---------|
| RL-1 | 术语锁定 — 金融/技术术语禁止替换为同义词或缩写 | 全部 |
| RL-2 | 信息注入禁止 — 不添加原文中不存在的事实、数据或论断 | 全部 |
| RL-3 | 主观表达禁止 — 零「思います」「感じます」 | 情报分析系 |
| RL-4 | 硬字数限制 — 各场景严格字数上限 | 6 个场景 |
| RL-5 | 敬体禁止 — 零「です」「ます」 | 开示文书 |
| RL-6 | 语言门控 — 非日语输入拒绝处理，引导使用翻译工具 | 全部 |
| RL-7 | 双重否定禁止 | 全部 |
| RL-8 | 名词堆叠禁止 — 4+ 连续名词必须拆分 | 全部 |
| RL-9 | 数据出典要求 — 具体数值必须标注来源 | 情报分析系 |
| RL-10 | 被动连续禁止 — 单句不超过 2 个被动构造 | 全部 |
| RL-11 | 文体混用禁止 — 动词词尾、敬语等级、语气标记等一致 | 全部 |
| RL-12 | 营销 CTA 必须 — 至少一个行动动词 | 营销系 5 场景 |

---

## 使用方法

### 前提条件

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI / Desktop / Web
- Claude Pro / Max / Team / Enterprise 订阅

### 安装

将本仓库克隆到 Claude Code 的技能目录：

```bash
# macOS / Linux
git clone https://github.com/<your-username>/jp-style-optimizer.git ~/.claude/skills/jp-style-optimizer

# Windows
git clone https://github.com/<your-username>/jp-style-optimizer.git %USERPROFILE%\.claude\skills\jp-style-optimizer
```

### 调用方式

在 Claude Code 对话中直接使用触发短语：

```
# 中文触发
润色日语文案 --style marketing --scene sns

# 日语触发
マーケティング向けに書き直して

# 英语触发
rewrite in report style
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
  [逐项验证结果]
  平均X字/文: ✓
  場面適合: X/N ✓
  自然さ: 問題なし

改動：[change1] [change2] ...
```

---

## 处理流程

1. **语言门控** — 检测输入语言，非日语则拒绝并引导使用翻译工具
2. **术语锁定 + 源文分析** — 提取金融术语、识别信息结构和主导论证维度
3. **风格路由** — 确定 Tier 1 风格 + Tier 2 场景（可自动推断）
4. **品牌匹配**（可选）— 加载品牌特定语音约束
5. **分群策略**（可选）— 注入用户分群心理策略
6. **三层变换** — 结构层 → 语言层 → 论证框架层
7. **内联验证** — 逐条检查所有适用的 Red Lines
8. **自然度检查** — 跨语体词汇泄漏、句长分布、参考对比

---

## 项目结构

```
jp-style-optimizer/
├── SKILL.md                  # 技能主定义文件（Claude Code 入口）
├── CHANGELOG.md              # 版本变更日志
├── README.md                 # 本文件
├── references/
│   ├── style-guide.md        # 风格指南：Tier 1/2 约束、改写模式、示例
│   └── case-library.md       # 品牌案例库：4 家券商的语音基准和反模式
├── build/                    # 构建过程文档
│   ├── domain-research.md    # 领域调研
│   ├── examples.md           # 示例库
│   ├── red-lines-and-criteria.md
│   ├── constraint-enforcement-plan.md
│   ├── resource-plan.md
│   ├── token-architecture.md # Token 预算架构
│   └── validation-checklist.md
├── diagnosis/                # 诊断与评估
│   ├── cross-style-quality-rubric.md  # 跨风格质量评分标准（D1-D9）
│   ├── behavioral-eval-suite.md       # 行为测试套件（13 个测试用例）
│   ├── marketing-quality-rubric.md    # 营销质量评分标准
│   ├── marketing-sample-eval.md       # 营销样本评估
│   └── ...                            # 其他诊断文件
└── docs/
    └── adr/
        └── ADR-001-llm-native-execution.md  # 架构决策：LLM 原生执行
```

---

## 设计理念

- **LLM 原生执行** — 所有风格转换直接由 LLM 推理完成，无需外部脚本或 API（见 [ADR-001](docs/adr/ADR-001-llm-native-execution.md)）
- **编辑纪律优先** — 只改风格，不改内容；只调整表达方式，不注入新信息
- **可验证的输出** — 每次输出都附带完整验证块，用户可逐项审核合规性
- **Token 预算管理** — SKILL.md 约 2,450 词（预算 3,000）；style-guide.md 约 5,191 词（软上限 5,000）

---

## 版本历史

详见 [CHANGELOG.md](CHANGELOG.md)。

主要里程碑：
- **v5.2.0** (2026-04-28) — 跨风格优化：全 5 种 T1 风格的 D9 评分维度 + 20 个场景的 Business Goal
- **v5.1.0** (2026-04-28) — 营销深度优化：质量评分标准 + 真实样本对比评估
- **v5.0.0** (2026-04-28) — 品牌语音匹配 + 13 项行为测试套件
- **v4.6.0** (2026-04-28) — 场景扩展至 20 个 + topic 双变体结构
- **v3.0.0** (2026-04-24) — LLM 原生执行架构（移除 Python 脚本）

---

## 许可

本项目供个人学习和参考使用。
