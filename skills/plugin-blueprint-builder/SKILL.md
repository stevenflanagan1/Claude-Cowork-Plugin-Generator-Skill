---
name: plugin-blueprint-builder
description: Interview a user about their workflow or role and generate a complete Claude Cowork plugin specification — including skills folder content, slash commands, MCP connector config, context files, and approval gates. Use this skill whenever someone wants to build a custom Cowork plugin, automate a workflow with Claude, or asks "how do I set up Claude for my work." Also use when someone says "help me build a plugin," "create a custom Claude setup," "I want Claude to help me with [workflow]," or "what connectors should I use." This skill produces tiered Blueprint options (Starter, Connected, Advanced) so the user can choose the right level of complexity and hand it straight to Plugin Create — no coding required.
---

# Plugin Blueprint Builder

Turn any workflow description into a complete, tiered Claude Cowork plugin specification — with options from beginner to fully automated.

## What This Skill Does

Runs a structured two-round interview to deeply understand the user's workflow, then:
1. Proactively suggests what's possible based on their workflow type — before asking them to choose
2. Presents three tiered Blueprint options: Starter, Connected, and Advanced
3. Generates a complete Blueprint for whichever tier they choose

The user doesn't need to know what connectors, skills, or MCP servers exist. This skill brings that intelligence. The output is a complete spec ready to hand to Plugin Create — no coding, no technical knowledge required.

---

## What Is a Cowork Plugin

A Cowork plugin is a folder of plain text files that turns Claude into a specialist for a specific workflow. Four components:

**Skills** (`skills/skill-name/SKILL.md`)
Always-on domain knowledge Claude draws on automatically. Teaches Claude your process, your voice, your rules, your platform formats. Claude reads the right skill files when they're relevant — the user never has to trigger them manually.

**Commands** (`commands/command-name.md`)
Slash commands the user triggers manually for specific repeatable tasks (e.g. `/research`, `/draft`, `/deliver`). Each command produces a predictable, specific output.

**MCP Connectors** (`.mcp.json`)
Live connections to external tools — Notion, Gmail, HubSpot, Ahrefs, Apify, Snowflake, and thousands more via the Model Context Protocol. Connectors let Claude read from and act in real tools during a session, not just work from what the user pastes in.

**Manifest** (`.claude-plugin/plugin.json`)
The label that tells Cowork the plugin's name, version, and where to find everything.

Plugin Create (a built-in Cowork plugin) builds all files automatically through conversation. The Blueprint this skill generates is the input to that conversation.

---

## Phase 1: Interview

Two rounds. Round 1 gets the big picture. Round 2 drills into every detail needed to build a complete, specific plugin. The goal is to understand the workflow so thoroughly that you could build the plugin yourself without asking another question.

You are acting as a business analyst doing a workflow discovery session — not collecting form responses.

---

### Round 1 — Workflow Overview

Send as a single conversational message:

> **Let's build your Plugin Blueprint.**
>
> I'll ask about your workflow in two quick rounds, then show you what's possible — including a simple starter version and a more powerful automated version with your tools connected. You pick the level that's right for you.
>
> ---
>
> **1. What's your role?**
> *(e.g. "Freelance copywriter", "Social media manager", "Marketing consultant", "E-commerce founder")*
>
> **2. Walk me through the workflow you want this plugin to handle — step by step, from when you start to when it's done.**
> *(Don't worry about being technical. Just describe what you actually do, in order. Include the manual and repetitive parts — those are exactly what we're looking to improve.)*
>
> **3. What does the finished output look like, and where does it need to end up?**
> *(e.g. "Scripts saved to Notion and emailed to me", "A client proposal sent via Gmail", "A published blog post")*
>
> **4. What slows you down the most right now?**

---

### Round 2 — Deep Discovery

After Round 1, analyse their answers carefully. Send targeted follow-up questions based specifically on what they said. Do not send generic questions — every probe must reference something they actually mentioned.

Use these frameworks to identify gaps. Only probe what wasn't already answered:

**Every manual step → connector opportunity**
For each step they described as manual (searching, browsing, copying, checking, reviewing):
- Where exactly is this coming from? A website, platform, email, file, database?
- How do you find it — do you search, or does it come to you?
- How long does this take?
- What would instant look like?

