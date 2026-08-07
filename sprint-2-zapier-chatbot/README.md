# Sprint 2 — AI Customer Service Chatbot

**Tools:** Zapier · OpenAI · Webhooks · HTML/JavaScript
**Sprint:** 2 of 7 | TripleTen AI Automation Bootcamp

---

## The Problem

Small businesses cannot staff a live chat 24/7. Customer questions go unanswered after hours, and support queues back up with repetitive, answerable inquiries.

---

## What I Built

An AI-powered customer service chatbot built on Zapier with OpenAI as the AI backbone, deployed as a functional web interface.

How it works:
1. User submits a question through the chat interface
2. Webhook fires and sends the message to Zapier
3. Zapier passes the message to OpenAI with a configured system prompt
4. OpenAI generates a response within the defined parameters
5. Response returned and displayed in the chat interface

---

## What Makes It Work

The system prompt is the control layer. It defines what the bot knows, what it can and cannot answer, tone, response format, and what to do when a question is out of scope.

---

## The Interface

Built as a standalone HTML/JavaScript page — no framework dependencies, deployable anywhere. The chatbot HTML file is included in this folder.

---

## Key Learnings

- The system prompt is the product — a bad prompt produces a bad chatbot regardless of the model
- Webhook latency matters for UX — fast trigger paths are worth configuring
- Scope the bot clearly — a chatbot that tries to answer everything answers nothing well
