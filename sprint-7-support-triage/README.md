# Sprint 7 — AI-Powered Customer Support Triage

**Tools:** Make.com · Google Gemini AI · Google Sheets · Gmail · Webhooks
**Sprint:** 7 of 7 — Final Project | TripleTen AI Automation Bootcamp | August 2026

---

## The Problem

Customer support teams spend the first part of every shift manually sorting emails — figuring out who handles what before any actual help gets delivered. For a small team, that sorting bottleneck is the whole job.

Before this build:
- Shared inbox opened manually each morning
- Each email read individually to determine type
- Ticket info copied into a spreadsheet by hand
- Routed to the right person or queue manually
- High volume = errors, missed tickets, slow response

---

## What I Built

An end-to-end email triage automation. Incoming support emails are captured via webhook, classified by Google Gemini AI, and routed to the correct queue with no human required to touch them first.

Pipeline:
1. Capture: Gmail forwards emails to a Make.com webhook automatically
2. Classify: Gemini AI reads the email and returns structured JSON with category, priority, queue, confidence score (0-100), and one-sentence summary
3. Route: Router checks the classification. High-confidence tickets go Auto-Ready. Everything else triggers Manual Review alert.

---

## AI Classification Logic

Model: Google Gemini 3.5 Flash

The prompt treats all email content as untrusted customer data — preventing prompt injection. Output is constrained to structured JSON with five fields.

| Field | Values |
|-------|--------|
| category | One of 8 allowed categories |
| priority | Low / Normal / High / Urgent |
| queue | Assigned support queue |
| confidence_score | Integer 0-100 |
| summary | One-sentence ticket summary |

Category to Queue Mapping:

| Category | Queue |
|----------|-------|
| Order Status | Fulfillment |
| Shipping / Delivery | Fulfillment |
| Return / Refund | Returns |
| Product / Stock | Sales Support |
| Billing / Payment | Billing |
| Account / Technical | Technical Support |
| Complaint / Escalation | Customer Experience |
| Other | Manual Review |

---

## Routing Logic

Auto-Ready fires when ALL of these are true:
- Category is Order Status, Shipping/Delivery, Return/Refund, or Billing
- Queue is NOT Manual Review
- Confidence Score is 90 or above

Result: Writes to Google Sheets. No alert sent. Ticket is immediately queue-ready.

Manual Review fires when Route 1 does not match:
- Category is Complaint, Technical, or Other
- Confidence Score is below 90
- Queue is Manual Review

Result: Writes to Google Sheets AND sends a Gmail alert to the support team.

---

## Error Handling

A dedicated error path connects to the Gemini AI module. If Gemini fails, the error path fires instead of breaking the scenario.

- Error logged to Google Sheets with Review Status = Automation Error
- Original email data preserved in the log row
- No data lost — a human can review and reprocess

---

## Test Results

| Metric | Result |
|--------|--------|
| Test emails sent | 12 |
| Auto-Ready | 5 |
| Manual Review | 7 |
| Avg Confidence Score | 95 |

Gemini handled every edge case during testing without triggering the error path.

---

## Key Learnings

- Make the simplest thing that actually works first
- Prompt engineering is real work — constraining output format and treating content as untrusted data took iteration
- AI output needs a structured landing zone — the Sheets schema follows the AI output, not the other way around
- Build in order — each phase creates the foundation the next one needs
