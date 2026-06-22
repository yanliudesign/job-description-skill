# Job Description Skill

> 🌐 **English** · [中文](./README.zh.md)

> **JD Decoder & Offer Strategy OS** — translate any Job Description into a complete go/no-go battle map: should you apply, how to apply, how to win. The entry point of the job-hunt chain.

A JD ≠ a recruiting blurb. It's the hiring manager's real expectations, the team's current pain, and the company's culture cues — all wrapped in HR boilerplate. This skill peels that wrapper back off.

---

## 5 Flows (ordered by frequency of use)

| Flow | Purpose | How users ask |
|------|---------|---------------|
| **1. JD Decoder** | 5-layer translation of what the JD actually means | "help me read this JD" / "decode this JD" |
| **2. Match Score** | Compute fit (0.6 / 0.2 / 0.2 weighted) + strengths / gaps / risks | "can I apply to this?" / "match me against this" |
| **3. Resume Tailor** | Three resume versions (ATS / Recruiter / HM) | "tailor my resume to this JD" |
| **4. Interview Predictor** | Top-20 interview questions + answer angles | "what will they ask me?" |
| **5. Should I Apply** | Five-part verdict (⭐ rating / values / risks / probability / next step) | "should I apply?" |

Entry lives in [`SKILL.md`](./SKILL.md) — routing table, three ironclad rules, file map.

---

## Three Ironclad Rules

1. **Decode before you act** — Flow 1 is mandatory before jumping to Flow 2/3. Matching against the wrong target = the match is wrong.
2. **No fabrication** — Never invent experience / skills / numbers the candidate didn't claim. If real evidence is missing, mark it ❌.
3. **One flow at a time** — No mixing. If Flow 1 left ambiguity, clarify before moving on.

---

## File Structure

```
job-description-skill/
├── SKILL.md                      # Entry · routing · three rules
├── prompts/                      # Execution prompts for each flow
│   ├── jd-decoder.md
│   ├── match-score.md
│   ├── resume-tailor.md
│   ├── interview-predictor.md
│   └── should-i-apply.md
├── frameworks/                   # Reusable frameworks / rubrics
│   ├── decode-patterns.md        # JD keyword → real intent dictionary
│   ├── match-rubric.md           # Scoring rubric (Must / Nice / Hidden)
│   ├── resume-tailoring.md       # Three-version resume strategy
│   └── go-no-go.md               # ⭐ rating + interview probability formula
└── jd-bank/                      # Local cache of analyzed JDs (gitignored)
    ├── _index.md                 # Index
    └── _jd-template.md           # Starter template for new JDs
```

---

## Design Principles

- **A JD is a mirror, not a quiz** — It reflects three layers: company, hiring manager, product. Our job is to see through the packaging.
- **Decision before optimization** — Most candidates keep polishing resumes for the wrong roles. This skill decides first whether to apply at all.
- **Reproducible logic, not magic** — Every score and probability comes from an explicit formula. Disagree with the premise? You can argue back.
- **Pairs with [BQ Skill](https://github.com/yanliudesign/bq-skill) (story mining) + [Resume Skill](https://github.com/yanliudesign/resume-skill) (resume polish) to form the full job-hunt chain.**

---

## License

MIT — fork it, remix it, ship your own version.

Created by [Dreameryanyan](https://www.linkedin.com/in/yanliudesign/) ·
[LinkedIn](https://www.linkedin.com/in/yanliudesign/) ·
[X](https://x.com/yanliudreamer) ·
[Xiaohongshu](https://www.xiaohongshu.com/user/profile/5b2afdf311be104ac3c22931)
