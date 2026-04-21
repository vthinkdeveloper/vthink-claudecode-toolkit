---
name: plan-research-build
description: A deliberate coding playbook — plan first, research externally when unsure, build manually with line-by-line confidence. Use when starting any non-trivial feature or change.
---

# Plan → Research → Build

A deliberate approach to agentic coding. Think before you type, verify before you ship.

## Overview

This playbook encodes a workflow where you plan carefully, use external research to resolve uncertainty, and make code changes with full awareness of each line. It avoids the trap of letting an agent write code you don't understand.

---

## Stage 1: Plan

Enter plan mode before writing a single line of code.

- Describe the problem clearly — what needs to change and why
- Read the relevant parts of the codebase to understand the current state
- Identify the smallest possible change that solves the problem
- Write the plan out explicitly — what files, what changes, what order
- **Do not proceed until you are satisfied with the plan**

If anything in the plan is unclear or uncertain, do not guess — move to Stage 2.

---

## Stage 2: Research

When you hit something uncertain — an API, a pattern, a library behaviour — stop and research it externally before writing code.

Use the `anonymize-prompt` skill to generate a safe, privacy-stripped version of your question:

```
Run the anonymize-prompt skill for: [describe your uncertainty]
```

Then take the anonymized prompt to your external research tools:

- **Google AI Mode** — best for broad explanations, language/framework behaviour, official docs synthesis
- **Perplexity** — best for targeted technical answers with citations

Rules:
- Never paste internal code, class names, URLs, or project names into external tools — always anonymize first
- Don't skip this step when uncertain — a 2-minute search prevents a 2-hour debugging session
- Bring the insight back and update your plan if needed before proceeding

---

## Stage 3: Build

Make code changes manually, with full awareness of each line.

- Follow the plan from Stage 1
- Change one logical unit at a time — don't batch unrelated changes
- For each change, ask: *do I understand why this line is here?*
- If a line feels uncertain, go back to Stage 2 before committing to it
- Use the `conventions-check` skill after changes to catch style/pattern drift:

```
Run the conventions-check skill on the changed files
```

---

## Stage 4: Verify

Before shipping, check your work.

- Read through the diff — every changed line, top to bottom
- For any line that gives you pause, use `anonymize-prompt` + external research to confirm it's correct
- Run tests if available (use the `test-runner` agent)
- Only ship when you can explain every line you changed

```
Use the test-runner agent to verify all tests pass
```

---

## Stage 5: Ship

Use the `ship` skill:

```
Run the ship skill
```

---

## Principles

- **Plan before code.** An hour of planning saves a day of debugging.
- **Uncertainty is a signal.** If you're not sure, research — don't guess.
- **Own every line.** If you can't explain it, don't ship it.
- **Anonymize before you paste.** External tools are powerful but don't get proprietary context.
