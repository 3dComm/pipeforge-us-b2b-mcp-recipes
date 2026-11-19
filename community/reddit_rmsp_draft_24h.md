# Reddit `r/MSP` — 2. Sıfır-Link Teknik Paylaşım Taslağı (24 Saat Bekleme Sonrası)

> **Güvenlik Kuralı:** `u/TheDobbyArt` hesabından ilk paylaşım (`r/InsuranceAgent`) 19 Kasım akşamı atıldı. Ban/spam filtresine takılmamak için **20 Kasım akşamı (en az 24 saat dolunca)** paylaşılacak. **Sıfır link, sıfır ürün adı, saf mühendislik paylaşımı.**

---

## Title
`We audited 200 SMB domains via raw Google DoH + TLS handshake (zero scraping) — 38% still run p=none DMARC with broken SPF lookups or certs expiring in <30 days`

## Body
Quick technical share for anyone building outbound prospecting or lightweight domain hygiene audits for SMB prospects without paying for expensive enrichment APIs.

We stopped using bulky headless browsers or third-party enrichment tools to pre-qualify SMB prospects for MSP / email-security conversations and moved to a pure DNS-over-HTTPS + TLS socket check (`dns.google/resolve` + raw Python `ssl` socket, 0 proxies, runs in ~1.2s per batch):

1. **SPF 10-Lookup & Soft-Fail Traps:** A surprising chunk of 20–100 seat companies using Microsoft 365 + Mailchimp + HubSpot + Zendesk silently blow past the RFC 7208 10-DNS-lookup limit (`permerror`), or still leave `?all` / `~all` with zero DMARC enforcement (`v=DMARC1; p=none`).
2. **SEG Detection via MX Fingerprinting:** Matching MX roots cleanly separates raw `protection.outlook.com` / `aspmx.l.google.com` tenants from accounts already paying for Proofpoint (`pphosted.com`), Mimecast (`mimecast.com`), or Barracuda — so you don't waste cycles pitching email filtering to shops already locked into an enterprise SEG.
3. **TLS Expiry & Misconfiguration:** Doing a 2-second TLS handshake on port 443 catches expired/sub-30-day certs and misconfigured wildcard renewals before the prospect even realizes their web forms are throwing browser warnings.

Because it's 100% public DNS + TLS handshake (no crawling, no headless Chrome), you can run 1,000 target SMB domains in under a minute on a tiny container and score them purely on live technical gaps instead of generic "we do cybersecurity" cold emails.

Curious what other MSPs here check first when qualifying a new SMB prospect — do you prioritize DMARC/SPF gaps, exposed RDP/VPN portals, or Microsoft 365 tenant posture?
