---
name: Add Blog Post
description: Creates a new blog post for the taylor-consulting.github.page Jekyll site (Minimal Mistakes theme). Use this skill whenever the user asks to write, draft, or create a new blog article or post.
---

# Add Blog Post Skill

## Site Overview

- **Theme**: Minimal Mistakes (`mmistakes/minimal-mistakes@4.27.3`)
- **Posts directory**: `docs/_posts/`
- **File naming**: `YYYY-MM-DD-slug-with-hyphens.md` (use today's date unless user specifies otherwise)
- **URL**: `https://www.taylor-consulting.com`
- **Author**: Joel Taylor, Taylor Consulting LLC
- **Timezone**: `America/Chicago`

## Front Matter Template

Every post MUST begin with this front matter:

```yaml
---
title: "Your Post Title Here"
date: YYYY-MM-DD
last_modified_at: YYYY-MM-DD
categories:
  - Category Name
tags:
  - tag-one
  - tag-two
excerpt: "A concise 1-2 sentence summary of the post shown in listings and social previews."
header:
  teaser: /assets/img/teasers/your-image.jpg  # optional, omit if no image
toc: true
toc_label: "Contents"
toc_icon: "list"
---
```

### Front Matter Rules

- **title**: Use title case. Wrap in double quotes.
- **date**: Today's date in `YYYY-MM-DD` format (America/Chicago timezone).
- **last_modified_at**: Same as `date` when first created.
- **categories**: Choose 1–2 from common site categories. Examples: `Book Review`, `Product Management`, `Technology`, `Leadership`, `Agile`, `Tools`.
- **tags**: Lowercase, hyphenated. Choose 2–6 relevant tags. Examples: `product-management`, `book-review`, `agile`, `leadership`, `software-development`, `tools`, `career`, `strategy`.
- **excerpt**: Required. Plain text, no markdown. 1–2 sentences max.
- **header.teaser**: Optional. Only include if a relevant image exists under `/assets/img/teasers/`. Otherwise omit the entire `header:` block.
- **toc**: Always `true` for posts longer than ~300 words. Set to `false` for very short posts.
- The following are set globally in `_config.yml` and do NOT need to be repeated in front matter unless overriding: `layout`, `author_profile`, `read_time`, `comments`, `share`, `related`, `show_date`.

## Post Body Guidelines

- Write in Joel's voice: conversational, practical, opinionated but humble, first-person.
- Use `##` for main sections (H2), `###` for subsections (H3). Never use H1 (`#`) — the title serves as H1.
- Use bullet lists for tips/takeaways, numbered lists for steps/sequences.
- Use `**bold**` for key terms and emphasis.
- Use `> blockquote` for notable quotes from books or people.
- End posts with a brief personal reflection or call-to-action section (e.g., "## My Takeaway" or "## Final Thoughts").
- For **book reviews**, include: a brief summary, key concepts/chapters, quotes, and personal takeaway.
- For **how-to posts**, include: problem statement, steps, example, and gotchas/tips.

## File Creation Steps

1. Determine today's date in `YYYY-MM-DD` format (America/Chicago).
2. Generate a URL-safe slug from the title: lowercase, words separated by hyphens, remove special characters.
3. Create the file at: `docs/_posts/YYYY-MM-DD-your-slug.md`
4. Write the complete front matter followed by the post body.
5. Confirm the file was created and show the user the file path and a preview of the front matter.

## Example

For a post titled "Book Review: The Mom Test" created on 2026-02-21:

- **File**: `docs/_posts/2026-02-21-book-review-the-mom-test.md`
- **Tags**: `book-review`, `product-management`, `customer-discovery`
- **Category**: `Book Review`
