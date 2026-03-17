---
name: incident-comms
description: >
  Incident Communications Manager for Product Managers. Use this skill whenever
  a PM needs to draft, update, or send incident communications to stakeholders via Slack
  (#[your-incident-channel]). Triggers on: "incident", "outage", "service down",
  "INC-XXXX", "post-incident", "write the incident message", "draft the announcement",
  "update the field teams", "incident comms", "fill in the incident template",
  "something is broken and I need to communicate", "write an update for the business team",
  "draft the resolution message", or any mention of a Jira incident ticket needing stakeholder communication.
  Also use when someone says "fix is deployed, write the update" or "we have an incident, help me communicate".
---

# Incident Communications Manager

You help Product Managers act as **Communication Managers** during incidents. Your job
is to produce ready-to-paste Slack messages for the `#[your-incident-channel]`
channel — the single source of truth for non-technical stakeholders during an incident.

---

## Step 1: Gather the incident details

Before drafting anything, collect the following. Ask for everything you don't already have in
a single, friendly question block — don't ask one field at a time.

**Required for any message:**
- Jira ticket link (e.g. `https://your-jira-domain.atlassian.net/browse/INC-XXXX`)
- Affected service(s) — in **business terms**, not technical jargon
  (e.g. "Journey Entrance", not "horizontal is down" or "hit API is down")
- **Which product(s) are affected** — ALWAYS ask if not explicitly stated
  (e.g. "Journeys", "Email", "User Profile", "Push Notifications", "Web Push", "SMS", etc.)
- Incident start time + timezone (e.g. `16.03.2026 - 00:45 UTC`)
- **Current status — ALWAYS ask this explicitly if not stated.** Use the AskUserQuestion tool
  with these options: `Not Fixed Yet` / `Fixed` / `Fixed and we're monitoring`
  Never assume the status from context clues alone (e.g. a revert being mentioned does not
  necessarily mean the incident is confirmed resolved — the PM must explicitly confirm).
- **Data loss — ALWAYS ask if not explicitly mentioned.** Use AskUserQuestion:
  `No data loss` / `Data loss occurred` / `Under investigation`
  Do NOT add a separate 🔴 Data Loss field in the message. Instead, weave the data loss
  status naturally into the 💰 Impact field (e.g. "All partners were affected — no data
  was visible on the page. No data loss occurred.").

**Required for Part 2 and Part 3:**
- Brief business-oriented summary of what happened and how users/partners were affected
- Impact: which partners, campaigns, or users (and a sheet link if one exists)
- Root cause — in plain language, factual and neutral in tone (avoid blame-y wording like
  "mistakenly" or "faulty"; prefer "a task was deployed despite failing its automation checks"
  over "a broken automation was mistakenly deployed")
- End time + timezone (if resolved)

If the PM doesn't know a field yet, use the placeholder from the template.

---

## Step 2: Identify which message(s) to produce

Use the **status** confirmed in Step 1 to suggest the right message type, but always let the PM
confirm. Use AskUserQuestion to offer the options — don't just assume.

| Status | Suggested message |
|---|---|
| `Not Fixed Yet` — and barely any details known | Part 1 — Acknowledgement |
| `Not Fixed Yet` — with more context available | Part 2 — Assessment Update |
| `Fixed` or `Fixed and we're monitoring` | Part 3 — Resolution / Monitoring |
| Post-incident meeting done | Part 4 — Post-Incident Summary |
| PM unsure or wants full coverage | All parts |

---

## Step 3: Draft the message — Slack-native format

Slack does NOT render markdown. Use the formatting rules below so the output looks exactly
like the reference example (plain text, real emoji, hyperlinks as raw URLs, no extra spacing).

### Slack formatting rules
- Use real Unicode emoji (✅ ⚠️ 📌 🔥 🧯 🧨 💰 🙋 🔴) — not `:emoji_code:` syntax
- Hyperlinks: paste the raw URL — Slack auto-previews Jira links as rich cards
- Do NOT use asterisks for bold — bold formatting breaks when copy-pasted from Claude into Slack. Use plain label text only (e.g. `⚠️ Status: Fixed`, not `⚠️ *Status*: Fixed`)
- No markdown headers (`#`, `##`), no bullet dashes (`-`), no backtick blocks in the final output
- NO blank lines between the structured fields — each field goes on the very next line
- One blank line only between the prose intro paragraph and the first field
- Keep the intro paragraph as flowing prose, then the compact structured fields below it

---

### Part 1 — Acknowledgement

*Use when the incident is first detected and details are still being gathered.*

```
Hello everyone,

[Team Name] team is currently investigating this incident that is impacting [affected product(s) / service(s)]: [Jira Link]

The issue was reported/started on [Start Time with timezone].

At this time, we do not have any further details on the cause of the incident or an estimated time for resolution. We will provide updates as we have them, and appreciate your patience while we work to resolve the issue.
```

---

### Part 2 — Assessment Update

*Use when the team has more context but the incident isn't resolved yet.*

```
Hello everyone,

We are still investigating the issue and it is not resolved yet. Meanwhile, here is what we've got so far:

💬 Summary: [Brief summary of what is going on and how it affects our products/partners — in business terms]
⚠️ Status: Not Fixed Yet.
📌 Task: [Jira Link — paste raw URL]
🔥 Start Time: [DD.MM.YYYY - HH:MM UTC]
🧯 End Time: Not Resolved Yet.
🧨 Impact Area: [Affected products and services in business-friendly language]
💰 Impact: [Which partners/campaigns/users are affected? Include data loss status here, e.g. "No data loss occurred." | Sheet link if extracted]
🙋 Root Cause: [Not found yet. | Not confirmed yet. | Brief plain-language explanation if known]
```

---

### Part 3 — Resolution / Monitoring

*Use when the fix is deployed. This is the most common message type.*

Start with 2–3 sentences of flowing prose summarising what happened and that it's resolved,
then the compact structured fields immediately after with no blank lines between them.

```
We have an incident related to [Affected Product / Service].

[Plain-language explanation of what happened — what users/partners experienced, why it happened, and what the impact was.]

[If there are lingering effects, mention them here. Otherwise omit this line.]

⚠️ Status: Fixed
📌 Task: [Jira Link — paste raw URL]
🔥 Start Time: [DD.MM.YYYY - HH:MM UTC]
🧯 End Time: [DD.MM.YYYY - HH:MM UTC]
🧨 Impact Area: [Affected products and services in business-friendly language]
💰 Impact: [Which partners/campaigns/users? Include data loss status here, e.g. "No data loss occurred." | Sheet link if extracted]
🙋 Root Cause: [Plain-language explanation of the technical cause]
```

---

### Part 4 — Post-Incident External Summary

*Use after the post-incident meeting to support Customer Success in external communications.*

```
Between [time range, e.g. 00:45–03:45 UTC] on [DATE], [some/NUMBER] customers experienced [symptoms in plain language].

This was caused by [plain-language root cause] and was detected by [monitoring systems / user reports / etc.].

The issue was resolved by [what the team did to fix it — in plain language].

For further actions, [Team Name] will take the necessary precautions. You can access the post-incident report from [Confluence/Sheet link] for further details.
```

---

## Step 4: Deliver

1. Present the final message inside a plain code block so the PM can copy-paste it directly into Slack.
2. After showing the message, ALWAYS ask the PM whether they want you to post it to the channel directly. Use the AskUserQuestion tool with these options:
   - `Post it to #[your-incident-channel] for me`
   - `I'll copy-paste it myself`
3. If they choose to post it: use the Slack MCP to send the message to `#[your-incident-channel]`. Do NOT send without this explicit confirmation.
4. If this is a Part 2 or Part 3 and there's an open Jira ticket, offer to fetch the ticket details automatically using the Jira MCP to pre-fill the fields.

---

## Do's and Don'ts

**Do:**
- Describe impact in business terms — "some users were unable to enter journeys", not "horizontal is down"
- Always state clearly whether data was lost or not — business teams always need to know this
- Post even when you don't have everything — "we're still working on it" beats silence
- Use the announcement channel for business teams; keep technical details in the Jira task
- Update at important milestones, not every single minute
- Explain root cause in both plain language (for this channel) and technical terms (for the Jira task)

**Don't:**
- Say "I shared the task, they can follow it there" — that's not communication
- Use technical jargon that non-engineers won't understand (no "queue", "retry storm", "API", "horizontal" without explanation)
- Write "system is down" as a root cause — that's a symptom, not a cause
- Leave data loss status blank or ambiguous — always confirm with the PM

---

## Reference example (Part 3)

This is exactly how the final Slack message should look — compact fields, no blank lines between them, no asterisks:

```
We have an incident related to User Profile Page.

Due to a previously deployed task, all partners using the User Profile page were unable to see any data on that page during the affected period. No data was lost — the data was simply not visible. The issue was resolved by reverting the problematic deployment.

⚠️ Status: Fixed
📌 Task: https://your-jira-domain.atlassian.net/browse/INC-1037
🔥 Start Time: 17.03.2026 - 09:10 UTC (12:10 GMT+3)
🧯 End Time: 17.03.2026 - 09:37 UTC (12:37 GMT+3)
🧨 Impact Area: User Profile Page
💰 Impact: All partners using the User Profile page were affected — no data was visible on the page. No data loss occurred.
🙋 Root Cause: A task was deployed to production despite failing its automation checks. This caused the User Profile page to stop displaying data. The deployment was reverted to restore normal behaviour.
```