*"I scroll TikTok for trending content" = Apify MCP. "I check YouTube" = YouTube MCP. "I read newsletters" = Web Search + Gmail. "I pull from my CRM" = HubSpot or Salesforce MCP. Never let a manual research or retrieval step stay manual if a connector can replace it.*

**Every input source → connector opportunity**
- Where does every piece of raw material come from?
- Is it already digital — in a doc, email, platform, database?
- Does anyone send inputs to you, or do you gather everything yourself?

**Every output destination → connector opportunity**
- Where does each output need to land when finished?
- Does anything get sent, published, or saved somewhere specific?
- Does it need to match a specific format or template?

**Human-in-the-loop moments → approval gates**
- Where do you need to review or approve before it continues?
- Has anything ever gone wrong in this workflow?
- Where would a mistake be most expensive or embarrassing?

**Platform and format rules → skill files**
- If outputs go to multiple platforms, what are the rules for each?
- What should Claude never do or say in this context?
- Do you have a tone, voice, or style it needs to match?
- Are there templates the output must follow?

**Repetition and variation → command design**
- How often does this workflow run?
- Does it always start the same way or does the trigger vary?
- Which parts are always identical vs which parts change each time?

**Connected systems → indirect connectors**
- What other tools does this workflow touch, even indirectly?
- Is there anything you check before starting — a calendar, dashboard, spreadsheet?
- Does this workflow feed into anything else downstream?

---

### When to Stop Probing

Stop when you can confidently answer all of these:
- [ ] Every data/content source is identified
- [ ] Every output destination is identified
- [ ] Every manual step is mapped to a potential connector or automation
- [ ] Every review/approval moment is identified
- [ ] All platform and format rules are captured
- [ ] What "done" looks like is clear

If any are uncertain, ask one more targeted follow-up. Do not generate a Blueprint from incomplete information.

---

## Phase 2: Proactive Suggestions + Tier Options

Before generating the Blueprint, show the user what's possible for their specific workflow. This is where the skill brings its own intelligence — not just mapping what the user said, but proposing what they didn't know to ask for.

Send a message in this format:

> **Here's what I can see for your workflow.**
>
> Based on what you've described, here's what's possible — from a simple setup you can use today, to a fully connected version that handles the heavy lifting automatically.
>
> **The biggest opportunities I can see:**
> [2–3 sentences identifying the highest-value automations specific to their situation. Name specific connectors, skills, and time savings. E.g. "The biggest win here is connecting Apify to pull live TikTok trend data automatically — that replaces 45 minutes of manual scrolling. Adding Notion means every output saves itself without copy-paste. Your brand voice and each platform's format rules each need their own skill file so Claude never needs re-briefing."]
>
> ---
>
> **Choose your build level:**
>
> 🟢 **Starter — Skills + Commands only**
> No connectors to set up. Works immediately after install.
> What it does: [Specific to their workflow — e.g. "Claude knows your brand voice and platform rules. You paste in a topic, run /draft, and get a TikTok script and LinkedIn post ready to review."]
> What you still do manually: [Honest list — e.g. "Find trending topics yourself, copy outputs to Notion, send your own summary email"]
> Time saved: [Honest estimate — e.g. "~1.5 hours/week on writing and reformatting"]
> Setup time: Under 5 minutes
>
> 🔵 **Connected — Starter + [2–3 specific native connectors]**
> What it adds: [Specific to their workflow — e.g. "Notion saves all outputs automatically. Gmail sends you a weekly summary with links. No copy-paste."]
> What you still do manually: [Honest list — e.g. "Find trending topics yourself"]
> Time saved: [Honest estimate — higher than Starter]
> Setup time: ~10 minutes (OAuth login for each tool)
>
> 🚀 **Advanced — Connected + [specific MCP connectors]**
> What it adds: [Specific to their workflow — e.g. "Apify pulls trending TikTok videos by hashtag automatically. YouTube MCP finds top-performing videos on your topic. One command kicks off the full pipeline — research, scripts, repurpose, save, email."]
> What you still do manually: [Should be very short — e.g. "Pick the topic from the ranked list, approve scripts before delivery"]
> Time saved: [Honest estimate — highest]
> Setup time: ~20 minutes (includes MCP server setup — step-by-step in the Blueprint)
>
> ---
> **Which level do you want the full Blueprint for?**
> *(Start with Starter if you want to get going today — your skills and commands carry straight over when you upgrade)*

---

## Phase 3: Generate the Blueprint

