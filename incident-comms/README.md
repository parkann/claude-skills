# Incident Communications Skill

A Claude skill that helps Product Managers draft and send incident communications to non-technical stakeholders via Slack.

## What it does

Guides you through the full incident lifecycle with ready-to-paste Slack messages:

| Message Type | When to use |
|---|---|
| **Part 1 — Acknowledgement** | Incident just detected, few details known |
| **Part 2 — Assessment Update** | More context available, still investigating |
| **Part 3 — Resolution** | Fix deployed, incident resolved |
| **Part 4 — Post-Incident Summary** | After the post-incident meeting |

## How it works

1. Asks clarifying questions — status, affected products, data loss, timing
2. Drafts a Slack-formatted message (no markdown, real emoji, compact fields)
3. Presents the message for review
4. Optionally posts directly to your incident channel via Slack MCP

## Setup

1. Copy [`SKILL.md`](./SKILL.md) into your Claude skills directory
2. Replace the placeholders:
   - `#[your-incident-channel]` → your Slack channel name
   - `your-jira-domain.atlassian.net` → your Jira domain
   - `INC-XXXX` → your ticket prefix
3. Connect Slack and Jira MCPs for full functionality (optional — copy-paste works without them)

## Example output

```
We have an incident related to User Profile Page.

Due to a previously deployed task, all partners using the User Profile page
were unable to see any data during the affected period. No data was lost.
The issue was resolved by reverting the problematic deployment.

⚠️ Status: Fixed
📌 Task: https://your-jira-domain.atlassian.net/browse/INC-1037
🔥 Start Time: 17.03.2026 - 09:10 UTC
🧯 End Time: 17.03.2026 - 09:37 UTC
🧨 Impact Area: User Profile Page
💰 Impact: All partners affected — no data loss occurred.
🙋 Root Cause: A task was deployed despite failing automation checks.
```
