---
name: how-to-read-a-paper
description: Read technical and academic papers efficiently and critically. Use when reading, studying, reviewing, or taking notes on a research paper, conference paper, journal article, or preprint; when learning a new research area; when deciding which papers to read; or when trying to understand a paper deeply enough to critique, extend, or build on it. Triggers - "read this paper", "how do I read papers", "help me understand this paper", "take notes on a paper", "review a paper", "study this research", "which papers should I read".
---

# How to Read a Technical Paper

A workflow for reading technical and academic papers efficiently, critically, and with lasting retention. Adapted from Jason Eisner's ["How to Read a Technical Paper"](http://cs.jhu.edu/~jason/advice/how-to-read-a-paper.html) (2009).

## Core Principle

Reading a paper is active work, not passive consumption. You read to *take something away* — understanding, ideas, techniques, or a critical judgment. Invest your time in proportion to why you are reading and what you need to extract.

## The Workflow

### 1. Multi-pass reading

Never read a paper start-to-finish on the first pass.

- **Pass 1 — Skim.** Skip anything that takes mental effort. Get the shape of the paper: where it's going, why it was written, what's old hat vs. new. Use a time budget per page to force momentum.
- **Pass 2 — Read carefully.** Only if the paper still seems worthwhile. Now go deep on the parts that matter (see "Which parts to focus on").
- Optionally follow Keshav's [three-pass method](https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf): each pass has a distinct goal (grasp, grasp content, fully understand).

### 2. Write as you read

Writing keeps attention focused and forces engagement. Produce two kinds of notes.

**Low-level notes** (in-context, on the paper or PDF):
- Restate unclear points in your own words
- Fill in missing details: assumptions, algebraic steps, proofs, pseudocode
- Annotate mathematical objects with their types
- Invent examples that illustrate the ideas — *and* examples that break them
- Draw connections to other methods and problems you know
- Ask questions about things unstated or confusing
- Challenge the paper's claims or methods
- Dream up follow-up work

**High-level notes** (a distillation for your future self):
- Summarize what interested you; contrast with other papers; record your own questions and ideas
- Re-explain the key ideas in your own words — enough to reconstruct your understanding later
- Don't repeat what's easy for you. Do write down hard-won insight, e.g.:
  > "Equation (2) is basically Pookie (2001) plus a reconfabulation step after the data purée. Their reconfabulator surprised me — it doesn't match Kachu (2004) — but it cures the exponential growth problem here. This example made the difference clear: ..."
