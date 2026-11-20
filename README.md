# PipeForge — Zero-Proxy US B2B Outbound & Federal Signal MCP Pack (6 Live Tools, 1 Endpoint)

Connect **Claude Desktop, Cursor, Windsurf, or n8n AI Agents** to 6 live US federal public-record, ATS hiring-intent & B2B domain intelligence engines in **15 seconds** — with **$0 proxy costs**, **256 MB RAM footprint**, and transparent Pay-Per-Event pricing (`$3.50–$4.50 / 1,000 verified records`).

[![PipeForge on Apify](https://img.shields.io/badge/Apify_Store-PipeForge_(6_Live_Actors)-00C853?style=for-the-badge)](https://apify.com/pipeforge)
[![Official MCP Registry](https://img.shields.io/badge/Official_MCP_Registry-io.github.3dComm%2Fpipeforge--b2b--signals-111111?style=for-the-badge)](https://registry.modelcontextprotocol.io/v0/servers?search=pipeforge)
[![Listed on mcpservers.org](https://mcpservers.org/badge.svg)](https://mcpservers.org/servers/3dcomm/pipeforge-us-b2b-mcp-recipes)
[![Glama MCP Connector](https://glama.ai/mcp/connectors/com.apify.mcp/pipe-forge-us-b2b-federal-and-domain-signal-engine/badges/score.svg)](https://glama.ai/mcp/connectors/com.apify.mcp/pipe-forge-us-b2b-federal-and-domain-signal-engine)
[![Clay & n8n Ready](https://img.shields.io/badge/Clay_&_n8n-Copy_Paste_Recipes-FF6D00?style=for-the-badge)](./clay/clay_http_api_recipes.md)

---

## Why PipeForge?

Most B2B scrapers burn residential proxies, break when DOM selectors change, or scrape stale directories with receptionist phone numbers. PipeForge queries **official federal registries, live XML filings, US Treasury award APIs, and direct DNS/TLS sockets**:

| # | Tool / Apify Actor | Signal Source | What You Get (100% Structured JSON) | Pricing (PPE) |
|---|---|---|---|---:|
| 1 | **[US FMCSA Insurance Gap, Permits & New LLC Engine](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine)** | Federal DOT Socrata (3-table join), Austin/NYC Permits, CO/TX SOS | Active trucking carriers with `$0` BIPD insurance gaps (`BMC-91X`), `$75K+` phone-verified commercial GCs, newly formed LLCs with direct-owner filter | `$4.50 / 1K` |
| 2 | **[B2B Domain Tech-Stack, SPF/DMARC/MX & SSL Trigger](https://apify.com/pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger)** | Google DoH (`MX/TXT`), 1-hop SPF, `_dmarc`, Direct TLS X.509 | Email gateway (`Workspace / M365 / Proofpoint / Mimecast / Null MX`), DMARC spoofing vulnerability, SSL expiry countdown, CMS/CRM/Pixel hooks | `$3.50 / 1K` |
| 3 | **[US SEC Form D Funded Startups & CEO Phone Engine](https://apify.com/pipeforge/us-sec-form-d-startup-funding-leads)** | Live SEC EDGAR Primary XML Form D | Newly funded operating startups (automatically strips ~76% Pooled Investment Funds/REITs/SPVs) with **CEO / Executive Name + Direct US Phone** | `$4.50 / 1K` |
| 4 | **[US CMS NPI-2 Dental & Medical Clinic Owner Phone Engine](https://apify.com/pipeforge/us-cms-npi2-clinic-owner-phone-leads)** | Federal CMS NPPES NPI-2 Registry | Corporate clinics sorted newest-first (2024–2026 openings), deduplicated by phone, with **Authorized Official (Owner/President) Direct Phone** | `$3.50 / 1K` |
| 5 | **[US Federal Contract Awards & Expiring Incumbents](https://apify.com/pipeforge/us-federal-contract-awards-expiring-incumbents)** | US Treasury `USAspending.gov` v2 API | `$250K–$50M+` prime federal contracts expiring in `30–365` days (re-compete incumbent triggers) & fresh prime awards with **100% Recipient UEI + NAICS/PSC** | `$4.50 / 1K` |
| 6 | **[Greenhouse, Lever & Ashby Jobs Search API — ATS Hiring Leads](https://apify.com/pipeforge/us-ats-hiring-intent-sales-triggers)** | Official Greenhouse, Lever & Ashby public JSON boards | Live US open roles classified into **6 B2B Buying-Intent tiers** (`SOC 2`, `RevOps/Clay`, `LLM/MCP`, `Executive Budget Holders`), salary bands & ready `sales_pitch_hook` | `$4.00 / 1K` |

> **Quick-Start Tip (Actor #1):** For a single clean 100%-filled table without mixing feeds, launch the pre-configured **[FMCSA `$0` BIPD Task](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine/examples/us-fmcsa-critical-0-bipd-trucking-leads)** or **[Austin/NYC `$75K+` Commercial Permits Task](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine/examples/austin-nyc-75k-commercial-gc-building-permits)** directly instead of `mode="all"`.

---

## 1-Click MCP Server Setup

All 6 live engines are exposed through a single hosted Apify MCP endpoint (published on the Official MCP Registry as `io.github.3dComm/pipeforge-b2b-signals`):

```text
https://mcp.apify.com/?tools=pipeforge/us-socrata-b2b-signal-crossjoin-engine,pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger,pipeforge/us-sec-form-d-startup-funding-leads,pipeforge/us-cms-npi2-clinic-owner-phone-leads,pipeforge/us-ats-hiring-intent-sales-triggers,pipeforge/us-federal-contract-awards-expiring-incumbents
```

### Claude Code CLI (1-Line Install)
```bash
claude mcp add --transport http pipeforge "https://mcp.apify.com/?tools=pipeforge/us-socrata-b2b-signal-crossjoin-engine,pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger,pipeforge/us-sec-form-d-startup-funding-leads,pipeforge/us-cms-npi2-clinic-owner-phone-leads,pipeforge/us-ats-hiring-intent-sales-triggers,pipeforge/us-federal-contract-awards-expiring-incumbents" --header "Authorization: Bearer YOUR_APIFY_API_TOKEN"
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
        "https://mcp.apify.com/?tools=pipeforge/us-socrata-b2b-signal-crossjoin-engine,pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger,pipeforge/us-sec-form-d-startup-funding-leads,pipeforge/us-cms-npi2-clinic-owner-phone-leads,pipeforge/us-ats-hiring-intent-sales-triggers,pipeforge/us-federal-contract-awards-expiring-incumbents",
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

- **GovCon / Federal Re-Compete:** *"Find 15 US federal IT and cybersecurity prime contracts (`NAICS 54`) worth over $500K expiring within the next 30–180 days on USAspending.gov with incumbent UEI and agency."*
- **VC / B2B SaaS Outbound:** *"Find 20 US operating startups that filed SEC Form D in the last 14 days with at least $1M sold, excluding investment funds, and return their CEO names and direct phone numbers."*
- **Healthcare / Dental Agency:** *"Pull the 25 newest dental clinics registered in Texas since 2024 with their Authorized Official owner name and direct phone, deduplicated by phone."*
- **Commercial Insurance Broker:** *"Query FMCSA 3-table cross-join for active trucking carriers with $0 BIPD on file and phone numbers."*
- **MSP / Cold Email Agency:** *"Audit these 15 prospect domains for missing DMARC (`p=none`), Proofpoint/Mimecast security gateways, and expiring SSL certificates."*

---

## Live Sample Outputs (Privacy-Masked Previews)

Inspect real structured schemas pulled directly from live US federal endpoints (last 4 phone digits masked as `XXXX` in this public repo — run any Apify Actor below for live unmasked phone numbers):

- **[USAspending.gov Expiring Federal Incumbent Contracts (20-row CSV)](./sample_outputs/usaspending_expiring_incumbents_sample.csv)** — Live `$500K–$50M+` prime contracts expiring in 30–180 days with 100% UEI & NAICS.
- **[SEC Form D Newly Funded Operating Startups (15-row CSV)](./sample_outputs/sec_form_d_sample_masked.csv)** — Real operating startups after filtering out ~76% Pooled Investment Funds/REITs/SPVs.
- **[CMS NPI-2 Texas Newly Opened Dental Clinic Owners (15-row CSV)](./sample_outputs/cms_npi2_dental_tx_sample_masked.csv)** — Newest-first corporate clinics deduplicated by Authorized Official direct phone.

## 13 Ready-to-Run Apify Saved Tasks

- [Expiring US Federal IT & Cyber Contracts (Re-Compete Leads)](https://apify.com/pipeforge/us-federal-contract-awards-expiring-incumbents/examples/expiring-federal-it-cyber-contracts-recompete-leads)
- [New US Federal Defense & Construction Awards ($1M+ Sub Leads)](https://apify.com/pipeforge/us-federal-contract-awards-expiring-incumbents/examples/new-federal-defense-construction-prime-contract-awards)
- [US $1M+ Newly Funded Startups & CEO Phone (SEC Form D)](https://apify.com/pipeforge/us-sec-form-d-startup-funding-leads/examples/us-1m-newly-funded-startups-ceo-phone-sec-form-d)
- [Texas Newly Opened Dental Clinic Owners Phone (NPI-2)](https://apify.com/pipeforge/us-cms-npi2-clinic-owner-phone-leads/examples/texas-newly-opened-dental-clinic-owners-phone-npi-2)
- [Florida & California Dermatology & Chiropractor Owners](https://apify.com/pipeforge/us-cms-npi2-clinic-owner-phone-leads/examples/florida-california-dermatology-chiropractor-owners)
- [US FMCSA Critical $0 BIPD Trucking Insurance Gap Leads](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine/examples/us-fmcsa-critical-0-bipd-trucking-leads)
- [Austin & NYC $75K+ Commercial GC Building Permits](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine/examples/austin-nyc-75k-commercial-gc-building-permits)
- [Colorado & Texas New LLC & Sales Tax Direct Owners](https://apify.com/pipeforge/us-socrata-b2b-signal-crossjoin-engine/examples/colorado-texas-new-llc-sales-tax-direct-owners)
- [B2B Cold Email MX / Proofpoint SEG & DMARC Audit](https://apify.com/pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger/examples/b2b-cold-email-mx-proofpoint-seg-dmarc-audit)
- [MSP Cybersecurity DMARC Spoofing & SSL Expiry Audit](https://apify.com/pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger/examples/msp-cybersecurity-dmarc-spoofing-ssl-expiry-audit)
- [Single-Domain DMARC, MX & Tech-Stack Webhook ($3.50/1K)](https://apify.com/pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger/examples/single-domain-dmarc-techstack-webhook-enrichment)
- [US B2B Companies Hiring SOC 2, CISO & Security Compliance](https://apify.com/pipeforge/us-ats-hiring-intent-sales-triggers/examples/b2b-companies-hiring-soc2-ciso-security-compliance-leads)
- [US Tech Startups Hiring RevOps, Clay, Salesforce & AI Teams](https://apify.com/pipeforge/us-ats-hiring-intent-sales-triggers/examples/tech-startups-hiring-revops-clay-salesforce-ai-engineers)

---

## Included Automation Recipes

- **Clay.com HTTP API Columns (All 6 Actors + 2-Column Waterfall):** [`clay/clay_http_api_recipes.md`](./clay/clay_http_api_recipes.md)
- **Featured Multi-Actor Enterprise & Dual n8n Chains (Header Auth, Reviewer-Safe JSON):**
  - [`enterprise_b2b_hiring_funding_dmarc_ai_pipeline.json`](./n8n/enterprise_b2b_hiring_funding_dmarc_ai_pipeline.json) — **20-Node Enterprise Pipeline:** ATS Hiring + `$1M+` SEC Form D -> Merge -> Google Sheets Dedup -> Live DMARC/MX/SSL Audit -> 3-Tier Urgency Switch -> OpenAI Outreach Gmail Draft + Slack + Sheets + Error Trigger
  - [`us_b2b_signal_to_domain_audit_killer_chain.json`](./n8n/us_b2b_signal_to_domain_audit_killer_chain.json) — 2-Actor chain: US Commercial Permits -> Domain Security Scoring
  - [`govcon_expiring_incumbents_and_sec_formd_radar.json`](./n8n/govcon_expiring_incumbents_and_sec_formd_radar.json) — Dual-signal radar: USAspending Re-Competes + `$1M+` SEC Form D Startups
  - [`ats_hiring_intent_to_dmarc_audit_pipeline.json`](./n8n/ats_hiring_intent_to_dmarc_audit_pipeline.json) — 2-Actor chain: ATS Hiring-Intent -> Domain DMARC/SSL Audit *(LIVE)*
- **Single-Vertical n8n Production Workflows (5 Templates):**
  - [`fmcsa_insurance_gap_alert.json`](./n8n/fmcsa_insurance_gap_alert.json) — Daily DOT `$0` BIPD insurance-gap Slack + Sheets alert
  - [`austin_nyc_permits_to_sheets.json`](./n8n/austin_nyc_permits_to_sheets.json) — Austin & NYC `$75K+` phone-verified commercial permit GCs to Google Sheets
  - [`b2b_domain_trigger_msp_sales_alert.json`](./n8n/b2b_domain_trigger_msp_sales_alert.json) — Bulk DMARC/MX/SSL audit for MSPs & agencies
  - [`sec_form_d_funded_startups_slack_sheets.json`](./n8n/sec_form_d_funded_startups_slack_sheets.json) — Daily `$1M+` SEC Form D Funded Startup + CEO Phone alert
  - [`cms_npi2_new_dental_clinics_slack_sheets.json`](./n8n/cms_npi2_new_dental_clinics_slack_sheets.json) — Weekly Newly Opened Dental/Medical Clinic Owner alert

---

## License
MIT — Built & maintained by **[PipeForge](https://apify.com/pipeforge)**.
