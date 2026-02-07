<p align="center">
  <img src="../Public/logo-icons/hunter.png" alt="Threat Hunting - Queries for Search Engines" width="480" style="max-width: 100%; max-height: 220px; width: auto; height: auto; object-fit: contain; display: block; margin: 0 auto;" />
</p>

<p align="center">
  <a href="https://github.com/frknaykc/Awesome-Malicious-Infra-Hunting-Queries/stargazers"><img src="https://img.shields.io/github/stars/frknaykc/Awesome-Malicious-Infra-Hunting-Queries?style=flat-square" alt="GitHub stars" /></a>
  <a href="https://github.com/frknaykc/Awesome-Malicious-Infra-Hunting-Queries/network/members"><img src="https://img.shields.io/github/forks/frknaykc/Awesome-Malicious-Infra-Hunting-Queries?style=flat-square" alt="GitHub forks" /></a>
  <a href="../LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square" alt="License" /></a>
  <a href="https://github.com/frknaykc/Awesome-Malicious-Infra-Hunting-Queries/commits"><img src="https://img.shields.io/github/last-commit/frknaykc/Awesome-Malicious-Infra-Hunting-Queries?style=flat-square" alt="Son commit" /></a>
</p>

<p align="center">
  <a href="../SHODAN_QUERIES.md"><img src="https://img.shields.io/badge/Shodan-Queries-orange?style=flat-square" alt="Shodan" /></a>
  <a href="../CENSYS_QUERIES.md"><img src="https://img.shields.io/badge/Censys-Queries-orange?style=flat-square" alt="Censys" /></a>
  <a href="../NETLAS_QUERIES.md"><img src="https://img.shields.io/badge/Netlas-Queries-orange?style=flat-square" alt="Netlas" /></a>
</p>

# Zararlı Altyapı Avı Sorguları

<p align="center">
  <strong>Shodan, Censys ve Netlas için hazır hunting query'leri — C2 sunucuları, RAT panelleri, phishing kit'leri ve zararlı altyapı tespiti.</strong>
</p>

<p align="center">
  <a href="#giriş">Giriş</a> •
  <a href="#temel-kavramlar">Temel Kavramlar</a> •
  <a href="#bu-repository-ne-içerir">Query Dosyaları</a> •
  <a href="../TOOLS_REFERENCES.md">Tool Referansları</a> •
  <a href="../CONTRIBUTING.md">Katkıda Bulunma</a>
</p>

<p align="center">
  🇬🇧 <a href="../README.md">Click for English version</a>
</p>

---

## Giriş

Bu repository, internet genelinde servisleri, sertifikaları ve HTTP yanıtlarını indeksleyen **Shodan**, **Censys** ve **Netlas** arama motorları için **hazır hunting query’leri** sunar. Güvenlik araştırmacıları, tehdit avcıları ve SOC ekipleri bu sorgularla:

- **Zararlı altyapıyı tespit edebilir** — C2 sunucuları, RAT panelleri, phishing kit’leri ve malware hosting
- **Threat hunting’i destekleyebilir** — Saldırılarda kullanılan bilinen araçların açığa çıkmış örneklerini bulabilir
- **IOC zenginleştirmesi yapabilir** — IP ve domain’leri fingerprint tabanlı sorgularla ilişkilendirebilir
- **Açık kaynak araçları tanımlayabilir** — Birçok C2 framework ve phishing aracı aranabilir fingerprint’ler (favicon hash, TLS sertifikası, HTML başlığı) bırakır

Query’ler hem **ticari** hem de **açık kaynak** araçları hedefler. Açık kaynak C2 framework’leri (Sliver, Mythic, Havoc, Covenant vb.) ve phishing platformları (GoPhish, Evilginx), varsayılan ayarlarında tutarlı ve aranabilir fingerprint’ler ürettikleri için özellikle tespit edilebilirdir. Cobalt Strike gibi ticari araçların da bilinen JARM imzaları ve sertifika kalıpları vardır.

---

## Temel Kavramlar

### C2 (Command & Control) Nedir?

**C2 sunucusu**, siber saldırganların bir botnet veya zararlı yazılım kampanyasındaki ele geçirilmiş cihazları (bilgisayarlar, sunucular, IoT cihazları) uzaktan kontrol etmek için kullandığı merkezi bir ağ servisidir. C2, saldırganın komutlarını alır ve enfekte host’lara dağıtır; aynı zamanda exfilte edilen verileri toplar. C2 altyapısını tespit etmek, tehdit avının temel hedeflerinden biridir.

