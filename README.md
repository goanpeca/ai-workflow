# AI Workflow

This repository demonstrates how to integrate Claude Code into GitHub workflows for automated code assistance and review.

## Overview

This project showcases two powerful ways to use Claude Code in your development workflow:

1. **Interactive Claude Assistant** - Trigger Claude to help with issues, answer questions, and implement code changes
2. **Automated Code Review** - Get automatic code reviews on every pull request

## Workflows

### Claude Code (`claude.yml`)

This workflow enables interactive Claude assistance triggered by:

- **Issues**: Label an issue with `claude` to have Claude work on it
- **Issue Comments**: Mention `@claude` in any issue comment
- **PR Review Comments**: Mention `@claude` in PR review comments
- **PR Reviews**: Mention `@claude` in PR reviews

**What Claude can do:**
- Answer questions about the codebase
- Implement features and bug fixes
- Create pull requests for issue resolutions
- Respond to feedback and make changes

**Access Control:**
- Issues labeled `claude`: Restricted to specific usernames
- Comments: Restricted to repository owners and members

### Claude Code Review (`claude-code-review.yml`)

This workflow provides automatic code reviews on pull requests:

- **Trigger**: Runs on PR opened, synchronized, ready for review, or reopened
- **Purpose**: Provides AI-powered code review feedback
- **Scope**: Reviews all changed files in the PR

## Setup

### Prerequisites

1. An [Anthropic API key](https://console.anthropic.com/)
2. Repository with GitHub Actions enabled

### Configuration

1. **Add your Anthropic API key** as a repository secret:
   - Go to Settings > Secrets and variables > Actions
   - Add a new secret named `ANTHROPIC_API_KEY`

2. **Copy the workflow files** to your repository:
   - `.github/workflows/claude.yml` - For interactive Claude assistance
   - `.github/workflows/claude-code-review.yml` - For automatic code reviews

3. **Customize access control** (optional):
   - Edit `claude.yml` to add/remove usernames in the allowed users list
   - Modify trigger conditions as needed

## Usage

### Getting Help on Issues

1. Create an issue describing the task
2. Add the `claude` label to the issue
3. Claude will analyze the issue and work on it
4. Once done, Claude creates a pull request with the changes

### Asking Questions

1. Comment on any issue or PR with `@claude` followed by your question
2. Claude will respond with an answer

### Code Reviews

Code reviews happen automatically on every pull request. Claude will analyze the changes and provide feedback on:

- Code quality and best practices
- Potential bugs or issues
- Suggestions for improvement

## Customization

### Allowed Tools

The `claude.yml` workflow specifies which tools Claude can use:

```yaml
claude_args: |
  --model "claude-opus-4-5"
  --max-turns 100
  --allowedTools "Bash(git:*),Bash(gh issue:*),Bash(gh pr:*),..."
```

### Custom Prompts

Both workflows support custom prompts to guide Claude's behavior. See the workflow files for examples.

## Resources

- [Claude Code Action](https://github.com/anthropics/claude-code-action) - GitHub Action for Claude Code
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code) - Official documentation
- [Anthropic Console](https://console.anthropic.com/) - API key management
