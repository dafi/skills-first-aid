---
name: technical-english-proofreader
description: >
  Check and rewrite input text in polished technical English for software and
  application contexts. Use when Codex receives Italian, English, or mixed text
  that needs grammar and syntax correction, translation into English, or
  refinement for code comments, bug reports, GitHub issues, commit notes,
  changelog entries, release notes, technical documentation, or
  programming-related posts. The text to proofread can be provided directly by
  the user, extracted from git-modified files (staged, unstaged, or a specific
  commit), or limited to a specific list of files.
---

# Technical English Proofreader

Rewrite the provided text into clear technical English suitable for software work.

---

## Input Sources

The text to proofread can come from three sources.
Detect which one applies from the user's request.

### 1. User-supplied text

The user pastes or types the text directly.
Use it as-is.

### 2. Git-modified files

When the user asks to proofread changes from git
(e.g. "check my staged changes", "proofread the diff"),
extract human-readable text from the diff:

- run `git diff` for unstaged changes, `git diff --cached` for staged changes,
  or `git diff <ref>` for a specific commit
- extract only added or modified lines (lines starting with `+`,
  excluding the `+++` header)
- skip binary files, generated files, and lock files
  (`*.lock`, `package-lock.json`, `yarn.lock`, etc.)
- extract prose and identifiers from: comments, docstrings, string literals,
  commit messages, markdown files, changelog entries, README files
- ignore pure code logic lines unless they contain inline comments
  or string literals with prose

### 3. Specific files

When the user provides a list of files
(e.g. "proofread CHANGELOG.md and README.md"),
read those files directly and extract human-readable text
using the same rules as above.

---

## Workflow

1. Identify the input source (user text / git diff / specific files)
2. Extract the text to proofread according to the rules above
3. Detect the source language of each extracted fragment
4. Preserve the original intent, factual meaning, and technical terminology
5. Correct grammar, syntax, spelling, wording, and punctuation
6. Translate to English when the source is not already English
7. Normalize the tone for technical communication
8. Return the corrected text grouped by file or section
   when the input comes from multiple files

---

## Output Rules

- Always return English, even when the source text is Italian
- Prefer concise wording that reads naturally in code comments,
  bug reports, issues, and developer discussions
- Keep domain terms, API names, identifiers, filenames, commands,
  and error strings unchanged unless the input clearly contains a typo
- Preserve structure when the input is already organized
  as paragraphs, bullets, or short labels
- Remove filler, repetition, and informal phrasing when they reduce clarity
- Do not add new technical claims, steps, or assumptions
- When the input comes from files, show the filename as a header
  before its corrected content
- When a line or fragment needs no changes, omit it from the output
  unless the user asks for a full rewrite

---

## Style Targets

- Use direct and neutral language
- Prefer terminology appropriate for application development
  and programming discussions
- Favor precise verbs such as `fail`, `return`, `update`, `remove`,
  `prevent`, or `trigger` over vague phrasing
- Keep comments and issue text compact unless the input requires
  more detail for clarity

---

## Response Shape

- Return only the improved English text unless the user explicitly asks
  for alternatives, explanations, or multiple variants
- When the input is a short fragment, return a short fragment
  rather than expanding it into a full paragraph
- When the input contains multiple items, keep them separated in the output
- When the input comes from a git diff or file list, group output by filename
  and show only the changed or corrected fragments