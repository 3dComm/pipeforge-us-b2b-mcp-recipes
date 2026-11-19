# PipeForge — Zero-Proxy US B2B Outbound & Federal Signal MCP Pack (4 Tools, 1 Endpoint)

Connect **Claude Desktop, Cursor, Windsurf, or n8n AI Agents** to 4 live US federal public-record & B2B domain intelligence engines in **15 seconds** — with **$0 proxy costs**, **256 MB RAM footprint**, and transparent Pay-Per-Event pricing (`$3.50–$4.50 / 1,000 verified records`).

[![PipeForge on Apify](https://img.shields.io/badge/Apify_Store-PipeForge_(4_Live_Actors)-00C853?style=for-the-badge)](https://apify.com/pipeforge)
[![Glama MCP Connector](https://glama.ai/mcp/connectors/com.apify.mcp/pipe-forge-us-b2b-federal-and-domain-signal-engine/badges/score.svg)](https://glama.ai/mcp/connectors/com.apify.mcp/pipe-forge-us-b2b-federal-and-domain-signal-engine)
[![Clay & n8n Ready](https://img.shields.io/badge/Clay_&_n8n-Copy_Paste_Recipes-FF6D00?style=for-the-badge)](./clay/clay_http_api_recipes.md)

---

## Why PipeForge?

Most B2B scrapers burn residential proxies, break when DOM selectors change, or scrape stale directories with receptionist phone numbers. PipeForge queries **official federal registries, live XML filings, and direct DNS/TLS sockets**:

| # | Tool / Apify Actor | Signal Source | What You Get (100% Structured JSON) | Pricing (PPE) |
|---|---|---|---|---:|
| 1 | **[US FMCSA Insurance Gap, Permits & New LLC Engine](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine)** | Federal DOT Socrata (3-table join), Austin/NYC Permits, CO/TX SOS | Active trucking carriers with `$0` BIPD insurance gaps (`BMC-91X`), `$75K+` phone-verified commercial GCs, newly formed LLCs with direct-owner filter | `$4.50 / 1K` |
| 2 | **[B2B Domain Tech-Stack, SPF/DMARC/MX & SSL Trigger](https://apify.com/pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger)** | Google DoH (`MX/TXT`), 1-hop SPF, `_dmarc`, Direct TLS X.509 | Email gateway (`Workspace / M365 / Proofpoint / Mimecast / Null MX`), DMARC spoofing vulnerability, SSL expiry countdown, CMS/CRM/Pixel hooks | `$3.50 / 1K` |
| 3 | **[US SEC Form D Funded Startups & CEO Phone Engine](https://apify.com/pipeforge/us-sec-form-d-startup-funding-leads)** | Live SEC EDGAR Primary XML Form D | Newly funded operating startups (automatically strips ~76% Pooled Investment Funds/REITs/SPVs) with **CEO / Executive Name + Direct US Phone** | `$4.50 / 1K` |
| 4 | **[US CMS NPI-2 Dental & Medical Clinic Owner Phone Engine](https://apify.com/pipeforge/us-cms-npi2-clinic-owner-phone-leads)** | Federal CMS NPPES NPI-2 Registry | Corporate clinics sorted newest-first (2024–2026 openings), deduplicated by phone, with **Authorized Official (Owner/President) Direct Phone** | `$3.50 / 1K` |

---

## 1-Click MCP Server Setup

All 4 engines are exposed through a single hosted Apify MCP endpoint:

```text
https://mcp.apify.com/?tools=pipeforge/us-socrata-b2b-signal-crossjoin-engine,pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger,pipeforge/us-sec-form-d-startup-funding-leads,pipeforge/us-cms-npi2-clinic-owner-phone-leads
```

### Claude Desktop (`claude_desktop_config.json`)
Copy [`configs/claude_desktop_config.json`](./configs/claude_desktop_config.json) and insert your free Apify API token:

```json
{
  "mcpServers": {
    "pipeforge-us-b2b": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://mcp.apify.com/?tools=pipeforge/us-socrata-b2b-signal-crossjoin-engine,pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger,pipeforge/us-sec-form-d-startup-funding-leads,pipeforge/us-cms-npi2-clinic-owner-phone-leads",
        "--header",
        "Authorization: Bearer YOUR_APIFY_API_TOKEN"
      ]
    }
  }
}
```

### Cursor (`~/.cursor/mcp.json`)
See [`configs/cursor_mcp.json`](./configs/cursor_mcp.json) for native streamable HTTP MCP config.

---

## Example AI Agent Prompts (Copy & Run)

- **VC / B2B SaaS Outbound:** *"Find 20 US operating startups that filed SEC Form D in the last 14 days with at least $1M sold, excluding investment funds, and return their CEO names and direct phone numbers."*
- **Healthcare / Dental Agency:** *"Pull the 25 newest dental clinics registered in Texas since 2024 with their Authorized Official owner name and direct phone, deduplicated by phone."*
- **Commercial Insurance Broker:** *"Query FMCSA 3-table cross-join for active trucking carriers with $0 BIPD on file and phone numbers."*
- **MSP / Cold Email Agency:** *"Audit these 15 prospect domains for missing DMARC (`p=none`), Proofpoint/Mimecast security gateways, and expiring SSL certificates."*

---

## Live Sample Outputs (Privacy-Masked Previews)

Inspect real structured schemas pulled directly from live US federal endpoints (last 4 phone digits masked as `XXXX` in this public repo — run any Apify Actor below for live unmasked phone numbers):

- **[SEC Form D Newly Funded Operating Startups (15-row CSV)](./sample_outputs/sec_form_d_sample_masked.csv)** — Real operating startups after filtering out ~76% Pooled Investment Funds/REITs/SPVs.
- **[CMS NPI-2 Texas Newly Opened Dental Clinic Owners (15-row CSV)](./sample_outputs/cms_npi2_dental_tx_sample_masked.csv)** — Newest-first corporate clinics deduplicated by Authorized Official direct phone.

## 1-Click Ready-to-Run Apify Tasks

- [US $1M+ Newly Funded Startups & CEO Phone (SEC Form D)](https://apify.com/pipeforge/us-sec-form-d-startup-funding-leads/examples/us-1m-newly-funded-startups-ceo-phone-sec-form-d)
- [Texas Newly Opened Dental Clinic Owners Phone (NPI-2)](https://apify.com/pipeforge/us-cms-npi2-clinic-owner-phone-leads/examples/texas-newly-opened-dental-clinic-owners-phone-npi-2)
- [Florida & California Dermatology & Chiropractor Owners](https://apify.com/pipeforge/us-cms-npi2-clinic-owner-phone-leads/examples/florida-california-dermatology-chiropractor-owners)
- [US FMCSA Critical $0 BIPD Trucking Insurance Gap Leads](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine/examples/us-fmcsa-critical-0-bipd-trucking-leads)
- [Austin & NYC $75K+ Commercial GC Building Permits](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine/examples/austin-nyc-75k-commercial-gc-building-permits)
- [Colorado & Texas New LLC & Sales Tax Direct Owners](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine/examples/colorado-texas-new-llc-sales-tax-direct-owners)
- [B2B Cold Email MX / Proofpoint SEG & DMARC Audit](https://apify.com/pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger/examples/b2b-cold-email-mx-proofpoint-seg-dmarc-audit)
- [MSP Cybersecurity DMARC Spoofing & SSL Expiry Audit](https://apify.com/pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger/examples/msp-cybersecurity-dmarc-spoofing-ssl-expiry-audit)

---

## Included Automation Recipes

- **Clay.com HTTP API Columns (30-Second Setup):** [`clay/clay_http_api_recipes.md`](./clay/clay_http_api_recipes.md)
- **n8n Production Workflows (Header Auth, Reviewer-Safe JSON):**
  - `fmcsa_insurance_gap_alert.json` — Daily DOT `$0` BIPD insurance-gap Slack + Sheets alert
  - `b2b_domain_trigger_msp_sales_alert.json` — Bulk DMARC/MX/SSL audit for MSPs & agencies
  - `us_b2b_signal_to_domain_audit_killer_chain.json` — 2-Actor chain: US Permits -> Domain Security Scoring
  - `sec_form_d_funded_startups_slack_sheets.json` — Daily `$1M+` SEC Form D Funded Startup + CEO Phone alert
  - `cms_npi2_new_dental_clinics_slack_sheets.json` — Weekly Newly Opened Dental/Medical Clinic Owner alert

---

## License
MIT — Built & maintained by **[PipeForge](https://apify.com/pipeforge)**.
