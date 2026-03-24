# eGain Visitor Intelligence — Sales Rep Portal

A prototype web application that empowers eGain sales representatives with actionable insights about companies visiting eGain.com. Built as a single-file, zero-dependency HTML application.

---

## Live Demo

> Deployed via Netlify Drop — see submission for live link.

---

## What It Does

This tool converts raw website visitor data (weblogs) into a prioritized, searchable intelligence dashboard for sales reps. Instead of raw log files, reps see:

- **Account-level visitor profiles** enriched with company size, industry, revenue, HQ, and tech stack
- **Intent scoring** (0–100) based on session depth, page views, and high-signal pages visited (Pricing, Demo Request)
- **Key signal flags** — Demo Request hit, Pricing viewed, Returning visitor, Case Study engaged
- **Known contact mapping** — personas and emails tied to visiting companies
- **Sales intelligence notes** — competitive displacement angles, urgency indicators, recommended next actions
- **Outreach brief export** — one-click copy of a complete account brief for use in email or CRM

---

## Features

| Feature | Description |
|---|---|
| Search | Live search by company name, domain, industry, or HQ city |
| Intent Filter | Hot (75+) / Warm (40–74) / Cold (<40) |
| Industry Filter | All major verticals in dataset |
| Size Filter | Enterprise / Mid-Market / SMB |
| Page Signal Filter | Filter by Pricing, Demo, Product, Case Study visits |
| Returning Filter | First-visit vs. repeat visitor |
| Sort | Click any column header to sort ascending/descending |
| Detail Panel | Click any row for full account profile + sales guidance |
| Copy Brief | One-click outreach brief to clipboard |

---

## How to Deploy (No Coding Required)

1. Download `egain-visitor-intelligence.html`
2. Go to [https://app.netlify.com/drop](https://app.netlify.com/drop)
3. Drag and drop the file onto the page
4. Get a live public URL instantly — no account required for 15-day links

---

## Data & Enrichment Architecture

### Current (Prototype)
The prototype uses **synthetic visitor data** modeled on realistic eGain.com weblog patterns, including:
- 20 named enterprise/mid-market accounts across 6 industries
- Realistic session counts, page view depths, and visit dates
- Simulated IP-to-company resolution
- Pre-populated tech stack intelligence and contact personas

### Production Path
To connect real weblog data, replace the `rawData` array with a pipeline that:

1. **Parses real weblogs** — extract IP, timestamp, URL path, user-agent, referrer
2. **Resolves IP → Company** using:
   - [Clearbit Reveal](https://clearbit.com/reveal) — IP-to-company enrichment
   - [6sense](https://6sense.com) — intent data + account identification
   - [Apollo.io](https://apollo.io) — contact-level enrichment
3. **Scores intent** — weight page types (Demo > Pricing > Product > Blog), session recency, visit frequency
4. **Maps contacts** — use enrichment APIs to surface personas at visiting companies
5. **Serves via API** — replace static array with a REST endpoint (Node.js/Python backend, hosted on Vercel or similar)

### Intent Score Formula (Prototype Logic)

```
Intent Score = 
  (sessions × 8) 
  + (pageViews × 1.2) 
  + (Demo page visited × 20) 
  + (Pricing page visited × 15) 
  + (Case Study visited × 10) 
  + (Returning visitor × 10)
  [capped at 100]
```

---

## File Structure

```
/
├── egain-visitor-intelligence.html   # Complete application (single file)
└── README.md                         # This file
```

---

## Tech Stack

| Layer | Choice | Reason |
|---|---|---|
| Framework | Vanilla HTML/CSS/JS | Zero dependencies, instant deploy |
| Fonts | Google Fonts (DM Sans + DM Mono) | Professional, legible, CDN-hosted |
| Hosting | Netlify Drop | Drag-and-drop, free, 15+ day links |
| Data | Synthetic (production-ready schema) | No real PII; swap-in ready |

---

## Roadmap (Production Features)

- [ ] Real-time weblog ingestion pipeline
- [ ] CRM integration (Salesforce, HubSpot) — push account to rep's pipeline
- [ ] Email alert system — notify rep when hot account visits
- [ ] Account scoring history — trend lines over time
- [ ] Territory filtering — route accounts to correct rep automatically
- [ ] Mobile-responsive sidebar collapse

---

## Author

Built for eGain Sales Engineering Take-Home Assignment.