Once the user selects a tier, generate the complete Blueprint. Fill every section with real, specific content — no placeholders. Make real decisions. If anything is vague, assume and note it with *(assumption — update if needed)*.

**Non-negotiable rules:**
- Never say "Project Instructions", "Project Knowledge", or "system prompt" — say "skill files", "skills folder", "plugin purpose"
- One skill file per distinct platform, output type, or domain area — never collapse what should be separate
- Starter: skills + commands + Web Search only
- Connected: skills + commands + Web Search + 2–4 native connectors
- Advanced: skills + commands + Web Search + native + MCP stack
- Every manual step from the interview must be addressed — automated via connector or covered by a gate
- Always include an Upgrade Path section showing exactly what to add to reach the next tier

---

### Blueprint Template

```
═══════════════════════════════════════════
CLAUDE COWORK PLUGIN BLUEPRINT
For: [Role]
Workflow: [Workflow name]
Tier: [🟢 Starter | 🔵 Connected | 🚀 Advanced]
═══════════════════════════════════════════

## 1. PLUGIN NAME
[Short descriptive name]

## 2. PLUGIN PURPOSE
[3–5 sentences in plain English. Paste this to Plugin Create to start the build.]

## 3. SKILLS TO CREATE
[One file per distinct area. Do not combine platform rules, brand voice, research process, or output formats.]

**Skill: [skill-folder-name]**
File: `skills/[skill-folder-name]/SKILL.md`
What it teaches Claude: [Specific domain knowledge]
Fires automatically when: [Context that triggers this skill]
What to put in it: [Exact content to paste — specific, not generic]
Test prompt: "[Real prompt that activates this skill]"

## 4. SLASH COMMANDS
[Minimum 4. Cover full arc: research → create → repurpose → review. Add delivery command if connectors included.]

**/[command-name]**
What it does: [One sentence]
How to use: [e.g. "/draft [paste topic here]"]
Output: [Specific description of what Claude produces]
Skills used: [Which skill files]
Connectors used: [Which live tools — Advanced tier only]

## 5. CONNECTORS
[Starter: omit this section. Connected: native only. Advanced: native + MCP.]

**[Tool Name]** · [🟢 Native | 🔵 MCP | ⚡ Built-in]
Why it's needed: [Specific to this workflow]
What Claude does with it: [Concrete actions — not "connects to" but what it actually does]
Priority: [Essential / Recommended / Optional]
Setup: [Native: "Settings → Connectors → Connect" | MCP: URL + instructions]

## 6. APPROVAL GATES
[Only for publishing, client delivery, multi-step dependencies, or brand/legal sensitivity. Skip for internal low-stakes work.]

**Gate [N]: [Checkpoint name]**
Triggers when: [Exact moment]
Claude should: [Exactly what to show/say before pausing]
You're checking for: [What to review]
Add to skill file: "[Exact paste-ready instruction]"

## 7. WHAT TO ADD TO YOUR SKILL FILES
[Exact content for each skill file — specific, not generic.]

**[Skill name]:** [Exactly what to paste and why — e.g. "3–5 sentences that sound like you, words you use vs avoid, one example of output you're proud of"]

> 💡 Rough notes work fine. Half a page of bullets beats a polished document you never write.

## 8. HOW TO BUILD THIS
1. Open Claude Desktop → Cowork tab
2. Customize → Browse plugins → install Plugin Create
3. Launch Plugin Create
4. Paste Section 2 (Plugin Purpose) when asked what you want to build
5. Feed each section as Plugin Create asks for it
6. Receive .plugin file in your outputs folder
7. Install via Customize → Browse plugins → Upload plugin
8. Run the test prompts below
9. Refine, test, improve — it gets better every time you run it

## 9. TEST PROMPTS
[5 specific prompts for their exact workflow.]

1. [Tests skills are active and tone is correct]
2. [Tests a slash command end-to-end]
3. [Tests connector pulling live data — or tests second command if Starter]
4. [Tests multi-step workflow]
5. [Tests approval gate — or tests refinement loop]

## 10. UPGRADE PATH
[Starter → Connected: exactly what to add and what it unlocks]
[Connected → Advanced: exactly what to add and what it unlocks]
[Advanced: one natural next extension]

═══════════════════════════════════════════
READY TO BUILD?
→ Claude Desktop → Cowork tab → Plugin Create → paste Section 2
→ Full guide: https://github.com/stevenflanagan1/Claude-Cowork-Plugin-Generator-Skill
═══════════════════════════════════════════
```

