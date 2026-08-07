# Sprint 3 — Multi-Step Make.com Automation

**Tools:** Make.com · APIs · Webhooks · Google Sheets
**Sprint:** 3 of 7 | TripleTen AI Automation Bootcamp

---

## What I Built

A multi-step automation scenario in Make.com that connects multiple services through a structured data pipeline — demonstrating scenario architecture, module configuration, error routing, and data transformation.

The full scenario blueprint (JSON) is included in this folder.

---

## Scenario Architecture

- Trigger: Webhook or scheduled trigger initiates the flow
- Data transformation: Fields mapped and formatted across modules
- Conditional routing: Filter conditions split execution paths based on data values
- Output: Structured data written to Google Sheets and/or delivered via API

---

## Key Concepts Demonstrated

- Module chaining: Output from one module feeds directly into the next
- Data mapping: Fields transformed between services without manual intervention
- Filter logic: Conditional branching — not all records follow the same path
- Error handling: Separate path configured to catch and log failures without breaking the main flow

---

## Key Learnings

- Make.com scenarios are only as reliable as their data mapping — field mismatches break silently
- Filters need to account for edge cases — a missing field can match or fail unexpectedly
- Blueprint JSON is your backup — export and version it, always
