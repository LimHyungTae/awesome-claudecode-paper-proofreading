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


- [Agent Shadow Brain](https://github.com/theihtisham/agent-shadow-brain) - Self-evolving AI coding intelligence with infinite memory (TurboQuant), genetic algorithm self-evolution, predictive bug detection, PageRank knowledge graphs, swarm intelligence, and adversarial defense.
- [Omni Skills Forge](https://github.com/theihtisham/omni-skills-forge) - 50,000+ curated AI agent skills for Claude Code, Cursor, Copilot, Windsurf, Cline. Visual dashboard, one-click install, skill doctor, auto-update.
This repository is designed to work with **both Claude Code and Codex** while preserving the original proofreading philosophy.

The detailed instructions live in two prompt files. You can use them directly in a session, or copy/merge them into Codex-oriented workspace instructions such as `AGENTS.md`.

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

### [`AGENTS.md`](AGENTS.md)

Optional Codex coordinator instructions for the workflow:

- detects first and waits before editing
- chooses between workspace audit and paper proofreading
- reads the full LaTeX workspace recursively
- applies only approved fixes in Phase 2
- points Codex to the authoritative prompt files

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

### Option 2 — Codex workspace setup with `AGENTS.md` plus `prompts/`

Copy `AGENTS.md` and the `prompts/` directory into your paper workspace:

```bash
cp ~/awesome-claudecode-paper-proofreading/AGENTS.md /path/to/your/paper/AGENTS.md
cp -R ~/awesome-claudecode-paper-proofreading/prompts /path/to/your/paper/
```

Launch Codex from the paper root so it can pick up `AGENTS.md`, then ask for the workflow you want:

```
Run the LaTeX workspace review on `main.tex`.
```

or

```
Proofread `main.tex` against `paper.pdf`.
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
2. Copy in `AGENTS.md` plus `prompts/`, or inline the prompt content into one file.
3. Ask the agent to run the workspace review or proofreading pass.

______________________________________________________________________

## :link: Related

- [paper-writing-checklist](https://github.com/LimHyungTae/paper-writing-checklist) — LaTeX workspace guidelines referenced by these prompts in Korean