---

## Phase 4: Offer to Refine

> **Your Blueprint is ready.**
>
> Paste Section 2 into Plugin Create to start building. If anything's off — wrong tier, missing a tool, needs different commands — tell me and I'll update it before you build.
>
> Want to upgrade later? Your skills and commands carry straight over — you just add connectors.
>
> Full build guide → https://github.com/stevenflanagan1/Claude-Cowork-Plugin-Generator-Skill

---

## Reference Library: Common Skills by Workflow Type

Use this to proactively suggest skills the user didn't mention. Every workflow type has predictable skill needs.

### Content & Social Media
| Skill | What it encodes |
|-------|----------------|
| `brand-voice` | Tone rules, words to use/avoid, example copy, what sounds like you vs what doesn't |
| `tiktok-content` | Hook in 2 seconds, 30–60s target, retention structure, pattern interrupt, CTA format |
| `linkedin-content` | Punchy opener, no hashtag spam, conversational not corporate, practical takeaway |
| `threads-content` | Short, opinionated, one idea, hot take not press release, 500 char max |
| `youtube-content` | Retention structure, chapter format, thumbnail angle, SEO title rules |
| `trend-research` | Editorial filter for what's worth covering, cross-platform validation, angle potential |
| `script-angles` | Framework for generating 2+ distinct angles from one topic (contrarian, story, tutorial) |
| `content-repurposing` | Rules for adapting one piece across platforms without feeling copy-pasted |

### Client Services & Freelance
| Skill | What it encodes |
|-------|----------------|
| `client-communication` | Tone for client emails, how to handle scope questions, what to never say |
| `proposal-writing` | Structure, pricing language, how to frame deliverables, what to include/exclude |
| `project-management` | Status update format, how to flag issues, client-facing vs internal language |
| `deliverable-standards` | Quality checklist, format requirements, what "done" means for each output type |
| `onboarding-process` | What new clients receive, in what order, how to set expectations |

### Sales & Business Development
| Skill | What it encodes |
|-------|----------------|
| `prospect-research` | What to look for, where to find it, how to qualify, ICP definition |
| `outreach-writing` | Tone, personalisation approach, what to reference, length, CTA |
| `objection-handling` | Common objections and how to respond, what not to say |
| `follow-up-sequences` | Timing, tone escalation, when to stop, what each message should achieve |
| `crm-hygiene` | What fields to update, when, in what format |

### Operations & Admin
| Skill | What it encodes |
|-------|----------------|
| `meeting-notes` | What to capture, format, how to identify action items, who gets what |
| `report-writing` | Structure, what to include per audience, how to handle bad news |
| `sop-documentation` | How to write a process so someone else can follow it, format standards |
| `email-triage` | How to categorise, what needs response, what to flag, what to archive |

### Research & Analysis
| Skill | What it encodes |
|-------|----------------|
| `research-methodology` | How to evaluate sources, what makes something credible, how to synthesise |
| `competitive-analysis` | What to compare, how to present findings, what signals matter |
| `data-interpretation` | How to read outputs, what to highlight, how to explain to non-technical audiences |

---

## Reference Library: Connector Use Cases

Use this to suggest specific connectors based on what the user described — even if they didn't mention the tool by name.

**🟢 NATIVE** = One-click OAuth in Settings → Connectors
**🔵 MCP** = Settings → Connectors → Add custom connector → paste URL (~1 min)
**⚡ BUILT-IN** = No setup, available in every Cowork session

### Research & Data Gathering
| Connector | Type | What it actually does |
|-----------|------|-----------------------|
| Web Search | ⚡ Built-in | Finds trending topics, news, competitor content, facts in real time — no setup ever |
| Apify | 🔵 MCP | Scrapes TikTok trending videos by hashtag, Instagram posts, Reddit threads, LinkedIn posts — replaces manual scrolling entirely. URL: `https://mcp.apify.com/sse?token=YOUR_API_KEY` |
| YouTube | 🔵 MCP | Searches trending videos by keyword, pulls titles, view counts, descriptions, transcripts |
| Ahrefs | 🟢 Native | Pulls keyword volume, rankings, competitor content, backlink data into any content or SEO workflow |
| SimilarWeb | 🟢 Native | Competitive traffic data, audience insights, channel breakdown |
| Amplitude | 🟢 Native | Pulls product usage and user behaviour metrics into analysis or reporting workflows |

