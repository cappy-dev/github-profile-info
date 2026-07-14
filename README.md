# github-profile-info

A Python CLI tool that generates a markdown info file for any GitHub profile. No authentication required. Uses the public GitHub REST API.

Perfect for AI agents that need GitHub profile context without burning tokens on web searches or multiple API calls.

## Install

```bash
curl -fsSL https://raw.githubusercontent.com/cappy-dev/github-profile-info/main/github-profile-info -o ~/.local/bin/github-profile-info
chmod +x ~/.local/bin/github-profile-info
```

Requires Python 3.8+. No dependencies beyond the standard library.

## Usage

```bash
# Basic: generate <username>-profile-info.md
github-profile-info torvalds

# Include top 20 repos by stars
github-profile-info torvalds --repos

# Skip pinned repos (faster, saves an API call)
github-profile-info torvalds --no-pinned

# Custom output path
github-profile-info torvalds --output ~/docs/linus.md

# Full profile with everything
github-profile-info torvalds --repos --output ~/docs/linus.md
```

## What It Fetches

- User profile (name, bio, company, location, blog, Twitter, email)
- Stats (public repos, gists, followers, following, total stars, total forks)
- Top languages across all public repos
- Pinned repos (scraped from the public profile page)
- Top 20 repos by stars (optional with `--repos` flag)

## Output

A clean markdown file structured as:

```
# Display Name (username)
  Profile section (company, location, blog, etc.)
  Stats section (repos, stars, forks, followers)
  Top Languages section
  Pinned Repos section
  Top Repos section (optional)
```

## Rate Limits

The GitHub API allows 60 unauthenticated requests per hour per IP. For users with many repos, fetching all repos may use several requests. Use `--no-pinned` to skip the profile page scrape.

## License

AGPL-3.0
