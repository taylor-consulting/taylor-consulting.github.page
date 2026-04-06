---
title: "Using Agent Skills and Workflows to Publish GitHub Pages"
date: 2026-03-31
last_modified_at: 2026-03-31
categories:
  - Technology
  - Tools
tags:
  - github-pages
  - jekyll
  - ai-tools
  - automation
  - git
  - workflows
excerpt: "How I set up a shared Git submodule of AI agent skills and slash-command workflows to streamline publishing to my GitHub Pages blog."
toc: true
toc_label: "Contents"
toc_icon: "list"
---

When I started using AI coding assistants to help manage my GitHub Pages blog, I quickly ran into a familiar problem: every time I wanted the AI to help me write a post, I had to re-explain the site structure, the front matter format, the Minimal Mistakes theme conventions, and my preferred writing style. It was repetitive, error-prone, and felt like exactly the kind of work that *should* be automatable.

So I built a system around **agent skills and workflows**, and I want to share how it works — and why using a **Git submodule** to host those files turned out to be the right call.

## What Are Agent Skills and Workflows?

My AI assistant (Antigravity, built on Gemini) supports two complementary concepts:

- **Skills** are markdown instruction files that teach the agent how to do a specific task — things like "how to structure a blog post front matter" or "how to run the Jekyll dev server." They live in a folder called `.agent/skills/` and each one has a `SKILL.md` file that the agent reads before acting.

- **Workflows** are step-by-step procedures, also written in markdown, that orchestrate one or more skills into a repeatable process. They live in `.agent/workflows/`. Workflow steps can be annotated with `// turbo` to allow the agent to auto-run terminal commands without prompting for approval.

Together, they let me invoke common tasks with slash commands like:

```
/add-blog-post
/preview-site
/create-pr
```

Instead of re-explaining everything from scratch, the agent reads the appropriate skill and workflow files, then executes the task with awareness of my site's specific conventions.

## The Skills in This Repo

The `.agent/skills/` directory currently contains four skills:

| Skill | What It Does |
|---|---|
| `add-blog-post` | Creates a new post with correct front matter, TOC, tags, and prose guidelines |
| `add-page` | Adds a new static page to the site |
| `create-pr` | Stages, commits, pushes changes, and generates a PR link |
| `preview-site` | Runs the local Jekyll dev server with live reload |

Each skill reads from `.agent-config.yml` — a root-level config file that captures site-specific settings like the author name, URL, timezone, and posts directory. This means the skills stay generic while the configuration stays specific to *this* site.

### Example: The `add-blog-post` Skill

Here's roughly what the `add-blog-post` SKILL.md tells the agent to do:

1. Read `.agent-config.yml` and `docs/_config.yml` to understand site conventions
2. Determine today's date in `America/Chicago` timezone
3. Generate a URL-safe slug from the post title
4. Create the file at `docs/_posts/YYYY-MM-DD-slug.md`
5. Populate the front matter with correct categories, tags, excerpt, and TOC settings
6. Write the post body in my voice — conversational, practical, first-person

The result? I type `/add-blog-post`, give a title and a few bullet points, and get a fully formatted draft ready to review.

## Why a Git Submodule?

Here's where it gets interesting. I don't just have *one* GitHub Pages site. As I build out more sites — portfolio pages, project microsites, reference docs — I want all of them to share the same agent skills and workflows without copying files around manually.

The solution is a **Git submodule**.

The `.agent` folder in this repo is not a regular directory — it's a submodule pointing to a separate shared repository:

```
https://github.com/taylor-consulting/github-pages-agent-workspace-shared
```

This is declared in `.gitmodules` at the root of the repo:

```ini
[submodule ".agent"]
    path = .agent
    url = https://github.com/taylor-consulting/github-pages-agent-workspace-shared.git
```

### How the Submodule Works

A Git submodule is a reference from one repository to a specific *commit* in another repository. When you clone the main repo, you get a pointer — not the actual files. To pull the submodule content, you run:

```bash
git submodule update --init --recursive
```

After that, the `.agent/` directory is populated with the current contents of the shared repo at the pinned commit.

### Updating the Shared Skills

When I improve a skill or add a new workflow, I push the change to `github-pages-agent-workspace-shared`. Then, in any site that uses it, I update the submodule to pull in the latest:

```bash
git submodule update --remote .agent
git add .agent
git commit -m "Update agent skills to latest"
```

This pattern is exactly how this site manages the **Minimal Mistakes Jekyll theme** — also included as a submodule. It's a proven approach for sharing versioned assets across repositories without duplicating them.

### What Gets Pinned vs. What's Site-Specific

The submodule pins the *shared* skills and workflows. Site-specific configuration stays in the main repo:

| Location | What It Contains |
|---|---|
| `.agent/` (submodule) | Skills, workflows — shared across all sites |
| `.agent-config.yml` | Site-specific settings (author, URL, paths, timezone) |
| `docs/_config.yml` | Jekyll configuration |

The skills are written to read from `.agent-config.yml` rather than hardcoding values, so the same `add-blog-post` skill works correctly on any site that defines that config file.

## The Workflow in Action

Here's what publishing this very post looked like:

1. I typed `/add-blog-post` in the chat
2. Gave the title and a rough outline
3. The agent read `SKILL.md`, checked `.agent-config.yml`, determined today's date, and drafted the full post
4. I reviewed and requested minor edits
5. Ran `/create-pr` to stage, commit, push, and open a pull request — all in one step

The whole process took a few minutes of my time. The agent handled all the boilerplate.

## Gotchas and Lessons Learned

A few things worth knowing if you try this pattern:

- **Submodule initialization matters in CI.** My GitHub Actions workflow needs `submodules: recursive` in the checkout step, or the `.agent` directory will be empty during the build. (Though since `.agent` isn't rendered by Jekyll, this mostly matters if you want skills available in automated pipelines.)

- **The pinned commit is intentional.** Submodules don't auto-update. You consciously choose when to pull in changes. This is a feature, not a bug — it prevents a skill update from breaking your workflow unexpectedly.

- **Keep `.agent-config.yml` in the main repo.** Don't put site-specific config in the submodule. The submodule should be generic enough to work anywhere.

## Final Thoughts

This setup has changed how I interact with AI tools when managing my site. Instead of treating the AI like a blank-slate assistant I have to re-train every session, I've given it a persistent, version-controlled set of instructions that live *in the repo itself*.

It's a small shift, but it makes the assistant dramatically more useful. The skills encode my conventions. The workflows encode my process. And the submodule ensures I can evolve both without managing N copies across N sites.

If you're building a GitHub Pages site and using an AI assistant to help manage it, I'd encourage you to think about your agent configuration the same way you think about your other project tooling — something worth investing in, version controlling, and sharing.
