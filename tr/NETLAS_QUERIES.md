# Netlas Hunting Query'leri

> **C2 ve Malware Avı için Kapsamlı Netlas Query Referansı**

🇬🇧 [Click for English version](../NETLAS_QUERIES.md)

[Netlas Featured Queries](https://netlas.io/resources/featured_queries/) ve [netlas-dorks GitHub repo](https://github.com/netlas-io/netlas-dorks) baz alınmıştır.

---

## 📖 İçindekiler

- [C2 Framework'leri](#-c2-frameworkleri)
- [RAT'lar](#-ratlar)
- [Phishing Araçları](#-phishing-araçları)
- [Bilgi Hırsızları](#-bilgi-hırsızları)
- [ClickFix Kampanyası](#-clickfix-phishing-kampanyası)
- [Açık Dizinler](#-açık-dizinler--payload-hosting)
- [Genel C2 Göstergeleri](#-genel-c2-göstergeleri)

---

> **Not:** Query'ler teknik olduğu için çevrilmemiştir. Detaylı query listesi için [İngilizce versiyona](../NETLAS_QUERIES.md) bakınız.

---

## C2 FRAMEWORK'LERİ

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

### Havoc C2
```
http.unknown_headers.key:"X_Havoc"
```

### Mythic C2
```
http.title:"Mythic"
certificate.subject.organization:"Mythic"
```

### Sliver C2
```
certificate.issuer.common_name:"operators"
jarm:"3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910"
```

---

## RAT'LAR

### AsyncRAT
```
certificate.subject.common_name:"AsyncRAT Server"
```

### Quasar RAT
```
certificate.subject.common_name:"Quasar Server CA"
```

### DcRAT
```
certificate.subject.common_name:"DcRat Server"
```

### XWorm
```
http.body:"XWorm"
certificate.subject.common_name:"XWorm"
```

---

## PHISHING ARAÇLARI

### GoPhish
```
http.title:"Gophish - Login"
certificate.issuer.organization:"Gophish"
http.headers.set_cookie:"gophish="
```

### EvilGinx2
```
jarm:"20d14d20d21d20d20c20d14d20d20daddf8a68a1444c74b6dbe09910a511e6"
```

---

## BİLGİ HIRSIZLARI

### Panda Stealer
```
http.title:"熊猫Stealer"
http.title:"Panda Stealer"
```

### Shadow C2
```
http.title:"Shadow C2 Panel"
http.body:"collect_telegram" AND http.body:"collect_wallets"
```

---

## CLICKFIX PHISHING KAMPANYASI

```
http.title:"Checking if you are human"
http.title:"Checking if you are human" AND http.body:"k4zrz92z"
http.body:"checkboxWindow"
certificate.issuer_dn:"CN=Let's Encrypt" AND http.title:"Checking if you are human"
```

---

## AÇIK DİZİNLER & PAYLOAD HOSTING

```
http.title:"/index of/"
http.title:"Index of" AND http.body:"sliver"
http.title:"Index of" AND http.body:"MimiKatz"
http.title:"Index of" AND http.body:".exe"
```

---

## GENEL C2 GÖSTERGELERİ

### Self-signed Sertifika Kalıpları
```
certificate.issuer.organization:"Internet Widgits Pty Ltd"
certificate.subject.common_name:"localhost"
```

### Flask/Werkzeug C2 Panelleri

> **Uyarı:** Genel kalıplar — çok FP çıkar. Diğer göstergelerle birleştirin.

```
http.headers.server:"Werkzeug" AND http.title:"Panel"
http.headers.server:"Werkzeug" AND http.body:"/api/bots"
```

---

## 📚 Netlas Syntax Hızlı Referans

| Netlas | Shodan | Censys |
|--------|--------|--------|
| `http.title` | `http.title` | `services.http.response.html_title` |
| `http.body` | `http.html` | `services.http.response.body` |
| `certificate.subject.common_name` | `ssl.cert.subject.cn` | `services.tls.certificates.leaf_data.subject.common_name` |
| `jarm` | `ssl.jarm` | `services.tls.jarm.fingerprint` |
| `http.favicon.hash_sha256` | `http.favicon.hash` | `services.http.response.favicons.sha256_hash` |

---

## 📖 Tam Query Listesi

Tüm query'lerin detaylı listesi için: [NETLAS_QUERIES.md (English)](../NETLAS_QUERIES.md)

---

## 📖 İlgili Dokümanlar

- [Ana Sayfa](README.md)
- [Shodan Query'leri](SHODAN_QUERIES.md)
- [Censys Query'leri](CENSYS_QUERIES.md)
- [ClickFix Vaka İncelemesi](ClickFixCampaign-CaseStudies.md)
- [Tool Referansları](TOOLS_REFERENCES.md)

---

## 📚 Referanslar

- [Netlas Featured Queries](https://netlas.io/resources/featured_queries/)
- [netlas-io/netlas-dorks GitHub](https://github.com/netlas-io/netlas-dorks)
- [Netlas Documentation](https://docs.netlas.io/)

---

**Son Güncelleme:** 2026-02-01
