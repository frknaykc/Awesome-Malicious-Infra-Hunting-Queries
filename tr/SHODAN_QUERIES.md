# Shodan Hunting Query'leri

> **C2 ve Malware Avı için Kapsamlı Shodan Query Referansı**

🇬🇧 [Click for English version](../SHODAN_QUERIES.md)

---

## 📖 İçindekiler

- [Phishing Framework'leri](#-gophish-phishing-framework)
- [Bilgi Hırsızları](#-panda-c2--panda-stealer)
- [C2 Framework'leri](#-cobalt-strike)
- [RAT'lar](#-asyncrat--quasar--orcus--dcrat)
- [Bankacılık Trojanları](#-icedid--gozi--bokbot)
- [Fidye Yazılımları](#-ransomhub-c2)
- [APT Altyapısı](#-apt41-double-dragon--barium--winnti)
- [Diğer Araçlar](#-open-directory--payload-hosting)

---

> **Not:** Query'ler teknik olduğu için çevrilmemiştir. Detaylı query listesi için [İngilizce versiyona](../SHODAN_QUERIES.md) bakınız.

---

## GOPHISH (Phishing Framework)

### Ürün Tespiti
```
product:"GoPhish"
```

### Başlık Bazlı
```
http.title:"Gophish - Login"
http.title:"Gophish"
```

### Favicon Hash (%98 - EN ETKİLİ)
```
http.favicon.hash:803527991
```

### SSL Sertifikası
```
ssl.cert.issuer.O:"Gophish"
ssl.cert.subject.O:"Gophish"
```

### Kombine Yüksek Güven
```
http.favicon.hash:803527991 http.title:"Gophish"
product:"GoPhish" "gophish="
```

---

## COBALT STRIKE

### Varsayılan Sertifika
```
ssl.cert.serial:"146473198"
ssl.cert.subject.cn:"Major Cobalt Strike"
ssl.cert.issuer.cn:"Major Cobalt Strike"
```

### JARM Fingerprint'leri
```
ssl.jarm:"07d14d16d21d21d00042d43d000000aa99ce74e2c6d013c745aa52b5cc042d"
ssl.jarm:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da"
```

---

## MYTHIC C2

```
http.title:"Mythic"
ssl.cert.subject.o:"Mythic"
ssl.jarm:"1dd40d40d00040d00042d43d000000831b6af40378e2dd35eeac4e9311926e"
```

---

## SLIVER C2

```
ssl.cert.issuer.cn:"operators"
ssl.jarm:3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910
```

---

## HAVOC C2

```
http.headers.unknown:"X_Havoc"
http.html:"Havoc"
ssl.cert.subject.cn:"Havoc"
```

---

## ASYNCRAT / QUASAR / ORCUS / DCRAT

```
ssl.cert.subject.cn:"AsyncRAT Server"
ssl.cert.subject.cn:"Quasar Server CA"
ssl.cert.subject.cn:"Orcus Server"
ssl.cert.subject.cn:"DcRat Server"
```

---

## HAK5 CLOUD C2

### Favicon Hash (%100 - EN ETKİLİ!)
```
http.favicon.hash:1294130019
```

### Ürün Tespiti
```
product:"Hak5 Cloud C2"
```

---

## CLICKFIX PHISHING

```
http.title:"Checking if you are human" http.html:"k4zrz92z"
http.title:"Checking if you are human" http.html:"Ctrl"
http.html:"checkboxWindow"
```

---

## 📖 Tam Query Listesi

Tüm query'lerin detaylı listesi için: [SHODAN_QUERIES.md (English)](../SHODAN_QUERIES.md)

---

## 📖 İlgili Dokümanlar

- [Ana Sayfa](README.md)
- [Censys Query'leri](CENSYS_QUERIES.md)
- [Netlas Query'leri](NETLAS_QUERIES.md)
- [ClickFix Vaka İncelemesi](ClickFixCampaign-CaseStudies.md)
- [Tool Referansları](TOOLS_REFERENCES.md)

---

**Son Güncelleme:** 2026-02-01
