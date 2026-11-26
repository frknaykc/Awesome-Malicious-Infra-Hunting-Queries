<p align="center">
  <img src="Public/logo-icons/hunter.png" alt="Threat Hunting - Queries for Search Engines" width="480" style="max-width: 100%; max-height: 220px; width: auto; height: auto; object-fit: contain; display: block; margin: 0 auto;" />
</p>

<p align="center">
  <a href="https://github.com/frknaykc/Awesome-Malicious-Infra-Hunting-Queries/stargazers"><img src="https://img.shields.io/github/stars/frknaykc/Awesome-Malicious-Infra-Hunting-Queries?style=flat-square" alt="GitHub stars" /></a>
  <a href="https://github.com/frknaykc/Awesome-Malicious-Infra-Hunting-Queries/network/members"><img src="https://img.shields.io/github/forks/frknaykc/Awesome-Malicious-Infra-Hunting-Queries?style=flat-square" alt="GitHub forks" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square" alt="License" /></a>
  <a href="https://github.com/frknaykc/Awesome-Malicious-Infra-Hunting-Queries/commits"><img src="https://img.shields.io/github/last-commit/frknaykc/Awesome-Malicious-Infra-Hunting-Queries?style=flat-square" alt="Last commit" /></a>
</p>

<p align="center">
  <a href="SHODAN_QUERIES.md"><img src="https://img.shields.io/badge/Shodan-Queries-orange?style=flat-square" alt="Shodan" /></a>
  <a href="CENSYS_QUERIES.md"><img src="https://img.shields.io/badge/Censys-Queries-orange?style=flat-square" alt="Censys" /></a>
  <a href="NETLAS_QUERIES.md"><img src="https://img.shields.io/badge/Netlas-Queries-orange?style=flat-square" alt="Netlas" /></a>
</p>

# Malicious Infrastructure Hunting Queries

<p align="center">
  <strong>Ready-to-use hunting queries for Shodan, Censys, and Netlas — detect C2 servers, RAT panels, phishing kits, and malware infrastructure.</strong>
</p>

<p align="center">
  <a href="#introduction">Introduction</a> •
  <a href="#core-concepts">Core Concepts</a> •
  <a href="#what-does-this-repository-contain">Query Files</a> •
  <a href="TOOLS_REFERENCES.md">Tool References</a> •
  <a href="CONTRIBUTING.md">Contributing</a>
</p>

<p align="center">
  🇹🇷 <a href="tr/README.md">Türkçe versiyon için tıklayın</a>
</p>

---

## Introduction

This repository provides **ready-to-use hunting queries** for **Shodan**, **Censys**, and **Netlas** — internet-wide search engines that index exposed services, certificates, and HTTP responses. These queries help security researchers, threat hunters, and SOC teams:

- **Detect malicious infrastructure** — C2 servers, RAT panels, phishing kits, and malware hosting
- **Support threat hunting** — Find exposed instances of known tools used in attacks
- **Enrich IOCs** — Correlate IPs and domains with fingerprint-based queries
- **Identify open-source tools** — Many C2 frameworks and phishing tools leave distinctive fingerprints (favicon hash, TLS cert, HTML title) that can be searched

The queries target both **commercial** and **open-source** tools. Open-source C2 frameworks (Sliver, Mythic, Havoc, Covenant, etc.) and phishing platforms (GoPhish, Evilginx) are particularly detectable because their default configurations produce consistent, searchable fingerprints. Commercial tools like Cobalt Strike also have known JARM signatures and certificate patterns.

---

## Core Concepts

### What is C2 (Command & Control)?

A **C2 server** is a central network service that cyber attackers use to remotely control compromised devices — infected computers, servers, or IoT devices — within a botnet or malware campaign. The C2 receives commands from the attacker and distributes them to infected hosts, while collecting exfiltrated data. Detecting C2 infrastructure is a key goal of threat hunting.

### What is a RAT (Remote Access Trojan)?

