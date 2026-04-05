# openclaw-github-skill

Teaches AI agents to manage GitHub repositories, pull requests, issues, releases, and Actions using the gh CLI.

## What It Does

This is a SKILL.md file (declarative, no code) that gives agents knowledge of GitHub CLI commands for:

- Creating and managing repositories
- Opening, reviewing, and merging pull requests
- Creating and triaging issues
- Creating releases with auto-generated notes
- Monitoring GitHub Actions CI/CD
- Searching code, issues, and PRs
- Managing gists

## Prerequisites

The user must authenticate via the GitHub CLI before the agent can use it:

```bash
# Install gh: https://cli.github.com
gh auth login
```

## Install

### Finch

```bash
cp -r . ~/.finch/skills/github-cli/
finch gateway restart
```

### OpenClaw

```bash
cp -r . ~/.agents/skills/github-cli/
```

Or place in any skills directory your agent scans.

## Compatibility

- Finch (SKILL.md format with YAML frontmatter)
- OpenClaw (AgentSkills spec)
- Any agent platform that loads SKILL.md files

## License

MIT
