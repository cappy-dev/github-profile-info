---
name: github-profile-info-usage
description: How to efficiently use the github-profile-info CLI tool to get GitHub profile context.
version: 1.0.0
author: Cappy
license: AGPL-3.0
metadata:
  hermes:
    tags: [GitHub, AI-Agent, Tools, Productivity]
---

# GitHub Profile Info Tool Usage

The `github-profile-info` tool is a lightweight CLI designed for AI agents to gather GitHub profile context in a single, token-efficient operation. It avoids the need for multiple web searches or repetitive API calls.

## Why use this tool?
Instead of searching for a user, navigating their profile, and piecing together their stats, the tool outputs a single markdown file (`<username>-profile-info.md`) containing everything an agent needs.

## Installation
The tool is installed at `~/.local/bin/github-profile-info`. Ensure `~/.local/bin` is in your PATH.

## Usage Commands

### Standard fetch (Profile + Stats + Languages + Pinned Repos)
```bash
github-profile-info <username>
```

### Fetch with detailed repository list (Top 20 by stars)
```bash
github-profile-info <username> --repos
```

### Faster fetch (Skip pinned repo scraping)
If you don't need pinned repos and want to stay within GitHub's 60req/hour unauthenticated API limit:
```bash
github-profile-info <username> --no-pinned
```

### Custom output file
```bash
github-profile-info <username> --output /tmp/profile.md
```

## Agent Workflow Pattern
When assigned to research or collaborate with a user:

1. **Check if profile info exists**: Does `~/.local/bin/github-profile-info` exist? If so, run it.
2. **Generate file**:
   ```bash
   github-profile-info <username> --repos
   ```
3. **Read content**:
   ```bash
   read_file("<username>-profile-info.md")
   ```
4. **Use information**: Use the data from the markdown file to answer questions about the user’s history, preferred languages, or top projects.
5. **Clean up**: After the session, the file `<username>-profile-info.md` can be deleted to keep your workspace clean.

## Limitations
- **Rate limits**: 60 unauthenticated requests/hour per IP.
- **Organization vs User**: Works for both; handles API response variations gracefully.
- **No authentication**: Does not access private data or private repositories.
