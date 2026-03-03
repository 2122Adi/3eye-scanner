# 👁 3eye — Advanced VAPT Web Recon Tool

<p align="center">
  <img src="https://img.shields.io/badge/version-2.0-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/python-3.8%2B-yellow?style=for-the-badge&logo=python" />
  <img src="https://img.shields.io/badge/license-MIT-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/type-passive%20recon-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/free%20%26%20open%20source-100%25-brightgreen?style=for-the-badge" />
</p>

```
  ████████╗██████╗ ███████╗██╗   ██╗███████╗
     ██╔══╝██╔══██╗██╔════╝╚██╗ ██╔╝██╔════╝
     ██║   ██████╔╝█████╗   ╚████╔╝ █████╗
     ██║   ██╔══██╗██╔══╝    ╚██╔╝  ██╔══╝
     ██║   ██║  ██║███████╗   ██║   ███████╗
     ╚═╝   ╚═╝  ╚═╝╚══════╝   ╚═╝   ╚══════╝

        👁  3 E Y E  v2.0  —  by Aditya Bhosale
     Advanced VAPT Web Recon — 100% Free & Open Source
```

> **3eye** is a powerful, all-in-one passive web reconnaissance tool built for VAPT professionals, bug bounty hunters, and security researchers. It performs 14 recon modules — from DNS enumeration to technology fingerprinting — using **100% free and open-source APIs**. No paid subscriptions. No API keys required.

---

## ⚠️ Legal Disclaimer

> This tool is intended **strictly for authorized security testing** on systems you own or have **explicit written permission** to test. Unauthorized use against systems you do not own is **illegal**. The author is not responsible for any misuse or damage caused by this tool.

---

## ✨ Features

| Module | Description |
|--------|-------------|
| 🌐 **DNS Enumeration** | A, AAAA, MX, NS, TXT, SOA, CAA, SRV, SPF, DMARC, DKIM (11 selectors), DNSSEC, Zone Transfer, Wildcard detection |
| 🔍 **Subdomain Bruteforce** | 65+ common subdomains resolved via DNS |
| 📋 **WHOIS Intelligence** | Registrar, domain age, expiry warning, registrant email exposure |
| 🌍 **IP / Geo / ASN** | Geolocation, ISP, ASN via ip-api.com + BGPView + IPinfo |
| ☁️ **Threat Intelligence** | Shodan InternetDB (open ports + CVEs), GreyNoise community API |
| 🔒 **SSL/TLS Deep Analysis** | Cert expiry, TLS version, weak ciphers, self-signed check, HTTP→HTTPS redirect, Certificate Transparency logs |
| 📡 **HTTP Header Analysis** | 11 security headers, server fingerprint leaks, cookie flags, CORS probe, clickjacking check |
| 🛠️ **Technology Fingerprinting** | 50+ tech signatures (CMS, frameworks, CDN, analytics, WAF), BuiltWith, meta generator, JS secrets |
| 🔌 **Port Scan** | 50 common ports (MySQL, Redis, MongoDB, RDP, Elasticsearch, Docker, K8s…) |
| 📂 **File & Path Enumeration** | 100+ sensitive paths (.env, .git, backups, admin panels, API docs, actuator endpoints…) |
| 🔑 **Login Page Analysis** | CSRF, method, CAPTCHA, hidden fields, rate-limiting, MFA detection, password policy |
| 🕵️ **Information Disclosure** | Emails, private IPs, HTML comments, error page leaks, source map exposure |
| ⏪ **Wayback Machine** | Historical URLs, old file types, subdomain history |
| 🔎 **Google Dorks** | 34 ready-to-run dork queries auto-generated for the target |
| 📊 **Content Analysis** | Links, URL parameters, forms, inline secrets, mixed content, iframes |
| 📝 **Risk Scoring** | Weighted CRITICAL/HIGH/MEDIUM/LOW score → risk label |
| 💾 **JSON Report** | Full machine-readable report auto-saved after every scan |

---

## 🚀 Quick Start

### Install & Run (auto-installs all dependencies)

```bash
git clone https://github.com/yourusername/3eye.git
cd 3eye
python 3eye.py
```

### Custom target

```bash
python 3eye.py https://example.com
```

### Save report to JSON

```bash
python 3eye.py https://example.com --output report.json
```

### Quick scan (skip slow modules)

```bash
python 3eye.py https://example.com --quick
```

---

## 📦 Dependencies

All dependencies are **auto-installed** on first run. No manual setup needed.