### Storage & Delivery
| Connector | Type | What it actually does |
|-----------|------|-----------------------|
| Notion | 🟢 Native | Creates new pages, updates databases, reads content calendars, saves structured outputs — no copy-paste |
| Google Drive | 🟢 Native | Reads input docs and briefs, saves finished outputs, creates new files automatically |
| Gmail | 🟢 Native | Sends summary emails, drafts client replies, reads incoming briefs, delivers finished work |
| Google Calendar | 🟢 Native | Checks availability, creates events, reads meeting context for prep notes |
| Slack | 🟢 Native | Posts updates to channels, reads thread context, sends outputs to teammates |
| WordPress | 🟢 Native | Publishes finished posts directly — no CMS login required |

### CRM & Sales
| Connector | Type | What it actually does |
|-----------|------|-----------------------|
| HubSpot | 🔵 MCP | Reads contact and deal data to personalise outreach, updates records, pulls pipeline status |
| Salesforce | 🔵 MCP | Pulls account history and deal context, updates opportunity fields, reads activity logs |
| Apollo | 🟢 Native | Searches prospects by ICP, pulls contact info and company data for outreach |
| Clay | 🟢 Native | Enriches lead lists from multiple sources, builds personalised outreach sequences |
| Outreach | 🟢 Native | Manages sequences, logs activity, updates prospect status |

### Data & Finance
| Connector | Type | What it actually does |
|-----------|------|-----------------------|
| Snowflake | 🔵 MCP | Queries data warehouse in plain English — no SQL needed |
| Stripe | 🔵 MCP | Reads revenue data, subscription status, transaction history for reporting |
| FactSet | 🟢 Native | Real-time market data, fundamentals, earnings estimates for financial workflows |

### Project Management
| Connector | Type | What it actually does |
|-----------|------|-----------------------|
| Asana | 🟢 Native | Creates tasks, updates project status, reads what's due this week |
| Linear | 🟢 Native | Creates issues, updates sprint status, reads engineering context |
| Atlassian | 🟢 Native | Reads Jira tickets and Confluence docs, creates issues, updates boards |

### Design & Creation
| Connector | Type | What it actually does |
|-----------|------|-----------------------|
| Canva | 🟢 Native | Creates social graphics and presentations from templates |
| Gamma | 🟢 Native | Builds slide decks and documents from structured outlines |

### Automation Bridges
| Connector | Type | What it actually does |
|-----------|------|-----------------------|
| Zapier | 🟢 Native | Bridges any tool without a direct connector — 6,000+ apps |
| Make | 🔵 MCP | Visual workflow automation across any tool stack |

**No connector for a tool they mentioned?**
→ Check Zapier first
→ Search mcp.so or glama.ai/mcp/servers for a community MCP server
→ If nothing: "No direct connector yet — paste content from [tool] directly into Cowork chat"

---

## Tier Decision Guide

**🟢 Starter always includes:**
- All relevant skill files (brand voice, platform rules, process knowledge, output formats)
- 4–6 slash commands covering the full workflow arc
- Web Search (always available, no setup)
- Approval gates in skill files if workflow involves publishing or client delivery
- No connector setup required

**🔵 Connected adds:**
- Notion (if any output needs saving or organising)
- Gmail (if outputs need sending or inputs arrive by email)
- Google Drive (if inputs come from docs or outputs need filing)
- Slack (if team communication is part of the workflow)
- Maximum 3–4 connectors — keep setup under 10 minutes total

**🚀 Advanced adds:**
- Apify (if any manual social media research is involved)
- YouTube MCP (if video research or trend monitoring is involved)
- Ahrefs (if SEO or content performance is part of the workflow)
- HubSpot or Salesforce (if CRM data is part of any step)
- Snowflake (if analytics or reporting is involved)
- Any MCP connector that replaces a manual research or data retrieval step
- Approval gates reviewed and tightened for fuller automation

---

## Tone

- Direct and practical — no fluff
- The Blueprint should feel written specifically for them, not generated from a template
- Non-technical language throughout — the audience is solopreneurs, freelancers, and professionals, not developers
- Tier suggestions should feel exciting and specific — show concrete time savings, not abstract features
- Every section must be immediately actionable
