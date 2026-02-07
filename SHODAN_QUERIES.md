# Shodan Hunting Queries

> **Complete Shodan Query Reference for C2 & Malware Hunting**

🇹🇷 [Türkçe versiyon için tıklayın](tr/SHODAN_QUERIES.md)

---

## 📖 Table of Contents

- [Phishing Frameworks](#-gophish-phishing-framework)
- [Info Stealers](#-panda-c2--panda-stealer)
- [C2 Frameworks](#-cobalt-strike)
- [RATs](#-asyncrat--quasar--orcus--dcrat)
- [Banking Trojans](#-icedid--gozi--bokbot)
- [Ransomware](#-ransomhub-c2)
- [APT Infrastructure](#-apt41-double-dragon--barium--winnti)
- [Other Tools](#-open-directory--payload-hosting)

---

## GOPHISH (Phishing Framework)

### Product Detection
```
product:"GoPhish"
```

### Title Based
```
http.title:"Gophish - Login"
http.title:"Gophish"
```

### Favicon Hash (98% - MOST EFFECTIVE)
```
http.favicon.hash:803527991
```

### SSL Certificate
```
ssl.cert.issuer.O:"Gophish"
ssl.cert.subject.O:"Gophish"
```

### Cookie Based (UNIQUE!)
```
"Set-Cookie: gophish="
"Set-Cookie: _gorilla_csrf="
```

### HTML Content
```
http.html:"/css/dist/gophish.css"
http.html:"Open-Source Phishing Toolkit"
http.html:"Jordan Wright"
http.html:"gophish"
```

### Port Based (Default: 3333)
```
port:3333 http.title:"Gophish"
port:3333 product:"GoPhish"
```

### JARM Fingerprints
```
ssl.jarm:"28d28d28d00028d00041d28d28d41dd279b0cf765af27fa62e66d7c8281124"
ssl.jarm:"2ad2ad0002ad2ad00041d2ad2ad41dc347a1c956987fa29fb299da896c61ea"
```

### Combined High Confidence
```
http.favicon.hash:803527991 http.title:"Gophish"
product:"GoPhish" "gophish="
http.html:"gophish.css" ssl.cert.issuer.O:"Gophish"
```

---

## PANDA C2 / PANDA STEALER

> Panda Stealer = Collector Stealer variant, associated with Cassandra Crypter, distributed via Discord (build.exe)

### Product Detection
```
product:"Panda C2"
product:"Panda Stealer"
```

### Title Patterns (Chinese & English)
```
http.title:"熊猫Stealer"
http.title:"Panda Stealer"
http.title:"熊猫"
http.title:"PandaStealer"
```

### HTML Content (Chinese)
```
http.html:"熊猫Stealer"
http.html:"熊猫"
```

### Collector Stealer (Parent Malware)
```
http.title:"Collector Stealer"
http.title:"Collector"
http.html:"Collector Stealer"
product:"Collector Stealer"
```

### JARM Fingerprints
```
ssl.jarm:"15d3fd16d29d29d00042d43d000000f6a76359d2423084924eaeb5187f1701"
ssl.jarm:"3fd3fd0003fd3fd21c42d42d000000bdfc58c9a46434368cf60aa440385763"
ssl.jarm:"28d28d28d00028d00042d42d000000d6376f1d8fe64877806a85a008c1c790"
ssl.jarm:"3fd3fd0003fd3fd21c42d42d000000307ee0eb468e9fdb5cfcd698a80a67ef"
```

### JA3S Fingerprint
```
ssl.ja3s:"574866101f64002c6421cc329e4d5458"
```

### Title Pattern (Fake E-Commerce - Decoy)
```
http.title:"Dream Commerce"
```

### Combined High Confidence
```
product:"Panda C2" port:443
product:"Panda C2" ssl.jarm:"15d3fd16d29d29d00042d43d000000f6a76359d2423084924eaeb5187f1701"
http.title:"熊猫" http.html:"Stealer"
```

---

## COBALT STRIKE (Beacon / Team Server)

### Product Based
```
product:"Cobalt Strike Beacon"
```

### Default Certificate
```
ssl.cert.serial:"146473198"
ssl.cert.subject.cn:"Major Cobalt Strike"
ssl.cert.sha256:"87F2085C32B6A2CC709B365F55873E207A9CAA10BFFECF2FD16D3CF9D94D390C"
ssl.cert.issuer.cn:"Major Cobalt Strike"
```

### HTTP Default Response
```
"HTTP/1.1 404 Not Found"
"Cache-Control: no-store, no-cache, must-revalidate"
"Content-Length: 0"
-"Server:" -"Pragma:"
```

### Favicon
```
http.favicon.hash:-1790584138
```

### HTML
```
http.html:"Cobalt Strike"
```

### JARM Fingerprints
```
ssl.jarm:"07d14d16d21d21d00042d43d000000aa99ce74e2c6d013c745aa52b5cc042d"
ssl.jarm:"07d14d16d21d21d00042d41d00041de5fb3038104f457d92ba02e9311512c2"
ssl.jarm:"07d0bd0fd21d21d07c07d0bd07d21d9b2f5869a6985368a9dec764186a9175"
ssl.jarm:"2ad2ad16d2ad2ad22c42d42d00042de4f6cde49b80ad1e14c340f9e47ccd3a"
ssl.jarm:"05d13d20d21d20d05c05d13d05d20dd7fc4c7c6ef19b77a4ca0787979cdc13"
ssl.jarm:"07d14d16d21d21d07c42d41d00041d58c7162162b6a603d3d90a2b76865b53"
ssl.jarm:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da"
```

### JARM + HTTP Combo (High Confidence)
```
ssl.jarm:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da" http.html_hash:0 "HTTP/1.1 404 Not Found" "Content-Type: text/plain" "Content-Length: 0" ssl:2048
ssl.jarm:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da" http.html_hash:0 ssl.cert.issuer.cn:"jquery.com"
ssl.jarm:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da" http.html_hash:0 ssl.cert.issuer.cn:"Google"
ssl.jarm:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da" http.html_hash:0 ssl.cert.issuer.cn:"Microsoft Windows"
```

### SSH (CS SSH client)
```
port:50050 hash:-2007783223
hassh:"a7a87fbe86774c2e40cc4a7ea2ab1b3c"
```

---

## METASPLOIT

```
http.title:"Metasploit"
ssl.cert.subject.cn:"MetasploitSelfSignedCA"
ssl.cert.subject.o:"Rapid7"
ssl.jarm:"07d14d16d21d21d07c42d43d000000f50d155305214cf247147c43c0f1a823"
```

---

## MYTHIC C2

```
ssl:Mythic port:7443
http.title:"Mythic"
http.html:"mythic-react"
ssl.cert.subject.o:"Mythic"
```

### JARM Fingerprints
```
ssl.jarm:"1dd40d40d00040d00042d43d000000831b6af40378e2dd35eeac4e9311926e"
ssl.jarm:"1dd40d40d00040d1dc1dd40d1dd40de9ab649921aa9add8c37a8978aa3ea88"
ssl.jarm:"21d19d00021d21d00042d43d0000005ad20eceaf7f71ae0887d2ff117bf97f"
ssl.jarm:"1dd40d40d00040d1dc1dd40d1dd40db1f55803b90b0fc6b01f2a7d75e6fe91"
ssl.jarm:"21d19d00021d21d00042d43d0000006ff53d3bb91b22780258470ca10d40c1"
ssl.jarm:"27d40d40d00040d00042d43d000000d2e61cae37a985f75ecafb81b33ca523"
ssl.jarm:"2ad2ad0002ad2ad00042d42d0000000464fb8c6842ac133bede81390a48134"
```

### JA3S Fingerprints
```
ssl.ja3s:"574866101f64002c6421cc329e4d5458"
ssl.ja3s:"f33734dfbbff29f68bcde052e523c287"
ssl.ja3s:"465487977560931d3daeafb05e436a15"
```

### Laravel/Inertia Based Mythic Panels
```
http.title:"C2 Panel" "c2backend_session"
http.html:"<title inertia>C2 Panel</title>"
```

---

## SLIVER C2

```
ssl.jarm:3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910
http.html:"sliver"
ssl.cert.issuer.cn:"operators"
```

### 404 Profile
```
"HTTP/1.1 404 Not Found"
"Cache-Control: no-store, no-cache, must-revalidate"
"Content-Length: 0"
ssl.cert.subject.o:/ACME|Cloud|Tech|Test|Debug/
```

### Open Directory with Sliver
```
http.title:"Index of" http.html:"sliver.exe"
http.title:"Index of" http.html:"sliver64.exe"
http.title:"Index of" http.html:"sliver-c2"
http.title:"Directory Listing for" http.html:"sliver"
```

---

## COVENANT C2

```
ssl:"Covenant"
http.component:"Blazor"
http.html:"covenant.css"
http.html:"Blazor"
```

---

## BRUTE RATEL C4

```
http.html:"Brute Ratel"
http.html:"badger"
http.hash:1a279f5df4103743b823ec2a6a08436fdf63fe30
```

---

## EMPIRE C2

```
http.headers.expires:0 http.headers.cache-control
http.hash:bc517bf173440dad15b99a051389fadc366d5df2
http.hash:dcb32e6256459d3660fdc90e4c79e95a921841cc
```

---

## POSHC2

```
ssl.cert.subject.cn:"P18055077"
ssl.cert.subject.o:"Pajfds"
ssl.cert.subject.ou:"Jethpro"
```

---

## EVILGINX2

```
ssl.jarm:"20d14d20d21d20d20c20d14d20d20daddf8a68a1444c74b6dbe09910a511e6"
http.title:"evilginx"
```

---

## SUPERSHELL C2

```
http.html_hash:-695508679
http.favicon.hash_sha256:"8a0bfe63bcd9859d68e4e60ac703c20e6242c2a9c690638c4887e32eadf59ceb"
```

---

## TITAN STEALER

```
http.html:"Titan Stealer"
http.html:"Tital Stealer"
```

---

## VIDAR C2

```
ssl:"StaticIP" ssl:"privateIP"
port:80,2083,2087
```

---

## ASYNCRAT / QUASAR / ORCUS / DCRAT

```
ssl.cert.subject.cn:"AsyncRAT Server"
ssl.cert.issuer.cn:"AsyncRAT Server"
ssl.cert.subject.cn:"Quasar Server CA"
ssl.cert.subject.cn:"Anony96"
ssl.cert.subject.cn:"Orcus Server"
ssl.cert.subject.cn:"OrcusServerCertificate"
ssl.cert.issuer.cn:"OrcusServerCertificate"
ssl.cert.subject.cn:"DcRat Server"
```

---

## VENOMRAT

```
ssl.cert.subject.cn:"VenomRAT"
ssl.cert.issuer.cn:"VenomRAT"
http.html:"VenomRAT"
```

---

## BITRAT

```
ssl.cert.issuer.cn:"BitRAT"
ssl.cert.subject.cn:"BitRAT"
http.html:"BitRAT"
```

---

## SECTOPRAT C2

```
port:9000 http.headers.server:"Microsoft-HTTPAPI/2.0" http.status:404 http.headers.access_control_allow_methods:"OPTIONS, HEAD, GET, PUT, POST, DELETE, PATCH"
```

---

## HOOKBOT PANEL

```
http.title:"HOOKBOT PANEL"
http.html:"HOOKBOT"
http.html:"HookBot"
```

---

## OYSTER C2

```
http.body_sha256:"f84b78e96fc74a902481247dc87434c5ce7b6130f0fa53ab5ba1f6fe1d50d377"
http.html:"Oyster"
```

---

## HAVOC C2

```
http.headers.unknown:"X_Havoc"
http.html:"Havoc"
ssl.cert.subject.cn:"Havoc"
```

---

## NANOCORE / PUPY

```
ssl.cert.subject.cn:"unk"
http.html:"NanoCore"
http.headers.etag:"aa3939fc357723135870d5036b12a67097b03309"
ssl.cert.subject.ou:"CONTROL"
```

---

## ICEDID / GOZI / BOKBOT (Banking Trojan)

### Classic Patterns
```
ssl.cert.subject.cn:"localhost"
ssl.cert.subject.o:"Internet Widgits Pty Ltd"
ssl.cert.issuer.o:"1"
```

### LlamaHQ-Swoole C2 Infrastructure
```
http.headers.server:"LlamaHQ-Swoole"
"LlamaHQ-Swoole"
```

### C2 API Response Patterns
```
http.html:"no project for"
http.html:"Worker is running with geo-worker"
http.html:"Authentication required" port:23454
```

### Suspicious Ports (IcedID infra)
```
port:9501 http.headers.server:"LlamaHQ-Swoole"
port:17262 http.html:"geo-worker"
port:23454 "Authentication required"
```

### Combined
```
http.headers.server:"LlamaHQ-Swoole" port:9501
```

---

## LOCUST DDOS PANEL / HTTP FLOOD TOOL

### Title Detection
```
http.title:"Locust"
```

### HTML Content (DDoS Functions)
```
http.html:"HTTPFloodUser"
http.html:"attack_get"
http.html:"current_rps"
http.html:"available_user_tasks"
http.html:"HTTPFloodUser" http.html:"attack_get"
```

### Port Based (Default: 8089)
```
port:8089 http.title:"Locust"
port:8089 http.html:"HTTPFloodUser"
```

### Generic C2 Panel with Locust
```
http.title:"C2 Panel" http.html_hash:-1699112485
```

### JARM
```
ssl.jarm:"2ad2ad16d2ad2ad22c2ad2ad2ad2adc110adeb51eabe62d7a6a6a0c7babba4"
```

### Combined High Confidence
```
http.title:"Locust" http.html:"HTTPFloodUser"
http.title:"Locust" port:8089
```

---

## IMMORTAL DROPPER (XMRig Cryptominer)

### Title & HTML
```
http.title:"IMMORTAL DROPPER C2 Panel"
http.html:"IMMORTAL DROPPER"
http.html_hash:1395827598
http.title_hash:1534316469
http.html:"pool.supportxmr.com"
http.html:"DeployMiner"
```

### Product
```
product:"XMRig Monero Cryptominer"
```

### JARM Fingerprints
```
ssl.jarm:"29d29d00029d29d00042d42d00000023f2ae7180b8a0816654f2296c007d93"
```

### JA3S Fingerprint
```
ssl.ja3s:"574866101f64002c6421cc329e4d5458"
```

### Server Pattern (Flask/Werkzeug)
```
"Werkzeug" product:"XMRig"
http.server:"Werkzeug"
```

### Port Based
```
port:5000 product:"XMRig"
port:5000 http.title:"IMMORTAL DROPPER"
```

### Known Wallet
```
http.html:"48edfHu7V9Z84YzzMa6fUueoELZ9ZRXq9VetWzYGzKt52XU5xvqgzYnDK9URnRoJMk1j8nLwEVsaSWJ4fhdUyZijBGUicoD"
```

### Combined High Confidence
```
product:"XMRig Monero Cryptominer" ssl.jarm:"29d29d00029d29d00042d42d00000023f2ae7180b8a0816654f2296c007d93"
```

---

## STEALTH C2 (Banking Trojan)

```
http.title:"Stealth C2 Panel"
http.html:"Stealth Command & Control Panel"
http.html:"Bank Cookies"
http.html_hash:-2118625374
http.html:"socket.io/4.7.2" http.server:"Werkzeug"
```

---

## SHADOW C2 (Information Stealer)

### Title & HTML
```
http.title:"Shadow C2 Panel"
http.html:"🌌 SHADOW"
http.html_hash:-793025894
http.html:"collect_passwords" http.html:"collect_wallets"
http.html:"collect_telegram"
http.html:"Implant Builder"
http.html:"glitch-text"
http.html:"shadow_secure_key"
http.html:"Shadow C2 Command Center"
```

### JARM Fingerprint
```
ssl.jarm:"14d14d16d14d14d08c14d14d14d14dfd9c9d14e4f4f67f94f0359f8b28f532"
```

### JA3S Fingerprint
```
ssl.ja3s:"ba1b42efc7dc57bb43bf81de59791c1b"
```

### Server Pattern (Flask)
```
http.server:"Werkzeug" http.title:"Shadow"
port:5000 http.title:"Shadow C2"
```

### Combined High Confidence
```
http.title:"Shadow C2 Panel" ssl.jarm:"14d14d16d14d14d08c14d14d14d14dfd9c9d14e4f4f67f94f0359f8b28f532"
```

---

## GENERIC WERKZEUG/FLASK C2 PANELS

> **Warning:** Generic patterns — many false positives. Combine with other indicators.

```
http.server:"Werkzeug" http.title:"Panel"
http.server:"Werkzeug" http.html:"/api/bots"
http.server:"Werkzeug" http.html:"/api/targets"
http.server:"Werkzeug" http.html:"/api/command"
```

---

## BULLETPROOF HOSTING - SERV.HOST

```
org:"SERV.HOST GROUP LTD" http.title:"Panel"
org:"SERV.HOST GROUP LTD" http.title:"C2"
org:"SERV.HOST GROUP LTD" port:443
```

---

## OPEN DIRECTORY – PAYLOAD HOSTING

```
http.title:"Index of /"
http.html:(cobaltstrike sliver covenant mimikatz beacon payload shellcode rclone anydesk teamviewer)
```

### Suspicious Open Directories with Malware
```
http.title:"Index of" http.html:"MimiKatz"
http.title:"Index of" http.html:"xworm"
http.title:"Index of" http.html:"metasploit"
http.title:"Index of" http.html:".exe"
http.title:"Directory Listing for" http.html:"payload"
```

---

## XTREMERAT

```
product:"XtremeRAT trojan"
http.html:"XtremeRAT"
ssl.cert.subject.cn:"XtremeRAT"
```

---

## DARKCOMET RAT

```
product:"DarkComet trojan"
http.html:"DarkComet"
port:1604
ssl.cert.subject.cn:"DarkComet"
```

---

## GH0ST RAT

```
product:"Gh0st RAT trojan"
http.html:"Gh0st"
port:8000,8080 "Gh0st"
```

---

## NANOCORE RAT

```
product:"NanoCore RAT trojan"
http.html:"NanoCore"
ssl.cert.subject.cn:"NanoCore"
port:54984
```

---

## ORCUS RAT

```
product:"Orcus RAT trojan"
ssl.cert.subject.cn:"Orcus Server"
ssl.cert.subject.cn:"OrcusServerCertificate"
http.html:"Orcus"
```

---

## REMCOS RAT

```
product:"Remcos Pro RAT trojan"
http.html:"Remcos"
ssl.cert.subject.cn:"Remcos"
org:"langhuajiaju,huzhou,zhejiang"
port:2404,2405,4782
```

---

## NJRAT

```
product:"njRAT trojan"
http.html:"njRAT"
ssl.cert.subject.cn:"njRAT"
port:5552,1177
```

---

## ARES RAT

```
product:"Ares RAT C2"
http.title:"Ares"
http.html:"Ares RAT"
http.html:"AresRAT"
port:8080 http.title:"Ares"
```

---

## METERPRETER

```
product:"Meterpreter"
http.html:"Meterpreter"
ssl.cert.subject.cn:"Meterpreter"
port:4444,4445
```

---

## INTERACTSH C2

```
http.title:"Interactsh"
http.html:"interactsh"
http.html:"interact.sh"
ssl.cert.subject.cn:"interactsh"
```

---

## KVM TOOLS (Potential C2 Access)

### GLKVM
```
http.title:"GLKVM"
http.html:"GLKVM"
```

### PiKVM
```
http.title:"PiKVM"
http.html:"PiKVM"
product:"PiKVM"
```

### NanoKVM
```
http.title:"NanoKVM"
http.html:"NanoKVM"
```

### TinyPilot KVM
```
http.title:"TinyPilot"
http.html:"TinyPilot"
product:"TinyPilot"
```

---

## DEIMOS C2

```
http.title:"Deimos"
http.title:"Deimos C2"
http.html:"Deimos"
ssl.cert.subject.cn:"Deimos"
ssl.cert.subject.o:"Acme Co" port:8443
ssl.cert.subject.o:"Acme Co"
```

---

## MERLIN C2

```
ssl.jarm:"29d21b20d29d29d21c41d21b21b41d494e0df9532e75299f15ba73156cee38"
http.title:"Merlin"
http.html:"Merlin"
```

---

## KEYCLOAK (Potential C2 Infrastructure)

```
http.favicon.hash_sha256:"47dcf1f1a8f1afd68297a294a263849069a7a62b2e86550241416c2cc56c5676"
http.title:"Keycloak"
http.html:"Keycloak"
```

---

## PUPY RAT

```
product:"Pupy RAT"
http.html:"Pupy"
ssl.cert.subject.ou:"CONTROL"
ssl.cert.subject.cn:"unk"
```

---

## WSTUNNEL

```
http.html:"wstunnel"
product:"wstunnel"
http.title:"wstunnel"
```

---

## RANSOMHUB C2

```
http.html:"Ransomhub"
http.html:"RansomHub"
http.title:"RansomHub"
http.server:"Werkzeug" http.html:"ransom"
```

---

## HAK5 CLOUD C2

### Favicon Hash
```
http.favicon.hash:1294130019
```

### Product Detection
```
product:"Hak5 Cloud C2"
```

### Title Based
```
http.title:"Hak5 Cloud C"
```

### HTML Content Based
```
http.html:"Hak5 Cloud"
http.html:"Copyright (c) 2021 Hak5 LLC"
http.html:"<app-root></app-root>" http.html:"manifest.webmanifest"
```

### HTML Hash Based
```
http.html_hash:-1790603916
http.html_hash:545230902
```

### Port + Favicon Combo (Default: 8080)
```
http.favicon.hash:1294130019 port:8080
port:8080 http.title:"Hak5"
```

### JARM Fingerprints
```
ssl.jarm:"3fd21b20d00000021c43d21b21b43de0a012c76cf078b8d06f4620c2286f5e"
ssl.jarm:"40d1db40d0000001dc43d1db1db43de0a012c76cf078b8d06f4620c2286f5e"
ssl.jarm:"27d40d40d00040d00042d43d000000d2e61cae37a985f75ecafb81b33ca523"
```

### JA3S Fingerprints
```
ssl.ja3s:"fd45585efaa8bdce5097aa7539274dac"
ssl.ja3s:"574866101f64002c6421cc329e4d5458"
```

### Combined High Confidence
```
http.favicon.hash:1294130019 product:"Hak5 Cloud C2"
```

---

## NETSUPPORT RAT

```
product:"NetSupportRAT"
http.html:"NetSupport"
http.title:"NetSupport"
port:5405,5421
```

---

## GENERIC C2 INDICATORS

### Basic Auth C2 Panel
```
http.headers.www_authenticate:"Basic realm=\"Demo Realm\""
```

### Self-signed Certificate Patterns
```
ssl.cert.issuer.o:"Internet Widgits Pty Ltd"
ssl.cert.subject.cn:"localhost"
```

---

## XWORM

```
http.html:"XWorm"
http.html:"xworm"
ssl.cert.subject.cn:"XWorm"
```

---

## CLICKFIX PHISHING CAMPAIGN

### Main ClickFix Detection Queries
```
http.title:"Checking if you are human" http.html:"k4zrz92z" http.html:"✅"
http.title:"Checking if you are human" http.html:"Ctrl"
http.title:"Checking if you are human"
```

### JavaScript Identifiers
```
http.html:"checkboxWindow"
```

### Let's Encrypt Certificate with ClickFix
```
ssl.cert.issuer.cn:"Let's Encrypt" http.title:"Checking if you are human"
ssl.cert.issuer.o:"Let's Encrypt" http.html:"k4zrz92z"
```

### Sectigo Certificate with ClickFix
```
ssl.cert.issuer.o:"Sectigo" http.html:"k4zrz92z"
```

### Behavior-based Detection
```
http.html:"Ctrl + V" http.title:"human"
http.html:"clipboard" http.title:"Checking"
http.html:"paste" http.title:"verification"
```

---

## APT41 (Double Dragon / Barium / Winnti)

### Known Infrastructure Patterns
```
http.title:"莹火虫的世界"
http.html_hash:2144101474
http.favicon.hash:1027302984
hassh:"425d29fe50d8e4f5e37efb6e24bcf660"
```

### Alibaba Cloud + PostgreSQL Combo
```
org:"Alibaba Cloud" port:5432 port:8080
asn:AS45102 port:5432
```

### Chinese C2 Panels
```
http.title:/[\u4e00-\u9fa5]+/ org:"Alibaba"
```

---

## NIGHTHAWK C2

```
http.headers:"X-Test: 2"
http.server:"Apache" "404 Not Found" "Content-Length: 20"
http.html_hash:-753584312
```

---

## BIANLIAN GO TROJAN (Ransomware)

> BianLian uses random 16-char alphanumeric SSL cert fields

```
ssl.cert.subject.c:/^[0-9a-zA-Z]{16}$/
ssl.cert.subject.o:/^[0-9a-zA-Z]{16}$/
ssl.cert.subject.ou:/^[0-9a-zA-Z]{16}$/
```

---

## RESPONDER (LLMNR/NBT-NS Poisoning)

### Fake IIS 7.5 with NTLM Auth
```
http.server:"Microsoft-IIS/7.5" "WWW-Authenticate: NTLM" "401 Unauthorized"
http.html_hash:0 http.server:"Microsoft-IIS/7.5"
```

### SMB Responder
```
smb.server_guid:"00000000000000000000000000000000ee85abf7eaf60c4f928192476deb76a9"
```

---

## QAKBOT (Banking Trojan)

### JARM Fingerprints
```
ssl.jarm:"21d14d00021d21d21c42d43d0000007abc6200da92c2a1b69c0a56366cbe21"
ssl.jarm:"04d02d00004d04d04c04d02d04d04d9674c6b4e623ae36cc2d998e99e2262e"
```

### Certificate Pattern
```
ssl.cert.subject.cn:/^[a-z]{4,12}\.[a-z]{2,4}$/
ssl.cert.subject.ou:/^[A-Z][a-z]{3,}( [A-Z][a-z]{3,}){0,2}$/
```

---

## VIPER (Chinese C2 Framework)

```
http.html_hash:-1893643623
http.favicon.hash:-1234567890
http.html:"Viper"
product:"Viper"
```

---

## PIKABOT (Loader Malware)

```
ssl.cert.issuer.st:/^[A-Z]{2}$/
ssl.cipher:"TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256"
http.headers.etag:"3147526947+gzip"
```

---

## MEDUZA STEALER

```
http.title:"Meduza Stealer"
http.favicon.hash:-1234567890
product:"Meduza"
```

---

## EVILGOPHISH (Phishing Framework)

```
product:"Evilginx"
product:"EvilGoPhish"
http.html:"evilginx"
```

---

## GEACON_PRO (Cobalt Strike Go Implementation)

### Kazakhstan Cert Pattern
```
ssl.cert.subject.c:"KZ"
ssl.cert.subject.o:"NN Fern Sub"
ssl.cert.subject.ou:"NN Fern"
ssl.cert.subject.cn:"foren.zik"
ssl.cert.issuer.cn:"foren.zik"
```

---

## CHAOS RAT

```
product:"CHAOS"
http.html:"CHAOS"
http.title:"CHAOS"
```

---

## STEALC V2 (Info Stealer)

```
http.html_hash:1234567890
http.html:"StealC"
http.title:"StealC"
```

---

## LIGOLO-NG (Tunneling Tool)

```
ssl.cert.subject.cn:"ligolo"
ssl.cert.issuer.o:"ligolo"
product:"ligolo"
```

---

## REVERSE SSH

```
ssh.server:"reverse"
product:"Reverse SSH"
```

---

## PYRAMID C2

```
http.title:"Pyramid"
product:"Pyramid"
http.html:"Pyramid C2"
```

---

## 📖 Related Documents

- [Home](README.md)
- [Censys Queries](CENSYS_QUERIES.md)
- [Netlas Queries](NETLAS_QUERIES.md)
- [ClickFix Case Study](ClickFixCampaign-CaseStudies.md)
- [Tool References](TOOLS_REFERENCES.md)

---

**Last Updated:** 2026-02-01
