---
name: job-description-skill
description: "Job Description 解码器 + Offer 策略系统。把任何 JD 翻译成「这家公司到底在招什么人 / 我的匹配度 / 该怎么改简历 / 面试会问什么 / 值不值得投」。支持 JD 解码、匹配度评分、简历定向改写、面试题预测、Should I Apply 决策五条流程。是整个求职链路的入口，向下衔接 Resume Skill 和 BQ Skill。关键词：job description, JD, 职位描述, 匹配度, ATS, resume tailor, 简历定制, 招聘经理, 投不投, should I apply, 面试预测。"
---

# Job Description Skill — JD Decoder & Offer Strategy OS

把一份 JD 从「招聘话术」翻译成「**你能用的求职情报**」。核心循环：

```
解码 (Decode) → 匹配 (Match) → 改写 (Tailor) → 预测 (Predict) → 决策 (Decide) → 沉淀 (Save)
```

下游可一键接 **Resume Skill**（拿着 tailor 结果继续打磨简历）和 **BQ Skill**（拿着预测题目去练故事），形成 Career Copilot 闭环。

---

## 三条铁律

**铁律一 · 先解码，再做任何事。**
任何流程进来，**必须先跑一遍 JD Decoder**（哪怕极简版）。直接拿原始 JD 去算匹配度、改简历、预测面试题，都是在跟「招聘话术」对齐，而不是跟「招聘经理真实需求」对齐——这是 90% 求职工具最大的盲区。

**铁律二 · 不替用户编简历内容、不编公司情报。**
- Resume Tailor 只能**重新组织 / 突出 / 翻译**用户简历里已有的事实，不能凭空捏造成就、数字、职责。
- 公司文化、团队信号只能从 JD 文本 + 用户提供的信息推断；不要装作知道某公司内部情况。所有推断都标"我从 ___ 推断"。

**铁律三 · 一次只走一条流程，走完再问下一步。**
五条流程产出形态不同、深度不同。不要试图一次把 decode + match + tailor + predict + go/no-go 全输出——会变成一份谁都看不完的报告。每条流程做完，**主动问用户**："要不要继续 ___ ？"

---

## 路由：用户进来时先判断意图

| 用户说的话 | 走哪条流程 |
|---|---|
| 贴 JD 链接 / JD 全文 / 「帮我看这个职位」 | **流程 1 · JD Decoder** → [prompts/jd-decoder.md](prompts/jd-decoder.md) |
| 「我的简历跟这个 JD 配吗」/ 同时给了 resume + JD / 「匹配度多少」 | **流程 2 · Match Score** → [prompts/match-score.md](prompts/match-score.md) |
| 「帮我改简历」/「按这个 JD tailor 一下」/「ATS 优化」 | **流程 3 · Resume Tailor** → [prompts/resume-tailor.md](prompts/resume-tailor.md) |
| 「这个职位面试会问什么」/「预测面试题」 | **流程 4 · Interview Predictor** → [prompts/interview-predictor.md](prompts/interview-predictor.md) |
| 「值不值得投」/「我该不该试一下」/「拿面概率多少」 | **流程 5 · Should I Apply?** → [prompts/should-i-apply.md](prompts/should-i-apply.md) |
| 「看看我存过哪些 JD」/「上次那个 OpenAI 的职位」 | 读 [jd-bank/_index.md](jd-bank/_index.md) 汇报，让用户挑一份继续。 |

判断不了就问一句："你是想**先解码这份 JD**，还是直接**算匹配度 / 改简历 / 决定要不要投**？"

---

## 数据要齐再开工

不同流程对输入要求不同。**别在缺关键输入的时候硬跑**，先要齐：

| 流程 | 必需 | 可选但强烈推荐 |
|---|---|---|
| 1 · Decode | JD 全文（或链接） | 公司名、团队、Level |
| 2 · Match | JD（已解码更好）+ 用户简历 / LinkedIn | 用户目标 Level、薪资期望 |
| 3 · Tailor | JD + 用户简历**全文**（不是摘要） | 想强调的 1-2 个亮点 |
| 4 · Predict | JD（已解码更好） | 公司近期产品 / 业务方向 |
| 5 · Should I Apply | JD + 用户背景概要 | 用户对薪资 / 地点 / 行业的硬约束 |

链接进来但抓不到内容 → 让用户**直接粘贴 JD 文本**，别瞎猜。

---

## 流程 1 — JD Decoder（核心入口）

完整步骤见 [prompts/jd-decoder.md](prompts/jd-decoder.md)。一句话版：

1. **先查库** — 读 [jd-bank/_index.md](jd-bank/_index.md)，同公司 / 同岗位是不是分析过？有就复用 + 增量更新。
2. **结构化拆解** —— 拆出 5 个图层：
   - **招聘经理真实需求**（把营销话术翻译成实际期望）
   - **Must Have**（不满足就直接 reject 的 3-5 条）
   - **Nice to Have**（加分项 3-5 条）
   - **Hidden Signals**（从 JD 措辞推断的文化 / 团队 / 阶段信号）
   - **Level / 团队 / 阶段判断**（推断这是个什么样的位置）
3. **沉淀** — 按 [jd-bank/_jd-template.md](jd-bank/_jd-template.md) 存进 `jd-bank/`，更新 `_index.md`。
4. **下一步导流** — 问用户："要不要算匹配度 / 改简历 / 看面试题 / 评估值不值得投？"

参考词典：[frameworks/decode-patterns.md](frameworks/decode-patterns.md)。

---

## 流程 2 — Match Score

