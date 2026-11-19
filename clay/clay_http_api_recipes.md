# 30-Second Clay.com HTTP API Column Recipes (All 4 PipeForge Actors)

Use Clay's native **HTTP API** enrichment column (`POST`, Header `Authorization: Bearer YOUR_APIFY_API_TOKEN`, `Content-Type: application/json`) to run any PipeForge engine directly inside your Clay table with **$0 proxy cost**.

---

## 1. Domain Tech-Stack, SPF/DMARC/MX & SSL Trigger (`$3.50 / 1K`)
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
- **Best Clay Columns to Extract:** `email_provider`, `has_seg_gateway`, `dmarc_policy`, `ssl_days_remaining`, `opportunity_score`, `sales_trigger_hook`.

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
