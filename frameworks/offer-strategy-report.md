# Offer Strategy Report — HTML 报告规格

把 Flow 1（Decode 精华）+ Flow 2（完整 Match）+ Flow 4（Top 10 题预览）+ Flow 5（完整 Should I Apply）+ 策略层（内推 / portfolio / 时间线）融合成**一份可分享的单文件 HTML 报告**。是 Onboarding Wizard 跑到 Step 7 后**默认产出**的终极交付物。

参考实现：[../examples/offer-strategy-template.html](../examples/offer-strategy-template.html)（CSS / 排版骨架）+ 用户桌面上已生成过的真实样例。

---

## 何时生成

- **Onboarding Wizard 跑完 Step 7（Should I Apply）→ 默认生成。**
- 用户单独要："给我出一份 HTML 报告" → 前提是 **Flow 1 + Flow 2 + Flow 5 至少都跑过**（否则数据不够）。
- 跑完 Flow 3 / Flow 4 之后用户要求更新报告 → 重新生成同文件名（覆盖）。

---

## 文件位置 + 命名

| 优先级 | 路径 |
|---|---|
| 1（默认） | `~/Desktop/Claude skills/offer-strategy-<company-slug>-<role-slug>-<YYYYMM>.html` |
| 2（兜底） | 本 skill 内 `jd-bank/<同名>.html`（如果用户没有 `~/Desktop/Claude skills/` 目录） |

> 历史命名兼容：`should-i-apply-<...>.html` 这种命名是早期版本，新报告统一改用 `offer-strategy-` 前缀。

---

## 报告骨架（必须按此顺序）

1. **Header** — 公司 × 岗位 · 地点 · 薪资带 · Level · JD 一句话定位
2. **Meta strip** — 候选人画像 / Track Record / Pedigree / 当前 Status
3. **Inside (TOC)** — 章节快速跳转锚点
4. **⚠️ Assumptions（最关键章节，放显眼位置）** — 列出报告所依赖的全部假设（薪资底线 / visa / on-site 接受度 / 心理价位 title / 行业切换接受度 / 当前手里 pipeline 数），每条单独成行，明确写："任一不对，告诉我重新生成"
5. **Verdict** — 一句话定性 + 3 行展开 + ⭐ 1-5 推荐指数
6. **If you only read three things** — 3 个最重要的 takeaway（要黑体加粗，是给"不会读完全文"的 reader 用的）
7. **Match Score gauge** — 数字（区间）+ 分项加权（Must / Nice / Hidden）+ 0–100 视觉条
8. **Interview Probability gauge** — 区间 + 各调节因子（基线 / tailor / 公司热度 / portfolio / 内推）+ 视觉条
9. **§i · Why this JD reads the way it does** — Flow 1 精华，每段 JD 原文 → 真实诉求
10. **Hidden Signal 词典命中** — 表格：JD 措辞 → 解读 → 是否命中你的画像
11. **§ii · Must Have 命中分析** — Flow 2 每条 Must Have 一张卡片：评分 + 简历原文证据 + 风险提示
12. **§iii · Nice to Have + Hidden Signal Fit** — 隐性 Nice 命中清单 + 10 维度雷达 / 评分
13. **§iv · 为什么投 vs 为什么不投** — 各 3 条，**"不投"每条必须附 "HM probe 应对"**（市面工具最缺这块）
14. **§v · 薪资 reality check** — JD 带宽 + 同岗位市场数据 + 谈判 talking points
15. **§vi · 为什么这个 role 是你叙事的下一步** — 职业弧线和这个 role 的匹配关系
16. **§vii · 内推 playbook** — 找谁（LinkedIn 搜法）/ 怎么开口 / 完整 DM 模板
17. **§viii · Portfolio audit** — 3-5 件 4 周内必须做的具体动作（不是泛泛而谈）
18. **§ix · Top 10 面试题预测** — Flow 4 preview，每题标"为什么会问 + 准备方向"。结尾导流："要完整 Top 20 + Behavior 故事，去 BQ Skill"
19. **§x · N 周行动时间线** — 按周拆解：投递前 / 投递后 / 面试前。每周 2-4 条具体 to-do
20. **Footer** — `JD SKILL.` brand mark + 生成时间戳 + 同 JD 的 markdown 文件链接

---

## 视觉规范（必须保留，否则报告看起来像玩具）

### 色板
- 底色：`#fafaf7` / `#faf8f3` 系 cream/sand
- 卡片背景：`#fff8e6` / `#fef0d4` 暖米
- 文字主色：`#1f1f1d` / `#2a2308` / `#2a1c04` 深棕近黑
- 文字次色：`#6b6b66` 中灰
- Accent 红：`#d11838` / `#ff2442`（单一红，不要再加红色）
- Accent 绿：`#0d8a45` / `#18a957`（用于"命中" / "值得投"）
- 警示橙：`#d97706` / `#f59e0b`（用于"假设"和"风险"）
- 边框 / 分隔线：`#ebebe4` / `#d9d9d2` / `#c8c8c3`

