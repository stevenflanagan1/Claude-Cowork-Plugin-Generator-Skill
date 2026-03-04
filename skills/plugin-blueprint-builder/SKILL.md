---
name: plugin-blueprint-builder
description: Interview a user about their workflow or role and generate a complete Claude plugin (Project) specification — including system prompt, recommended skills, connectors, triggers, and example use cases. Use this skill whenever someone wants to build a custom Claude plugin, set up a Claude Project for a specific job function, automate a workflow with Claude, or asks "how do I set up Claude for my work." Also use when someone says "help me build a plugin," "create a custom Claude setup," "I want Claude to help me with [workflow]," or "what connectors should I use." This skill does the diagnostic work so the user ends up with a ready-to-use blueprint they can implement immediately.
---

# Plugin Blueprint Builder

Turn any workflow or role description into a complete, ready-to-implement Claude plugin specification.

## What This Skill Does

Runs a structured interview with the user to understand their workflow, tools, and goals — then generates a complete Plugin Blueprint they can use to build a custom Claude Project (plugin) from scratch.

The output is not advice. It is a spec document they can copy and implement immediately.

---

## Phase 1: Interview

Run the interview in a single conversational message. Do NOT ask questions one at a time — present all questions together so the user can answer in one go. Frame it as quick and low-effort.

### Opening Message (use this exactly):

> **Let's build your Plugin Blueprint.**
>
> Answer these 7 questions and I'll generate a complete spec for your custom Claude plugin — including the system prompt, which skills to use, which connectors to enable, and example prompts to test it with.
>
> ---
>
> **1. What's your role or job title?**
> *(e.g. "Marketing Manager", "Freelance Copywriter", "E-commerce founder")*
>
> **2. What's the ONE task or workflow you want this plugin to help with most?**
> *(Be specific — e.g. "Writing and scheduling LinkedIn posts" or "Summarising client emails and drafting replies")*
>
> **3. What tools or apps are part of this workflow right now?**
> *(e.g. Gmail, Notion, Google Docs, Slack, Asana, Canva, HubSpot — list as many as you use)*
>
> **4. What does the INPUT to this workflow usually look like?**
> *(e.g. "A client brief in a Google Doc", "Raw notes from a meeting", "A URL I want to analyse")*
>
> **5. What does the OUTPUT need to be?**
> *(e.g. "A finished email draft", "A slide deck outline", "A summary with action items")*
>
> **6. How often do you do this task, and what slows you down most?**
> *(e.g. "Daily — I spend 30 mins rewriting the same types of emails")*
>
> **7. What tone, style, or rules should Claude always follow for this work?**
> *(e.g. "Always formal", "Match my brand voice: direct and punchy", "Never use bullet points", "Always ask for approval before finalising")*

---

## Phase 2: Generate the Blueprint

Once the user answers, generate the Plugin Blueprint using the template below. Fill in every section based on their answers. Do not leave placeholders — make real decisions and write real content.

If any answers are vague, make a reasonable assumption and note it with: *(assumption — update if needed)*

---

### Output Template

Use this exact structure when generating the Blueprint:

