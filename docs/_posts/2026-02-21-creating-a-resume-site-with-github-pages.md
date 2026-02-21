---
title: "Creating a Resume Site with GitHub Pages"
date: 2026-02-21
last_modified_at: 2026-02-21
categories:
  - Technology
tags:
  - github-pages
  - jekyll
  - resume
  - portfolio
  - web-development
  - career
excerpt: "A step-by-step guide to building a free, professional resume site using GitHub Pages — no hosting fees, no CMS, just a repository and a theme."
toc: true
toc_label: "Contents"
toc_icon: "list"
---

I built this blog on GitHub Pages, and along the way I realized how well this approach works for a personal resume or portfolio site. If you're looking to create a resume site, with a custom URL to show off your work portfolio is worth the two hours it takes to set up, especially when it's almost free.

Here's exactly how I'd do it today.

## Why GitHub Pages?

There are plenty of ways to host a personal site. WordPress, Squarespace, Wix — they all work. But GitHub Pages has a few things going for it:

- **Free hosting** with a `username.github.io` URL (or your own custom domain)
- **Version-controlled content** — your site lives in a Git repo like everything else
- **Jekyll support** built-in, meaning you can use themes without running a build pipeline yourself
- **No lock-in** — it's just markdown files, you can move them anywhere

The trade-off is that it takes a bit more setup than a drag-and-drop site builder. But once it's done, updating your resume is just editing a markdown file.

## Step 1: Create the Repository

Go to GitHub and create a new repository named exactly:

```
username.github.io
```

Replace `username` with your actual GitHub username. This naming convention tells GitHub Pages to automatically serve the repository as a website at `https://username.github.io`.



Make it **public** — GitHub Pages is free for public repositories. If you want a private repo, you'll need a paid plan.

## Step 2: Choose a Theme

Jekyll has a huge ecosystem of themes. For my resume site, I used Minimal Mistakes: [mmistakes.github.io](https://mmistakes.github.io/minimal-mistakes/).

**Minimal Mistakes** is greate if you want a portfolio + blog hybrid (which is what this site uses).

Most themes can be enabled via `remote_theme` in your `_config.yml`, which means no local build toolchain required.

## Step 3: Configure `_config.yml`

This file controls your entire site. Here's a minimal starting config using Minimal Mistakes:

```yaml
title: "Resume"
permalink: /resume/
excerpt: "Senior Technical Product Manager with 15+ years experience in SaaS enterprise software for asset-intensive industries."
date: 2026-02-21
toc: true
toc_label: "Contents"
toc_icon: "list"
---

A few things worth considering:

- **`title`**: This shows in browser tabs and search results. Put your name and role here.
- **`author.bio`**: Keep it short and human. This shows in the sidebar on every page.
- **`links`**: Add LinkedIn, GitHub, Twitter/X, or whatever is relevant to your field.

## Step 4: Build Your Resume Page

Create a file at `_pages/resume.md`. This will be your main resume page:

```markdown
---
title: "Resume"
permalink: /resume/
layout: single
author_profile: true
---

## Experience

**Senior Product Manager** — Acme Corp *(2022–Present)*
- Led cross-functional teams to ship X, resulting in Y
- Defined roadmap for Z product line

**Product Manager** — StartupCo *(2019–2022)*
- Launched MVP of core feature in 3 months
- Grew active users from 10k to 80k in 18 months

## Education

**B.S. Computer Science** — Carroll University

## Skills

Product strategy, roadmapping, Agile/Scrum, SQL, Figma, user research
```

Then add it to your navigation in `_data/navigation.yml`:

```yaml
main:
  - title: "Home"
    url: "/"
  - title: "Resume"
    url: "/resume/"
```

## Step 5: Enable GitHub Pages

In your repository settings:

1. Go to **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Choose `main` branch, `/ (root)` folder
4. Click **Save**

GitHub will build and deploy your site in about a minute. You'll see the live URL at the top of the Pages settings screen.

## Step 6 (Optional): Add a Custom Domain

If you want `www.yourname.com` instead of `username.github.io`:

1. Buy a domain from Namecheap, Google Domains, or wherever you prefer
2. In your repo, add a file named `CNAME` containing just your domain:
   ```
   www.yourname.com
   ```
3. In your DNS settings, add a `CNAME` record pointing `www` to `username.github.io`
4. For the apex domain (`www.yourname.com`), add `A` records pointing to GitHub's IPs:
    Find them here: [Manage a custom domain GitHub documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages?utm_source=chatgpt.com)
5. Back in GitHub Pages settings, enter your custom domain and enable **Enforce HTTPS**
6. [optional] Add a redirect from `yourname.com` to `www.yourname.com`. 
    - In my registry I was unable to add a redirect for the apex domain, so I added a redirect for the `www` domain to `yourname.com` using a S3 bucket. 

DNS changes can take up to 24 hours to propagate, but it's usually much faster.

## Tips and Gotchas

- **Keep content in `docs/`** if you want to separate your site source from any other files in the repo root. Set your GitHub Pages source to `docs/` instead of `/`.
- **Images**: Put them in `/assets/img/` and reference with `/assets/img/your-image.jpg`. Avoid absolute external URLs — they'll break if the source moves.
- **Drafts**: Files in `_drafts/` won't publish. Great for working on posts before they're ready.
- **Local preview**: Install the `github-pages` gem and run `bundle exec jekyll serve` to preview locally before pushing. It saves a lot of `git push` cycles.

## My Takeaway

A GitHub Pages resume site takes a couple of hours to set up, but it pays off. It's a real URL you control, it's fast, and it's one less subscription to pay. If you're already comfortable with Git and markdown, the editing workflow feels completely natural.

The main investment is picking the right theme upfront — it's easier to start with one that fits your use case than to switch later. Spend some time looking at options before committing.

If you're building a site similar to this one and run into questions, the [Minimal Mistakes documentation](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) is excellent.
