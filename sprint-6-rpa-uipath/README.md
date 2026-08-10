# Sprint 6 — Invoice Processing RPA Bot

**Tools:** UiPath · Document Understanding · Gmail · Google Drive · Google Sheets · GenAI
**Sprint:** 6 of 7 | TripleTen AI Automation Bootcamp

---

## The Problem

Processing invoices manually required opening each email, downloading attachments, extracting data, and entering it into a spreadsheet — every time a new invoice arrived. Slow, error-prone, and unscalable.

---

## What I Built

A UiPath RPA bot that monitors Gmail for incoming invoice emails, downloads attachments to Google Drive, uses Document Understanding to extract structured invoice data, validates confidence before writing output, and logs everything to Google Sheets with AI-generated purchase descriptions.

Pipeline:
1. Gmail trigger monitors inbox for new invoice emails
2. Attachment downloaded and saved to designated Google Drive folder
3. Document Understanding extracts structured data using the Invoices extractor
4. Confidence gate checks extraction confidence BEFORE writing any output
5. High-confidence invoices auto-logged to Google Sheets with AI-generated purchase description
6. Low-confidence invoices routed to manual review log

---

## Key Design Decision: Gate Before Writing

Confidence validation runs BEFORE any data is written to the Sheet. Low-confidence output does not get cleaned up retroactively — it routes to a separate review log and stays there until a human clears it.

This is the correct design pattern for any pipeline touching financial or compliance data.

---

## Confidence Validation

- High confidence: auto-log to Google Sheets, mark as processed
- Low confidence: route to manual review log with flag
- Test invoice with low OCR confidence correctly routed to manual review — the guardrail worked as designed

---

## Output

Google Sheets log includes:
- Vendor name, invoice number, invoice date
- Line items and amounts, total
- AI-generated purchase description (via GenAI activity)
- Processing status: Auto-Processed or Manual Review

---

## Key Learnings

- Confidence gates belong before writes, not after — fix the architecture, not the data
- Low-confidence routing is a feature, not a bug — the guardrail flagging an edge case means it worked
- Automated logic scales better than manual thresholds — expression-based filters beat hardcoded cutoffs
