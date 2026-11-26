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

`=~` kullanan regex sorguları Censys Starter veya enterprise planı gerektirir. Belgelenmiş alan yolu tek başına tehdit atfını veya güncel arama sonuçlarını doğrulamaz.

---

> **Not:** Query'ler teknik olduğu için çevrilmemiştir. Detaylı query listesi için [İngilizce versiyona](../CENSYS_QUERIES.md) bakınız.

---

## GOPHISH (Phishing Framework)

Tekil göstergeler **düşük güvenli adaylardır**; her satırı ayrı sorgulayın. Birleşik sorgular **henüz doğrulanmamış adaylardır**, yüksek güvenli tespit olarak değerlendirilmemelidir. Tespit seviyesini yükseltmeden önce Gophish ile ilişkilerini doğrulayın.

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
host.services.cert.parsed.issuer.organization:"Gophish"
host.services.cert.parsed.subject.organization:"Gophish"
```

### Cookie Bazlı
```
host.services.endpoints.http.headers:(key="Set-Cookie" and value:"gophish=")
host.services.endpoints.http.headers:(key="Set-Cookie" and value:"_gorilla_csrf=")
```

### HTML İçeriği
```
host.services.endpoints.http.body:"/css/dist/gophish.css"
host.services.endpoints.http.body:"Open-Source Phishing Toolkit"
web.endpoints.http.body:"gophish.css"
```

### Favicon Fingerprint'i
```
host.services.endpoints.http.favicons.hash_sha256="6f383235d8dec5350c1233c04b035b116bbbd2b287c13deb298a123dc5e49d03"
```

### Port Bazlı (Varsayılan: 3333)
```
host.services:(port=3333 and endpoints.http.html_title:"Gophish")
```

### JARM Fingerprint'leri
```
host.services.jarm.fingerprint="28d28d28d00028d00041d28d28d41dd279b0cf765af27fa62e66d7c8281124"
host.services.jarm.fingerprint="2ad2ad0002ad2ad00041d2ad2ad41dc347a1c956987fa29fb299da896c61ea"
```

### Birleşik Adaylar (Henüz Doğrulanmadı)
```
host.services:(endpoints.http.html_title:"Gophish" and cert.parsed.issuer.organization:"Gophish")
host.services:(endpoints.http.body:"gophish.css" and endpoints.http.html_title:"Gophish")
host.services:(endpoints.http.favicons.hash_sha256="6f383235d8dec5350c1233c04b035b116bbbd2b287c13deb298a123dc5e49d03" and endpoints.http.body:"/css/dist/gophish.css")
host.services:(endpoints.http.favicons.hash_sha256="6f383235d8dec5350c1233c04b035b116bbbd2b287c13deb298a123dc5e49d03" and cert.parsed.issuer.organization:"Gophish")
```

---

## COBALT STRIKE (CERT / JARM)

```
host.services.cert.parsed.subject.common_name:"Major Cobalt Strike"
host.services.cert.parsed.serial_number="146473198"
host.services.jarm.fingerprint:"2ad2ad16d2ad2ad00042d42d00042ddb04deffa1705e2edc44cae1ed24a4da"
```

---

## SLIVER C2

```
host.services.cert.parsed.issuer.common_name:"operators"
host.services.jarm.fingerprint:"3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910"
```

---

## MYTHIC C2

### Başlık
```
host.services.endpoints.http.html_title:"Mythic"
```

### Port + Başlık (aynı servis)
```
host.services:(port=7443 and endpoints.http.html_title:"Mythic")
```

### Sertifika
```
host.services.cert.parsed.subject.organization:"Mythic"
host.services.cert.parsed.issuer.organization:"Mythic"
```

### Favicon Fingerprint'i
```
host.services.endpoints.http.favicons.hash_sha256:"3cbf2084fe1733debe21f33511754191ed8f46268d1a8a122a29cccfc7c969f2"
```

> **Not:** Bu favicon gözlenen Mythic kurulumlarıyla güçlü biçimde ilişkili olsa da yalnızca Mythic'e özgü değildir. Daha güvenilir tespit için başka Mythic göstergeleriyle birleştirin.

### Aynı Serviste Birleşik Sorgular
```
host.services:(endpoints.http.html_title:"Mythic" and cert.parsed.subject.organization:"Mythic")
host.services:(endpoints.http.favicons.hash_sha256:"3cbf2084fe1733debe21f33511754191ed8f46268d1a8a122a29cccfc7c969f2" and endpoints.http.html_title:"Mythic")
host.services:(port=7443 and endpoints.http.html_title:"Mythic" and cert.parsed.subject.organization:"Mythic")
```

### JARM Fingerprint'leri
```
host.services.jarm.fingerprint:"1dd40d40d00040d00042d43d000000831b6af40378e2dd35eeac4e9311926e"
host.services.jarm.fingerprint:"27d40d40d00040d00042d43d000000d2e61cae37a985f75ecafb81b33ca523"
```

### Laravel/Inertia Tabanlı Paneller
```
host.services:(endpoints.http.html_title:"C2 Panel" and endpoints.http.headers:(key="Set-Cookie" and value:"c2backend_session"))
host.services.endpoints.http.body:"<title inertia>C2 Panel</title>"
```

---

## HAVOC C2

```
host.services.endpoints.http.headers:"X_Havoc"
host.services.endpoints.http.body:"Havoc"
host.services.cert.parsed.subject.common_name:"Havoc"
```

---

## ASYNCRAT

```
host.services.cert.parsed.issuer_dn="CN=AsyncRAT Server"
host.services.cert.parsed.subject.common_name:"AsyncRAT Server"
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

**Son Güncelleme:** 2026-09-30
