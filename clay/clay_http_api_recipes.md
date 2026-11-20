# 30-Second Clay.com HTTP API Column Recipes (All 6 PipeForge Actors + 2-Column Waterfall)

Use Clay's native **HTTP API** enrichment column (`POST`, Header `Authorization: Bearer YOUR_APIFY_API_TOKEN`, `Content-Type: application/json`) to run any PipeForge engine directly inside your Clay table with **$0 proxy cost**.

---

## 1. Domain Tech-Stack, SPF/DMARC/MX & SSL Trigger (`$3.50 / 1K`, LIVE)
- **Endpoint:** `https://api.apify.com/v2/acts/pipeforge~b2b-domain-tech-stack-dns-ssl-sales-trigger/run-sync-get-dataset-items`
- **Body:**
```json
{
  "domains": ["{{Domain}}"],
  "maxConcurrency": 5,
  "timeoutSeconds": 6,
  "minSeverityScore": 0
}
```
- **Best Clay Columns to Extract:** `cold_email_mx_provider`, `dmarc_policy`, `spf_strictness`, `ssl_days_remaining`, `detected_tech_stack`, `severity_score`, `msp_security_hook`, `ecom_agency_hook`.
- **1-Domain Webhook Mode (`1 run = 1 domain`, `~3.3s`, `256 MB`, `$0` proxy):** Pass `{"domains": ["{{Domain}}"], "maxConcurrency": 1}` directly to `run-sync-get-dataset-items`, or test the 1-click zero-config Public Task: [single-domain-dmarc-techstack-webhook-enrichment](https://apify.com/pipeforge/b2b-domain-tech-stack-dns-ssl-sales-trigger/examples/single-domain-dmarc-techstack-webhook-enrichment).

---

## 2. US SEC Form D Newly Funded Startups & CEO Phone (`$4.50 / 1K`)
- **Endpoint:** `https://api.apify.com/v2/acts/pipeforge~us-sec-form-d-startup-funding-leads/run-sync-get-dataset-items`
- **Body:**
```json
{
  "limit": 25,
  "lookbackDays": 14,
  "minAmountSoldUsd": 1000000,
  "excludeFundsAndRealEstate": true,
  "states": [],
  "maxXmlScans": 100
}
```
- **Best Clay Columns to Extract:** `entity_name`, `industry_group`, `total_amount_sold_usd`, `executive_name`, `executive_roles`, `phone_formatted`, `sec_xml_url`.

---

## 3. US CMS NPI-2 Dental & Medical Clinic Owner Phone (`$3.50 / 1K`)
- **Endpoint:** `https://api.apify.com/v2/acts/pipeforge~us-cms-npi2-clinic-owner-phone-leads/run-sync-get-dataset-items`
- **Body:**
```json
{
  "states": ["TX", "FL"],
  "taxonomyDescriptions": ["Dentist", "Dermatology"],
  "city": "",
  "limit": 25,
  "minEnumerationYear": 2024,
  "deduplicateByPhone": true,
  "maxPagesPerQuery": 3
}
```
- **Best Clay Columns to Extract:** `organization_name`, `primary_taxonomy`, `enumeration_date`, `official_full_name`, `official_title`, `official_direct_phone`, `npi_registry_url`.

---

## 4. US FMCSA Insurance Gap, Commercial Permits & New LLC (`$4.50 / 1K`)
- **Endpoint:** `https://api.apify.com/v2/acts/pipeforge~us-socrata-b2b-signal-crossjoin-engine/run-sync-get-dataset-items`
- **Body (FMCSA `$0` BIPD Insurance Gap):**
```json
{
  "mode": "fmcsa_crossjoin",
  "limit": 25,
  "onlyCriticalBipdZero": true
}
```
- **Body (Austin/NYC `$75K+` Commercial Permits):**
```json
{
  "mode": "permits_verified_phone",
  "limit": 25,
  "minPermitValuationUsd": 75000
}
```

---

## 5. US Federal Contract Awards & Expiring Incumbents (`$4.50 / 1K`, LIVE)
- **Endpoint:** `https://api.apify.com/v2/acts/pipeforge~us-federal-contract-awards-expiring-incumbents/run-sync-get-dataset-items`
- **Body:**
```json
{
  "mode": "expiring_incumbents",
  "minAwardAmount": 250000,
  "naicsPrefixes": ["54", "51"],
  "minDaysUntilExpiry": 30,
  "maxDaysUntilExpiry": 180,
  "limit": 25
}
```
- **Best Clay Columns to Extract:** `award_id`, `recipient_name`, `recipient_uei`, `award_amount_usd`, `end_date`, `days_until_expiration`, `recompete_urgency_tier`, `awarding_agency`, `naics_code`, `place_of_performance_state`, `sales_pitch_hook`, `usaspending_award_url`.

---

## 6. US ATS Hiring-Intent Sales Triggers (`$4.00 / 1K`, Greenhouse/Lever/Ashby, LIVE)
- **Endpoint:** `https://api.apify.com/v2/acts/pipeforge~us-ats-hiring-intent-sales-triggers/run-sync-get-dataset-items`
- **Body:**
```json
{
  "platforms": ["greenhouse", "lever", "ashby"],
  "intentCategories": ["SECURITY_COMPLIANCE_URGENCY", "REVOPS_GTM_STACK_BUYER"],
  "maxPostingAgeDays": 30,
  "maxCompanies": 15,
  "limit": 25
}
```
- **Best Clay Columns to Extract:** `company_name`, `company_slug`, `ats_platform`, `job_title`, `primary_intent`, `intent_categories`, `detected_tools`, `is_exec_budget_holder`, `salary_summary`, `intent_score`, `sales_pitch_hook`, `job_url`.

---

## 7. Clay 2-Column Waterfall (`Signal Actor -> Actor #2 Domain DNS/DMARC Audit`)
1. **Column 1 (Trigger Source):** Pull fresh target accounts from **SEC Form D**, **USAspending GovCon**, **Commercial Permits**, or **ATS Hiring-Intent** (`run-sync-get-dataset-items`) and resolve each company's root domain into `{{Company Domain}}`.
2. **Column 2 (Domain Security & Tech Audit):** Add an HTTP API enrichment calling **`b2b-domain-tech-stack-dns-ssl-sales-trigger`** with `{"domains": ["{{Company Domain}}"], "maxConcurrency": 5, "timeoutSeconds": 6, "minSeverityScore": 0}`.
3. **Output Ready for Sequencer:** Map `cold_email_mx_provider`, `dmarc_policy`, `ssl_days_remaining`, and `msp_security_hook` directly into Smartlead, Instantly, or HubSpot custom variables with **$0 proxy cost**.