```
═══════════════════════════════════════════
CLAUDE PLUGIN BLUEPRINT
Generated for: [Role from Q1]
Workflow: [Task from Q2]
═══════════════════════════════════════════

## 1. PLUGIN NAME
[Short, descriptive name — e.g. "LinkedIn Content Assistant" or "Client Email Manager"]

## 2. SYSTEM PROMPT
[Write a complete, ready-to-paste system prompt. 150–300 words. Include:]
- Who Claude is acting as (a specific assistant for their role)
- What the plugin is designed to help with (the core workflow)
- The tools and context it has access to
- Tone and style rules (from Q7)
- Any hard rules or constraints (what it should never do)
- How it should handle ambiguity (e.g. "always ask before finalising")

## 3. RECOMMENDED SKILLS
[List 2–5 skills that would make this plugin more powerful. For each:]

**Skill Name**
- What it does in this context
- When it should trigger
- Example prompt that would activate it

## 4. CONNECTORS TO ENABLE
[List the connectors that match their tools from Q3. For each, specify whether it's Native or MCP:]

**Connector Name** · [🟢 Native — one-click setup | 🔵 MCP — add via custom connector URL]
- Why it's useful for this workflow
- What the plugin will use it to do
- Priority: [Essential / Recommended / Optional]
- For MCP connectors: include the MCP server URL if known, or note where to find it

If a tool they mentioned doesn't have a connector, note: "No direct connector available — use Zapier to bridge it, or paste content directly from [tool]."

## 5. SLASH COMMANDS
[Generate slash commands scaled to workflow complexity:
- Simple, single-task workflows: 3 commands
- Multi-step or multi-output workflows: 4–5 commands
- Complex workflows spanning multiple tools/outputs: up to 6 commands

For each command:]

**/[command-name]**
What it does: [One sentence description]
How to use it: [e.g. "/draft [paste brief here]" or "/review [paste copy here]"]
What Claude will output: [Specific output description]

[Commands should cover the core action, a review/editing variant, and at least one shortcut for the most repetitive sub-task in their workflow]

## 6. CONTEXT FILES TO UPLOAD
[This section tells the user what to drop into their Project's knowledge base to dramatically improve output quality. Tailor specifically to their role and workflow.]

These are files and documents Claude will reference every time it works in this plugin. The more context you give it, the better the output.

**Essential (upload before your first session):**
- [File type + what it should contain — e.g. "Brand Voice Guide — your tone rules, words to use/avoid, example copy"]
- [e.g. "Audience Persona doc — who you're writing for, their pain points, vocabulary they use"]
- [e.g. "Output Template — an example of your ideal finished output so Claude matches your format"]

**Recommended (add when available):**
- [e.g. "Past campaign examples — 3–5 pieces of high-performing content Claude can learn your style from"]
- [e.g. "Competitor reference doc — brands/creators you admire or want to differentiate from"]

**Optional but high-value:**
- [e.g. "Product/service one-pager — what you sell, key messages, USPs"]
- [e.g. "Client brief template — your standard intake format so Claude knows what questions to ask"]

> 💡 Tip: You don't need perfect documents. Even rough notes work. A half-page on your brand voice beats nothing.

## 7. PROJECT SETUP: WHAT GOES WHERE
[This section explains the difference between the system prompt and uploaded files — always include this, written simply for non-technical users]

When you build this plugin, you have two places to give Claude information. Here's the difference:

**Project Instructions (the system prompt above)**
This is Claude's permanent briefing. It tells Claude *who it is*, *what it's for*, and *how it should always behave* in this plugin. Paste the system prompt from Section 2 here. Don't put specific documents or data here — keep it to rules and role definition.

**Project Knowledge (uploaded files)**
This is Claude's reference library. Upload the context files listed in Section 6 here. Claude will automatically refer to these whenever it's working in this plugin. Update them as your brand, audience, or campaigns evolve.

Think of it this way: Instructions = the job description. Knowledge = the briefing folder.

## 8. APPROVAL GATES
[Only include this section if the workflow involves any of the following: publishing or sending outputs, client-facing deliverables, multi-step workflows where step 2 depends on step 1 being correct, or brand/legal sensitivity. If the workflow is purely internal and low-stakes (e.g. summarising notes for personal use), skip this section entirely and note why.]

These are the moments in your workflow where Claude should stop and wait for your sign-off before continuing. Without these, Claude will barrel through to the end — which sounds efficient until it sends the wrong email.

[Generate 2–4 gates scaled to workflow complexity. For each:]

**Gate [N]: [Name of the checkpoint — e.g. "Brief Confirmation" or "Draft Review"]**
- When it triggers: [At what point in the workflow this pause happens]
- What Claude should do: [e.g. "Present the draft and ask: 'Does this look right before I format it for sending?'"]
- What you're checking for: [What the user should actually review at this moment]
- How to enforce it: Add this line to your system prompt → "[exact instruction to paste]"

> ⚠️ If you're using this plugin for anything that gets sent to a client or published publicly, at minimum add Gate 1 (output review before delivery). One bad send costs more time than the review ever would.

## 9. EXAMPLE PROMPTS TO TEST YOUR PLUGIN
[Write 5 real example prompts the user can paste immediately to test the plugin works correctly. Make them specific to their workflow — not generic. At least one should test a slash command, and one should trigger an approval gate if Section 8 is included.]

1. [Prompt]
2. [Prompt]
3. [Prompt]
4. [Prompt — tests a slash command]
5. [Prompt — triggers an approval gate, if applicable]

## 10. WHAT TO BUILD NEXT
[1–3 sentences. Suggest one natural extension or upgrade they could add once the core plugin is working — e.g. adding a second skill, enabling an additional connector, refining the system prompt, or improving context files.]

═══════════════════════════════════════════
READY TO BUILD? Follow the step-by-step setup guide at [your guide URL].
═══════════════════════════════════════════
```

