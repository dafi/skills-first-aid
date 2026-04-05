---
name: technical-english-proofreader
description: Check and rewrite input text in polished technical English for software and application contexts. Use when Codex receives Italian, English, or mixed text that needs grammar and syntax correction, translation into English, or refinement for code comments, bug reports, GitHub issues, commit notes, changelog entries, release notes, technical documentation, or programming-related posts.
---

# Technical English Proofreader

Rewrite the provided text into clear technical English suitable for software work.

## Workflow

1. Detect the source language
2. Preserve the original intent, factual meaning, and technical terminology
3. Correct grammar, syntax, spelling, wording, and punctuation
4. Translate to English when the source is not already English
5. Normalize the tone for technical communication
6. Return the final text in English

## Output Rules

- always return English, even when the source text is Italian
- prefer concise wording that reads naturally in code comments, bug reports, issues, and developer discussions
- keep domain terms, API names, identifiers, filenames, commands, and error strings unchanged unless the input clearly contains a typo
- preserve structure when the input is already organized as paragraphs, bullets, or short labels
- remove filler, repetition, and informal phrasing when they reduce clarity
- do not add new technical claims, steps, or assumptions

## Style Targets

- use direct and neutral language
- prefer terminology appropriate for application development and programming discussions
- favor precise verbs such as `fail`, `return`, `update`, `remove`, `prevent`, or `trigger` over vague phrasing
- keep comments and issue text compact unless the input requires more detail for clarity

## Response Shape

- return only the improved English text unless the user explicitly asks for alternatives, explanations, or multiple variants
- when the input is a short fragment, return a short fragment rather than expanding it into a full paragraph
- when the input contains multiple items, keep them separated in the output
