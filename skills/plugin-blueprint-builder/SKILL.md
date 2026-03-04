---
name: plugin-blueprint-builder
description: Interview a user about their workflow or role and generate a complete Claude Cowork plugin specification — including skills folder content, slash commands, MCP connector config, context files, and approval gates. Use this skill whenever someone wants to build a custom Cowork plugin, automate a workflow with Claude, or asks "how do I set up Claude for my work." Also use when someone says "help me build a plugin," "create a custom Claude setup," "I want Claude to help me with [workflow]," or "what connectors should I use." This skill produces a ready-to-hand-to-Plugin-Create Blueprint so the user can build their plugin immediately — no coding required.
---

# Plugin Blueprint Builder

Turn any workflow or role description into a complete, ready-to-build Claude Cowork plugin specification.

## What This Skill Does

Runs a structured interview with the user to understand their workflow, tools, and goals — then generates a complete Plugin Blueprint covering every component of a Cowork plugin: skills, slash commands, MCP connectors, context files, and approval gates.

The Blueprint is designed to be handed directly to Plugin Create (Claude's built-in plugin builder in Cowork) so the user can build their plugin immediately through a guided conversation — no coding, no manual file editing.

The output is not advice. It is a complete spec document ready to implement.

---

## What Is a Cowork Plugin

Before generating the Blueprint, understand what you are designing. A Cowork plugin is a folder of plain text files that turns Claude into a specialist for a specific workflow. It has four core components:

**Skills** (`skills/skill-name/SKILL.md`)
Domain knowledge Claude draws on automatically when the context is relevant. Skills are always-on — the user doesn't trigger them manually. A skill file teaches Claude how to do something: your brand voice rules, your platform-specific content format, your workflow process, your industry knowledge.

**Commands** (`commands/command-name.md`)
Specific actions the user triggers manually with a slash command (e.g. `/draft`, `/ideate`, `/review`). Commands are for discrete, repeatable tasks where the user decides when to run them.

**MCP Connectors** (`.mcp.json`)
The tools Claude connects to — Gmail, Notion, Google Drive, Slack, HubSpot, and hundreds more via the Model Context Protocol. Connectors let Claude read from and take actions in the user's actual tools during a Cowork session.

**Manifest** (`.claude-plugin/plugin.json`)
The label on the package. Tells Cowork the plugin's name, version, and where to find everything else.

Plugin Create (a built-in Cowork plugin) builds all of these files automatically through a conversation. The Blueprint this skill generates is the input to that conversation.

---

## Phase 1: Interview

Run the interview in a single conversational message. Do NOT ask questions one at a time — present all questions together so the user can answer in one go. Frame it as quick and low-effort.

### Opening Message (use this exactly):

> **Let's build your Plugin Blueprint.**
>
> Answer these 7 questions and I'll generate a complete spec for your custom Cowork plugin — including which skills to create, which tools to connect, what slash commands to set up, and example prompts to test it with. Then you can hand the Blueprint straight to Plugin Create and build it in minutes.
>
> ---
>
> **1. What's your role or job title?**
> *(e.g. "Freelance Copywriter", "Social Media Manager", "E-commerce founder", "Marketing Consultant")*
>
> **2. What's the ONE workflow you want this plugin to handle?**
> *(Be specific about the full flow — e.g. "Every week I find trending topics, turn them into LinkedIn posts and TikTok scripts, then schedule them" or "I receive client briefs by email, write copy, send for approval, then publish")*
>
> **3. What tools or apps are part of this workflow right now?**
> *(List everything you touch — e.g. Gmail, Notion, Google Drive, Slack, Asana, Canva, HubSpot, Airtable. The more you list, the better Claude can connect to them directly.)*
>
> **4. What does the INPUT to this workflow usually look like?**
> *(e.g. "A client brief in a Google Doc", "Raw notes from a voice memo", "A URL or article I want to react to", "A trending topic I spotted")*
>
> **5. What does the finished OUTPUT need to be?**
> *(e.g. "A ready-to-post LinkedIn carousel", "A TikTok script with hook", "A client email draft", "A summary with action items saved to Notion")*
>
> **6. How often do you do this, and what slows you down most?**
> *(e.g. "Daily — I waste 45 mins going from idea to first draft" or "Weekly — the bottleneck is repurposing one piece into 3 formats")*
>
> **7. What tone, style, or rules must Claude always follow?**
> *(e.g. "Direct and punchy, no corporate speak", "Always match my brand voice", "Never publish without my approval", "Platform rules: TikTok needs a hook in 2 seconds, LinkedIn no hashtags")*

---

## Phase 2: Generate the Blueprint

Once the user answers, generate the Plugin Blueprint using the template below. Fill in every section based on their answers. Do not leave placeholders — make real decisions and write real content.

If any answers are vague, make a reasonable assumption and note it with: *(assumption — update if needed)*

**Critical rules for this Blueprint:**
- This is a Cowork plugin spec, NOT a Claude Project spec. Never use the words "Project Instructions" or "Project Knowledge" — use "skills folder" and "skill files" instead.
- Always recommend MCP connectors for any tool the user mentioned. Do not skip connectors because they require setup — explain the setup is one minute.
- Always generate at least 4 skills and 4 slash commands for any workflow with multiple steps or outputs.
- Web search is a built-in Cowork capability — recommend it as a connector for any workflow involving research, trend monitoring, or external data.

---

### Output Template

Use this exact structure when generating the Blueprint:

```
═══════════════════════════════════════════
CLAUDE COWORK PLUGIN BLUEPRINT
Generated for: [Role from Q1]
Workflow: [Task from Q2]
═══════════════════════════════════════════

## 1. PLUGIN NAME
[Short, descriptive name — e.g. "AI Content Pipeline" or "Client Email Manager"]

## 2. PLUGIN PURPOSE (for Plugin Create)
[Write 3–5 sentences describing what this plugin does, who it's for, and what problem it solves. This is what you paste to Plugin Create when it asks what you want to build. Write it in plain English — not technical language.]

## 3. SKILLS TO CREATE
[Generate 3–6 skill files. For multi-platform or multi-step workflows, each major area gets its own skill. Skills are always-on — Claude draws on them automatically when relevant.]

For each skill:

**Skill: [skill-folder-name]**
File location: `skills/[skill-folder-name]/SKILL.md`
Purpose: [What domain knowledge or process this skill encodes]
Always active when: [What context or task triggers Claude to use this skill]
What to put in it: [Specific content to include — e.g. "Your brand voice rules, tone examples, words to avoid, platform-specific formatting rules for TikTok, LinkedIn, and Threads"]
Example that activates it: "[A real example prompt that would trigger this skill]"

[Minimum skills to include based on workflow type:
- Content/marketing workflows: brand-voice skill + one skill per platform/output type + trend-research skill
- Client-facing workflows: communication-style skill + deliverable-format skill + client-context skill
- Operations workflows: process-rules skill + template skill + output-format skill
- Research workflows: research-methodology skill + synthesis-format skill + source-evaluation skill]

## 4. SLASH COMMANDS
[Generate 4–6 commands scaled to workflow complexity. Commands are manually triggered by the user for specific, repeatable tasks.]

For each command:

**/[command-name]**
What it does: [One sentence]
How to use it: [e.g. "/draft [paste your brief or topic here]"]
What Claude outputs: [Specific, concrete description of the output]
Which skills it uses: [Which skill files Claude draws on when this command runs]

[Always include:
- At least one "research or gather input" command (e.g. /trends, /research, /brief)
- At least one "create or draft" command (e.g. /draft, /write, /create)  
- At least one "repurpose or adapt" command (e.g. /repurpose, /adapt, /reformat)
- At least one "review or refine" command (e.g. /review, /refine, /edit)
- Optional: a "save or organise" command if Notion/Drive connectors are included]

## 5. MCP CONNECTORS (.mcp.json)
[This is the most important section for Cowork. List every connector needed based on the tools from Q3. Always specify type and setup method.]

**How connectors work in Cowork:**
- 🟢 Native connectors: Enable in Settings → Connectors with one click (OAuth login)
- 🔵 MCP connectors: Add in Settings → Connectors → "Add custom connector" → paste the MCP server URL (takes ~1 minute)
- Plugin Create will write the .mcp.json file automatically when you tell it which tools to connect

For each connector:

**[Tool Name]** · [🟢 Native | 🔵 MCP]
Why it's needed: [Specific reason based on their workflow]
What Claude will do with it: [Concrete actions — e.g. "Read your content calendar, create new entries when a draft is approved"]
Priority: [Essential / Recommended / Optional]
Setup: [For Native: "Enable in Settings → Connectors" | For MCP: include server URL or where to find it]

[Standard connector recommendations by workflow type:
- Content/social media: Google Drive 🟢 (store scripts/assets), Notion 🟢 (content calendar), Gmail 🟢 (brand comms), Web Search (built-in, trend research)
- Client services: Gmail 🟢 (client comms), Google Drive 🟢 (briefs/deliverables), Notion 🟢 (project tracking), Slack 🟢 (team comms)
- Sales/BD: HubSpot 🔵 or Salesforce 🔵 (CRM), Gmail 🟢 (outreach), Notion 🟢 (pipeline notes), Google Drive 🟢 (proposals)
- Operations: Notion 🟢 (SOPs/docs), Asana 🟢 (tasks), Gmail 🟢 (comms), Google Drive 🟢 (files)

Always recommend Web Search as a connector for any workflow involving research, trends, or external information — it is built into Cowork and requires no setup.]

**No connector available for a tool they mentioned?**
→ Check if Zapier 🟢 (Native) can bridge it
→ If not: "No direct connector available — paste content from [tool] directly into your Cowork chat"

## 6. CONTEXT FILES FOR SKILL FOLDERS
[Tell the user exactly what content to add to each skill file to maximise output quality. This replaces the generic "upload files" advice — in Cowork, context lives inside the skill files themselves, not in a separate knowledge base.]

For each skill from Section 3, specify what real-world content to paste into it:

**For [skill-name]:**
Paste in: [Specific content — e.g. "Your brand voice rules: 3–5 sentences that sound like you, a list of words you use vs words to avoid, your tone description in plain English"]
Also add: [Secondary content — e.g. "2–3 examples of content you've written that you're proud of — Claude will use these to match your style"]
Optional: [Nice-to-have content]

> 💡 Rough notes work fine. A half-page of bullet points about your brand voice beats a polished document you never write. Add context now, refine it later.

## 7. HOW TO BUILD THIS PLUGIN
[Plain-English instructions for using Plugin Create to turn this Blueprint into an actual plugin. Always include this section.]

You don't need to create any files manually. Plugin Create does all of it.

**Step 1:** Open Claude Desktop → switch to the Cowork tab
**Step 2:** Go to Customize → Browse plugins → find and install Plugin Create
**Step 3:** Launch Plugin Create (type /plugin-create or click + → Plugin Create)
**Step 4:** When Plugin Create asks what you want to build, paste Section 2 (Plugin Purpose) from this Blueprint
**Step 5:** When it asks about skills, paste Section 3
**Step 6:** When it asks about commands, paste Section 4
**Step 7:** When it asks about connectors/tools, paste Section 5
**Step 8:** Plugin Create builds all the files and delivers a .plugin file to your outputs folder
**Step 9:** Install it via Customize → Browse plugins → Upload plugin
**Step 10:** Run the test prompts from Section 9 to confirm everything works

## 8. APPROVAL GATES
[Only include this section if the workflow involves: publishing content publicly, sending to clients, multi-step workflows where step 2 depends on step 1, or brand/legal sensitivity. Skip for purely internal workflows and explain why.]

These are moments where Claude should stop and wait for your sign-off before continuing. Add these as instructions inside the relevant skill files.

**Gate [N]: [Checkpoint Name]**
Triggers when: [What moment in the workflow]
Claude should: [Exactly what to say/show before pausing]
You're checking for: [What to review at this moment]
Add this to your skill file: "[Exact instruction text to paste into the skill file]"

> ⚠️ If this plugin publishes or sends anything publicly or to clients, Gate 1 (draft review before delivery) is non-negotiable. One wrong send costs more time than the review ever would.

## 9. TEST PROMPTS
[Write 5 specific prompts the user can paste immediately after installing to verify the plugin works. Make them real and specific to their workflow — not generic. At least one tests a slash command, one tests a connector, one tests an approval gate if included.]

Use these in order after installing:

1. [Tests that skills are active and tone is correct]
2. [Tests a slash command end-to-end]
3. [Tests that a connector is pulling real data]
4. [Tests a multi-step workflow]
5. [Tests an approval gate, if applicable — or tests a second slash command]

## 10. WHAT TO BUILD NEXT
[1–3 sentences. One specific upgrade once the core plugin is running — an additional skill, a new connector, a scheduled task, or a refinement to the approval gates.]

═══════════════════════════════════════════
READY TO BUILD?
→ Open Claude Desktop → Cowork tab → install Plugin Create → paste this Blueprint
→ Full step-by-step guide: https://github.com/stevenflanagan1/Claude-Cowork-Plugin-Generator-Skill
═══════════════════════════════════════════
```

---

## Phase 3: Offer to Refine

After delivering the Blueprint, say:

> **Your Plugin Blueprint is ready.**
>
> Copy Section 2 (Plugin Purpose) and paste it to Plugin Create in Cowork to start building. If anything doesn't look right — missing a tool, wrong commands, needs a different focus — just tell me and I'll update the Blueprint before you build.
>
> Need the step-by-step build guide? → https://github.com/stevenflanagan1/Claude-Cowork-Plugin-Generator-Skill

---

## Writing Rules for the Blueprint

**Skills quality standards:**
- Each skill should have a clear, specific name that describes what it knows (not what it does)
- Good skill names: `brand-voice`, `tiktok-content-rules`, `client-communication-style`, `trend-research-process`
- Bad skill names: `helper`, `main-skill`, `writing`
- Tell the user exactly what real-world content to paste into each skill — not just "add your brand voice" but "paste 3–5 sentences that sound like you, your tone rules, words you use vs avoid"
- Skills for content workflows should always be platform-specific when the workflow involves multiple platforms

**Slash command standards:**
- Commands should feel like natural shortcuts for the most repeated actions
- Name them intuitively — `/draft`, `/ideate`, `/trends`, `/review`, `/repurpose`, `/brief`, `/respond`
- Each command must have a clear, predictable output the user can describe in one sentence
- Always cover the full workflow arc: research → create → repurpose → review
- Scale to complexity: 4 commands minimum for any multi-step workflow, up to 6 for complex multi-tool workflows

**MCP connector standards:**
- Never recommend zero connectors for a workflow that involves external tools
- Always explain what Claude will specifically DO with each connector — not just that it "connects"
- Prioritise Native connectors (easier) but never skip MCP connectors just because they need setup
- Web Search is free and built in — always recommend it for research/trend workflows
- For every tool the user mentioned with no connector, explicitly suggest Zapier as a bridge

**Approval gate standards:**
- Only include when output is published, sent to clients, or has multi-step dependencies
- Each gate instruction must be a literal, paste-ready sentence for the skill file — not a description
- Name gates for the moment they occur, not the action (e.g. "Draft Review" not "Check the draft")
- Scale: 1–2 gates for simple publish workflows, 3–4 for complex client-facing multi-step workflows
- The ⚠️ warning is mandatory for any public or client-facing workflow

**Cowork-specific language rules:**
- Never say "Project Instructions" — say "skill files" or "skills folder"
- Never say "Project Knowledge" — say "context in your skill files"  
- Never say "system prompt" to the user — say "plugin purpose" or "how Claude is briefed"
- Always refer to Plugin Create as the build tool, not manual file creation
- The output goes to a .plugin file the user installs — always mention this

---

## Available Connectors Reference

**🟢 NATIVE** = One-click in Settings → Connectors. Verified by Anthropic.
**🔵 MCP** = Settings → Connectors → "Add custom connector" → paste MCP URL. ~1 minute setup.
**⚡ BUILT-IN** = Available in Cowork by default, no setup needed.

### Always-Available (Built-in to Cowork)
| Capability | Type | Best for |
|-----------|------|----------|
| Web Search | ⚡ Built-in | Trend research, current events, competitor analysis, fact-checking |
| Local File Access | ⚡ Built-in | Reading/writing files on the user's computer |

### Productivity & Project Management
| Connector | Type | Best for |
|-----------|------|----------|
| Asana | 🟢 Native | Task creation, project tracking, status updates |
| Notion | 🟢 Native | Docs, wikis, content calendars, project notes |
| Atlassian Rovo | 🟢 Native | Jira tickets, Confluence docs |
| Linear | 🟢 Native | Engineering issue tracking |
| Zapier | 🟢 Native | Bridge to any tool without a direct connector |
| Box | 🟢 Native | Cloud file storage |

### Communication & Email
| Connector | Type | Best for |
|-----------|------|----------|
| Gmail | 🟢 Native | Email drafting, thread summaries, sending |
| Google Calendar | 🟢 Native | Scheduling, meeting prep |
| Slack | 🟢 Native | Team comms, message drafting, channel summaries |
| Microsoft 365 | 🟢 Native | Outlook, Teams, SharePoint |

### Files & Knowledge
| Connector | Type | Best for |
|-----------|------|----------|
| Google Drive | 🟢 Native | Read/write docs, store outputs, access assets |
| Dropbox | 🔵 MCP | Cloud file access |

### Design & Content
| Connector | Type | Best for |
|-----------|------|----------|
| Canva | 🟢 Native | Social graphics, visual content |
| Gamma | 🟢 Native | Slide decks, documents |
| Figma | 🟢 Native | Design files |
| WordPress.com | 🟢 Native | Blog publishing |

### Sales, Marketing & CRM
| Connector | Type | Best for |
|-----------|------|----------|
| HubSpot | 🔵 MCP | CRM, deals, email sequences |
| Salesforce | 🔵 MCP | Pipeline, accounts, reporting |
| ActiveCampaign | 🟢 Native | Email marketing automation |
| Ahrefs | 🟢 Native | SEO research, keyword data |
| Amplitude | 🟢 Native | Product analytics |

### Developer & Data
| Connector | Type | Best for |
|-----------|------|----------|
| GitHub | 🔵 MCP | Code review, PRs, repo management |
| Snowflake | 🔵 MCP | Data warehouse queries |
| Stripe | 🔵 MCP | Payment data, subscriptions |

### Automation Bridges
| Connector | Type | Best for |
|-----------|------|----------|
| Zapier | 🟢 Native | 6,000+ app automations |
| Make | 🔵 MCP | Visual workflow automation |

---

## Tone for This Skill

- Direct and practical — no fluff
- The Blueprint should feel like it was written specifically for them, not generated
- Avoid technical jargon — the audience is non-technical professionals
- Every section must feel immediately actionable
- When in doubt, be more specific — a vague recommendation helps no one
