# skills-first-aid

A collection of AI skills for developers, focused on quick fixes and productivity improvements.

## Available Skills

- **dafi-conventional-commit-generator**: Generate proper Conventional Commit messages.
- **dafi-github-issue-creator**: Create GitHub issues in a clean, consistent format.
- **dafi-english-translator-proofreader**: Translate and proofread technical English.

## Installation

### Codex

#### Local Repository Installation (Recommended)

Clone the repository:

```bash
git clone https://github.com/dafi/skills-first-aid.git
```

Then create the symlinks:

```bash
cd skills-first-aid
ln -sfn $PWD/skills/* ~/.codex/skills
```

#### Installation with `skill-installer`

Install each skill individually:

```bash
$skill-installer install https://github.com/dafi/skills-first-aid/tree/main/skills/dafi-conventional-commit-generator
$skill-installer install https://github.com/dafi/skills-first-aid/tree/main/skills/dafi-english-translator-proofreader
$skill-installer install https://github.com/dafi/skills-first-aid/tree/main/skills/dafi-github-issue-creator
```
