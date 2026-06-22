# Job Description Skill

> **JD Decoder & Offer Strategy OS** — 把任何 Job Description 翻译成"该不该投 / 怎么投 / 怎么赢"的完整作战图。求职链路的入口。

一份 JD ≠ 一份招聘文案。它是招聘经理的真实期望、团队当前的痛点、公司文化的暗号——只是被 HR 模板包了一层。这个 Skill 把它解码回来。

---

## 5 个流程（按使用频率排序）

| Flow | 用途 | 用户问法 |
|------|------|----------|
| **1. JD Decoder** | 5 层翻译 JD 的真实意图 | "帮我看看这份 JD" / "decode this JD" |
| **2. Match Score** | 算匹配度（0.6/0.2/0.2 加权）+ 强项 / Gap / 风险 | "我能投这个吗？" / "match 一下" |
| **3. Resume Tailor** | 出三版简历（ATS / Recruiter / HM） | "改简历适配这个 JD" |
| **4. Interview Predictor** | Top 20 面试题 + 应答方向 | "面这个会被问什么" |
| **5. Should I Apply** | 五件套决策（⭐推荐 / values / risks / 概率 / 下一步） | "该不该投？" / "should I apply" |

入口在 [`SKILL.md`](./SKILL.md) — 路由表 + 三铁律 + 文件地图。

---

## 三铁律

1. **先解码，再行动** — 没跑过 Flow 1 不允许直接跳 Flow 2/3。匹配错对象 = 匹配错了。
2. **不杜撰** — 候选人没说过的经历 / 技能 / 数字一律不发明。出不了真实证据就标 ❌。
3. **一次只走一条流程** — 不混跑。Flow 1 出来如果还有 ambiguity，先澄清再前进。

---

## 文件结构

```
job-description-skill/
├── SKILL.md                      # 入口 · 路由 · 三铁律
├── prompts/                      # 5 条流程的执行 prompt
│   ├── jd-decoder.md
│   ├── match-score.md
│   ├── resume-tailor.md
│   ├── interview-predictor.md
│   └── should-i-apply.md
├── frameworks/                   # 复用的框架 / 评分尺
│   ├── decode-patterns.md        # JD 关键词 → 真实意图字典
│   ├── match-rubric.md           # 评分尺 (Must / Nice / Hidden)
│   ├── resume-tailoring.md       # 三版本简历策略
│   └── go-no-go.md               # ⭐ 推荐指数 + 拿面概率公式
└── jd-bank/                      # 已分析过的 JD 反查库（本地不进 git）
    ├── _index.md                 # 索引
    └── _jd-template.md           # 新 JD 起手模板
```

---

## 设计原则

- **JD 是一面镜子，不是一份题目** — 它照出公司、HM、产品三层信息。我们要做的是看穿包装层。
- **决策优先于优化** — 大多数候选人在错的 role 上反复优化简历。这个 Skill 先帮你决定该不该投。
- **可复现的逻辑，不是玄学** — 每个评分 / 概率都有显式公式，不喜欢可以反驳前提。
- **配合 [BQ Skill](https://github.com/yanliudesign/bq-skill)（故事挖掘）+ [Resume Skill](https://github.com/yanliudesign/resume-skill)（简历美化）形成完整求职链路。**

---

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[小红书](https://www.xiaohongshu.com/user/profile/5b2afdf311be104ac3c22931)
