---
name: ai-research-writing
description: >
  Academic paper writing, polishing, logic checking, figure/chart design, experiment analysis,
  and reviewer-style critique for CS/AI conferences and Chinese core journals. Extracted and
  adapted from Leey21/awesome-ai-research-writing. Use when the user asks to rewrite Chinese
  paper drafts (Word), condense/expand English LaTeX paragraphs, polish English LaTeX or Chinese
  journal text, run a final logic red-line check, remove AI writing patterns in LaTeX or Word,
  design architecture figures or select experiment charts, generate figure/table captions, analyze
  experiment tables into LaTeX paragraphs, or review an entire paper from a top-venue Reviewer
  perspective.
---

# AI Research Writing

Practical academic writing, polishing, visualization, and peer-review workflows distilled from [Leey21/awesome-ai-research-writing](https://github.com/Leey21/awesome-ai-research-writing).

> **Scope note:** For general-purpose prose de-AI-ification outside academic LaTeX/Word formatting rules, see the sibling [`humanizer`](../humanizer/SKILL.md) skill. For cross-language Chinese ↔ English translation, see [`ai-research-translation`](../../翻译/ai-research-translation/SKILL.md).

## Task Routing

Identify the user's writing stage and **read only the matching reference file** before responding:

| User Request / Task | Prompt Modes Covered | Reference to Load |
|---|---|---|
| 中文草稿重构为期刊正文 (Word)、LaTeX 缩写 / 扩写、英文或中文论文表达润色 | `中转中-word` · `缩写` · `扩写` · `表达润色（英文论文）` · `表达润色（中文论文）` | [references/polishing-and-rewriting.md](references/polishing-and-rewriting.md) |
| 英文 LaTeX 终稿红线逻辑审查、LaTeX 英文去 AI 味（含高频 AI 词表）、Word 中文去 AI 味 | `逻辑检查` · `去 AI 味（LaTeX 英文）` · `去 AI 味（Word 中文）` | [references/logic-and-anti-ai.md](references/logic-and-anti-ai.md) |
| 论文方法架构图（中/英 Prompt）、实验图表类型推荐、英文图/表标题生成、实验数据 → LaTeX 分析 | `论文架构图` · `实验绘图推荐` · `生成图的标题` · `生成表的标题` · `实验分析` | [references/figures-tables-and-experiments.md](references/figures-tables-and-experiments.md) |
| 整篇 PDF 论文顶会 Reviewer 视角审稿 + 改稿策略、写作/润色模型选型参考 | `论文整体以 Reviewer 视角进行审视` · `模型选择` | [references/reviewer-and-models.md](references/reviewer-and-models.md) |

## Cross-Cutting Principles

1. **LaTeX vs. Word format hygiene:**
   - **LaTeX tasks:** Keep source pure (no gratuitous `\textbf{}` / `\emph{}` / quotes, no `\item` lists in body paragraphs, avoid em-dashes `—`), preserve existing `\cite{}` / `\ref{}` / math `$...$`, and escape special characters (`\%`, `\_`, `\&`).
   - **Word tasks:** Output clean plain text with ZERO Markdown markers (`**`, `*`, `#`, `>`), and use Chinese full-width punctuation (`，。；：“”`) with proper spacing around English terms/math in Chinese manuscripts.
2. **Restraint threshold (`宁缺毋滥`):**
   - For Chinese polishing, logic red-line checks, and de-AI-ification, if the input is already clear, rigorous, and natural, **do not rewrite just to look busy** — return the original text unchanged and emit the explicit pass verdict specified in the reference prompt.
3. **Zero data fabrication:**
   - For experiment analysis and reviewer critiques, ground every statement strictly in provided data/PDF contents. Never invent improvements, numbers, or claims.
4. **Structured outputs:**
   - Follow each mode's exact `Part 1` / `Part 2` / `Part 3` layout (such as literal Chinese back-translation `[Translation]` and `[Modification Log]`) without extra conversational filler unless the user asks follow-up questions.