---

## Phase 3: Offer to Refine

After delivering the Blueprint, say:

> **Your Plugin Blueprint is ready.**
>
> You can copy the system prompt directly into your Claude Project settings. If anything doesn't look right — wrong tone, missing a tool, needs a different focus — just tell me and I'll update it.
>
> Ready to build it? [Link to setup guide]

---

## Writing Rules for the Blueprint

**System Prompt quality standards:**
- Write in second person to Claude ("You are a [role] assistant...")
- Be specific about what Claude should and should not do
- Include at least one concrete example of the expected output format if helpful
- Keep it scannable — use short paragraphs, not walls of text

**Slash command standards:**
- Commands should feel like natural shortcuts for the most repeated actions in the workflow
- Name them intuitively — `/draft`, `/review`, `/summarise`, `/repurpose`, `/brief`, `/respond`
- Each command should have a clear, predictable output so the user knows exactly what they'll get
- Scale quantity to complexity: 3 for simple workflows, up to 6 for complex multi-output workflows
- Always include at least one "input → output" command (the core task) and one editing/review command

**Context file recommendations:**
- Think role-first: what does someone in this job actually have sitting on their desktop?
- Separate Essential (must-have before first use) from Recommended and Optional
- Be specific about what should be IN each file, not just what to call it
- Always include the "rough notes work fine" reassurance — non-technical users often wait for perfect docs
- Common high-value files by workflow type:
  - Content/marketing: brand voice doc, audience personas, past examples, competitor refs
  - Sales/BD: product one-pager, objection handling doc, email templates, ICP profile
  - Operations/admin: SOP docs, templates, team contacts, approval process notes
  - Finance/reporting: report templates, terminology glossary, stakeholder preferences

**Project instructions vs. knowledge explainer:**
- Always include Section 7 — most users don't know this distinction exists
- Keep the language simple: "Instructions = job description, Knowledge = briefing folder"
- Never use technical terms like "system prompt" in this section without explaining them

**Approval gates standards:**
- ONLY include Section 8 when the workflow involves: sending/publishing outputs, client-facing deliverables, multi-step dependencies, or brand/legal sensitivity
- Purely internal, low-stakes workflows (e.g. personal note summaries, research lookups) should skip it — note why so users understand the logic
- Gates should be named for the *moment* they occur, not the action (e.g. "Brief Confirmation" not "Check the brief")
- Each "How to enforce it" line should be a literal paste-ready sentence for the system prompt — not a description of what to write
- Scale to complexity: simple workflows get 1–2 gates max, complex multi-step workflows can have 3–4
- The warning callout (⚠️) is mandatory whenever client-facing or published content is involved

**Connector recommendations:**
- Recommend connectors in two tiers: **Native** (one-click, in the Claude directory) and **MCP** (custom URL, requires a minute of setup)
- Native connectors are easier — prioritise these when available
- MCP connectors unlock hundreds more tools — don't avoid them, just explain the extra step
- If a tool has no connector at all, note the Zapier/Make workaround
- See the full reference table below

