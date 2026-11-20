# Reddit `r/MSP` — 2. Sıfır-Link Teknik Paylaşım Taslağı (24 Saat Bekleme Sonrası)

> **Güvenlik Kuralı:** `u/TheDobbyArt` hesabından ilk paylaşım (`r/InsuranceAgent`) 19 Kasım akşamı atıldı. Ban/spam filtresine takılmamak için **20 Kasım akşamı (en az 24 saat dolunca)** paylaşılacak. **Sıfır link, sıfır ürün adı, saf mühendislik paylaşımı.**

---

## Title
`We audited 98 live US SMB & clinic domains (from 360 scanned) via raw Google DoH + TLS handshake — 74.5% lack enforcing DMARC (59.2% missing, 15.3% p=none), only 4.1% run a 3rd-party SEG, and 19.4% have expired or sub-30d certs`

## Body
Quick technical share from this week's outbound hygiene benchmark if you pre-qualify SMB or healthcare/clinic prospects without paying for bloated enrichment APIs.

We stopped using bulky headless browsers and third-party enrichment databases for initial DNS/TLS triage and ran a pure DNS-over-HTTPS + port-443 TLS socket check (`Google DoH TXT/MX JSON lookups` + raw Python `ssl` socket, zero proxies) across **360 US SMB candidate domains** pulled from public commercial contractor registries and medical/dental clinic directories.

**98 domains resolved as live, reachable websites (HTTP 200–399)**. Here is the actual breakdown across those 98 live SMBs:

| Signal Checked | Verified Breakdown (`n = 98` live domains) |
|---|---|
| **DMARC Policy** | **74.5% unenforced (`73/98`)** — **59.2%** missing DMARC completely (`58`), **15.3%** stuck at `p=none` (`15`); only **13.3%** `p=quarantine` (`13`) and **12.2%** `p=reject` (`12`) |
| **MX / Mail Routing** | **24.5%** Microsoft 365 (`24`), **19.4%** Google Workspace (`19`), **43.9%** custom / ISP / cPanel MX (`43`), **8.2%** null / no MX (`8`), and **only 4.1%** behind a 3rd-party enterprise SEG like Proofpoint / Mimecast / Barracuda (`4`) |
| **SPF Posture** | **40.8%** `-all` hardfail (`40`), **32.7%** `~all` softfail (`32`), **26.5%** missing, neutral, or broken / `permerror` (`26`) |
| **Port 443 TLS / SSL** | **19.4% failing or expiring (`19/98`)** — `14` expired or throwing TLS handshake errors + `5` expiring within `<30 days` |

Three practical takeaways from running this raw check before spending cycles on outreach:

1. **Over 7 in 10 Live SMBs Have Zero Spoofing Enforcement:** Even among licensed commercial contractors and multi-provider medical/dental clinics actively taking web traffic, `59.2%` have never published a DMARC record and another `15.3%` left `p=none` sitting in monitoring mode indefinitely.
2. **SEG Filtering Is Nearly Nonexistent Downmarket (`4.1%`):** Checking MX roots immediately separates the ~`44%` running raw M365 or Google Workspace without a 3rd-party SEG from the `4.1%` already paying for Proofpoint, Mimecast, or Barracuda — so you avoid pitching email security to shops already locked into an enterprise renewal.
3. **SPF & Cert Neglect Travel Together:** Between `26.5%` missing/broken SPF records (`permerror` from exceeding the RFC 7208 10-lookup limit after bolting on marketing tools) and `19.4%` broken or sub-30-day TLS certs, pure public-protocol checks flag operational neglect far more reliably than generic firmographics.

Because it is 100% public DNS + a 2-second TLS handshake (zero scraping, zero headless Chrome), you can triage 1,000 target SMB domains in under a minute on a minimal container and lead with concrete, verifiable configuration gaps instead of generic security pitches.

Curious what other MSPs here check first when qualifying a new SMB prospect — do you lead with DMARC/SPF gaps, M365 tenant posture / MFA hygiene, or exposed remote access / perimeter checks?
