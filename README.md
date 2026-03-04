# Claude Cowork Plugin Generator Skill

**By [The AI Impact]**

A free Claude skill that turns any workflow description into a complete, ready-to-build Cowork plugin spec — in one conversation. No coding. No tech experience needed.

---

## What This Skill Does

Most people don't know where to start when building a custom Claude plugin. This skill fixes that.

It runs a structured 7-question interview, then generates a complete **Plugin Blueprint** — a full spec document you can hand directly to Plugin Create (Claude's built-in plugin builder) to build your plugin immediately.

**The Blueprint includes:**
- A ready-to-use system prompt for your plugin
- Which skills to include and when they trigger
- Which connectors to enable (Native vs MCP) and why
- Slash commands tailored to your workflow
- Context files to upload (brand voice, personas, templates)
- Approval gates so Claude pauses before sending anything important
- 5 test prompts to validate your plugin works
- What to build next once it's running

The output isn't generic advice. It's a spec document written specifically for your role and workflow — ready to implement immediately.

---

## Who This Is For

Non-technical solopreneurs, freelancers, and small business owners who want to build a custom Claude plugin without writing code or figuring out the structure themselves.

If you've ever thought "I want Claude to just *know* my workflow" — this is how you do it.

---

## Requirements

- Claude (any paid plan: Pro, Max, Team, or Enterprise)
- Claude Desktop app for macOS or Windows (required for Cowork)
- No coding skills needed

---

## How to Install

### Option 1 — Install directly in Claude Settings

1. Download `SKILL.md` from this repo (click the file → click the download icon)
2. Open Claude → **Settings → Skills**
3. Click **"Install skill"** and upload the `SKILL.md` file
4. The skill is now active in any Claude conversation

### Option 2 — Copy the raw SKILL.md

1. Open `SKILL.md` in this repo
2. Click **"Raw"** to view the plain text
3. Copy the entire contents
4. In Claude Settings → Skills → **"Add skill manually"** → paste and save

---

## How to Use It

Once installed, open any Claude conversation and type:

> **"Help me build a plugin blueprint for my workflow"**

Claude will launch the interview automatically. Answer all 7 questions in one reply — rough notes are fine, you don't need perfect answers.

Claude then generates your complete Plugin Blueprint.

---

## What Comes Next

Once you have your Blueprint:

1. Open **Claude Desktop → Cowork tab**
2. Go to **Customize → Browse plugins → install Plugin Create**
3. Launch Plugin Create and feed it your Blueprint section by section
4. Plugin Create builds all the files and delivers a ready-to-install `.plugin` file
5. Upload it via **Customize → Browse plugins → Upload plugin**
6. Run the 5 test prompts from your Blueprint to validate it works

**Want the full step-by-step guide?**
→ [Download the free Build Your Custom Cowork Plugin Guide](#) *(https://docs.google.com/document/d/1Qkv4tGYC9D18K1ctopdkcMdyM317p-hI/edit#heading=h.dd5z79bnlgdd)*

---

## Repo Structure

```
Claude-Cowork-Plugin-Generator-Skill/
├── .claude-plugin/
│   └── plugin.json       ← Skill manifest
├── SKILL.md              ← The skill file (install this)
└── README.md             ← You are here
```

---

## About The AI Impact

The AI Impact is a practical AI education platform for non-technical professionals — solopreneurs, freelancers, marketers, and business owners who want to use AI without the overwhelm.

No hype. No jargon. Just tools that actually work.

- TikTok: [@theaiimpact](https://www.tiktok.com/@theaiimpact)
- YouTube: [The AI Impact](https://www.youtube.com/@the-ai-impact)
- Instagram: [@theaiimpact](https://www.instagram.com/theaiimpact/)
- Threads: [@theaiimpact](https://www.threads.com/@theaiimpact)

---

## License

Free to use and adapt. If you build something with it, tag us — we'd love to see what you create.
