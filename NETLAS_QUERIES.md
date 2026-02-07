# Netlas Hunting Queries

> **Complete Netlas Query Reference for C2 & Malware Hunting**

🇹🇷 [Türkçe versiyon için tıklayın](tr/NETLAS_QUERIES.md)

Based on [Netlas Featured Queries](https://netlas.io/resources/featured_queries/) and [netlas-dorks GitHub repo](https://github.com/netlas-io/netlas-dorks)

---

## 📖 Table of Contents

- [C2 Frameworks](#-c2-frameworks)
- [RATs](#-rats)
- [Phishing Tools](#-phishing-tools)
- [Info Stealers](#-info-stealers)
- [ClickFix Campaign](#-clickfix-phishing-campaign)
- [Open Directories](#-open-directories--payload-hosting)
- [Generic C2 Indicators](#-generic-c2-indicators)
- [CVE Hunting](#-cve-hunting)

---

## C2 FRAMEWORKS

### Deimos C2
```
http.title:"Deimos C2" OR certificate.subject.organization:"Acme Co" AND port:8443
```

### EvilGinx2
```
jarm:"20d14d20d21d20d20c20d14d20d20daddf8a68a1444c74b6dbe09910a511e6"
```

### Merlin C2
```
jarm:"29d21b20d29d29d21c41d21b21b41d494e0df9532e75299f15ba73156cee38"
```

### NimPlant C2
```
http.headers.server:"NimPlant C2 Server"
```

### Cobalt Strike

#### JARM Fingerprints
```
jarm:"07d14d16d21d21d00042d43d000000aa99ce74e2c6d013c745aa52b5cc042d"
jarm:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da"
jarm:"07d14d16d21d21d00042d41d00041de5fb3038104f457d92ba02e9311512c2"
```

#### Certificate
```
certificate.subject.common_name:"Major Cobalt Strike"
certificate.issuer.common_name:"Major Cobalt Strike"
```

### Havoc C2
```
http.unknown_headers.key:"X_Havoc"
http.body:"Havoc"
certificate.subject.common_name:"Havoc"
```

### Mythic C2
```
http.title:"Mythic"
http.body:"mythic-react"
certificate.subject.organization:"Mythic"
```

#### JARM Fingerprints
```
jarm:"1dd40d40d00040d00042d43d000000831b6af40378e2dd35eeac4e9311926e"
jarm:"27d40d40d00040d00042d43d000000d2e61cae37a985f75ecafb81b33ca523"
```

### Sliver C2
```
certificate.issuer.common_name:"operators"
http.body:"sliver"
```

#### JARM Fingerprint
```
jarm:"3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910"
```

### Metasploit
```
certificate.subject.common_name:"MetasploitSelfSignedCA"
http.title:"Metasploit"
```

### Supershell C2
```
http.favicon.hash_sha256:8a0bfe63bcd9859d68e4e60ac703c20e6242c2a9c690638c4887e32eadf59ceb
```

### Covenant C2
```
http.body:"Blazor"
http.body:"covenant.css"
```

### Brute Ratel C4
```
http.body:"Brute Ratel"
http.body:"badger"
```

### Empire C2
```
http.headers.expires:0
```

### PoshC2
```
certificate.subject.common_name:"P18055077"
certificate.subject.organization:"Pajfds"
certificate.subject.organizational_unit:"Jethpro"
```

### Nighthawk C2
```
http.unknown_headers.key:"X-Test"
http.headers.server:"Apache" AND http.body:"404 Not Found"
```

### Viper (Chinese C2 Framework)
```
http.body:"Viper"
http.title:"Viper"
```

### Pyramid C2
```
http.title:"Pyramid"
http.body:"Pyramid C2"
```

---

## RATS

### NanoCore
```
certificate.subject.common_name:"unk"
http.body:"NanoCore"
```

### AsyncRAT
```
certificate.subject.common_name:"AsyncRAT Server"
certificate.issuer.common_name:"AsyncRAT Server"
```

### Quasar RAT
```
certificate.subject.common_name:"Quasar Server CA"
certificate.subject.common_name:"Quasar Server"
```

### Orcus RAT
```
certificate.subject.common_name:"Orcus Server"
certificate.subject.common_name:"OrcusServerCertificate"
```

### DcRAT
```
certificate.subject.common_name:"DcRat Server"
certificate.issuer.common_name:"DcRat Server"
```

### VenomRAT
```
certificate.subject.common_name:"VenomRAT"
certificate.issuer.common_name:"VenomRAT"
```

### BitRAT
```
certificate.subject.common_name:"BitRAT"
certificate.issuer.common_name:"BitRAT"
```

### XWorm
```
http.body:"XWorm"
http.body:"xworm"
certificate.subject.common_name:"XWorm"
```

### Pupy RAT
```
certificate.subject.organizational_unit:"CONTROL"
http.body:"Pupy"
```

### Gh0st RAT
```
http.body:"Gh0st"
```

### DarkComet RAT
```
http.body:"DarkComet"
port:1604
```

### XtremeRAT
```
http.body:"XtremeRAT"
certificate.subject.common_name:"XtremeRAT"
```

### njRAT
```
http.body:"njRAT"
port:5552 OR port:1177
```

### Remcos RAT
```
http.body:"Remcos"
certificate.subject.common_name:"Remcos"
port:2404 OR port:2405 OR port:4782
```

### Ares RAT
```
http.title:"Ares"
http.body:"Ares RAT"
http.body:"AresRAT"
port:8080 AND http.title:"Ares"
```

### Meterpreter
```
http.body:"Meterpreter"
certificate.subject.common_name:"Meterpreter"
port:4444 OR port:4445
```

### NetSupport RAT
```
http.body:"NetSupport"
http.title:"NetSupport"
port:5405 OR port:5421
```

### CHAOS RAT
```
http.body:"CHAOS"
http.title:"CHAOS"
```

---

## PHISHING TOOLS

### GoPhish

#### Title Based
```
http.title:"Gophish - Login"
http.title:"Gophish"
```

#### Certificate
```
certificate.issuer.organization:"Gophish"
certificate.subject.organization:"Gophish"
```

#### Cookie Based (UNIQUE!)
```
http.headers.set_cookie:"gophish="
http.headers.set_cookie:"_gorilla_csrf="
```

#### HTML Content
```
http.body:"/css/dist/gophish.css"
http.body:"Open-Source Phishing Toolkit"
http.body:"Jordan Wright"
```

#### Port Based (Default: 3333)
```
port:3333 AND http.title:"Gophish"
```

#### JARM Fingerprints
```
jarm:"28d28d28d00028d00041d28d28d41dd279b0cf765af27fa62e66d7c8281124"
jarm:"2ad2ad0002ad2ad00041d2ad2ad41dc347a1c956987fa29fb299da896c61ea"
```

#### Combined High Confidence
```
http.title:"Gophish" AND certificate.issuer.organization:"Gophish"
http.body:"gophish.css" AND http.title:"Gophish"
```

### EvilGinx2
```
jarm:"20d14d20d21d20d20c20d14d20d20daddf8a68a1444c74b6dbe09910a511e6"
http.title:"evilginx"
```

### EvilGoPhish
```
http.body:"evilginx"
http.body:"EvilGoPhish"
```

---

## INFO STEALERS

### Panda C2 / Panda Stealer

#### Title Patterns (Chinese & English)
```
http.title:"熊猫Stealer"
http.title:"Panda Stealer"
http.title:"熊猫"
http.title:"PandaStealer"
```

#### HTML Content (Chinese)
```
http.body:"熊猫Stealer"
http.body:"熊猫"
```

#### JARM Fingerprints
```
jarm:"15d3fd16d29d29d00042d43d000000f6a76359d2423084924eaeb5187f1701"
jarm:"3fd3fd0003fd3fd21c42d42d000000bdfc58c9a46434368cf60aa440385763"
```

#### Combined
```
http.title:"熊猫" AND http.body:"Stealer"
```

### Titan Stealer
```
http.body:"Titan Stealer"
http.body:"Tital Stealer"
```

### Vidar C2
```
certificate.issuer.organization:"StaticIP"
certificate.issuer.organizational_unit:"privateIP"
```

### Shadow C2 (Information Stealer)
```
http.title:"Shadow C2 Panel"
http.body:"collect_telegram" AND http.body:"collect_wallets"
http.body:"Implant Builder" AND http.body:"Shadow"
http.body:"shadow_secure_key"
http.body:"Shadow C2 Command Center"
```

#### JARM Fingerprint
```
jarm:"14d14d16d14d14d08c14d14d14d14dfd9c9d14e4f4f67f94f0359f8b28f532"
```

#### Server Pattern (Flask)
```
http.headers.server:"Werkzeug" AND http.title:"Shadow"
port:5000 AND http.title:"Shadow C2"
```

### Stealth C2 (Banking Trojan)
```
http.title:"Stealth C2 Panel"
http.body:"Stealth Command & Control Panel"
http.body:"Bank Cookies" AND http.body:"socket.io"
```

### Meduza Stealer
```
http.title:"Meduza Stealer"
```

### Collector Stealer (Parent Malware)
```
http.title:"Collector Stealer"
http.title:"Collector"
http.body:"Collector Stealer"
```

### StealC V2
```
http.body:"StealC"
http.title:"StealC"
```

---

## CLICKFIX PHISHING CAMPAIGN

### Main Detection Queries
```
http.title:"Checking if you are human"
http.title:"Checking if you are human" AND http.body:"k4zrz92z"
http.title:"Checking if you are human" AND http.body:"Ctrl"
http.title:"Checking if you are human" AND http.body:"✅"
```

### JavaScript Identifiers
```
http.body:"checkboxWindow"
```

### Let's Encrypt Certificate with ClickFix
```
certificate.issuer_dn:"CN=Let's Encrypt" AND http.title:"Checking if you are human"
certificate.issuer.organization:"Let's Encrypt" AND http.body:"k4zrz92z"
```

### Sectigo Certificate with ClickFix
```
certificate.issuer.organization:"Sectigo" AND http.body:"k4zrz92z"
```

### Behavior-based Detection
```
http.body:"Ctrl + V" AND http.title:"human"
http.body:"clipboard" AND http.title:"Checking"
```

---

## DDOS & FLOOD TOOLS

### Locust DDoS Panel

#### Title Detection
```
http.title:"Locust"
```

#### HTML Content (DDoS Functions)
```
http.body:"HTTPFloodUser"
http.body:"attack_get"
http.body:"current_rps"
http.body:"available_user_tasks"
```

#### Port Based (Default: 8089)
```
port:8089 AND http.title:"Locust"
port:8089 AND http.body:"HTTPFloodUser"
```

#### Combined
```
http.title:"Locust" AND http.body:"HTTPFloodUser"
```

---

## CRYPTOMINERS

### Immortal Dropper (XMRig)
```
http.title:"IMMORTAL DROPPER C2 Panel"
http.body:"IMMORTAL DROPPER"
http.body:"pool.supportxmr.com"
http.body:"DeployMiner"
```

#### JARM Fingerprint
```
jarm:"29d29d00029d29d00042d42d00000023f2ae7180b8a0816654f2296c007d93"
```

#### Server Pattern (Flask/Werkzeug)
```
http.headers.server:"Werkzeug"
port:5000 AND http.title:"IMMORTAL DROPPER"
```

---

## BANKING TROJANS

### IcedID / Gozi / BokBot

#### Classic Patterns
```
certificate.subject.common_name:"localhost"
certificate.subject.organization:"Internet Widgits Pty Ltd"
certificate.issuer.organization:"1"
```

#### LlamaHQ-Swoole C2 Infrastructure
```
http.headers.server:"LlamaHQ-Swoole"
```

#### C2 API Response Patterns
```
http.body:"no project for"
http.body:"Worker is running with geo-worker"
port:23454 AND http.body:"Authentication required"
```

#### Suspicious Ports (IcedID infra)
```
port:9501 AND http.headers.server:"LlamaHQ-Swoole"
port:17262 AND http.body:"geo-worker"
```

### Qakbot (Banking Trojan)

#### JARM Fingerprints
```
jarm:"21d14d00021d21d21c42d43d0000007abc6200da92c2a1b69c0a56366cbe21"
jarm:"04d02d00004d04d04c04d02d04d04d9674c6b4e623ae36cc2d998e99e2262e"
```

---

## RANSOMWARE

### BianLian GO Trojan
> BianLian uses random 16-char alphanumeric SSL cert fields
```
certificate.subject.country:/^[0-9a-zA-Z]{16}$/
certificate.subject.organization:/^[0-9a-zA-Z]{16}$/
```

---

## LOADERS & DROPPERS

### SectopRAT C2
```
port:9000 AND http.headers.server:"Microsoft-HTTPAPI/2.0"
```

### Oyster C2
```
http.body:"Oyster"
```

### Pikabot (Loader Malware)
```
http.headers.etag:"3147526947+gzip"
```

---

## TUNNELING TOOLS

### Ligolo-NG
```
certificate.subject.common_name:"ligolo"
certificate.issuer.organization:"ligolo"
```

### Reverse SSH
```
ssh.server:"reverse"
```

---

## RED TEAM TOOLS

### Responder (LLMNR/NBT-NS Poisoning)
```
http.headers.server:"Microsoft-IIS/7.5" AND http.body:"WWW-Authenticate: NTLM"
```

### Geacon_Pro (Cobalt Strike Go Implementation)
```
certificate.subject.country:"KZ"
certificate.subject.organization:"NN Fern Sub"
certificate.subject.organizational_unit:"NN Fern"
certificate.subject.common_name:"foren.zik"
```

---

## OTHER C2 & TOOLS

### Hak5 Cloud C2
```
http.title:"Hak5 Cloud C"
http.body:"Hak5 Cloud"
http.body:"Copyright (c) 2021 Hak5 LLC"
```

#### JARM Fingerprints
```
jarm:"3fd21b20d00000021c43d21b21b43de0a012c76cf078b8d06f4620c2286f5e"
jarm:"40d1db40d0000001dc43d1db1db43de0a012c76cf078b8d06f4620c2286f5e"
```

### HookBot Panel
```
http.title:"HOOKBOT PANEL"
http.body:"HOOKBOT"
http.body:"HookBot"
```

### RansomHub C2
```
http.body:"Ransomhub"
http.body:"RansomHub"
http.title:"RansomHub"
```

### Interactsh C2
```
http.title:"Interactsh"
http.body:"interactsh"
certificate.subject.common_name:"interactsh"
```

### wstunnel
```
http.body:"wstunnel"
http.title:"wstunnel"
```

### Keycloak (Potential C2 Infrastructure)
```
http.favicon.hash_sha256:47dcf1f1a8f1afd68297a294a263849069a7a62b2e86550241416c2cc56c5676
http.title:"Keycloak"
http.body:"Keycloak"
```

---

## OPEN DIRECTORIES & PAYLOAD HOSTING

### Directory Listings
```
http.title:"/index of/"
```

### Suspicious Open Directories with Malware
```
http.title:"Index of" AND http.body:"sliver"
http.title:"Index of" AND http.body:"sliver.exe"
http.title:"Index of" AND http.body:"MimiKatz"
http.title:"Index of" AND http.body:"xworm"
http.title:"Index of" AND http.body:"metasploit"
http.title:"Index of" AND http.body:".exe"
http.title:"Directory Listing for" AND http.body:"payload"
```

---

## GENERIC C2 INDICATORS

### Self-signed Certificate Patterns
```
certificate.issuer.organization:"Internet Widgits Pty Ltd"
certificate.subject.common_name:"localhost"
```

### Flask/Werkzeug C2 Panels

> **Warning:** Generic patterns — many false positives. Combine with other indicators.

```
http.headers.server:"Werkzeug" AND http.title:"Panel"
http.headers.server:"Werkzeug" AND http.body:"/api/bots"
http.headers.server:"Werkzeug" AND http.body:"/api/targets"
http.headers.server:"Werkzeug" AND http.body:"/api/command"
```

### Bulletproof Hosting - SERV.HOST
```
asn.name:"SERV.HOST GROUP LTD"
asn.name:"SERV.HOST GROUP LTD" AND http.title:"Panel"
```

---

## KVM TOOLS (Potential C2 Access)

### GLKVM
```
http.title:"GLKVM"
http.body:"GLKVM"
```

### PiKVM
```
http.title:"PiKVM"
http.body:"PiKVM"
tag.name:"PiKVM"
```

### NanoKVM
```
http.title:"NanoKVM"
http.body:"NanoKVM"
```

### TinyPilot KVM
```
http.title:"TinyPilot"
http.body:"TinyPilot"
```

---

## APT INFRASTRUCTURE

### APT41 (Double Dragon / Barium / Winnti)
```
http.title:"莹火虫的世界"
asn.name:"Alibaba" AND port:8080 AND port:5432
```

---

## CVE HUNTING

### CVE-2024-1708, -1709 (ConnectWise ScreenConnect)
```
http.headers.server:"ScreenConnect"
```

### CVE-2024-20356 (Cisco IMC)
```
http.title:"Cisco Integrated Management Controller"
```

### CVE-2024-20767 (Adobe ColdFusion)
```
tag.name:"adobe_coldfusion"
```

### CVE-2024-21410 (MS Exchange)
```
tag.name:"microsoft_exchange"
```

### CVE-2024-22024 (Ivanti Connect Secure)
```
http.body:"welcome.cgi?p=logo"
```

### CVE-2024-23897 (Jenkins)
```
http.headers.x_jenkins:[0 TO 2.441]
```

### CVE-2024-24919 (Check Point)
```
http.favicon.hash_sha256:9a3a865d8911afcd95389ec701e5e8abcad69d928efd5b52b5d0bcc70a60d11a
tag.name:"checkpoint"
```

### CVE-2024-3400 (Palo Alto Networks PAN-OS)
```
tag.name:"palo_alto"
```

### CVE-2024-4835 (GitLab)
```
http.meta:"Gitlab"
```

### CVE-2023-22515 (Atlassian Confluence)
```
tag.name:"atlassian_confluence"
http.meta:"confluence-base-url"
```

### CVE-2023-27997 (Fortigate VPN)
```
http.favicon.hash_sha256:d18b3c9feb76c3c1cfdcc51c732f113327e3c33fb3f63b479951f7da6ed1216f
tag.name:"fortigate_vpn"
```

### CVE-2023-42793 (JetBrains TeamCity)
```
http.headers.set_cookie:TCSESSIONID NOT http.body:"2023.05.4"
tag.name:"teamcity"
```

---

## 📚 Netlas Syntax Quick Reference

| Netlas | Shodan | Censys |
|--------|--------|--------|
| `http.title` | `http.title` | `services.http.response.html_title` |
| `http.body` | `http.html` | `services.http.response.body` |
| `http.headers.server` | `http.headers.server` | `services.http.response.headers.server` |
| `certificate.subject.common_name` | `ssl.cert.subject.cn` | `services.tls.certificates.leaf_data.subject.common_name` |
| `certificate.issuer.common_name` | `ssl.cert.issuer.cn` | `services.tls.certificates.leaf_data.issuer.common_name` |
| `jarm` | `ssl.jarm` | `services.tls.jarm.fingerprint` |
| `http.favicon.hash_sha256` | `http.favicon.hash` | `services.http.response.favicons.sha256_hash` |
| `http.unknown_headers.key` | `http.headers.unknown` | `services.http.response.headers` |
| `tag.name` | `product` | `services.software.product` |
| `port` | `port` | `services.port` |

---

## 📖 Related Documents

- [Home](README.md)
- [Shodan Queries](SHODAN_QUERIES.md)
- [Censys Queries](CENSYS_QUERIES.md)
- [ClickFix Case Study](ClickFixCampaign-CaseStudies.md)
- [Tool References](TOOLS_REFERENCES.md)

---

## 📚 References

- [Netlas Featured Queries](https://netlas.io/resources/featured_queries/)
- [netlas-io/netlas-dorks GitHub](https://github.com/netlas-io/netlas-dorks)
- [Netlas Documentation](https://docs.netlas.io/)

---

**Last Updated:** 2026-02-01
