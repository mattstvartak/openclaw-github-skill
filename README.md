# openclaw-github-skill

Teaches AI agents to manage GitHub repositories, pull requests, issues, releases, and workflows using the gh CLI. No API keys needed -- the agent uses the authenticated CLI directly.

Compatible with [Finch](https://github.com/mattstvartak/finch-core), [OpenClaw](https://github.com/openclaw), and any agent platform that loads SKILL.md files.

## What This Skill Covers

| Area | Capabilities |
|------|-------------|
| **Repositories** | Create (public/private), clone, fork, view, list |
| **Pull Requests** | Create, review, merge, close, check CI status, view diffs |
| **Issues** | Create, triage, label, assign, close, reopen |
| **Releases** | Create with auto-generated notes, upload assets, manage |
| **GitHub Actions** | List runs, view logs, re-run failed workflows, trigger manual runs |
| **Code Search** | Search code, issues, and PRs across repos |
| **Gists** | Create, list, view, edit |

## Prerequisites

The user must install and authenticate the GitHub CLI:

```bash
# Install: https://cli.github.com
gh auth login
```

The agent runs `gh` commands directly through the shell. No API tokens needed in config.

## Install

### Finch

```bash
git clone https://github.com/mattstvartak/openclaw-github-skill.git
cp -r openclaw-github-skill ~/.finch/skills/github-cli/
finch gateway restart
```

### OpenClaw

```bash
git clone https://github.com/mattstvartak/openclaw-github-skill.git
cp -r openclaw-github-skill ~/.agents/skills/github-cli/
```

Or place in any skills directory your agent scans.

## How It Works

This is a **SKILL.md file** (declarative, no code). It teaches the agent:

- The exact `gh` commands for every GitHub operation
- Common workflows (feature branch flow, triage issues, create releases, debug CI failures)
- Best practices (check CI before merging, use squash merges, use `--fill` for PRs)
- Command flags and options for each operation

The agent reads this skill and knows how to use `gh`. It runs commands via its shell execution tool.

## What the Agent Can Do With This Skill

- Create and manage GitHub repositories
- Open pull requests from the current branch with auto-filled descriptions
- Review PRs, approve, or request changes with comments
- Merge PRs with squash, rebase, or merge commit
- Create and triage issues with labels and assignees
- Create releases with auto-generated changelogs
- Monitor GitHub Actions runs and re-run failures
- Search code, issues, and PRs across repositories
- Create and manage gists for sharing code snippets

## Common Workflows the Agent Knows

**Feature branch flow:**
1. Create branch, make changes, push
2. `gh pr create --fill`
3. `gh pr checks` (wait for CI)
4. `gh pr merge --squash --delete-branch`

**Triage issues:**
1. `gh issue list --state open`
2. Review, label, and assign

**Create a release:**
1. Tag the commit
2. `gh release create v1.0.0 --generate-notes`

**Debug CI failure:**
1. `gh pr checks <number>`
2. `gh run view <id> --log`

## What the Agent Cannot Do

- Create a GitHub account (you do this)
- Authenticate (you run `gh auth login`)
- Access GitHub billing or organization settings
- Manage GitHub Apps or OAuth apps

## License

MIT
