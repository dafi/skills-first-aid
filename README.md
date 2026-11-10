# skills-first-aid

A collection of AI skills for developers, focused on quick fixes and productivity improvements.

## Available Skills

- **dafi-conventional-commit-generator**: Generate proper Conventional Commit messages.
- **dafi-github-issue-creator**: Create GitHub issues in a clean, consistent format.
- **dafi-english-translator-proofreader**: Translate and proofread technical English.
- **dafi-opendoc**: Generate or update OpenAPI documentation for changed REST resources.

## Installation

### Claude Code

#### Plugin Marketplace Installation (Recommended)

This repository is a Claude Code plugin marketplace. Each skill is published as a separate plugin, so you can install only the ones you need:

```
/plugin install conventional-commit-generator --marketplace dafi/skills-first-aid
/plugin install github-issue-creator --marketplace dafi/skills-first-aid
/plugin install english-translator-proofreader --marketplace dafi/skills-first-aid
/plugin install opendoc --marketplace dafi/skills-first-aid
```

On older Claude Code versions, add the marketplace first and then install the plugins:

```
/plugin marketplace add dafi/skills-first-aid
/plugin install conventional-commit-generator@skills-first-aid
```

#### Local Repository Installation

Clone the repository:

```bash
git clone https://github.com/dafi/skills-first-aid.git
```

Then create the symlinks:

```bash
cd skills-first-aid
ln -sfn $PWD/skills/* ~/.claude/skills
```


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