### RAT (Remote Access Trojan) Nedir?

**RAT**, saldırgana enfekte bir sistem üzerinde gizli uzaktan kontrol sağlayan zararlı yazılımdır. C2 sunucusu ile haberleşir. Genelde tuş kaydı, ekran görüntüsü, dosya erişimi, webcam kontrolü ve uzaktan komut çalıştırma gibi özellikler içerir. AsyncRAT, Quasar ve NjRAT gibi RAT’lar sıklıkla aranabilir TLS sertifikası veya HTTP imzaları sergiler.

### Zararlı Altyapı (Malicious Infrastructure) Nedir?

**Zararlı altyapı**, siber saldırıları destekleyen sunucuları, domain’leri ve ağ varlıklarını ifade eder: C2 sunucuları, phishing panelleri, malware dağıtım host’ları, credential stealer backend’leri ve exploit kit’leri. Bu altyapıyı avlamak, kampanyaların ölçeklenmeden önce tespit edilmesine ve blokaj/incident response için IOC üretilmesine yardımcı olur.

### Phishing Araçları Nedir?

**Phishing araçları**, kimlik bilgisi toplama kampanyaları oluşturmak ve yürütmek için kullanılan platformlardır. **GoPhish**, **Evilginx** ve **EvilGoPhish** örnek verilebilir. Sahte giriş sayfaları barındırır ve kimlik bilgilerini yakalar. Birçoğunun Shodan, Censys ve Netlas ile aranabilir, belirgin fingerprint’leri (favicon hash, cookie’ler, HTML içeriği) vardır.

### Red Team Araçları Nedir?

**Red team araçları**, düşman simülasyonu, penetrasyon testi ve yetkili güvenlik değerlendirmeleri için kullanılan framework’lerdir. **Cobalt Strike**, **Sliver**, **Mythic** ve **Havoc** gibi C2 framework’leri meşru red team çalışmalarında kullanılır ancak tehdit aktörleri tarafından da kötüye kullanılır. Ağ ve TLS fingerprint’leri iyi belgelenmiştir; hem savunma (açığa çıkmış örnekleri bulmak) hem de ofansif araştırma için aranabilirler.

---

## Bu Repository Ne İçerir?

| Dosya | İçerik |
|-------|--------|
| [SHODAN_QUERIES.md](SHODAN_QUERIES.md) | Tüm Shodan hunting query'leri |
| [CENSYS_QUERIES.md](CENSYS_QUERIES.md) | Tüm Censys hunting query'leri |
| [NETLAS_QUERIES.md](NETLAS_QUERIES.md) | Tüm Netlas hunting query'leri |
| [ClickFixCampaign-CaseStudies.md](ClickFixCampaign-CaseStudies.md) | ClickFix sosyal mühendislik saldırısı analizi |
| [TOOLS_REFERENCES.md](TOOLS_REFERENCES.md) | Tüm RAT, C2 ve tool GitHub linkleri |

---

## Fingerprint Türleri

| Tür | Açıklama | Örnek |
|-----|----------|-------|
| **Favicon Hash** | Web sitesi ikonunun hash'i | `http.favicon.hash:803527991` |
| **HTTP Header** | Sunucu yanıt header'ları | `"X-Havoc: true"` |
| **TLS Cert** | SSL sertifika alanları | `ssl.cert.subject.cn:"AsyncRAT Server"` |
| **JARM** | TLS handshake fingerprint | `ssl.jarm:"07d14d16d21d21d..."` |
| **HTML Title** | Sayfa başlığı | `http.title:"Mythic"` |
| **HTML Body** | Sayfa içeriği | `http.html:"mythic-react"` |

---

## Birleşik Fingerprint Örnekleri

### Yüksek Doğruluklu Tespit

Birden fazla fingerprint'i birleştirmek tespit doğruluğunu artırır:

**Mythic C2:**
```bash
# Shodan - Title + Certificate
http.title:"Mythic" ssl.cert.subject.o:"Mythic"

# Censys - same_service ile birleşik
same_service(services.tls.certificates.leaf_data.subject.dn="O=Mythic" AND services.http.response.html_title="Mythic")

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

# Cookie + HTML İçeriği
"Set-Cookie: gophish=" http.html:"gophish.css"
```

