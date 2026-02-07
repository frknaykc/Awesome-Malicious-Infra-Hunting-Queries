# Censys Hunting Query'leri

> **C2 ve Malware Avı için Kapsamlı Censys Query Referansı**

🇬🇧 [Click for English version](../CENSYS_QUERIES.md)

---

## 📖 İçindekiler

- [Phishing Framework'leri](#-gophish-phishing-framework)
- [Bilgi Hırsızları](#-panda-c2--panda-stealer)
- [C2 Framework'leri](#-cobalt-strike-cert--jarm)
- [RAT'lar](#-asyncrat)
- [Bankacılık Trojanları](#-icedid--gozi--bokbot)
- [APT Altyapısı](#-apt41-double-dragon--barium--winnti)
- [Diğer Araçlar](#-open-directory---suspicious)

---

## ⚠️ Censys Platform Sözdizimi

Bu query'ler **Censys Platform** (CenQL) sözdizimi kullanır. Censys Legacy Search'ten `host`, `cert` ve `web` dataset prefix'li yeni veri modeline geçti. Software/product tespiti için host+web kapsamlı query kullanın. Bkz: [Censys Platform Syntax Differences](https://docs.censys.com/docs/censys-platform-syntax-differences) | [Query Converter](https://docs.censys.com/docs/query-converter)

---

> **Not:** Query'ler teknik olduğu için çevrilmemiştir. Detaylı query listesi için [İngilizce versiyona](../CENSYS_QUERIES.md) bakınız.

---

## GOPHISH (Phishing Framework)

### Ürün Tespiti (host + web kapsamı)
```
host.services.software.product:"GoPhish" or host.services.hardware.product:"GoPhish" or host.services.operating_systems.product:"GoPhish" or web.software.product:"GoPhish" or web.hardware.product:"GoPhish" or web.operating_systems.product:"GoPhish"
```

### Başlık Bazlı
```
host.services.endpoints.http.html_title:"Gophish - Login"
host.services.endpoints.http.html_title:"Gophish"
web.endpoints.http.html_title:"Gophish"
```

### SSL Sertifikası
```
host.services.tls.certificates.leaf_data.issuer.organization:"Gophish"
host.services.tls.certificates.leaf_data.subject.organization:"Gophish"
```

---

## COBALT STRIKE (CERT / JARM)

```
host.services.tls.certificates.leaf_data.subject.common_name:"Major Cobalt Strike"
host.services.tls.certificates.leaf_data.serial_number:146473198
host.services.tls.jarm.fingerprint:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da"
```

---

## SLIVER C2

```
host.services.tls.certificates.leaf_data.issuer.common_name:"operators"
host.services.tls.jarm.fingerprint:"3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910"
```

---

## MYTHIC C2

```
host.services.endpoints.http.html_title:"Mythic"
host.services.tls.certificates.leaf_data.subject.organization:"Mythic"
host.services.tls.jarm.fingerprint:"1dd40d40d00040d00042d43d000000831b6af40378e2dd35eeac4e9311926e"
```

---

## HAVOC C2

```
host.services.endpoints.http.headers:"X_Havoc"
host.services.endpoints.http.body:"Havoc"
host.services.tls.certificates.leaf_data.subject.common_name:"Havoc"
```

---

## ASYNCRAT

```
host.services.tls.certificates.leaf_data.issuer_dn="CN=AsyncRAT Server"
host.services.tls.certificates.leaf_data.subject.common_name:"AsyncRAT Server"
```

---

## HAK5 CLOUD C2

```
host.services.software.product:"Hak5 Cloud C2" or host.services.hardware.product:"Hak5 Cloud C2" or host.services.operating_systems.product:"Hak5 Cloud C2" or web.software.product:"Hak5 Cloud C2" or web.hardware.product:"Hak5 Cloud C2" or web.operating_systems.product:"Hak5 Cloud C2"
host.services.endpoints.http.html_title:"Hak5 Cloud C"
```

---

## CLICKFIX PHISHING

```
host.services.endpoints.http.html_title:"Checking if you are human" AND host.services.endpoints.http.body:"k4zrz92z"
host.services.endpoints.http.html_title:"Checking if you are human" AND host.services.endpoints.http.body:"Ctrl"
host.services.endpoints.http.body:"checkboxWindow"
```

---

## EVILGOPHISH (Phishing Framework)

```
host.services.software.product:"Evilginx" or host.services.hardware.product:"Evilginx" or host.services.operating_systems.product:"Evilginx" or web.software.product:"Evilginx" or web.hardware.product:"Evilginx" or web.operating_systems.product:"Evilginx" or host.services.software.product:"EvilGoPhish" or host.services.hardware.product:"EvilGoPhish" or host.services.operating_systems.product:"EvilGoPhish" or web.software.product:"EvilGoPhish" or web.hardware.product:"EvilGoPhish" or web.operating_systems.product:"EvilGoPhish"
```

---

## 📖 Tam Query Listesi

Tüm query'lerin detaylı listesi için: [CENSYS_QUERIES.md (English)](../CENSYS_QUERIES.md)

---

## 📖 İlgili Dokümanlar

- [Ana Sayfa](README.md)
- [Shodan Query'leri](SHODAN_QUERIES.md)
- [Netlas Query'leri](NETLAS_QUERIES.md)
- [ClickFix Vaka İncelemesi](ClickFixCampaign-CaseStudies.md)
- [Tool Referansları](TOOLS_REFERENCES.md)
- [Censys Platform Sözdizimi](https://docs.censys.com/docs/censys-platform-syntax-differences) | [Query Converter](https://docs.censys.com/docs/query-converter)

---

**Son Güncelleme:** 2026-02-01
