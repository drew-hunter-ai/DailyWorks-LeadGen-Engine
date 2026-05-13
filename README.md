# DailyWorks Lead Generation Engine (v7.2)
**Architect:** Andrew Hunter | **Status:** Live Deployment

## Overview
A fully free, zero-SaaS Python pipeline that scrapes Google Maps for local 
businesses and runs each result through a 7-stage email finding and 
verification chain, delivering confirmed contacts into Google Sheets in real time.

No paid APIs. No subscriptions. Runs on raw Python.

**Live result:** 53 verified leads from 100 businesses.  
20 minutes on Rayleigh config. Under 1 hour at full scale.

## How It Works

### Stage 1 — Google Maps Discovery
Selenium with full bot-detection bypass scrapes Maps by sector and location.
Headless Chrome, navigator.webdriver fingerprint spoofed via JS injection,
automation flags stripped. EU consent wall handled automatically.

### Stages 2–6 — Email Enrichment Chain
Each business passes through the chain in order, stopping when verified:

| Stage | Method |
|---|---|
| 2 | Business website — homepage + contact page crawl |
| 3 | Bing search cross-reference |
| 4 | Companies House — director lookup + email pattern synthesis |
| 5 | Facebook page About section |
| 6 | LinkedIn via Bing |

### Stage 7 — Verification
MX record resolution + SMTP handshake check. No email sent —
confirms the address is live before writing to sheet.

### Output
Verified leads → **Businesses tab**  
Unresolved leads → **Needs Email tab** (manual review queue)  
Bulk write via gspread. Duplicate detection on every run.  
Progress saved to `progress.json` — survives interruptions mid-run.

## Config
Three lines control any deployment:
```python
SEARCH_AREAS = ["Rayleigh Essex"]
SECTORS      = ["accountants", "estate agents", ...]
TOTAL_CAP    = 100   # Configurable — set to any target volume
```

## Stack
Python · Selenium · BeautifulSoup · requests · gspread  
smtplib · dns.resolver · webdriver_manager · socket

## Security Note
`service_account.json` credentials excluded. Proprietary CSS selectors
and SMTP verification logic abstracted. Full documentation available
to verified recruiters on request.

---
*DailyWorks AI Operations Fleet — Andrew Hunter — 2026*
