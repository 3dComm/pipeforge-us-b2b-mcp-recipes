# Community Distribution Snippets (Zero-Spam Technical Value Posts)

## 1. `community.n8n.io` — Category: **Built with n8n**
**Title:** `How I automated daily $1M+ SEC Form D startup alerts (filtering out 76% investment fund noise) with n8n + Slack`

**Body:**
> Most Form D monitors dump every filing into Slack — which means 3 out of 4 alerts are actually Pooled Investment Funds, REITs, or SPVs instead of real operating startups.
>
> I put together a lightweight 6-node n8n workflow (using Header Auth + Schedule Trigger + IF routing) that pulls live SEC EDGAR primary XML Form D filings, excludes funds/REITs/LPs automatically, and only pings Slack when an operating startup sells `$1M+` with an executive name and direct US phone number on the filing. Lower raises still log quietly into Google Sheets.
>
> Full workflow JSON (`sec_form_d_funded_startups_slack_sheets.json`) + 5 other federal US signal workflows (FMCSA insurance gaps, CMS NPI-2 clinic owners, DMARC/SSL domain audits) are free to import here:
> `https://github.com/pipeforge/pipeforge-us-b2b-mcp-recipes` (and live on Apify at `https://apify.com/pipeforge`).
>
> Happy to share the XML parsing logic or `IF` routing setup if anyone wants to adapt it for specific US states or verticals!

---

## 2. X (Twitter) / Clay Community Thread (Short, High-Signal)
**Post:**
> Stop scraping Google Maps for dental & medical clinic leads — you only get the front desk receptionist.
>
> The federal CMS NPPES `NPI-2` registry legally requires every corporate clinic to list its **Authorized Official (Owner / President)** + **direct phone** + **enumeration date**.
>
> By pulling 200-row pages in memory and sorting `enumeration_date DESC`, you get 2025–2026 newly opened clinics first — and deduplicating by owner phone strips multi-location DSOs so you never dial the same owner twice.
>
> Runs in 0.8s on 256 MB RAM with $0 proxies. Free Clay HTTP API + n8n JSON + 1-click MCP endpoint in our open repo.

---

## 3. Awesome-MCP Servers PR Line (1-Line Contribution Format)
```markdown
- [PipeForge US B2B Federal & Domain Signal MCP](https://github.com/pipeforge/pipeforge-us-b2b-mcp-recipes) - Zero-proxy hosted MCP bundle exposing 4 live US B2B data tools (SEC Form D funded startups, CMS NPI-2 clinic owners, FMCSA DOT insurance gaps & permits, and DoH SPF/DMARC/SSL domain triggers).
```
