# AI Workflow

This repository demonstrates how to integrate [Claude](https://claude.ai) — Anthropic's AI assistant — directly into your GitHub workflows. It provides two GitHub Actions workflows that automate code review and issue/PR assistance using Claude.

## Workflows

### 1. Claude Code (`claude.yml`)

This workflow enables you to interact with Claude directly in GitHub by mentioning `@claude` in:

- **Issue bodies** (when an issue is opened or assigned)
- **Issue comments**
- **Pull request review comments**
- **Pull request reviews**

**How it works:**

1. You mention `@claude` anywhere in a GitHub issue or PR comment
2. The workflow triggers and Claude analyzes the context (issue body, PR diff, relevant code, etc.)
3. Claude responds directly in the comment thread with answers, code suggestions, or implementations
4. For implementation requests on issues, Claude creates a branch, commits changes, and provides a pull request link

**Example usage:**

```
@claude Can you review this function for performance issues?

@claude Please implement the feature described in this issue.

@claude What does this code do?
```

**Setup requirements:**

- Add `ANTHROPIC_API_KEY` as a repository secret (Settings → Secrets and variables → Actions)
- The workflow requires `contents: read`, `pull-requests: read`, `issues: read`, and `id-token: write` permissions

### 2. Claude Code Review (`claude-code-review.yml`)

This workflow automatically runs a code review on every pull request when it is opened, updated, or marked ready for review.

**How it works:**

1. A pull request is opened or updated
2. Claude automatically analyzes all changed files in the PR
3. Claude posts a detailed code review comment covering:
   - Bugs and potential issues
   - Security vulnerabilities
   - Performance considerations
   - Code style and best practices
   - Suggestions for improvement

**Setup requirements:**

- Add `ANTHROPIC_API_KEY` as a repository secret
- The workflow uses the `code-review` plugin from the Claude Code plugins marketplace

## Setup

### 1. Add your Anthropic API Key

Go to your repository **Settings → Secrets and variables → Actions** and add a new repository secret:

- **Name:** `ANTHROPIC_API_KEY`
- **Value:** Your API key from [console.anthropic.com](https://console.anthropic.com)

### 2. Add the workflows

Copy the workflow files from `.github/workflows/` into your own repository:

- `.github/workflows/claude.yml` — for `@claude` mention support
- `.github/workflows/claude-code-review.yml` — for automatic PR reviews

### 3. Start using Claude

Once set up, you can immediately start interacting with Claude by mentioning `@claude` in any issue or PR comment.

## Configuration

Both workflows use the [`anthropics/claude-code-action@v1`](https://github.com/anthropics/claude-code-action) GitHub Action. You can customize behavior through the following options in the workflow files:

| Option | Description |
|--------|-------------|
| `anthropic_api_key` | Your Anthropic API key (use a secret) |
| `prompt` | Override the default prompt for the action |
| `claude_args` | Additional CLI arguments (e.g., restrict allowed tools) |
| `additional_permissions` | Extra permissions like `actions: read` for CI result access |
| `plugins` | Plugins to load (e.g., `code-review@claude-code-plugins`) |

For the full list of options, see the [claude-code-action documentation](https://github.com/anthropics/claude-code-action/blob/main/docs/usage.md).

## References

- [Claude Code Action](https://github.com/anthropics/claude-code-action) — the GitHub Action powering these workflows
- [Claude Code documentation](https://code.claude.com/docs) — full CLI and SDK reference
- [Anthropic Console](https://console.anthropic.com) — manage your API keys