完整步骤见 [prompts/match-score.md](prompts/match-score.md)。输出固定四件套：

- **匹配度**（数字 + 一句话定性，参考 [frameworks/match-rubric.md](frameworks/match-rubric.md) 的评分方法，不能凭感觉打分）
- **强项**（用户简历里能直接命中 JD must-have 的 3-5 条）
- **Gap**（缺的 / 弱的，分「能补」「难补」「无关紧要」三档）
- **风险**（招聘经理可能担心的画像问题，如「大厂背景能不能适应创业」「Level 跨度」「行业切换」）

---

## 流程 3 — Resume Tailor（最容易付费的功能）

完整步骤见 [prompts/resume-tailor.md](prompts/resume-tailor.md)。必须同时输出三个版本：

- **ATS 版** — 关键词命中最大化，机器友好
- **Recruiter 版** — 30 秒扫读友好，强项前置
- **Hiring Manager 版** — 体现思考、判断、影响力

每条改写要**给 diff**：原文 vs 改后，并标"对齐了 JD 的 ___"。规则与边界见 [frameworks/resume-tailoring.md](frameworks/resume-tailoring.md)。

> **绝不杜撰**。所有改写只能基于用户提供的简历事实，重新组织 / 突出 / 翻译话术。

---

## 流程 4 — Interview Predictor

完整步骤见 [prompts/interview-predictor.md](prompts/interview-predictor.md)。输出 **Top 20 题**，分四类：

- Behavior（行为题）
- Product Thinking / Domain（专业题）
- Technical / Craft（技能题）
- Company-specific（针对该公司 / 团队的定制题）

每道题标**为什么会被问**（对应 JD 哪条要求 / 哪个 Hidden Signal）。

→ **Behavior 部分直接导流到 BQ Skill**：告诉用户"这几道题可以用 BQ Skill 挖故事 / 查故事库"。

---

## 流程 5 — Should I Apply?（最有传播性的功能）

完整步骤见 [prompts/should-i-apply.md](prompts/should-i-apply.md)。输出五件套：

- **推荐指数**（⭐ 1–5）
- **为什么值得投**（3 条）
- **为什么不值得投**（3 条，必须给，不能只说好话）
- **预估拿面概率**（参考 [frameworks/go-no-go.md](frameworks/go-no-go.md) 估算，给区间不给单点）
- **建议下一步**（直接投 / 先 tailor / 先补 Gap / 放弃 / 找内推）

打分方法和 deal-breaker 清单见 [frameworks/go-no-go.md](frameworks/go-no-go.md)。

---

## JD Bank（情报沉淀）

- 位置：本 skill 目录下 `jd-bank/`，每份分析过的 JD 一个 `.md`。
- 文件名：`<公司缩写>-<岗位slug>-<YYYYMM>.md`，如 `openai-product-designer-202606.md`。
- frontmatter 必填：company / role / level / source_url / decoded_at / status（decoded / matched / tailored / applied / interview / closed）。
- [jd-bank/_index.md](jd-bank/_index.md) 是反查表：按公司、按岗位类型、按状态分组。**每次新增或更新一份 JD 文件都要同步 `_index.md`**。
- 用户回头说"上次那个 ___"时，先查 index，别让用户重新粘 JD。

---

## 与 Resume Skill / BQ Skill 的衔接

这个 skill 不替代另外两个：

- **Resume Skill** 负责把一份简历做到「整体优秀 + 个人故事一致」。JD Skill 的 Tailor 流程只做**针对单个 JD 的定向调整**——产出 diff 后，告诉用户"要做整体优化去 Resume Skill"。
- **BQ Skill** 负责挖掘 / 结构化 / 沉淀故事库。JD Skill 的 Interview Predictor 只给"会被问什么"——告诉用户"用 BQ Skill 把这些题挖成故事"。

三者形成的用户路径：

```
看到 Dream Job
   ↓
JD Skill 解码 + 匹配 + Should I Apply
   ↓（决定投）
JD Skill 定向 Tailor → Resume Skill 整体打磨
   ↓（拿到面试）
JD Skill 预测面试题 → BQ Skill 挖故事 / 模拟面试
   ↓
拿 Offer
```

---

## 参考文件（按需读取，别一次全加载）

**Prompts（流程脚本）**
- [prompts/jd-decoder.md](prompts/jd-decoder.md) — 流程 1：JD 解码
- [prompts/match-score.md](prompts/match-score.md) — 流程 2：匹配度评分
- [prompts/resume-tailor.md](prompts/resume-tailor.md) — 流程 3：简历定向改写
- [prompts/interview-predictor.md](prompts/interview-predictor.md) — 流程 4：面试题预测
- [prompts/should-i-apply.md](prompts/should-i-apply.md) — 流程 5：投不投决策

**Frameworks（知识词典）**
- [frameworks/decode-patterns.md](frameworks/decode-patterns.md) — JD 话术翻译表 + Hidden Signal 词典
- [frameworks/match-rubric.md](frameworks/match-rubric.md) — 匹配度评分规则 + Gap 三档分类
- [frameworks/resume-tailoring.md](frameworks/resume-tailoring.md) — ATS / Recruiter / HM 三版改写法
- [frameworks/go-no-go.md](frameworks/go-no-go.md) — Should I Apply 打分法 + 拿面概率估算

**JD Bank（情报库）**
- [jd-bank/_jd-template.md](jd-bank/_jd-template.md) — JD 分析文件模板
- [jd-bank/_index.md](jd-bank/_index.md) — JD 反查索引
