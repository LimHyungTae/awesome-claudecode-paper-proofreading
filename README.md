<div align="center">
    <h1>Awesome Claude Code / Codex — Paper Proofreading</h1>
    <a href="https://github.com/LimHyungTae/awesome-claudecode-paper-proofreading"><img src="https://img.shields.io/badge/Claude_Code_+_Codex-Dual_Compatible-2b6cb0" /></a>
    <br />
    <br />
    <p align="center"><img src="https://github.com/user-attachments/assets/b2a97cb8-8535-4beb-b6af-2f641d1962c9" alt="Demo" width="95%"/></p>
    <p><strong><em>Detect first. Fix with confidence.</em></strong></p>
</div>

______________________________________________________________________

## :rocket: Overview

This repository is designed to work with **both Claude Code and Codex** while preserving the original proofreading philosophy.

The detailed instructions live in the `prompts/` folder. You can use them directly in a session, or copy/merge them into Codex-oriented workspace instructions such as `AGENTS.md`. For PhD theses in robotics, use [`prompts/04_thesis_proofreading.md`](prompts/04_thesis_proofreading.md).

The workflow remains **two-phase**: the agent detects and lists all issues with unique numbers `[1]`, `[2]`, `[3]`..., then waits. The user selects which issues to fix or discard before any file is modified.

______________________________________________________________________

## :bust_in_silhouette: About the Author

<p align="center"><img src="https://github.com/user-attachments/assets/4af4b29f-ce85-47a0-9472-406f2ca95572" alt="Hyungtae Lim" width="75%"/></p>

