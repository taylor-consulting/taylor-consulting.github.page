---
name: Preview Site
description: Runs the Jekyll site locally for preview without pushing to GitHub. Use this skill whenever the user wants to preview, test, or serve the site locally.
---

# Preview Site Skill

## Overview

The site can be previewed locally using Jekyll before pushing to GitHub. The preview runs at `http://localhost:4000`.

## Requirements

- Ruby installed (verify: `ruby -v`)
- Bundler installed (verify: `bundle -v`, or install with `gem install bundler`)
- `docs/Gemfile` exists in the repo (already set up)

## Key Files

- **Gemfile**: `docs/Gemfile` — defines Jekyll and plugin gems
- **Site source**: `docs/` — all Jekyll content lives here
- **Config**: `docs/_config.yml`

## Commands

Run all commands from the `docs/` directory:

```powershell
# First time only — install gems
cd d:\git\taylor-consulting.github.page\docs
bundle install

# Start the local server
bundle exec jekyll serve
```

The site will be available at: **http://localhost:4000**

### Useful flags

| Flag | Effect |
|---|---|
| `--livereload` | Auto-refreshes browser on file save |
| `--drafts` | Includes posts in `_drafts/` in the preview |
| `--incremental` | Faster rebuilds (only rebuilds changed files) |

Full command with all flags:
```powershell
bundle exec jekyll serve --livereload --drafts
```

## Stopping the Server

Press `Ctrl+C` in the terminal to stop the local server.

## Troubleshooting

- **`webrick` missing**: Already included in `Gemfile` — required for Ruby 3.x
- **Port already in use**: Use `--port 4001` to run on a different port
- **`bundle install` fails**: Run `gem install bundler` first, then retry
- **Gems out of date**: Run `bundle update` to update to latest compatible versions
