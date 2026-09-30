# TA AI Solutions — Solution Page Intake Prompt
### Paste this into a conversation to generate everything needed for a solution page.
### Works two ways: in an existing build conversation, or with a fresh URL.

---

You are helping document an AI solution built by a Talent Attraction team for a public-facing showcase page. Your goal is to produce a complete, ready-to-publish structured summary with as little input from me as possible.

---

## STEP 1 — Figure out what you already know

**Check which situation applies, and act accordingly:**

**→ If this prompt is being added to an existing conversation where we already built or discussed this tool:**
You already have everything you need to understand the tool — what it does, how it works, the tech stack, the problem it solves, and its current status. Do NOT ask me to explain the tool again. Extract that knowledge directly from our conversation history and proceed.

**→ If a URL has been provided alongside this prompt:**
Fetch and study the URL thoroughly. Read the page as if you're a new user encountering this tool for the first time. Understand what it does, who it's for, the key features, and how it works. Do not ask me to describe the tool — you should be able to infer it from the page.

In both cases, make smart assumptions where a reasonable estimate is possible. Clearly label any assumed values with "(estimated)" in the final output so they can be corrected later.

---

## STEP 2 — Ask only what you cannot figure out on your own

Once you understand the tool, ask me **all of your questions in a single message** — no back and forth. Only ask what you genuinely cannot infer.

The only things you will likely need to ask about are:

- **Team size & usage frequency:** How many people on the team use this tool, and roughly how often? (e.g., "5 recruiters, about 3 times per week each")
- **Time before vs. after:** Before this tool, roughly how long did [the task] take a person manually? And with the tool, how long does it take now? (If this is obvious from the nature of the task — e.g., it's clearly a task that took 30–60 min manually — make a reasonable estimate and flag it.)
- **Run costs (only if unclear from the conversation):** If you don't already know the AI model, hosting setup, or API usage, ask in one compact question. If you can infer the tech stack, estimate costs using your knowledge of current API pricing and skip this question.

Do not ask about anything else. If you're uncertain about something non-critical, make a reasonable assumption and note it.

---

## STEP 3 — Research enterprise alternatives automatically

Without asking me anything, search the web for **3 real enterprise SaaS products** that offer a comparable service to this tool. For each one find:

- Product name and parent company
- What it does in one sentence
- Published pricing if available, or a realistic estimate for a TA team of 10–50 people based on market knowledge
- Estimated annual cost for a team this size

Then calculate:
- Average annual cost across the 3 alternatives
- Estimated annual savings of the in-house tool vs. that average

If you cannot find current pricing for a product, use your best estimate based on comparable enterprise software in that category and label it "(estimated from market data)".

---

## STEP 4 — Produce the final output

Once you have everything (from the conversation, the URL, my answers to Step 2, and your research), output the full summary below. Use this exact format — it maps directly to the website template.

Do not include any preamble or explanation before the output block. Just produce the block.

---

```
════════════════════════════════════════════════
TA AI LABS — SOLUTION PAGE SUMMARY
════════════════════════════════════════════════

TOOL NAME:
CATEGORY TAG:   [one of: Automation / Analytics / Content / Research / Communication / Workflow]
ICON EMOJI:     [one emoji that best represents this tool]
STATUS:         [Live / Beta / In Development / Coming Soon]
LAUNCH DATE:    [Month Year  — or —  Expected: Month Year]
ONE-LINER:      [One sentence for the landing page card. Plain language, no jargon.]

────────────────────────────────────────────────
SECTION 1 · WHAT IT DOES
────────────────────────────────────────────────
THE PROBLEM:
[1–2 sentences describing the manual pain point this tool was built to solve.]

THE SOLUTION:
[2–3 sentences explaining how the tool works at a high level: input → process → output.]

FEATURES & CAPABILITIES:
• [Feature 1 — one sentence]
• [Feature 2 — one sentence]
• [Feature 3 — one sentence]
• [Feature 4 — one sentence]

────────────────────────────────────────────────
SECTION 2 · HOW IT HELPS THE TEAM
────────────────────────────────────────────────
BEFORE:
[1–2 sentences: what the manual process looked like, time spent, friction involved.]

AFTER:
[1–2 sentences: what the process looks like now with the tool.]

IMPACT BULLETS:
• Saves approximately [X] hours per [week / month] across the team
• [Quality or consistency improvement]
• [Any other meaningful benefit]

────────────────────────────────────────────────
SECTION 3 · DEMO & SCREENSHOTS
────────────────────────────────────────────────
LIVE LINK:    [URL  — or —  Not yet available]
SCREENSHOTS:  [To be added  — or —  Provided]
NOTES:        [Anything relevant about accessing or demoing the tool]

────────────────────────────────────────────────
SECTION 4 · TECH STACK
────────────────────────────────────────────────
TECHNOLOGIES: [Comma-separated list]
NOTES:        [Optional: one sentence on key architectural decisions if relevant]

────────────────────────────────────────────────
SECTION 5 · COST BREAKDOWN
────────────────────────────────────────────────

RUN COSTS:
┌─────────────────────────┬────────────┬────────────┐
│ Item                    │ Monthly    │ Annual     │
├─────────────────────────┼────────────┼────────────┤
│ AI API usage            │ $X         │ $X         │
│ Hosting / infrastructure│ $X         │ $X         │
│ Maintenance (dev time)  │ ~X hrs     │ ~X hrs     │
│ Other                   │ $X         │ $X         │
├─────────────────────────┼────────────┼────────────┤
│ TOTAL RUN COST          │ ~$X / mo   │ ~$X / yr   │
└─────────────────────────┴────────────┴────────────┘

ENTERPRISE ALTERNATIVES:
┌──────────────────┬───────────────┬────────────────────────────────────┬─────────────────────┐
│ Product          │ Company       │ What It Does                       │ Est. Annual Cost     │
├──────────────────┼───────────────┼────────────────────────────────────┼─────────────────────┤
│ [Product 1]      │ [Company]     │ [One sentence]                     │ $X–Y / yr           │
│ [Product 2]      │ [Company]     │ [One sentence]                     │ $X–Y / yr           │
│ [Product 3]      │ [Company]     │ [One sentence]                     │ $X–Y / yr           │
└──────────────────┴───────────────┴────────────────────────────────────┴─────────────────────┘

Average enterprise cost:      $X / year
Our annual run cost:          $X / year
──────────────────────────────────────────
Estimated annual savings:     $X / year

════════════════════════════════════════════════
END OF SUMMARY — Ready to publish
════════════════════════════════════════════════
```

---

**Start now. State which mode you're operating in (existing conversation or URL), summarize in one sentence what you already know about the tool, then ask your Step 2 questions (if any) all at once.**
