---
name: github-cli
description: Manage GitHub repositories, pull requests, issues, releases, and workflows using the gh CLI. Use when creating repos, opening PRs, managing issues, checking CI status, creating releases, managing GitHub Actions, reviewing code, or any GitHub-related task. The user has authenticated via gh auth login -- Finch has direct access.
---

# GitHub CLI

Manage repos, PRs, issues, releases, and Actions via the `gh` CLI. The user has already authenticated -- you have full access.

## Repositories

```bash
# Create a new repo
gh repo create my-repo --public --description "My project"
gh repo create my-repo --private --source=. --push

# Clone a repo
gh repo clone owner/repo

# View repo info
gh repo view owner/repo

# List your repos
gh repo list --limit 20

# Fork a repo
gh repo fork owner/repo --clone
```

## Pull Requests

```bash
# Create a PR from current branch
gh pr create --title "Add feature" --body "Description here"

# Create with auto-fill from commits
gh pr create --fill

# List open PRs
gh pr list

# View PR details
gh pr view 123

# Check out a PR locally
gh pr checkout 123

# Merge a PR
gh pr merge 123 --squash --delete-branch

# Review a PR
gh pr review 123 --approve
gh pr review 123 --request-changes --body "Fix the tests"

# Close a PR
gh pr close 123

# View PR diff
gh pr diff 123

# View PR checks/CI status
gh pr checks 123
```

## Issues

```bash
# Create an issue
gh issue create --title "Bug: login broken" --body "Steps to reproduce..."
gh issue create --title "Feature request" --label "enhancement"

# List issues
gh issue list
gh issue list --label "bug" --state open

# View issue
gh issue view 42

# Close an issue
gh issue close 42 --comment "Fixed in #45"

# Reopen an issue
gh issue reopen 42

# Add labels
gh issue edit 42 --add-label "priority:high"

# Assign
gh issue edit 42 --add-assignee username
```

## Releases

```bash
# Create a release
gh release create v1.0.0 --title "Version 1.0.0" --notes "First stable release"

# Create from tag with auto-generated notes
gh release create v1.2.0 --generate-notes

# Upload assets to a release
gh release upload v1.0.0 ./dist/app.zip

# List releases
gh release list

# View a release
gh release view v1.0.0

# Delete a release
gh release delete v1.0.0
```

## GitHub Actions / CI

```bash
# List workflow runs
gh run list

# View a specific run
gh run view 12345

# Watch a running workflow
gh run watch 12345

# Re-run a failed workflow
gh run rerun 12345

# View workflow logs
gh run view 12345 --log

# List workflows
gh workflow list

# Trigger a workflow manually
gh workflow run build.yml
```

## Code Browsing

```bash
# Search code in a repo
gh search code "function login" --repo owner/repo

# Search issues
gh search issues "bug login" --repo owner/repo

# Search PRs
gh search prs "feature" --state open

# View a file on GitHub
gh browse src/index.ts

# Open repo in browser
gh browse
```

## Gists

```bash
# Create a gist
gh gist create file.txt --public --desc "My snippet"

# List your gists
gh gist list

# View a gist
gh gist view <gist-id>

# Edit a gist
gh gist edit <gist-id>
```

## Common Workflows

**Feature branch workflow:**
1. `git checkout -b feature/my-feature`
2. Make changes, commit
3. `git push -u origin feature/my-feature`
4. `gh pr create --fill`
5. `gh pr checks` (wait for CI)
6. `gh pr merge --squash --delete-branch`

**Triage issues:**
1. `gh issue list --state open --limit 50`
2. `gh issue view <number>` for details
3. `gh issue edit <number> --add-label "bug"` to categorize
4. `gh issue edit <number> --add-assignee username` to assign

**Create a release:**
1. `git tag v1.0.0`
2. `git push origin v1.0.0`
3. `gh release create v1.0.0 --generate-notes`

**Check why CI failed:**
1. `gh pr checks <pr-number>`
2. `gh run view <run-id> --log`

## Important

- Always check CI status before merging PRs
- Use `--squash` for merge to keep history clean
- Creating repos with `--source=. --push` initializes from current directory
- Use `gh auth status` to verify authentication
- Use `gh api` for any GitHub API endpoint not covered by built-in commands
