# GitHub Copilot Agent with Signed Commits

This repository demonstrates how to create a GitHub Copilot agent that exclusively uses signed commits via the GitHub API.

## Overview

This repository contains a custom GitHub Copilot agent configuration that ensures all commits are automatically signed when using the GitHub CLI API. This is particularly useful for maintaining commit verification requirements in repositories.

## Features

- **Automatic Commit Signing**: All commits made through this agent are automatically signed via the GitHub API
- **GitHub CLI Integration**: Uses `gh api` commands to create signed commits
- **Custom Agent Configuration**: Includes a pre-configured agent that enforces signed commit practices

## Agent Configuration

The custom agent is defined in `.github/agents/signed-copilot.agent.md` and is configured to:

- Always use the GitHub API for commits to ensure they are signed
- Never push unsigned commits to work branches
- Provide clear feedback if signed commits cannot be created

## Usage

The agent uses the following pattern for creating signed commits:

```bash
gh api --method POST \
  -H "Accept: application/vnd.github.v3+json" \
  /repos/OWNER/REPO/git/commits \
  -f message="Your commit message" \
  -f tree=$(git write-tree) \
  -F parents[]=$(git rev-parse HEAD)
```

Replace `OWNER/REPO` with your repository owner and name (e.g., `davidgamero/gh-copilot-agent-signed-commits`).

## Why Signed Commits?

Signed commits provide:

- **Authentication**: Verify that commits actually come from trusted sources
- **Integrity**: Ensure that the commit content hasn't been tampered with
- **Compliance**: Meet security and compliance requirements for code provenance

## Requirements

- GitHub CLI (`gh`) installed and authenticated
- Appropriate repository permissions to create commits via the API

## License

This is a demonstration repository for educational purposes.

## Contributing

This repository is primarily for demonstration purposes. If you have suggestions or improvements, feel free to open an issue or pull request.
