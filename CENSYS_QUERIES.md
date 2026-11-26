# Censys Hunting Queries

> **Complete Censys Query Reference for C2 & Malware Hunting**

🇹🇷 [Türkçe versiyon için tıklayın](tr/CENSYS_QUERIES.md)

---

## ⚠️ Censys Platform Syntax

These queries use **Censys Platform** (CenQL) syntax. Censys has moved from Legacy Search to a new data model with `host`, `cert`, and `web` dataset prefixes. For software/product detection, use the full host+web coverage query. See: [Censys Platform Syntax Differences](https://docs.censys.com/docs/censys-platform-syntax-differences) | [Query Converter](https://docs.censys.com/docs/query-converter)

Queries using `=~` require Censys Starter or an enterprise plan. A documented field path does not by itself validate a threat attribution or guarantee current search results.

---

## 📖 Table of Contents

- [Phishing Frameworks](#-gophish-phishing-framework)
- [Info Stealers](#-panda-c2--panda-stealer-collector-stealer-variant)
- [C2 Frameworks](#-cobalt-strike-cert--jarm)
- [RATs](#-asyncrat)
- [Banking Trojans](#-icedid--gozi--bokbot-banking-trojan)
- [APT Infrastructure](#-apt41-double-dragon--barium--winnti)
- [Other Tools](#-open-directory---suspicious)

---

## GOPHISH (Phishing Framework)

The single-indicator searches below are **low-confidence candidates**; run each line separately. The combined searches are **unvalidated candidates**, not confirmed high-confidence detections. Validate their relationship to Gophish before raising the detection level.

### Product Detection (host + web coverage)
```
host.services.software.product:"GoPhish" or host.services.hardware.product:"GoPhish" or host.services.operating_systems.product:"GoPhish" or web.software.product:"GoPhish" or web.hardware.product:"GoPhish" or web.operating_systems.product:"GoPhish"
```

### Title Based
```
host.services.endpoints.http.html_title:"Gophish - Login"
host.services.endpoints.http.html_title:"Gophish"
web.endpoints.http.html_title:"Gophish"
```

### SSL Certificate
```
host.services.cert.parsed.issuer.organization:"Gophish"
host.services.cert.parsed.subject.organization:"Gophish"
```

### Cookie Based
```
host.services.endpoints.http.headers:(key="Set-Cookie" and value:"gophish=")
host.services.endpoints.http.headers:(key="Set-Cookie" and value:"_gorilla_csrf=")
```

### HTML Content
```
host.services.endpoints.http.body:"/css/dist/gophish.css"
host.services.endpoints.http.body:"Open-Source Phishing Toolkit"
web.endpoints.http.body:"gophish.css"
```

### Favicon Fingerprint
```
host.services.endpoints.http.favicons.hash_sha256="6f383235d8dec5350c1233c04b035b116bbbd2b287c13deb298a123dc5e49d03"
```

### Port Based (Default: 3333)
```
host.services:(port=3333 and endpoints.http.html_title:"Gophish")
```

### JARM Fingerprints
```
host.services.jarm.fingerprint="28d28d28d00028d00041d28d28d41dd279b0cf765af27fa62e66d7c8281124"
host.services.jarm.fingerprint="2ad2ad0002ad2ad00041d2ad2ad41dc347a1c956987fa29fb299da896c61ea"
```

### Combined Candidates (Not Yet Validated)
```
host.services:(endpoints.http.html_title:"Gophish" and cert.parsed.issuer.organization:"Gophish")
host.services:(endpoints.http.body:"gophish.css" and endpoints.http.html_title:"Gophish")
host.services:(endpoints.http.favicons.hash_sha256="6f383235d8dec5350c1233c04b035b116bbbd2b287c13deb298a123dc5e49d03" and endpoints.http.body:"/css/dist/gophish.css")
host.services:(endpoints.http.favicons.hash_sha256="6f383235d8dec5350c1233c04b035b116bbbd2b287c13deb298a123dc5e49d03" and cert.parsed.issuer.organization:"Gophish")
```

---

## PANDA C2 / PANDA STEALER (Collector Stealer Variant)

> Panda Stealer = Collector Stealer variant, associated with Cassandra Crypter, distributed via Discord (build.exe)

### Product Detection
```
host.services.software.product:"Panda C2" or host.services.hardware.product:"Panda C2" or host.services.operating_systems.product:"Panda C2" or web.software.product:"Panda C2" or web.hardware.product:"Panda C2" or web.operating_systems.product:"Panda C2"
host.services.software.product:"Panda Stealer" or host.services.hardware.product:"Panda Stealer" or host.services.operating_systems.product:"Panda Stealer" or web.software.product:"Panda Stealer" or web.hardware.product:"Panda Stealer" or web.operating_systems.product:"Panda Stealer"
```

### Title Patterns (Chinese & English)
```
host.services.endpoints.http.html_title:"熊猫Stealer"
host.services.endpoints.http.html_title:"Panda Stealer"
host.services.endpoints.http.html_title:"熊猫"
host.services.endpoints.http.html_title:"PandaStealer"
```

### HTML Content (Chinese)
```
host.services.endpoints.http.body:"熊猫Stealer"
host.services.endpoints.http.body:"熊猫"
```

### Collector Stealer (Parent Malware)
```
host.services.endpoints.http.html_title:"Collector Stealer"
host.services.endpoints.http.html_title:"Collector"
host.services.endpoints.http.body:"Collector Stealer"
host.services.software.product:"Collector Stealer" or host.services.hardware.product:"Collector Stealer" or host.services.operating_systems.product:"Collector Stealer" or web.software.product:"Collector Stealer" or web.hardware.product:"Collector Stealer" or web.operating_systems.product:"Collector Stealer"
```

### JARM Fingerprints
```
host.services.jarm.fingerprint:"15d3fd16d29d29d00042d43d000000f6a76359d2423084924eaeb5187f1701"
host.services.jarm.fingerprint:"3fd3fd0003fd3fd21c42d42d000000bdfc58c9a46434368cf60aa440385763"
host.services.jarm.fingerprint:"28d28d28d00028d00042d42d000000d6376f1d8fe64877806a85a008c1c790"
host.services.jarm.fingerprint:"3fd3fd0003fd3fd21c42d42d000000307ee0eb468e9fdb5cfcd698a80a67ef"
```

### JA3S Fingerprint
```
host.services.tls.ja3s:"574866101f64002c6421cc329e4d5458"
```

### Title Pattern (Fake E-Commerce - Decoy)
```
host.services.endpoints.http.html_title:"Dream Commerce"
```

### Combined
```
(host.services.software.product:"Panda C2" or web.software.product:"Panda C2") AND host.services.port:443
host.services.endpoints.http.html_title:"熊猫" AND host.services.endpoints.http.body:"Stealer"
```

---

## METASPLOIT

```
host.services.cert.parsed.subject.common_name:"MetasploitSelfSignedCA"
```

---

## ICEDID / GOZI / BOKBOT (Banking Trojan)

### Classic Patterns
```
host.services.cert.parsed.subject.common_name:"localhost"
host.services.cert.parsed.subject.organization:"Internet Widgits Pty Ltd"
host.services.cert.parsed.issuer.organization:"1"
```

### LlamaHQ-Swoole C2 Infrastructure
```
host.services.endpoints.http.headers:(key="Server" and value:"LlamaHQ-Swoole")
```

### C2 API Response Patterns
```
host.services.endpoints.http.body:"no project for"
host.services.endpoints.http.body:"Worker is running with geo-worker"
host.services:(port=23454 and endpoints.http.body:"Authentication required")
```

### Suspicious Ports (IcedID infra)
```
host.services:(port=9501 and endpoints.http.headers:(key="Server" and value:"LlamaHQ-Swoole"))
host.services:(port=17262 and endpoints.http.body:"geo-worker")
```

### Combined
```
host.services:(endpoints.http.headers:(key="Server" and value:"LlamaHQ-Swoole") and port=9501)
```

---

## COVENANT C2

```
host.services.endpoints.http.html_tags:"Blazor"
```

---

## SUPERSHELL C2

```
host.services.endpoints.http.body_hash_sha1="c023c2f42e6fa22f6b0f5284f2c24d8abcef6191"
```

---

## TITAN STEALER

```
host.services.endpoints.http.html_tags:"Tital Stealer"
```

---

## VIDAR C2

```
host.services.cert.parsed.issuer.organization:"StaticIP"
host.services.cert.parsed.issuer.organizational_unit:"privateIP"
```

---

## COBALT STRIKE (CERT / JARM)

```
host.services.cert.parsed.subject.common_name:"Major Cobalt Strike"
host.services.cert.parsed.issuer.common_name:"Major Cobalt Strike"
host.services.cert.parsed.serial_number="146473198"
host.services.jarm.fingerprint:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da"
```

### JARM + Certificate Combo (fake issuer names)
```
host.services:(jarm.fingerprint:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da" and cert.parsed.issuer.common_name:"jquery.com")
host.services:(jarm.fingerprint:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da" and cert.parsed.issuer.common_name:"Google")
host.services:(jarm.fingerprint:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da" and cert.parsed.issuer.common_name:"Microsoft Windows")
```

---

## SLIVER C2

```
host.services.endpoints.http.body:"sliver"
host.services.cert.parsed.issuer.common_name:"operators"
host.services.jarm.fingerprint:"3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910"
```

### Open Directory with Sliver
```
host.services:((labels.value="SUSPICIOUS_OPEN_DIR" or labels.value="OPEN_DIRECTORY") and endpoints.http.body:"sliver")
host.services.endpoints.http.body:"sliver.exe" AND host.services.endpoints.http.html_title:"Index of"
host.services:(endpoints.http.body:"MimiKatz" and (labels.value="SUSPICIOUS_OPEN_DIR" or labels.value="OPEN_DIRECTORY"))
host.services:(endpoints.http.body:"xworm" and (labels.value="SUSPICIOUS_OPEN_DIR" or labels.value="OPEN_DIRECTORY"))
host.services:(endpoints.http.body:"metasploit" and (labels.value="SUSPICIOUS_OPEN_DIR" or labels.value="OPEN_DIRECTORY"))
```

---

## MYTHIC C2

### Title
```
host.services.endpoints.http.html_title:"Mythic"
```

### Port + Title (same service)
```
host.services:(port=7443 and endpoints.http.html_title:"Mythic")
```

### Certificate
```
host.services.cert.parsed.subject.organization:"Mythic"
host.services.cert.parsed.issuer.organization:"Mythic"
```

### Favicon Fingerprint
```
host.services.endpoints.http.favicons.hash_sha256:"3cbf2084fe1733debe21f33511754191ed8f46268d1a8a122a29cccfc7c969f2"
```

> **Note:** This favicon is strongly associated with observed Mythic deployments but is not exclusive to Mythic. Prefer combining it with additional Mythic indicators for higher-confidence detection.

### Same-service Combinations
```
host.services:(endpoints.http.html_title:"Mythic" and cert.parsed.subject.organization:"Mythic")
host.services:(endpoints.http.favicons.hash_sha256:"3cbf2084fe1733debe21f33511754191ed8f46268d1a8a122a29cccfc7c969f2" and endpoints.http.html_title:"Mythic")
host.services:(port=7443 and endpoints.http.html_title:"Mythic" and cert.parsed.subject.organization:"Mythic")
```

### JARM Fingerprints
```
host.services.jarm.fingerprint:"1dd40d40d00040d00042d43d000000831b6af40378e2dd35eeac4e9311926e"
host.services.jarm.fingerprint:"27d40d40d00040d00042d43d000000d2e61cae37a985f75ecafb81b33ca523"
```

### Laravel/Inertia Based Panels
```
host.services:(endpoints.http.html_title:"C2 Panel" and endpoints.http.headers:(key="Set-Cookie" and value:"c2backend_session"))
host.services.endpoints.http.body:"<title inertia>C2 Panel</title>"
```

---

## LOCUST DDOS PANEL / HTTP FLOOD TOOL

### Title Detection
```
host.services.endpoints.http.html_title:"Locust"
```

### HTML Content (DDoS Functions)
```
host.services.endpoints.http.body:"HTTPFloodUser"
host.services.endpoints.http.body:"attack_get"
host.services.endpoints.http.body:"current_rps"
host.services.endpoints.http.body:"available_user_tasks"
```

### Port Based (Default: 8089)
```
host.services:(port=8089 and endpoints.http.html_title:"Locust")
host.services:(port=8089 and endpoints.http.body:"HTTPFloodUser")
```

### Generic C2 Panel with Locust
```
host.services.endpoints.http.html_title:"C2 Panel" AND host.services.endpoints.http.body:"index-CcY992-3.js"
```

### Combined
```
host.services.endpoints.http.html_title:"Locust" AND host.services.endpoints.http.body:"HTTPFloodUser"
```

---

## IMMORTAL DROPPER (Cryptominer)

### Title & HTML
```
host.services.endpoints.http.html_title:"IMMORTAL DROPPER C2 Panel"
host.services.endpoints.http.body:"DeployMiner" AND host.services.endpoints.http.body:"pool.supportxmr.com"
```

### Product
```
host.services.software.product:"XMRig Monero Cryptominer"
```

### JARM Fingerprint
```
host.services.jarm.fingerprint:"29d29d00029d29d00042d42d00000023f2ae7180b8a0816654f2296c007d93"
```

### JA3S Fingerprint
```
host.services.tls.ja3s:"574866101f64002c6421cc329e4d5458"
```

### Server Pattern (Flask/Werkzeug)
```
host.services.endpoints.http.headers:(key="Server" and value:"Werkzeug")
```

### Port Based
```
host.services:(port=5000 and endpoints.http.html_title:"IMMORTAL DROPPER")
```

### Known Wallet
```
host.services.endpoints.http.body:"48edfHu7V9Z84YzzMa6fUueoELZ9ZRXq9VetWzYGzKt52XU5xvqgzYnDK9URnRoJMk1j8nLwEVsaSWJ4fhdUyZijBGUicoD"
```

### Combined
```
host.services:(software.product:"XMRig" and jarm.fingerprint:"29d29d00029d29d00042d42d00000023f2ae7180b8a0816654f2296c007d93")
```

---

## STEALTH C2 (Banking Trojan)

```
host.services.endpoints.http.html_title:"Stealth C2 Panel"
host.services.endpoints.http.body:"Stealth Command & Control Panel"
host.services.endpoints.http.body:"Bank Cookies" AND host.services.endpoints.http.body:"socket.io"
```

---

## SHADOW C2 (Information Stealer)

### Title & HTML
```
host.services.endpoints.http.html_title:"Shadow C2 Panel"
host.services.endpoints.http.body:"collect_telegram" AND host.services.endpoints.http.body:"collect_wallets"
host.services.endpoints.http.body:"Implant Builder" AND host.services.endpoints.http.body:"Shadow"
host.services.endpoints.http.body:"shadow_secure_key"
host.services.endpoints.http.body:"Shadow C2 Command Center"
```

### JARM Fingerprint
```
host.services.jarm.fingerprint:"14d14d16d14d14d08c14d14d14d14dfd9c9d14e4f4f67f94f0359f8b28f532"
```

### JA3S Fingerprint
```
host.services.tls.ja3s:"ba1b42efc7dc57bb43bf81de59791c1b"
```

### Server Pattern (Flask)
```
host.services:(endpoints.http.headers:(key="Server" and value:"Werkzeug") and endpoints.http.html_title:"Shadow")
host.services:(port=5000 and endpoints.http.html_title:"Shadow C2")
```

### Combined
```
host.services:(endpoints.http.html_title:"Shadow C2 Panel" and jarm.fingerprint:"14d14d16d14d14d08c14d14d14d14dfd9c9d14e4f4f67f94f0359f8b28f532")
```

---

## GENERIC WERKZEUG/FLASK C2

> **Warning:** Generic patterns — many false positives. Combine with other indicators.

```
host.services.software.product:"Werkzeug" AND host.services.endpoints.http.body:"/api/bots"
host.services.software.product:"Werkzeug" AND host.services.endpoints.http.body:"/api/targets"
host.services.software.product:"Werkzeug" AND host.services.endpoints.http.body:"/api/command"
```

---

## BULLETPROOF HOSTING - SERV.HOST

```
host.autonomous_system.name:"SERV.HOST GROUP LTD"
host.autonomous_system.name:"SERV.HOST GROUP LTD" AND host.services.endpoints.http.html_title:"Panel"
```

---

## XTREMERAT

```
host.services.software.product:"XtremeRAT"
host.services.endpoints.http.body:"XtremeRAT"
host.services.cert.parsed.subject.common_name:"XtremeRAT"
```

---

## DARKCOMET RAT

```
host.services.software.product:"DarkComet"
host.services.endpoints.http.body:"DarkComet"
host.services.port:1604
```

---

## GH0ST RAT

```
host.services.software.product:"Gh0st RAT"
host.services.endpoints.http.body:"Gh0st"
```

---

## NANOCORE RAT

```
host.services.software.product:"NanoCore"
host.services.endpoints.http.body:"NanoCore"
host.services.cert.parsed.subject.common_name:"NanoCore"
host.services.port:54984
```

---

## ORCUS RAT

```
host.services.software.product:"Orcus"
host.services.cert.parsed.subject.common_name:"Orcus Server"
host.services.cert.parsed.issuer_dn="CN=OrcusServerCertificate"
host.services.endpoints.http.body:"Orcus"
```

---

## REMCOS RAT

```
host.services.software.product:"Remcos"
host.services.endpoints.http.body:"Remcos"
host.services.cert.parsed.subject.common_name:"Remcos"
host.autonomous_system.organization:"langhuajiaju"
```

---

## NJRAT

```
host.services.software.product:"njRAT"
host.services.endpoints.http.body:"njRAT"
host.services.port:5552 OR host.services.port:1177
```

---

## ARES RAT

```
host.services.endpoints.http.html_title:"Ares"
host.services.endpoints.http.body:"Ares RAT"
host.services.endpoints.http.body:"AresRAT"
```

---

## METERPRETER

```
host.services.software.product:"Meterpreter"
host.services.endpoints.http.body:"Meterpreter"
host.services.port:4444 OR host.services.port:4445
```

---

## INTERACTSH C2

```
host.services.endpoints.http.html_title:"Interactsh"
host.services.endpoints.http.body:"interactsh"
host.services.cert.parsed.subject.common_name:"interactsh"
```

---

## KVM TOOLS (Potential C2 Access)

### GLKVM
```
host.services.endpoints.http.html_title:"GLKVM"
host.services.endpoints.http.body:"GLKVM"
```

### PiKVM
```
host.services.endpoints.http.html_title:"PiKVM"
host.services.endpoints.http.body:"PiKVM"
host.services.software.product:"PiKVM"
```

### NanoKVM
```
host.services.endpoints.http.html_title:"NanoKVM"
host.services.endpoints.http.body:"NanoKVM"
```

### TinyPilot KVM
```
host.services.endpoints.http.html_title:"TinyPilot"
host.services.endpoints.http.body:"TinyPilot"
```

---

## DEIMOS C2

```
host.services.endpoints.http.html_title:"Deimos"
host.services.endpoints.http.html_title:"Deimos C2"
host.services.endpoints.http.body:"Deimos"
host.services.cert.parsed.subject.common_name:"Deimos"
host.services:(cert.parsed.subject.organization:"Acme Co" and port=8443)
host.services.cert.parsed.subject.organization:"Acme Co"
```

---

## MERLIN C2

```
host.services.jarm.fingerprint:"29d21b20d29d29d21c41d21b21b41d494e0df9532e75299f15ba73156cee38"
host.services.endpoints.http.html_title:"Merlin"
host.services.endpoints.http.body:"Merlin"
```

---

## KEYCLOAK (Potential C2 Infrastructure)

```
host.services.endpoints.http.favicons.hash_sha256:"47dcf1f1a8f1afd68297a294a263849069a7a62b2e86550241416c2cc56c5676"
host.services.endpoints.http.html_title:"Keycloak"
host.services.endpoints.http.body:"Keycloak"
```

---

## PUPY RAT

```
host.services.software.product:"Pupy"
host.services.endpoints.http.body:"Pupy"
host.services.cert.parsed.subject.organizational_unit:"CONTROL"
```

---

## WSTUNNEL

```
host.services.endpoints.http.body:"wstunnel"
host.services.software.product:"wstunnel"
host.services.endpoints.http.html_title:"wstunnel"
```

---

## RANSOMHUB C2

```
host.services.endpoints.http.body:"Ransomhub"
host.services.endpoints.http.body:"RansomHub"
host.services.endpoints.http.html_title:"RansomHub"
```

---

## HAK5 CLOUD C2

### Product Detection
```
host.services.software.product:"Hak5 Cloud C2" or host.services.hardware.product:"Hak5 Cloud C2" or host.services.operating_systems.product:"Hak5 Cloud C2" or web.software.product:"Hak5 Cloud C2" or web.hardware.product:"Hak5 Cloud C2" or web.operating_systems.product:"Hak5 Cloud C2"
```

### Title Based
```
host.services.endpoints.http.html_title:"Hak5 Cloud C"
```

### HTML Content Based
```
host.services.endpoints.http.body:"Hak5 Cloud"
host.services.endpoints.http.body:"Copyright (c) 2021 Hak5 LLC"
host.services.endpoints.http.body:"<app-root></app-root>" AND host.services.endpoints.http.body:"manifest.webmanifest"
```

### Port Based (Default: 8080)
```
host.services:(port=8080 and endpoints.http.html_title:"Hak5")
```

### JARM Fingerprints
```
host.services.jarm.fingerprint:"3fd21b20d00000021c43d21b21b43de0a012c76cf078b8d06f4620c2286f5e"
host.services.jarm.fingerprint:"40d1db40d0000001dc43d1db1db43de0a012c76cf078b8d06f4620c2286f5e"
host.services.jarm.fingerprint:"27d40d40d00040d00042d43d000000d2e61cae37a985f75ecafb81b33ca523"
```

### JA3S Fingerprints
```
host.services.tls.ja3s:"fd45585efaa8bdce5097aa7539274dac"
host.services.tls.ja3s:"574866101f64002c6421cc329e4d5458"
```

### Combined
```
host.services.software.product:"Hak5 Cloud C2" AND host.services.port:8080
```

---

## NETSUPPORT RAT

```
host.services.software.product:"NetSupport"
host.services.endpoints.http.body:"NetSupport"
host.services.endpoints.http.html_title:"NetSupport"
host.services.port:5405 OR host.services.port:5421
```

---

## ASYNCRAT

```
host.services.cert.parsed.issuer_dn="CN=AsyncRAT Server"
host.services.cert.parsed.subject.common_name:"AsyncRAT Server"
```

---

## VENOMRAT

```
host.services.cert.parsed.subject.common_name:"VenomRAT"
host.services.cert.parsed.issuer.common_name:"VenomRAT"
host.services.endpoints.http.body:"VenomRAT"
```

---

## BITRAT

```
host.services.cert.parsed.issuer_dn="CN=BitRAT"
host.services.cert.parsed.subject.common_name:"BitRAT"
host.services.endpoints.http.body:"BitRAT"
```

---

## SECTOPRAT C2

```
host.services:(port=9000 and endpoints.http.headers:(key="Server" and value:"Microsoft-HTTPAPI/2.0") and endpoints.http.status_code=404)
```

---

## HOOKBOT PANEL

```
host.services.endpoints.http.html_title:"HOOKBOT PANEL"
host.services.endpoints.http.body:"HOOKBOT"
host.services.endpoints.http.body:"HookBot"
```

---

## OYSTER C2

```
host.services.endpoints.http.body_hash_sha256="f84b78e96fc74a902481247dc87434c5ce7b6130f0fa53ab5ba1f6fe1d50d377"
host.services.endpoints.http.body:"Oyster"
```

---

## HAVOC C2

```
host.services.endpoints.http.headers:(key="X_Havoc")
host.services.endpoints.http.body:"Havoc"
host.services.cert.parsed.subject.common_name:"Havoc"
```

---

## XWORM

```
host.services.endpoints.http.body:"XWorm"
host.services.endpoints.http.body:"xworm"
host.services.cert.parsed.subject.common_name:"XWorm"
```

---

## OPEN DIRECTORY - SUSPICIOUS

```
host.services.labels.value:"SUSPICIOUS_OPEN_DIR" or host.services.labels.value:"OPEN_DIRECTORY"
host.services.endpoints.http.html_title:"Index of" AND host.services.endpoints.http.body:".exe"
host.services.endpoints.http.html_title:"Directory Listing for" AND host.services.endpoints.http.body:"payload"
```

---

## GENERIC C2 INDICATORS

### Self-signed Certificate Patterns
```
host.services.cert.parsed.issuer.organization:"Internet Widgits Pty Ltd"
host.services.cert.parsed.subject.common_name:"localhost"
```

---

## CLICKFIX PHISHING CAMPAIGN

### Main ClickFix Detection Queries
```
host.services.endpoints.http.html_title:"Checking if you are human" AND host.services.endpoints.http.body:"k4zrz92z"
host.services.endpoints.http.html_title:"Checking if you are human" AND host.services.endpoints.http.body:"Ctrl"
host.services.endpoints.http.html_title:"Checking if you are human"
```

### JavaScript Identifiers
```
host.services.endpoints.http.body:"checkboxWindow"
```

### Let's Encrypt Certificate with ClickFix
```
host.services:(cert.parsed.issuer_dn:"CN=Let's Encrypt" and endpoints.http.html_title:"Checking if you are human")
host.services:(cert.parsed.issuer.organization:"Let's Encrypt" and endpoints.http.body:"k4zrz92z")
```

### Sectigo Certificate with ClickFix
```
host.services:(cert.parsed.issuer.organization:"Sectigo" and endpoints.http.body:"k4zrz92z")
```

### Behavior-based Detection
```
host.services.endpoints.http.body:"Ctrl + V" AND host.services.endpoints.http.html_title:"human"
host.services.endpoints.http.body:"clipboard" AND host.services.endpoints.http.html_title:"Checking"
```

---

## APT41 (Double Dragon / Barium / Winnti)

### Known Infrastructure Patterns
```
host.services.endpoints.http.html_title:"莹火虫的世界"
```

### Alibaba Cloud Infrastructure
```
host.autonomous_system.asn:45102 AND host.services.port:5432
host.autonomous_system.name:"Alibaba" AND host.services.port:8080 AND host.services.port:5432
```

### Chinese Language Panels
```
host.services.endpoints.http.html_title=~`[一-龥]+` and host.autonomous_system.name:"Alibaba"
```

---

## BIANLIAN GO TROJAN

```
host.services:(cert.parsed.subject_dn=~`C=[0-9a-zA-Z]{16}, O=[0-9a-zA-Z]{16}, OU=[0-9a-zA-Z]{16}` and cert.parsed.issuer_dn=~`C=[0-9a-zA-Z]{16}, O=[0-9a-zA-Z]{16}, OU=[0-9a-zA-Z]{16}`)
```

---

## RESPONDER (LLMNR/NBT-NS Poisoning)

```
host.services.banner_hash_sha256="0fa31c8c34a370931d8ffe8097e998f778db63e2e036fbd7727a71a0dcf5d28c"
host.services.smb.negotiation_log.server_guid="00000000000000000000000000000000ee85abf7eaf60c4f928192476deb76a9"
```

---

## QAKBOT (Banking Trojan)

```
host.services:((jarm.fingerprint="21d14d00021d21d21c42d43d0000007abc6200da92c2a1b69c0a56366cbe21" or jarm.fingerprint="04d02d00004d04d04c04d02d04d04d9674c6b4e623ae36cc2d998e99e2262e") and endpoints.http.body_hash_sha1="22e5446e82b3e46da34b5ebce6de5751664fb867")
host.services:(banner_hash_sha256="5234096d7003929ad67037af6f5816933cab9e85f9b286468249ac9ab9bfb861" and endpoints.http.body_hash_sha1="22e5446e82b3e46da34b5ebce6de5751664fb867")
host.services:(cert.parsed.subject_dn=~`C=[A-Z]{2}, OU=([A-Z][a-z]{3,})( [A-Z][a-z]{3,}){0,2}, CN=[a-z]{4,12}\.[a-z]{2,4}` and not cert.parsed.subject_dn:"OU=Domain Control Validated")
```

---

## VIPER (Chinese C2 Framework)

```
host.services.endpoints.http.body_hash_sha1="cd40dbcdae84b1c8606f29342066547069ed5a33"
host.services.endpoints.http.favicons.hash_md5="a7469955bff5e489d2270d9b389064e1"
```

---

## MEDUZA STEALER

```
host.services.endpoints.http.html_title="Meduza Stealer"
host.services.endpoints.http.favicons.hash_md5="e7a2bb050f7ec5ec2ba405400170a27d"
```

---

## EVILGOPHISH (Phishing Framework)

```
host.services.software.product:"Evilginx" or host.services.hardware.product:"Evilginx" or host.services.operating_systems.product:"Evilginx" or web.software.product:"Evilginx" or web.hardware.product:"Evilginx" or web.operating_systems.product:"Evilginx" or host.services.software.product:"EvilGoPhish" or host.services.hardware.product:"EvilGoPhish" or host.services.operating_systems.product:"EvilGoPhish" or web.software.product:"EvilGoPhish" or web.hardware.product:"EvilGoPhish" or web.operating_systems.product:"EvilGoPhish"
```

---

## GEACON_PRO (Cobalt Strike Go Implementation)

```
host.services:(cert.parsed.subject_dn="C=KZ, ST=KZ, L=, O=NN Fern Sub, OU=NN Fern, CN=foren.zik" and cert.parsed.issuer_dn="C=KZ, ST=KZ, L=, O=NN Fern Sub, OU=NN Fern, CN=foren.zik")
```

---

## CHAOS RAT

```
host.services.software.cpe=~`^cpe:2\.3:a:chaos:chaos:`
```

---

## STEALC V2 (Info Stealer)

```
host.services.endpoints.http.body_hash_sha256="067b25c7c2e27041dc47a0a4564b56a6bbfdc41e5dd630dbf070fdada4dbff71"
```

---

## LIGOLO-NG (Tunneling)

```
host.services.cert.parsed.subject.common_name:"ligolo"
host.services.cert.parsed.issuer.organization:"ligolo"
```

---

## REVERSE SSH

```
host.services.ssh.server_id.software:"reverse"
```

---

## PYRAMID C2

```
host.services.endpoints.http.html_title:"Pyramid"
host.services.software.product:"Pyramid"
```

---

## 📖 Related Documents

- [Home](README.md)
- [Shodan Queries](SHODAN_QUERIES.md)
- [Netlas Queries](NETLAS_QUERIES.md)
- [ClickFix Case Study](ClickFixCampaign-CaseStudies.md)
- [Tool References](TOOLS_REFERENCES.md)
- [Censys Platform Syntax](https://docs.censys.com/docs/censys-platform-syntax-differences) | [Query Converter](https://docs.censys.com/docs/query-converter)

---

**Last Updated:** 2026-09-30
