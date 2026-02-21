---
description: Preview the Jekyll site locally without pushing to GitHub
---

# Preview Site Workflow

Use this workflow to run the Jekyll site locally at http://localhost:4000.
Read `.agent/skills/preview-site/SKILL.md` before starting.

## Steps

// turbo
1. **Install gems** (first time only) — Run `bundle install` from the `docs/` directory:
   ```powershell
   cd d:\git\taylor-consulting.github.page\docs; bundle install
   ```

// turbo
2. **Start the local server** — Run Jekyll serve with live reload and drafts enabled:
   ```powershell
   cd d:\git\taylor-consulting.github.page\docs; bundle exec jekyll serve --livereload --drafts
   ```

3. **Open the browser** — Navigate to http://localhost:4000 to view the site.

4. **Stop the server** — Press `Ctrl+C` in the terminal when done.