### 字体系统（CSS variables）
```css
--display: serif（如 Tiempos / Source Serif / Crimson）—— 36–72px，用于章节大标题和 Verdict
--serif:   serif —— body 引用 / case quote
--body:    sans（如 Inter / Söhne / system-ui）—— 15–17px，用于正文
--mono:    monospace（如 JetBrains Mono / Berkeley Mono / SF Mono）—— 数字 / score / code
```

### 关键 UI 组件
- **对角线条纹背景**：用于区分 ✓ 值得投 / ✗ 不值得投 / ⚠️ 假设 三类块（每类一种条纹色 + 角度）
- **Gauge**（评分条）：纯 SVG 或 CSS，不要外部库；显示数字 + 0/55/70/85/100 刻度
- **雷达图**（Hidden Signal Fit）：纯 SVG 10 维度多边形
- **TOC**：左侧 sticky 或顶部 inline，点击平滑滚动到锚点

### 文件特性
- **单文件、零外部依赖**（CSS 内联、字体用 system 或 base64，图表用 SVG）
- 可离线打开 / 邮件附件直接传
- 总体积控制在 80KB 以内
- **右下角固定有一个“导出 PDF”按钮**：黑色 pill 样式，点击后调 `window.print()`。在 `@media print` 中 `display: none` 隐藏，所以导出出来的 PDF 不会带这个按钮。用户点击 → 浏览器打印对话框 → 选“另存为 PDF”即可。

---

## 内容铁律

1. **数字必须给区间，不给单点** —— Match Score / 拿面概率 / 薪资预期都给范围。给"78%"这种单点数字是这类工具最大的可信度杀手。
2. **每条假设单独可纠错** —— Assumptions 区列 5-7 条，每条独立成行，明确写"任一不对，告诉我重新生成"。
3. **"不投"那部分每条必须给 HM probe 应对** —— 不是只说"有风险"，要给"如果 HM 这么问，你这么答"。
4. **简历事实必须引用原文** —— Must Have 命中分析里的证据必须是简历 / LinkedIn 里能查到的原文片段，不能是"我推断你大概有"。
5. **绝不杜撰** —— 数字 / 公司 / 项目 / Title 用户没说过的，标 `[需用户补充]`，不要凭空填。
6. **Verdict 不许中性** —— ⭐ 1-5 必须明确，倾向不投也要敢说，模糊就标"Match 不足或假设缺失，建议先补 ___ 再生成"。

---

## 与五条 Flow 的关系

| 章节 | 数据来源 |
|---|---|
| §i Why this JD reads the way it does | Flow 1（精简版，2-3 段就够） |
| §ii Must Have 命中分析 | Flow 2（完整 6 条左右） |
| §iii Nice to Have + Hidden Signal Fit | Flow 2 续 |
| §iv 为什么投 vs 不投 | Flow 5 |
| §v 薪资 reality check | Flow 5 + 外部数据（Levels.fyi 等） |
| §vi 叙事下一步 | Flow 5 + 候选人画像推断 |
| §vii 内推 playbook | Flow 5 推荐动作 |
| §viii Portfolio audit | Flow 5 + Flow 3 简版（不替代完整 Tailor） |
| §ix Top 10 面试题 | Flow 4 preview（不替代完整 Top 20） |
| §x N 周行动时间线 | Flow 5 collapse 后的执行版 |

**这份报告不替代单独跑 Flow 3 / Flow 4 完整版。** 报告底部要明确导流：
- 想要三版简历 → 跑 Flow 3 Resume Tailor
- 想要完整 Top 20 + Behavior 故事 → 跑 Flow 4 + 转 BQ Skill

---

## 生成流程

1. 确认 Flow 1 / 2 / 5 数据齐全（至少这三条）。少了就**告诉用户"先跑完 ___ 再生成报告"**，不要硬出。
2. 在内存里组装 20 个章节的内容。
3. 用 [examples/offer-strategy-template.html](../examples/offer-strategy-template.html) 的 CSS / 结构当骨架，把内容填进去。
4. 写到 `~/Desktop/Claude skills/offer-strategy-<slug>.html`。
5. **同步更新 jd-bank 文件**：把 §6 / §8 / §9 三个占位符回填 + 在文件最后加一行 `> 📊 HTML 报告：~/Desktop/Claude skills/offer-strategy-<slug>.html`。
6. **同步更新 [jd-bank/_index.md](../jd-bank/_index.md)**：status 改为 `matched` 或更高，加一列 `report` 链接。

---

## 常见卡点

| 症状 | 处理 |
|---|---|
| 用户没跑完 Flow 5 就要报告 | 拒绝 + 一句话引导："还需要先跑 Should I Apply 才能出报告，要不要现在跑？" |
| 用户简历事实不足，§ii 写不出证据 | **标 `[需用户补充：具体项目 / 数字]`**，不要编。报告顶部 Assumptions 加一条"简历未完全提供，部分章节为占位" |
| 用户希望"只要 Verdict 那一段" | 给一份**极简单页摘要**（5 个 block：Verdict / Match / 概率 / 3 投 3 不投 / 下一步），不要塞 20 章 |
| 公司是中国公司 | 字体换思源宋体 / 思源黑体；薪资章节用 RMB 区间 + level 对标（P7/P8 等）|
| 报告超过 80KB | 砍 §x 时间线和 §vii 内推模板的字数，保留所有视觉组件 |
