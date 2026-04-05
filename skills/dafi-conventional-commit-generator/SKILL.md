---
name: conventional-commit-comment
description: Draft a short conventional-commit message from a rough change description or local repository context. Use when the user asks for a commit message, commit comment, conventional commit, ccm, concise commit summary, or wants to turn `$DESC`, modified files, staged changes, or branch context into a conventional-commit line. The skill cleans up grammar in the starting text, infers the commit type from the current git branch when possible, asks the user to choose the scope from changelog-scopes.local.md in the current directory, proposes up to 3 short alternatives, and copies the selected final message to the clipboard.
---

# Conventional Commit Comment

Create a short conventional-commit message from the user's starting text or from local repository context.

Keep the workflow interactive and deterministic. Ask for decisions only in this order:
1. `type`
2. `scope`
3. final description choice

## Workflow

1. Inspect the user's request and extract `$DESC` if provided
2. If `$DESC` is present:
   - check grammar and syntax
   - rewrite it into a shorter conventional-commit description
3. If `$DESC` is absent:
   - tell the user you need a starting point
   - offer to proceed using the modified files, staged diff, branch context, or another short description they provide
4. Determine the commit `type`
5. Ask the user to choose the `scope`
6. Produce at most 3 final commit-message alternatives
7. Ask the user to choose one
8. Copy the selected message to the clipboard with `pbcopy`

## Type Selection

Try to infer the commit `type` from the current git branch name first.

Use a direct mapping when the branch name clearly contains one of these tokens or an obvious variant:
- `feat`
- `fix`
- `docs`
- `style`
- `refactor`
- `perf`
- `test`
- `chore`
- `build`

If the branch name does not provide a reliable answer, ask the user to choose from this numbered list:
1. `feat`
2. `fix`
3. `docs`
4. `style`
5. `refactor`
6. `perf`
7. `test`
8. `chore`
9. `build`

If you ask for both `type` and `scope`, always ask for `type` first.

## Scope Selection

Read `changelog-scopes.local.md` from the current working directory and build a numbered list of scopes from its entries.

Offer those scopes to the user as a numbered list and let them choose exactly one.

If the selected scope is `none`, omit the scope from the final conventional-commit string.

## Description Rules

Keep the description as short as possible while still describing the code change.

Follow conventional-commit style:
- use lowercase
- use an imperative summary
- avoid trailing punctuation
- focus on the change, not the process
- avoid unnecessary detail

When proposing final options:
- generate at most 3 alternatives
- keep them very short
- use the chosen `type`
- include the chosen `scope` only if it is not `none`

Format alternatives exactly as a numbered list of full conventional-commit messages, for example:
1. `fix(parser): handle multiple spaces in array values`
2. `fix(parser): preserve array parsing with repeated spaces`
3. `fix: handle multiple spaces in array values`

## Clipboard

After the user picks one alternative, copy the exact selected message to the clipboard using `pbcopy`.

Confirm which message was copied.

## Notes

- Prefer using local repository evidence when shortening the description if the user did not provide enough detail
- Do not skip the user choice for `scope`
- Do not skip the user choice for the final description
- If the scopes file is missing or unreadable, say so briefly and continue by asking the user for the scope explicitly
