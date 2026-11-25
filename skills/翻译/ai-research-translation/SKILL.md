---
name: ai-research-translation
description: >
  Translate academic paper snippets between Chinese and English for LaTeX or Word workflows.
  Extracted and adapted from Leey21/awesome-ai-research-writing translation prompts
  (中转英-latex, 英转中-latex, 中转英-word). Use when the user asks to translate a Chinese
  draft into top-venue English LaTeX or Word prose with a literal Chinese back-translation check,
  or translate English LaTeX snippets into faithful, readable Chinese text without citation or
  macro clutter.
---

# AI Research Translation

Fast, single-pass academic translation workflows tailored for computer science / AI research drafting in **LaTeX** and **Microsoft Word**, derived from [Leey21/awesome-ai-research-writing](https://github.com/Leey21/awesome-ai-research-writing).

> **Scope note:** Use this skill for fast snippet/paragraph-level translation tailored directly to LaTeX or Word copy-paste. For full-paper arXiv/PDF pipelines, built-in venue glossaries, or three-step literal → reflection → polishing workflows (`直译 → 反思 → 雅化`), prefer [`academic-translation`](../academic-translation/SKILL.md).

## Mode Routing

Before executing a translation, identify the user's source/target format and **read the corresponding reference file**:

| Scenario | Source → Target | Output Format | Reference to Load |
|---|---|---|---|
| **中转英 (LaTeX)** | Chinese draft → English LaTeX snippet | `Part 1 [LaTeX]` + `Part 2 [Translation]` | [references/zh-to-en-latex.md](references/zh-to-en-latex.md) |
| **英转中 (LaTeX)** | English LaTeX snippet → Chinese prose | Clean Chinese paragraph(s), no LaTeX tags | [references/en-to-zh-latex.md](references/en-to-zh-latex.md) |
| **中转英 (Word)** | Chinese draft → English plain text for Word | `Part 1 [English Draft]` + `Part 2 [Translation]` | [references/zh-to-en-word.md](references/zh-to-en-word.md) |

If the user does not specify LaTeX vs. Word when translating Chinese to English:
- If the input contains LaTeX macros (`\cite`, `\ref`, `\textbf`, `\%`, etc.) or the context is a `.tex` project, use **中转英 (LaTeX)**.
- Otherwise, ask briefly or default to **中转英 (Word)** when plain text / `.docx` is clearly intended.

## Key Contrasts Across Modes

1. **Special character escaping:**
   - **LaTeX mode (`zh-to-en-latex`):** MUST escape LaTeX special characters (`95%` → `95\%`, `model_v1` → `model\_v1`, `R&D` → `R\&D`) while keeping `$...$` math formulas intact.
   - **Word mode (`zh-to-en-word`):** MUST NOT add backslash escapes (`95%`, `model_v1`, `R&D` stay raw) and MUST NOT emit Markdown formatting (`**`, `*`, `#`, `>`), while preserving `$` delimiters for Word equation entry.
2. **English output style (`zh-to-en-*`):**
   - Top-venue reviewer standard (ICML / ICLR / NeurIPS / ACL): concise, rigorous, natural, free of AI clichés.
   - Avoid bold/italics/unnecessary quotes, avoid em-dashes (`—`, prefer clauses or appositives), and never output bullet lists (`\item` or bullets) — write cohesive paragraphs.
   - Use present tense for methods, architectures, and experimental conclusions; past tense only for specific historical events.
   - Always include `Part 2 [Translation]` (literal Chinese back-translation) so the author can verify semantic fidelity, and omit extraneous chatter.
3. **English-to-Chinese comprehension (`en-to-zh-latex`):**
   - Strip `\cite{...}`, `\ref{...}`, `\label{...}` completely; extract inner text from `\textbf{text}` / `\emph{text}`; render LaTeX math into readable natural language or plain symbols (e.g., `$\alpha$` → `alpha`, `\frac{a}{b}` → `a/b`).
   - Translate strictly and literally, preserving English sentence structure and even awkwardness/errors without silent polishing, so the reader can map back 1:1 to the source.