| Package | Purpose |
|---------|---------|
| `requests` | HTTP requests |
| `beautifulsoup4` | HTML parsing |
| `dnspython` | DNS enumeration |
| `python-whois` | WHOIS lookups |
| `builtwith` | Technology fingerprinting |
| `tldextract` | Domain parsing |

Or install manually:
```bash
pip install requests beautifulsoup4 dnspython python-whois builtwith tldextract
```

---

## 🖥️ Usage

```
usage: 3eye.py [-h] [--output OUTPUT] [--skip-ports] [--skip-paths]
               [--skip-wayback] [--quick] [url]

positional arguments:
  url                   Target URL (default: https://testuser.joterp.online/login)

options:
  -h, --help            show this help message and exit
  --output, -o OUTPUT   Save findings to JSON file
  --skip-ports          Skip TCP port scan
  --skip-paths          Skip file/directory enumeration
  --skip-wayback        Skip Wayback Machine check
  --quick, -q           Quick mode: skips ports + Wayback
```

---

## 📊 Sample Output

```
  👁  3EYE RECON REPORT  —  by Aditya Bhosale
  ════════════════════════════════════════════════════
  Target     : https://example.com
  Scanned at : 2025-01-01 12:00:00
  Duration   : 38.4s
  Risk Score : 72  →  🟠 HIGH RISK
  ────────────────────────────────────────────────────
  Critical: 2   High: 8   Medium:11   Low: 6   Info:24   Good: 9
  ════════════════════════════════════════════════════

🔴 CRITICAL (2)
  [SSL] CVE-2021-XXXXX on this IP
  [Paths] [HTTP 200 ACCESSIBLE] /.env

🟠 HIGH (8)
  [Headers] Missing: Strict-Transport-Security
  [Headers] Missing: Content-Security-Policy
  [DNS] Subdomain found: admin.example.com
  [SSL] Server accepts TLSv1.1
  ...
```

---

## 🆓 Free APIs Used

| API | What it provides | Key needed? |
|-----|-----------------|-------------|
| [ip-api.com](http://ip-api.com) | Geo, ISP, proxy detection | ❌ No |
| [Shodan InternetDB](https://internetdb.shodan.io) | Open ports, CVEs, CPEs | ❌ No |
| [GreyNoise Community](https://greynoise.io) | Threat intelligence | ❌ No |
| [IPinfo.io](https://ipinfo.io) | Org, ASN, bogon check | ❌ No |
| [BGPView](https://bgpview.io) | ASN, BGP prefixes | ❌ No |
| [crt.sh](https://crt.sh) | Certificate Transparency logs | ❌ No |
| [Wayback Machine](https://web.archive.org) | Historical URLs | ❌ No |

---

## 📁 Project Structure

```
3eye/
├── 3eye.py          # Main script (single file, self-contained)
├── README.md        # This file
└── reports/         # Auto-generated JSON reports (gitignored)
```

---

## 🛡️ Modules In Detail

### DNS Enumeration
Queries 11 record types (A, AAAA, MX, NS, TXT, CNAME, SOA, SRV, CAA, PTR, NAPTR), checks SPF/DMARC/DKIM configuration, probes for zone transfer vulnerability, detects wildcard DNS, and brute-forces 65+ common subdomains.

### Threat Intelligence
Uses Shodan's free InternetDB to get known open ports and CVEs for the target IP without any API key. Cross-references with GreyNoise community API to detect if the IP is known for internet-wide scanning or malicious activity.

### SSL/TLS Analysis
Checks certificate validity, expiry, issuer, SANs, weak ciphers, outdated protocol support (TLS 1.0/1.1), self-signed detection, and HTTP-to-HTTPS redirect enforcement. Also queries Certificate Transparency logs to discover subdomains.

### Login Page Analysis
Inspects login forms for CSRF token presence and strength, insecure HTTP submission, GET method usage, missing CAPTCHA, lack of rate limiting headers, MFA availability, and weak password policies.

### Technology Fingerprinting
Detects 50+ technologies including CMS (WordPress, Joomla, Drupal), frameworks (Laravel, Django, Rails, Express, ASP.NET), JS frameworks (React, Vue, Angular, Next.js), CDNs (Cloudflare, AWS, Vercel), WAFs, analytics platforms, and payment processors. Also scans inline JavaScript for exposed API keys, tokens, and passwords.

---

## 📄 License

MIT License — free to use, modify, and distribute with attribution.

---

## 👤 Author

**Aditya Bhosale**

- Tool: 3eye v2.0
- Purpose: VAPT Web Reconnaissance
- Type: Passive / Detection only — no exploitation

---

## ⭐ If this tool helped you, give it a star!