**Skill recommendations:**
- Draw from the user's actual installed skills if context is available
- If unknown, recommend based on workflow type
- Never recommend more than 5 skills — focus on the highest-impact ones

---

## Available Connectors Reference

There are two types of connectors. Always indicate which type when recommending one.

**🟢 NATIVE** = One-click setup from Settings > Connectors. Verified by Anthropic.
**🔵 MCP** = Add via Settings > Connectors > "Add custom connector" using an MCP server URL. Takes ~1 minute. Not verified by Anthropic but widely used.

### Productivity & Project Management
| Connector | Type | Best for |
|-----------|------|----------|
| Asana | 🟢 Native | Task creation, project tracking, status updates |
| Notion | 🟢 Native | Docs, wikis, knowledge bases, project notes |
| Atlassian Rovo | 🟢 Native | Jira tickets, Confluence docs, dev team workflows |
| Linear | 🟢 Native | Engineering issue tracking, sprint management |
| Zapier | 🟢 Native | Connecting any tool without a direct connector |
| Box | 🟢 Native | Cloud file storage and document access |

### Communication & Email
| Connector | Type | Best for |
|-----------|------|----------|
| Gmail | 🟢 Native | Email drafting, thread summaries, auto-replies |
| Google Calendar | 🟢 Native | Scheduling, meeting prep, agenda creation |
| Slack | 🟢 Native | Team comms, channel summaries, message drafting |
| Microsoft 365 | 🟢 Native | Outlook, Teams, SharePoint (Team/Enterprise plans only) |

### Files & Knowledge
| Connector | Type | Best for |
|-----------|------|----------|
| Google Drive | 🟢 Native | Reading/writing docs, research, storing outputs |
| Dropbox | 🔵 MCP | File access and document retrieval |
| OneDrive | 🟢 Native (via M365) | Microsoft file ecosystem |

### Design & Content Creation
| Connector | Type | Best for |
|-----------|------|----------|
| Canva | 🟢 Native | Social graphics, presentations, visual content |
| Gamma | 🟢 Native | Slide decks and document generation |
| Figma | 🟢 Native | Design file access, UI/UX workflows |
| WordPress.com | 🟢 Native | Publishing blog posts, managing CMS content |

### Sales, Marketing & CRM
| Connector | Type | Best for |
|-----------|------|----------|
| HubSpot | 🔵 MCP | CRM contacts, deals, email sequences |
| Salesforce | 🔵 MCP | Pipeline management, account records, reporting |
| ActiveCampaign | 🟢 Native | Email marketing automation and campaign data |
| Amplitude | 🟢 Native | Product analytics and user behaviour insights |
| Ahrefs | 🟢 Native | SEO research, keyword data, backlink analysis |
| Bitly | 🟢 Native | Link shortening and click tracking |

### Developer & Data Tools
| Connector | Type | Best for |
|-----------|------|----------|
| GitHub | 🔵 MCP | Code review, PR summaries, repo management |
| Snowflake | 🔵 MCP | Data warehouse queries and analytics |
| Stripe | 🔵 MCP | Payment data, subscription info, transaction history |
| PayPal / Square | 🟢 Native | Payment and business transaction data |
| AWS Marketplace | 🟢 Native | Cloud service discovery and management |

### Finance & Operations
| Connector | Type | Best for |
|-----------|------|----------|
| Airwallex | 🟢 Native | Financial operations and payment workflows |
| Aiera | 🟢 Native | Financial events, filings, company intelligence |

### The "Connect Everything Else" Options
| Connector | Type | Best for |
|-----------|------|----------|
| Zapier | 🟢 Native | 6,000+ app automations via triggers |
| Make (Integromat) | 🔵 MCP | Visual workflow automation across any tool |

**No connector for a tool the user mentioned?**
→ First check if Zapier or Make can bridge it.
→ If not, note: "No direct connector available — Claude can work with copy-pasted content from [tool] instead."

---

## Tone for This Skill

- Direct and practical — no fluff
- The Blueprint should feel like it was made specifically for them, not generated
- Avoid jargon — the audience is non-technical professionals
- Every section should feel immediately actionable
