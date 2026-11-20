# How to Read a Paper: Agent Skill

A portable agent skill that teaches AI coding assistants (Claude, OpenCode, and others that support the `SKILL.md` format) how to read technical and academic papers with more care and better retention.

Adapted from Jason Eisner's [*How to Read a Technical Paper*](http://cs.jhu.edu/~jason/advice/how-to-read-a-paper.html) (2009).

## What it does

When loaded, this skill guides the agent to:

- Skim first, with a time budget, before committing to a careful read
- Set reading depth by purpose: why you're reading decides how deep you go
- Take low-level notes. Restate unclear points, fill in missing steps, and invent examples that illustrate the ideas as well as examples that break them
- Write a high-level distillation in plain language, with a citation and URL, so you can recall the paper later
- Read creatively, not just critically. Look for the good ideas, the extensions, and the next steps
- Focus effort by section. Read the motivation in full, skim math you already know or that is ad hoc or too advanced for now, and grasp a method's interface even when you skip its internals
- Scrutinize the experiments when the conclusions matter
- Track references backward and forward to build context
- Find papers through creative search, citation chasing, surveys and syllabi, and background reading

## Installation

Clone the skill directly into the directory your tool loads skills from.

For OpenCode:

```sh
git clone https://github.com/thisisrick25/how-to-read-a-paper ~/.config/opencode/skills/how-to-read-a-paper
```

On Windows, the OpenCode skills directory is `C:\Users\<you>\.config\opencode\skills\`.

> **Restart required (OpenCode).** OpenCode builds its skill registry at session startup. After installing, start a **new session** so the skill is discovered and registered.

For any other SKILL.md-compatible agent (Claude, etc.), keep the `how-to-read-a-paper/` folder wherever that tool loads skills from. The `SKILL.md` frontmatter (`name`, and `description` with trigger phrases) is standard and portable.

If you are not sure where that is, check your tool's README, website, or usage docs for its skills directory and loading behavior. Paths and registration rules vary between tools.

## Usage

Once installed and registered, trigger it naturally:

- "Help me read this paper: `<url>`"
- "How do I read papers?"
- "Take notes on this paper for me"
- "Review this research paper"

The agent loads the skill and applies the multi-pass workflow: skim first, then do a purpose-driven deep read with structured notes and a creative critique.

## Source & credit

Workflow adapted from **Jason Eisner's** ***["How to Read a Technical Paper" (2009)](http://cs.jhu.edu/~jason/advice/how-to-read-a-paper.html)***.

Incorporates ideas referenced therein from:

- [Keshav](https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf): the three-pass method
- [Michael Mitzenmacher](https://www.eecs.harvard.edu/~michaelm/postscripts/ReadPaper.pdf): reading creatively, not just critically
- [Terry Tao](https://terrytao.wordpress.com/career-advice/ask-yourself-dumb-questions-and-answer-them/): ask yourself dumb questions (and answer them)
- [Delip Rao](https://deliprao.com/essays/): read several later papers before the original