**AsyncRAT:**
```bash
# Certificate Issuer + Subject
ssl.cert.subject.cn:"AsyncRAT Server" ssl.cert.issuer.cn:"AsyncRAT Server"

# Censys
same_service(services.tls.certificates.leaf_data.issuer_dn="CN=AsyncRAT Server" and services.tls.certificates.leaf_data.subject_dn="CN=AsyncRAT Server")
```

**Sliver C2:**
```bash
# Certificate + JARM
ssl.cert.issuer.cn:"operators" ssl.jarm:"3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910"
```

---

## Önemli Uyarılar

1. **JARM tek başına yeterli değil** - Mutlaka diğer göstergelerle birleştirin
2. **Korelasyon önemli** - Tek fingerprint yerine birden fazla gösterge kullanın
3. **Yasal kullanım** - Sadece yetkilendirildiğiniz sistemlerde kullanın
4. **Yanlış pozitifler** - Tüm eşleşmeler kötü amaçlı değildir; raporlamadan önce doğrulayın

**Doğruluk garantisi yoktur.** Bu sorgular her zaman gerçek veya zararlı içerik döndürmez. **Honeypot**’lara, **tehdit avcılarını avlayan aktörlerin** altyapılarına veya **meşru red team / yetkili penetrasyon testi** altyapılarına denk gelebilirsiniz. Araştırmalar, **birden fazla fingerprint’i birleştirmenin** — TLS sertifikası + JARM + HTTP header’ları + HTML içeriği — tek bir göstergeden daha güvenilir sonuçlar verdiğini göstermektedir. Bu sorguları başlangıç noktası olarak kullanın; sonuç çıkarmadan veya aksiyon almadan önce bulguları ek bağlamla doğrulayın.

---

## İstihbarat Kaynakları

### Tehdit İstihbarat Feedleri

| Kaynak | URL | API |
|--------|-----|-----|
| **ThreatFox** | https://threatfox.abuse.ch | `curl -X POST -d '{"query":"search_ioc","search_term":"IP"}' https://threatfox-api.abuse.ch/api/v1/` |
| **URLhaus** | https://urlhaus.abuse.ch | `curl https://urlhaus.abuse.ch/api/v1/url/IP/` |
| **MalwareBazaar** | https://bazaar.abuse.ch | `curl -X POST -d 'query=get_taginfo&tag=TAG' https://mb-api.abuse.ch/api/v1/` |
| **Feodo Tracker** | https://feodotracker.abuse.ch | `curl https://feodotracker.abuse.ch/blocklist/` |
| **SSL Blacklist** | https://sslbl.abuse.ch | Sertifika kara listesi |

### Tarama Platformları

| Kaynak | URL | GitHub | Kullanım |
|--------|-----|--------|----------|
| **Shodan** | [shodan.io](https://www.shodan.io) | [achillean](https://github.com/achillean) | C2 avı |
| **Censys** | [search.censys.io](https://search.censys.io) | [censys](https://github.com/censys) | TLS/Servis avı |
| **Netlas** | [netlas.io](https://netlas.io) | [netlas-io](https://github.com/netlas-io) | HTTP/TLS avı |
| **URLScan.io** | [urlscan.io](https://urlscan.io) | [urlscan](https://github.com/urlscan) | URL analizi |
| **VirusTotal** | [virustotal.com](https://www.virustotal.com) | — | Multi-AV tarama |

### IOC Kaynakları

| Kaynak | GitHub |
|--------|--------|
| **C2IntelFeeds** | [drb-ra/C2IntelFeeds](https://github.com/drb-ra/C2IntelFeeds) |
| **deepdarkCTI** | [fastfire/deepdarkCTI](https://github.com/fastfire/deepdarkCTI) |
| **Maltrail** | [stamparm/maltrail](https://github.com/stamparm/maltrail) |

---

## Detaylı Dokümantasyon

- **Shodan Query'leri:** [SHODAN_QUERIES.md](SHODAN_QUERIES.md)
- **Censys Query'leri:** [CENSYS_QUERIES.md](CENSYS_QUERIES.md)
- **Netlas Query'leri:** [NETLAS_QUERIES.md](NETLAS_QUERIES.md)
- **ClickFix Vaka İncelemesi:** [ClickFixCampaign-CaseStudies.md](ClickFixCampaign-CaseStudies.md)
- **Tool Referansları:** [TOOLS_REFERENCES.md](TOOLS_REFERENCES.md)

---

**Son Güncelleme:** 2026-02-01
