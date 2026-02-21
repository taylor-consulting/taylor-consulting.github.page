---
name: Add Page
description: Creates a new static page for the taylor-consulting.github.page Jekyll site (Minimal Mistakes theme). Use this skill whenever the user asks to add, create, or build a new site page (not a blog post).
---

# Add Page Skill

## Site Overview

- **Theme**: Minimal Mistakes (`mmistakes/minimal-mistakes@4.27.3`)
- **Pages directory**: `docs/_pages/`
- **Navigation config**: `docs/_data/navigation.yml`
- **`_config.yml`** sets `layout: single` and `author_profile: true` as defaults for all pages — do NOT repeat these in front matter unless overriding.

## Front Matter Template

```yaml
---
title: "Page Title"
permalink: /your-url-slug/
excerpt: "One sentence describing the page for SEO and social previews."
date: YYYY-MM-DD
---
```

### Front Matter Rules

- **title**: Title case. Shown as the page H1 heading.
- **permalink**: Always use trailing slash. Lowercase, hyphenated. Must match the URL you add to `navigation.yml`. Examples: `/resume/`, `/speaking/`, `/uses/`.
- **excerpt**: Plain text. Used by search engines and social cards. 1 sentence.
- **date**: Today's date (`YYYY-MM-DD`). Required for Jekyll to process the page correctly.
- **layout**: Omit unless using something other than `single` (the site default). Special layouts available: `tags` (for tag archive), `categories` (for category archive), `home` (for post listing).
- **author_profile**: Omit unless you want to disable the sidebar (`author_profile: false`).
- **toc**: Add `toc: true` for longer pages with multiple sections. Add `toc_label: "Contents"` and `toc_icon: "list"` alongside it.

## Common Page Types

| Page Type | Layout | Notes |
|---|---|---|
| Standard content page | `single` (default) | About, Resume, Speaking, Uses, etc. |
| Tag archive | `tags` | One exists at `/tags/` already — don't duplicate |
| Category archive | `categories` | Add if categories navigation is needed |
| Post listing / home | `home` | Use for a dedicated posts index page |

## Navigation

After creating the page file, **always update `docs/_data/navigation.yml`** to add the page to the site menu (unless the user says to omit it):

```yaml
main:
  - title: "New Page Title"
    url: "/your-url-slug/"
```

Insert the new item in a logical position. Current nav order: Home → Resume → About → Tags → Contact → Terms & Privacy.

## File Naming

Pages use descriptive filenames but the URL is controlled by `permalink`, not the filename. Convention:

```
docs/_pages/page-name.md
```

Use a name that matches the page's purpose (e.g., `resume.md`, `speaking.md`, `uses.md`).

## File Creation Steps

1. Confirm the page title, permalink/URL slug, and any content the user wants included.
2. Determine today's date (`YYYY-MM-DD`, `America/Chicago` timezone).
3. Create the file at `docs/_pages/page-name.md` with complete front matter and body content.
4. Update `docs/_data/navigation.yml` to add the new page to the main nav (unless user says otherwise).
5. Confirm both files were updated and show the user the permalink URL it will be live at.

## Example

For a "Speaking" page:

- **File**: `docs/_pages/speaking.md`
- **Permalink**: `/speaking/`
- **Navigation entry**: `{ title: "Speaking", url: "/speaking/" }`
