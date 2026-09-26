<h1 align="center">talk-skills</h1>

<p align="center">
  Four steps to say it right: skeleton → audience → tone → read as the reader.<br/>
  An expression standard shared by AI agents and humans.
</p>

<p align="center">
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/license-MIT-0f766e.svg" /></a>
  <img alt="Skills" src="https://img.shields.io/badge/skills-6-111827.svg" />
  <img alt="Claude Code" src="https://img.shields.io/badge/Claude%20Code-ready-d97706.svg" />
  <img alt="Codex" src="https://img.shields.io/badge/Codex-ready-111827.svg?logo=openai&logoColor=white" />
  <img alt="Cursor" src="https://img.shields.io/badge/Cursor-ready-000000.svg" />
</p>

---

Writing docs, filing tickets, posting updates, customer service — **when the content is right but nobody reads it, or it smells like generic robotic AI generation**, it's usually not the content's fault. It's these four steps done out of order, plus a lack of atomic granularity for audience minds:

```
① Skeleton   conclusion-first · SCQA · MECE (no overlap, no gaps)
② Audience   for human vs agent; up vs across; platform audience psychology
③ Tone       situational attribution · self-disclosure · anti-AI · no fake platitudes
④ Read-aloud read as a first-time reader, check against a list
```

The cost of skipping ④, measured: a 9,918-word technical report, after a read-aloud pass, surfaced 20 problems — **19 only found by reading**. Content drift into adjacent sections, references to deleted chapters, the same document contradicting itself in two places. Linters only catch leftover wording.

## Six skills and atomic matrix

| Skill / Matrix | Covers | When to use |
|---|---|---|
| **how-to-write** | The full method — the four steps above | Before writing anything meant to be read by someone else |
| **atomic-matrix** | **5D Atomic Expression Matrix**: [View CheatSheet](skills/atomic-matrix.md) | Composing custom [Who]×[Where]×[Scenario]×[Tone] blocks |
| **platform-voices** | Platform mindsets: NetEase/Xiaohongshu/X/GitHub/WeChat | Publishing on specific media with platform-native voices |
| **scenario-openers** | Scenario openers & Anti-AI authenticity guide | Customer inquiries, issue handling, hook phrases, killing AI taste |
| **peer-facing-writing** | Written peer communication: ticket skeleton, per-sentence substitution table | Issues, review comments, cross-team reports |
| **talk-text-review** | Talk posture: is this an "I'll teach you" or a "let's talk" piece | Before sharing with peers or seniors |
| **talk-visual-review** | Visual acceptance for the deck | Before producing the final visual |


## Drop-in ready

```bash
git clone git@github.com:webkubor/talk-skills.git
cp -r talk-skills/skills/* ~/.claude/skills/     # Claude Code
```

Install paths for other agents, plus the reasoning behind each rule, in [AGENTS.md](AGENTS.md).

## What it doesn't cover

Expression splits into four layers. This repo owns only the first; the rest live elsewhere with no overlap:

| What to say | What it looks like | How it's spoken | Where you write |
|---|---|---|---|
| **talk-skills** | [facet](https://github.com/webkubor/facet) | [voxflow](https://github.com/webkubor/voxflow) | [typora-Bloom-theme](https://github.com/webkubor/typora-Bloom-theme) |
| structure · tone · attribution | type scale · whitespace · pagination · rendering | voice design · stage presence · pacing | editor environment |

Quick ownership test: "what should I say, in what order, will this offend?" → this repo. "How big a font, how much whitespace?" → facet. "How do I deliver this line?" → voxflow. Full breakdown in [BOUNDARY.md](BOUNDARY.md).

## Why the rules look like this

Every tone rule is anchored to a psychological mechanism, not "be nicer":

- **Fundamental attribution error** → don't write "your test method is wrong"; write "this trap isn't visible from the UI" (attribute to the situation, not the person)
- **Face threat** → imperative tone triggers defensiveness; people protect ego before processing information
- **Backfire effect** → "you're wrong" makes people dig in harder, especially in tickets with third-party observers
- **Self-disclosure lowers defense** → if you've stepped in the same hole, say so first

Structure follows the Pyramid Principle (Barbara Minto): conclusion first, top-down, grouped (MECE), logical progression.

MIT License.