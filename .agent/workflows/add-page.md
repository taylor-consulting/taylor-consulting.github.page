---
description: Add a new static page to the taylor-consulting.github.page Jekyll site
---

# Add Page Workflow

Use this workflow when the user wants to create a new site page (not a blog post).
Read `.agent/skills/add-page/SKILL.md` before starting.

## Steps

1. **Gather information** — Ask the user for the following if not already provided:
   - Page title (required)
   - Desired URL slug / permalink (e.g., `/resume/`, `/speaking/`)
   - Page content or outline
   - Whether to add it to the main navigation (default: yes)

2. **Determine filename and permalink** — Use the permalink slug as the filename: `docs/_pages/slug.md`

3. **Write the page** — Create the file with complete front matter and body content following the skill guidelines.

4. **Create the page file** — Write to `docs/_pages/page-name.md`

// turbo
5. **Update navigation** — Edit `docs/_data/navigation.yml` to add the new page to the `main` nav in a logical position (unless user said to skip).

6. **Confirm with the user** — Show the file path, permalink, and navigation entry. Ask if they want any revisions.
