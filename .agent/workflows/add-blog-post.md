---
description: Add a new blog post to the taylor-consulting.github.page Jekyll site
---

# Add Blog Post Workflow

Use this workflow when the user wants to write or publish a new blog article.
Read `.agent/skills/add-blog-post/SKILL.md` before starting.

## Steps

1. **Gather information** — Ask the user for the following if not already provided:
   - Post title (required)
   - Post type / category (e.g., Book Review, How-To, Opinion, News)
   - Key points, outline, or source material (e.g., book name, topic summary, notes)
   - Any specific tags they want applied
   - Whether they want a draft (placeholder body) or a fully written post

2. **Determine date and filename** — Use today's date in `America/Chicago` timezone. Generate a slug from the title. Confirm the target file path: `docs/_posts/YYYY-MM-DD-your-slug.md`

3. **Write the post** — Create the file with complete front matter and body content following the skill guidelines. For book reviews, structure as: intro → summary → key concepts → notable quotes → personal takeaway.

4. **Create the file** — Write to `docs/_posts/YYYY-MM-DD-slug.md`

5. **Confirm with the user** — Show the file path and the front matter block. Ask if they want any revisions before committing.

// turbo
6. **Optionally stage the file** — Run `git add docs/_posts/YYYY-MM-DD-slug.md` from the repo root (`d:\git\taylor-consulting.github.page`) if the user confirms they are ready to commit.