- **Read creatively, not just critically** ([Mitzenmacher](https://www.eecs.harvard.edu/~michaelm/postscripts/ReadPaper.pdf)): tearing down is easy. Ask instead — what are the *good* ideas? Do they extend or generalize? What practical improvements are possible? If you started research from this paper, what would you do next?

**Organizing notes:**
- Sort chronologically by read date (helps you recall vaguely-remembered papers and what else you were reading then)
- Start each entry with a rough citation (author/title/year) so you can search later
- Include a URL to the original; reference "Figure 1", "equation (2)", "section 3.3" as needed
- If a point took real effort to understand, consider improving the relevant Wikipedia page

### 3. When and where to read

- **Start early.** Leave slack so you can put the paper down when your attention wanders and return in a better mood. Don't force it against a deadline.
- Exploit habits and place: read while eating, walking, on an exercise bike; leave papers where you naturally pick things up to read.
- **Read with a friend.** Sit together, stay synchronized sentence-by-sentence, read aloud through hard parts, discuss as you go. You keep each other moving.

### 4. Set aside enough time

- A conference paper in a new area can take *hours* to read thoroughly. That is normal and worth it for a good or foundational paper.
- It gets faster: ideas recur across papers, and familiar motivation/setup lets experts read a paper in 30 minutes.
- **There is no shame in reading slowly.** Even experts spend hours on genuinely unfamiliar material, and reviewing takes hours because the burden is to find every flaw.

## Which parts to focus on

You don't always have to read every detail on pass 2. It depends on *why* you're reading. When learning a new area, read at least *some* papers extremely thoroughly — know what every sentence and subscript does, and *why* things were done that way. [Ask yourself dumb questions and answer them.](https://terrytao.wordpress.com/career-advice/ask-yourself-dumb-questions-and-answer-them/) This sharpens the critical eye you'll turn on your own work.

By section:

- **Motivation** — Understand this well, or there's no point reading. If motivation depends on background/prior work you lack, you may defer chasing those references and just raise their priority on your reading list.

- **Mathematics & algorithms** — The technical heart. Don't habitually skim. But you *may* skim a technical section when:
  - It explains something you already know (just verify it says what you expect)
  - This paper is a poor place to learn the method, or it's too advanced right now (understand what you can, then list it to learn properly — ask someone or find a better source)
  - It's an ugly *ad hoc* solution no one would use (still grasp the authors' intuitions; think how to capture them more elegantly)
  - It's enough for now to know the method *exists* and is specialized. Even then, get clarity on its **interface**: what it accomplishes, when it applies, how hard it is to use, what drives its runtime and accuracy. Skip only the internal **implementation** and correctness/efficiency proofs.

- **Experiments** — When new to a field, study carefully *how* evaluation is done (and whether you approve). Note datasets and code you might reuse. Once experienced, you may skim experimental detail if you're only reading for inspiration — but examples and error analysis often shed light. **If you care whether the method actually worked / whether to use it,** examine the experimental design and data rigorously: Were experiments fair? Do they support the claims? Will conclusions generalize beyond this scenario?

**Invest time wisely — extract what's valuable.** If you can't tell which parts are most important, *ask someone who knows.* If you don't know who to ask, find papers citing this one (via [Google Scholar](http://scholar.google.com)) and see what they say about it.

> [Delip Rao](https://deliprao.com/essays/): "Never read the original paper on X first. Read several later papers on what they say about X, get an idea of X, then read the original. The research community often explains ideas more clearly than the original authors."

## What to read (finding papers)

- **Creative web search** — try several searches; think like an author about phrasing; learn your search engine's power features; search [ACL Anthology](http://aclweb.org/anthology-new), [Google Scholar](http://scholar.google.com), etc.
- **Track related work** from a relevant paper:
  - *Backward references* — follow the bibliography to earlier work
  - *Forward references* — see who cites it (Google Scholar)
- **Reuse others' curation** — survey/review articles, course syllabi, reading-group pages, textbook chapters, online tutorials, dissertation literature-review chapters, direct recommendations from friends/professors.
- **Breadth-first exploration** — read many abstracts before choosing what to read deeply; read related papers together so they clarify each other; skim a recent workshop/conference proceedings to feel the research landscape.
- **When the going gets tough, switch to background reading** — textbooks, tutorials, review articles, dissertation intros/lit reviews, heavily-cited early papers, sometimes Wikipedia.

## Quick Checklist

- [ ] Skim first (time-boxed) before committing to a careful read
- [ ] Decide *why* you're reading — set the depth accordingly
- [ ] Take low-level notes (questions, restatements, examples, filled-in steps)
- [ ] Write a high-level distillation in your own words, with citation + URL
- [ ] Read creatively: identify good ideas, extensions, improvements, next steps
- [ ] Focus effort — read motivation fully; skim known/ad-hoc/too-advanced sections; grasp method interfaces even when skipping internals
- [ ] Scrutinize experiments if you care about the conclusions
- [ ] Track backward and forward references to build context
- [ ] When stuck, drop to background reading, or ask someone

## Source

Workflow adapted from **Jason Eisner's** ***["How to Read a Technical Paper" (2009)](http://cs.jhu.edu/~jason/advice/how-to-read-a-paper.html)***.

Incorporates ideas referenced therein from:

- [Keshav](https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf) — "How to Read a Paper" (the three-pass method)
- [Michael Mitzenmacher](https://www.eecs.harvard.edu/~michaelm/postscripts/ReadPaper.pdf) — "How to Read a Research Paper" (reading creatively, not just critically)
- [Terry Tao](https://terrytao.wordpress.com/career-advice/ask-yourself-dumb-questions-and-answer-them/) — "Ask yourself dumb questions – and answer them"
- [Delip Rao](https://deliprao.com/essays/) — read several later papers before the original
