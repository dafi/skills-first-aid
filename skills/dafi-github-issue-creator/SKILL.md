---
name: github-issue
description: Draft GitHub bug reports and feature requests in Markdown from the current repository state. Use when AI agent needs to review modified files, inspect the local diff, ask for any missing product or reproduction details, write a GitHub-ready issue body with the required sections, and copy the final text to the clipboard with pbcopy. Trigger this skill when the user asks to create or draft a GitHub issue, bug report, or feature request, or when the user writes `gbug` for a bug report or `gfeat` for a feature request.
---

# GitHub Issue

## Overview

Draft a GitHub issue from the current local changes before the user opens the tracker manually

Always inspect the modified files and git diff first, then write the issue in English and copy the final Markdown to the clipboard with `pbcopy`

Treat `gbug` as a direct request for a bug report and `gfeat` as a direct request for a feature request

## Workflow

1. Review the repository state first
2. Infer whether the user wants a bug report or a feature request
3. Extract the relevant behavior, intent, and impact from the modified files and diff
4. Ask concise follow-up questions only when a required section cannot be supported from the available evidence
5. Produce the final Markdown in the correct issue format
6. Copy the exact final Markdown to the clipboard with `pbcopy`

## Gather Context

Start with the working tree, not with assumptions

- check modified files with a non-destructive git status command
- inspect the relevant diff for files that appear tied to the request
- read the changed code when the diff alone is not enough to understand the behavior
- treat the modified files as the primary source of truth
- use the user prompt and follow-up answers only to fill gaps the diff cannot answer

If the diff is empty or unrelated to the request, say that clearly and ask for the missing context before drafting the issue

## Choose the Issue Type

Infer the issue type from the user request whenever possible

- use a bug report when the user wants to describe broken, incorrect, regressed, or unexpected behavior
- use a feature request when the user wants to propose an addition, enhancement, or new capability

If the intent is ambiguous, ask one short question before drafting

## Draft a Bug Report

Use this exact section order:

```markdown
Title

What happens?

What did you expect to happen?

Steps to reproduce
```

Write each section from the strongest evidence available

- `Title`: make it short, specific, and behavior-oriented
- `What happens?`: describe the current observed behavior clearly and concretely
- `What did you expect to happen?`: describe the correct or intended behavior
- `Steps to reproduce`: list the shortest reliable sequence that reproduces the problem

Ask follow-up questions only when the reproduction path or expected behavior cannot be inferred safely from the diff, file names, or prompt

Do not invent reproduction steps, user actions, environments, or regressions that are not supported by evidence

## Draft a Feature Request

Use this exact section order:

```markdown
Title

Feature description

Why is this useful?
```

Write each section from the strongest evidence available

- `Title`: make it short, specific, and outcome-oriented
- `Feature description`: explain what should be added or changed
- `Why is this useful?`: explain the problem solved, friction removed, or benefit created

Ask follow-up questions only when the user value, audience, or problem statement cannot be inferred safely from the diff and prompt

Do not fabricate business rationale, user pain, or workflow details that are not supported by evidence

## Writing Rules

- write in English
- produce GitHub-ready Markdown
- keep the wording direct and specific
- prefer concrete behavior over implementation jargon
- mention only details that are relevant to the issue
- avoid hedging when the evidence is clear
- avoid claiming certainty when the evidence is incomplete

When evidence is incomplete, use neutral wording such as `based on the current diff` or ask one targeted question instead of guessing

## Output Format

For a bug report, produce:

```markdown
# Title

## What happens?
...

## What did you expect to happen?
...

## Steps to reproduce
1. ...
2. ...
3. ...
```

For a feature request, produce:

```markdown
# Title

## Feature description
...

## Why is this useful?
...
```

Do not add extra sections unless the user explicitly asks for them

## Finalize

After writing the final Markdown:

1. copy the exact issue text to the clipboard with `pbcopy`
2. present the same Markdown in the response

If clipboard copy fails, report that clearly and still return the final Markdown