A **RAT** is malware that gives an attacker covert, remote control over an infected system. It communicates with a C2 server as its command hub. Capabilities typically include keylogging, screen capture, file access, webcam control, and remote command execution. RATs like AsyncRAT, Quasar, and NjRAT often expose identifiable TLS certificate or HTTP signatures that can be searched.

### What is Malicious Infrastructure?

**Malicious infrastructure** refers to the servers, domains, and network assets that support cyber attacks: C2 servers, phishing panels, malware distribution hosts, credential stealers’ backends, and exploit kits. Hunting for this infrastructure helps disrupt campaigns before they scale and provides IOCs for blocking and incident response.

### What are Phishing Tools?

**Phishing tools** are platforms used to build and run credential-harvesting campaigns. Examples include **GoPhish**, **Evilginx**, and **EvilGoPhish**. They host fake login pages and capture credentials. Many have distinctive fingerprints (favicon hash, cookies, HTML content) that make them detectable via Shodan, Censys, and Netlas.

### What are Red Team Tools?

**Red team tools** are frameworks used for adversary simulation, penetration testing, and authorized security assessments. C2 frameworks like **Cobalt Strike**, **Sliver**, **Mythic**, and **Havoc** are used legitimately by red teams but are also abused by threat actors. Their network and TLS fingerprints are well-documented, making them searchable for both defense (finding exposed instances) and offensive research (understanding detection surfaces).

---

## What Does This Repository Contain?

| File | Content |
|------|---------|
| [SHODAN_QUERIES.md](SHODAN_QUERIES.md) | Complete Shodan hunting queries |
| [CENSYS_QUERIES.md](CENSYS_QUERIES.md) | Complete Censys hunting queries |
| [NETLAS_QUERIES.md](NETLAS_QUERIES.md) | Complete Netlas hunting queries |
| [ClickFixCampaign-CaseStudies.md](ClickFixCampaign-CaseStudies.md) | ClickFix social engineering attack analysis |
| [TOOLS_REFERENCES.md](TOOLS_REFERENCES.md) | All RAT, C2 and tool GitHub links |

---

## Fingerprint Types

| Type | Description | Example |
|------|-------------|---------|
| **Favicon Hash** | Hash of website icon | `http.favicon.hash:803527991` |
| **HTTP Header** | Server response headers | `"X-Havoc: true"` |
| **TLS Cert** | SSL certificate fields | `ssl.cert.subject.cn:"AsyncRAT Server"` |
| **JARM** | TLS handshake fingerprint | `ssl.jarm:"07d14d16d21d21d..."` |
| **HTML Title** | Page title | `http.title:"Mythic"` |
| **HTML Body** | Page content | `http.html:"mythic-react"` |

---

## Combined Fingerprint Examples

### High Confidence Detection

Combining multiple fingerprints increases detection accuracy:

**Mythic C2:**
```bash
# Shodan - Title + Certificate
http.title:"Mythic" ssl.cert.subject.o:"Mythic"

# Censys - Same-service title and certificate
host.services:(endpoints.http.html_title:"Mythic" and cert.parsed.subject.organization:"Mythic")

# Netlas
http.title:"Mythic" AND certificate.subject.organization:"Mythic"
```

**Cobalt Strike:**
```bash
# JARM + Certificate
ssl.jarm:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da" ssl.cert.issuer.cn:"jquery.com"

# JARM + HTTP Response
ssl.jarm:"07d14d16d21d21d00042d43d000000aa99ce74e2c6d013c745aa52b5cc042d" "HTTP/1.1 404 Not Found" "Content-Length: 0"
```

**GoPhish:**
```bash
# Favicon + Title + Certificate
http.favicon.hash:803527991 http.title:"Gophish" ssl.cert.issuer.O:"Gophish"

# Cookie + HTML Content
"Set-Cookie: gophish=" http.html:"gophish.css"
```

**AsyncRAT:**
```bash
# Certificate Issuer + Subject
ssl.cert.subject.cn:"AsyncRAT Server" ssl.cert.issuer.cn:"AsyncRAT Server"

# Censys
host.services:(cert.parsed.issuer_dn="CN=AsyncRAT Server" and cert.parsed.subject_dn="CN=AsyncRAT Server")
```

