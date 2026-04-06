---
title: "OpenClaw: From Tool to Personal AI OS"
date: 2026-04-06
last_modified_at: 2026-04-06
categories:
  - Technology
tags:
  - ai
  - productivity
  - openclaw
  - automation
excerpt: "How I transitioned from using scattered productivity tools to creating my own personal AI operating system, using OpenClaw."
toc: true
toc_label: "Contents"
toc_icon: "list"
---

## The Problem

I've been getting increasingly busy, lots of interests and too many new tools to try and lots of meetings back to back. In my personal life I’ve been using Obsidian with Kanban for task tracking, Obsidian for note taking, [readwise](https://readwise.io/) for tracking read-later and highlights, goodreads for tracking what I read, and [mesh](https://me.sh/) for tracking my contacts. The pattern is always the same: I set it up, use it for two weeks, then it starts to get out of sync and I have to do a Friday evening catchup to bring it all back together when the boards goes stale. The reminders pile up unread. The system becomes another thing to maintain.

What I actually wanted wasn't another tool. I wanted something that *knows* me & my projects, my priorities, my patterns. Something that keeps me on track without me having to babysit it.

That's what led me to OpenClaw. I wanted something I could send a quick comment to. This adds a todo and then I can keep adding free form brain dumps to update the to-do's and add context before I start them.

---

## What Is OpenClaw?

OpenClaw is a self-hosted personal AI gateway. It connects large language models (like Claude or GPT) to your actual life. If you want it can access your files, your calendar, your messaging apps, your tools. Think of it as the connective tissue between AI and your day-to-day workflow.

Out of the box it comes with:
- Built-in skills (web search, reminders, weather, etc.)
- Channel integrations (Discord, Telegram, WhatsApp)
- A cron scheduler for automated tasks
- Memory files that persist between sessions

---

## The Many Ways to Run It

One of the things I appreciate about OpenClaw is that it meets you where you are. There's no single "right" way to run it:

**Cloud-hosted (Abacus.AI)**
The easiest entry point. Abacus.AI hosts everything for you — no server to spin up, no infra to manage. You just configure and go. This is what I use through my chatllm account. I only give it limited access to my information. Mostly through git repos that the agent syncs.

**Self-hosted VPS**
More control, more work. Rent a $5/month server, install OpenClaw, own your data end-to-end. Good for privacy-focused users or tinkerers. I tried a droplet from digital ocean but it wasn’t as easy for me as abacus.

**Local machine**
Run it on your laptop or home server. Most control, most maintenance, most risk as it could mess with your files. Great for developers who want to hack on it. I was way too nervous to give an AI access to my PC, I wanted it firewalled from my actual accounts and files. 

Each has tradeoffs between convenience, control, and cost. For most people starting out, cloud-hosted is the right call. It keeps it separated from your files and you choose what to give it access too.

---

## Default Mode: Smart Assistant

Out of the box, OpenClaw works great as a smart assistant. Ask it questions, set reminders, search the web, get weather. It's genuinely useful from day one.

Most people stop here. And that's fine — it's already better than most chatbots because it's connected to your context.

But the real power is what comes next. Tailoring it to your tools and rhythms.

---

## Level 2: Giving It Memory

The first thing I customized was memory. OpenClaw uses a set of markdown files to persist context between sessions:

- **SOUL.md** — the agent's personality and values
- **USER.md** — who you are, your preferences, your context
- **MEMORY.md** — curated long-term memories
- **Daily notes** — raw logs of what happened each session

Every time the agent wakes up, it reads these files. It knows your name, your projects, your communication style. It remembers decisions you made last week. It's not starting from scratch every conversation.

This alone changes the dynamic from "AI assistant" to something closer to a colleague who's been paying attention.

I named mine Joet because this was related to Moltbook which was in the news while I was working on it. Although I didn’t have my bot create an account on Moltbook. The social network for bots.

I’d keep these files private as these are what makes your bot special. I checked these into a separate repo just for the agent.

---

## Level 3: Custom Skills & Workflows

This is where it gets interesting. OpenClaw has a skill system with reusable capabilities you define in markdown files and store in a Git repo.

I built a whole set of custom skills:
- **backup-all** — commits and pushes all my repos in one command
- **restore-joet** — full restore procedure if something goes wrong
- **decision-log** — writes decisions to my Obsidian vault

Skills are just markdown with instructions. If I can describe a workflow, I can make it a skill.

These are all stored in git source control. It makes cloning and experimenting safe. It is its own repo and they could be based on anything. Agent skills could be secret but they are often templates and workflows that are not secret. 

Skills are more specific and detailed than the tools.md file. The tools.md file is where the agent has been putting simple calls. The skills all have multi-step workflows, templates, and preferences.

---

## What We Built Together

Here's the actual system I'm running:

**Task board:** Obsidian kanban plugin, stored in a Git repo the agent can read and write. When I say "show me todos," it reads the file. When I complete something, it updates the board. It also allows me to create files and give the agent more context using Obsidian on my iPad or PC. I can keep adding details to notes here for my todos so when I start them we can get a leg up. Obsidian naturally allows Git as a source for notes.

**Interface:** Discord. I have a private server with threads for each task. In threads, the agent auto-responds. No @mention needed. In #general, I @mention it for quick tasks. Again Discord runs natively on my phone, PC, or iPad.

**Cron jobs:** The nervous system.
- Weekly Sunday review: reads the kanban, summarizes what's open, gets context from notes attached to the kanban.
- Blog nudge: checks my sites every Monday, only pings me if I haven't posted in 14+ days. It’s smart reminders. Only alert me if I need to be alerted.
- Token expiry warning: fires 3 days before my GitHub token expires.

**Git backups:** Three repos: one for core identity files, one for custom skills, one for the Obsidian vault. The agent can back up and restore itself with these repos. 

I’m prioritizing tools that work the same whether on my phone, iPad or computer. I’m using the same git repos and Discord chats. Then working jointly on files in Obsidian. It works so easily to just ask it to add some tasks and continue to give it context. 

---

## The Key Insight

Default OpenClaw is a tool you use.

Customized OpenClaw is a system that works with you and your other tools. Organizing your data and integrating into your workflows.

The difference is intentional design. You have to decide what you want it to know, what you want it to do automatically, and what you want it to leave alone. That takes some upfront investment, but once it's set up, it compounds.

The agent gets better at serving you the more you put into it. And unlike a static tool, it can evolve.

---

## What It Takes

I won't sugarcoat it, there's setup involved:
- Comfort with markdown helps
- Basic Git knowledge is useful
- Some tinkering to get the integrations right for the Discord bot

But you don't need to be a developer. If you can write a README, you can build skills. If you can manage a GitHub repo, you can handle the backup system.

The payoff is an AI that actually knows your context, tracks your work, and keeps you accountable. All without nagging you, because it can check your status automatically; and without you having to babysit it.

---

## What's Next

I'm still building. On the roadmap:
- Calendar integrations
- Obsidian CLI for richer vault operations
- Content pipeline tracking for both my blogs
- Expanding what the agent can access and act on
- Adding connections to my read later app 

I'll keep writing about it as it evolves.

---

*Have questions or want to try OpenClaw yourself? Check out [openclaw.ai](https://openclaw.ai) and the [community Discord](https://discord.com/invite/clawd).*
