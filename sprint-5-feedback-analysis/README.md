# Sprint 5 — Weather-Based Sales & Staffing Automation

**Tools:** Zapier · OpenWeather API · Google Gemini AI · Gmail · JSON
**Sprint:** 5 of 7 | TripleTen AI Automation Bootcamp

---

## The Problem

Cafe managers at Bayside Brews & Scoops spent 30+ minutes every morning manually reviewing weather forecasts to decide what to promote, how many staff to schedule, and what operational adjustments to make — with no system to support these recurring daily decisions.

---

## What I Built

A scheduled Zapier automation that fetches real-time weather data from the OpenWeather API, sends it to Google Gemini AI for analysis, and delivers formatted operational recommendations directly to management via Gmail — every morning, automatically.

Pipeline:
1. Scheduled trigger fires each morning
2. OpenWeather API call fetches current forecast for Miami, FL
3. Structured JSON passed to Gemini AI with a decision-support prompt
4. Gemini returns three sections: PRODUCT FOCUS, STAFFING, and PROMO recommendations
5. Formatted email delivered to management inbox

---

## AI Prompt Design

The Gemini prompt treats weather data as structured input and instructs the model to return decision-ready recommendations — not a weather summary. The output is formatted for immediate operational use, not further analysis.

---

## Value Added

- Eliminated 30+ minutes of daily manual planning per manager
- Consistent, data-driven guidance every morning with zero ongoing manual input
- Scales to any location with an OpenWeather API call

---

## Key Learnings

- Scheduled triggers are the foundation of any recurring operational automation
- The prompt determines the output format — designing for readability in the final email matters as much as getting the logic right
- Structured JSON from APIs maps cleanly to AI inputs when the data schema is understood first