**Sliver C2:**
```bash
# Certificate + JARM
ssl.cert.issuer.cn:"operators" ssl.jarm:"3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910"
```

---

## Query Validation Methodology

Start with a reported threat or known infrastructure, use a seed query to find candidates, and compare independent instances before extracting reusable HTTP, TLS, or service fingerprints. Search each candidate fingerprint globally for collisions and false positives; combine independent signals where possible before publishing a query. Finding a JARM, JA3S/JA4S, favicon, port, certificate property, header, server version, ASN, frontend asset, or body hash on one known instance does **not** prove it is exclusive to that threat. Keep host counts, example IPs, and unvalidated candidates out of the query reference.

## Important Warnings

1. **JARM alone is not enough** - Always combine with other indicators
2. **Correlation is important** - Use multiple fingerprints instead of a single one
3. **Legal use** - Only use on systems you are authorized to test
4. **False positives** - Not all matches are malicious; verify before reporting

**No guarantee of accuracy.** These queries do not always return real or malicious content. You may encounter **honeypots**, infrastructure operated by adversaries who **hunt threat hunters**, or **legitimate red team / authorized pentest** infrastructure. Research consistently shows that **combining multiple fingerprints** — TLS cert + JARM + HTTP headers + HTML content — yields more reliable results than any single indicator. Use these queries as a starting point; validate findings with additional context before drawing conclusions or taking action.

---

## Intelligence Sources

### Threat Intelligence Feeds

| Resource | URL | API |
|----------|-----|-----|
| **ThreatFox** | https://threatfox.abuse.ch | `curl -X POST -d '{"query":"search_ioc","search_term":"IP"}' https://threatfox-api.abuse.ch/api/v1/` |
| **URLhaus** | https://urlhaus.abuse.ch | `curl https://urlhaus.abuse.ch/api/v1/url/IP/` |
| **MalwareBazaar** | https://bazaar.abuse.ch | `curl -X POST -d 'query=get_taginfo&tag=TAG' https://mb-api.abuse.ch/api/v1/` |
| **Feodo Tracker** | https://feodotracker.abuse.ch | `curl https://feodotracker.abuse.ch/blocklist/` |
| **SSL Blacklist** | https://sslbl.abuse.ch | Certificate blacklist |

### Scanning Platforms

| Resource | URL | GitHub | Usage |
|----------|-----|--------|-------|
| **Shodan** | [shodan.io](https://www.shodan.io) | C2 hunting |
| **Censys** | [search.censys.io](https://search.censys.io) | [censys](https://github.com/censys) | TLS/Service hunting |
| **Netlas** | [netlas.io](https://netlas.io) | [netlas-io](https://github.com/netlas-io) | HTTP/TLS hunting |
| **URLScan.io** | [urlscan.io](https://urlscan.io) | [urlscan](https://github.com/urlscan) | URL analysis |
| **VirusTotal** | [virustotal.com](https://www.virustotal.com) | — | Multi-AV scanning |

### IOC Repositories

| Resource | GitHub |
|----------|--------|
| **C2IntelFeeds** | [drb-ra/C2IntelFeeds](https://github.com/drb-ra/C2IntelFeeds) |
| **deepdarkCTI** | [fastfire/deepdarkCTI](https://github.com/fastfire/deepdarkCTI) |
| **Maltrail** | [stamparm/maltrail](https://github.com/stamparm/maltrail) |

---

## Detailed Documentation

- **Shodan Queries:** [SHODAN_QUERIES.md](SHODAN_QUERIES.md)
- **Censys Queries:** [CENSYS_QUERIES.md](CENSYS_QUERIES.md)
- **Netlas Queries:** [NETLAS_QUERIES.md](NETLAS_QUERIES.md)
- **ClickFix Case Study:** [ClickFixCampaign-CaseStudies.md](ClickFixCampaign-CaseStudies.md)
- **Tool References:** [TOOLS_REFERENCES.md](TOOLS_REFERENCES.md)

---

**Last Updated:** 2026-09-30