These prompts are distilled from years of hands-on paper reviewing and mentoring experience by **[Hyungtae Lim](https://github.com/LimHyungTae)**, a researcher in robotics and 3D perception.

- 📝 **[Associate Editor](https://www.ieee-ras.org/publications/ra-l/editorial-board/)**, IEEE Robotics and Automation Letters (RA-L)
- 🌟 **[RSS Pioneer 2024](https://sites.google.com/view/rsspioneers2024/participants)**
- 🎖️ **[ICRA 2025 Outstanding Reviewer](https://2025.ieee-icra.org/program/awards-and-finalists/#outstandingreviewer)** — selected from 7,400+ reviewers
- 📄 **Conducted 100+ paper reviews** across top robotics and CV venues

The review rules in these prompts reflect the standards expected at top robotics and computer vision venues, refined through real paper reviews and publications across ICRA, IROS, RSS, CVPR, ICCV, NeurIPS, AAAI, RA-L, T-RO, IJRR, T-PAMI, T-IV, etc.

______________________________________________________________________

## :page_facing_up: Files

### [`prompts/01_latex_workspace_review.md`](prompts/01_latex_workspace_review.md)

**LaTeX infrastructure audit** — detailed checklist for workspace-level errors before submission.

| Check | Description |
|-------|-------------|
| C1 | Preamble configuration (`hyperref`, `cleveref`, `caption` setup) |
| C2 | Package load order & conflicts |
| C3 | Macro safety, `\methodname` consistency, subscript macros, `\etalcite` |
| C4 | Cross-reference consistency (multi-ref, subcaption `Fig. 5(a)` format) |
| C5 | Label naming conventions, duplicate labels |
| C6 | Citation & bibliography integrity, duplicate BibTeX keys |
| C7 | Figure & table safety (missing files, dummy figures, label placement) |
| C8 | Hidden human errors (TODOs, inconsistent naming, `\vspace` hacks) |
| C9 | Academic writing patterns detectable in source (`\ie`, `\eg`, units) |

### [`prompts/02_paper_proofreading.md`](prompts/02_paper_proofreading.md)

**Paper content proofreading** — detailed checklist for strict conference-level review.

| Category | Description |
|----------|-------------|
| A | Language & grammar, tense consistency, Related Work tense |
| B | Language quality & awkward expression: typos, nominalization, filler phrases, citation-as-noun style |
| C | Scientific clarity: overclaiming, "significantly", unsupported claims |
| D | Structure & flow: intro claims, experiment purpose, equation narrative |
| E | Figure/table/caption review: self-containedness, reference order, quantitative consistency |
| F | LaTeX formatting: units, thousand separators, `\ie`/`\eg` macros |
| G | Abstract (WHY→PROBLEM→HOW→RESULTS) & conclusion quality |
| H | Notation consistency: symbol overload, boldface vectors, coordinate frames |
| I | Hyphenation: compound adjectives, `-ly` adverb rule |

### [`prompts/04_thesis_proofreading.md`](prompts/04_thesis_proofreading.md)

**PhD thesis proofreading (robotics)** — the paper checklist extended with checks for long, multi-chapter documents, from the perspective of an external examiner.

| Category | Description |
|----------|-------------|
| A | Thesis architecture: T-structure, chapters building on each other, research question traceability, consistent chapter structure |
| B | Chapter-level structure: chapter introductions and summaries, equation narrative, experiment purpose, real-robot validation |
| C | Paragraph flow and motivation reminders: paragraph logic, signposting, stale cross-references |
| D | Standalone and adjacent-field readability |
| E | Cross-chapter consistency and contradictions: claims, numbers, names, spelling variant, "we" vs "I" |
| F | Abbreviations across a long document: re-introduction after long gaps, per-chapter expansion, list of abbreviations |
| G | Heading hierarchy and casing: Title Case vs Sentence case, no lone subsections, stacked headings |
| H | Literature review coverage of every technical chapter, gaps, currency |
| I–P | Paper checks adapted to theses: language, paper leftovers ("in this paper"), claims, captions (short captions, attribution of reused figures), LaTeX, abstract/intro/conclusion, notation, hyphenation |
| Q | Front matter, back matter, and bibliography: statements of contribution, publication notices, appendices |

______________________________________________________________________

## :hammer: How to Use

There are two supported ways to use this repository.

### Setup — Clone this repo once

```bash
git clone https://github.com/LimHyungTae/awesome-claudecode-paper-proofreading.git ~/awesome-claudecode-paper-proofreading
```

### Option 1 — Claude Code direct prompt use

These prompts are used from **inside your paper workspace**, not from inside this repository.
The `@` file reference in Claude Code resolves paths relative to the directory where `claude` is launched.

### Step 1 — Navigate to your paper workspace and launch Claude Code

```bash
cd /path/to/your/paper
claude
```

### Step 2 — Run the workspace audit first

In the Claude Code session, reference the prompt by its **absolute path**, then attach your paper files:

```text
@~/awesome-claudecode-paper-proofreading/prompts/01_latex_workspace_review.md

@main.tex @shortcuts.tex
```

### Step 3 — Run the content proofreader

Provide the root `.tex` file and the compiled PDF. The prompt automatically instructs Claude to follow all `\input{...}` calls and read every included section file:

```text
@~/awesome-claudecode-paper-proofreading/prompts/02_paper_proofreading.md

@main.tex @paper.pdf
```

> **Why the PDF?**
> The compiled PDF lets Claude cross-check two things invisible in source alone:
> - **Figure placement** — figures displaced far from their in-text reference
> - **PDF-level annotations** — leftover review comments not yet resolved

### Step 4 — Decide which issues to fix

After Phase 1 output, respond with:

```text
discard 3, 7, 12    ← skip specific issues
fix all critical    ← fix only CRITICAL issues
proceed with all    ← fix everything
```

### Step 5 (theses) — Run the thesis proofreader

For a PhD thesis, use the thesis prompt instead of the paper prompt in Step 3. Provide the root `.tex` file and the compiled PDF; the PDF is needed for page distances, the List of Figures, and figure placement:

```text
@~/awesome-claudecode-paper-proofreading/prompts/04_thesis_proofreading.md

@thesis.tex @thesis.pdf
```

For long theses, `thesis-level only` and `show chapter X only` keep the review focused.

### Option 2 — Codex workspace setup with `prompts/`

Copy the `prompts/` directory into your paper or thesis workspace:

```bash
cp -R ~/awesome-claudecode-paper-proofreading/prompts /path/to/your/paper/
```

Launch Codex from the workspace root and point it at the prompt you want:

```
Follow prompts/01_latex_workspace_review.md for `main.tex`.
```

or

```
Follow prompts/04_thesis_proofreading.md for `thesis.tex` and `thesis.pdf`.
```

______________________________________________________________________

## :bulb: Design Principles

- **Detect first, fix later** — the agent never modifies files until the user explicitly confirms
- **Modular categories** — each check is a labeled block; reorder or disable by editing the table at the top of each prompt
- **Real-world patterns** — rules extracted from annotated paper reviews across ICRA, RA-L, AAAI, BMVC, and CVPR submissions
- **Non-native writer aware** — covers patterns common in papers by Korean/Japanese researchers
- **`figures/` vs `pics/`** — distinguishes final manuscript figures from raw image sources

______________________________________________________________________

## :computer: CI / Headless Use

This setup also works in CI or other non-GUI environments as long as the agent runs from the paper workspace and sees the relevant instructions.

Recommended pattern:

1. Check out your paper repository.
2. Copy in `prompts/`, or inline the prompt content into your workspace's `AGENTS.md`.
3. Ask the agent to run the workspace review or proofreading pass.

______________________________________________________________________

## :link: Related

- [paper-writing-checklist](https://github.com/LimHyungTae/paper-writing-checklist) — LaTeX workspace guidelines referenced by these prompts in Korean
