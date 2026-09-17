# Serra Bilişim — Kurumsal Web Sitesi

Saf HTML/CSS/JS ile yapılmış, ürün odaklı kurumsal site. Framework yok, build adımı yok.
Yayında: https://serrabilisim.com

## Dosyalar
- `index.html` — ana sayfa (ürünler, hizmetler, hakkımızda, iletişim)
- `urunler/<slug>/index.html` — her ürünün kendi detay sayfası (aşağıda)
- `hizmetler/<slug>/index.html` — hizmet detay sayfaları (aşağıda)
- `gizlilik.html` — KVKK aydınlatma metni ve çerez politikası (`noindex`)
- `styles.css` — tasarım, açık/koyu tema ve ürün arayüz mockup'ları
- `script.js` — tema geçişi, mobil menü, reveal animasyonları, metrik sayaçları
- `robots.txt` — tüm botlara açık, sitemap'i işaret eder
- `sitemap.xml` — ana sayfa + 6 ürün + 3 hizmet sayfası
- `llms.txt` — yapay zekâ araçları için site özeti (ürün/hizmet listesi ve linkleri)
- `assets/og/<slug>.png` — her sayfanın 1200×630 paylaşım görseli (`og:image`)
- `assets/logo.png` — 512×512 logo (JSON-LD `Organization.logo`)
- `google*.html` — Google Search Console doğrulama dosyası (silme)
- `CNAME` — özel alan adı (serrabilisim.com)
- `.nojekyll` — GitHub Pages'in Jekyll işlemesini atlaması için

## Ürünler

Her ürün **iki yerde** yaşıyor:

1. **Ana sayfa kartı** — `index.html` içindeki `<div class="products">` altında
   bir `<article class="pcard">`. Kısa tanıtım.
2. **Detay sayfası** — `urunler/<slug>/index.html`. Google'da o ürünün anahtar
   kelimesiyle sıralanan sayfa budur; içeriği ana sayfa kartıyla birebir aynıdır.

Sıra ve slug'lar:

| Ürün | Slug | Vurgu rengi |
|---|---|---|
| Panora (öne çıkan, `pcard--feature`) | `panora` | `#06b6d4` |
| Serra Bordro | `serra-bordro` | `#0f766e` |
| Serra Banka | `serra-banka` | `#2563eb` |
| Serra Üretim | `serra-uretim` | `#d97706` |
| SAWBot | `sawbot` | `#16a34a` |
| Serra e-Dönüşüm | `serra-e-donusum` | `#7c3aed` |

### Yeni ürün eklemek

Beş adımın **hepsini** yap, yoksa sayfa Google'da görünmez:

1. `index.html` içinde mevcut bir `pcard`'ı kopyala, şunları değiştir:
   - `style="--p:#RENK"` — ürünün vurgu rengi (tüm mockup öğeleri bunu kullanır)
   - `pcard--rev` sınıfı — görselin sağa mı sola mı geleceğini belirler (sırayla ekle)
   - `pcard__kicker`, `h3`, `p`, `pcard__feats` ve `tags` içeriği
   - `pcard__visual` içindeki mockup
   - alttaki `pcard__cta` linkini yeni slug'a çevir
2. `urunler/<yeni-slug>/index.html` — mevcut bir ürün sayfasını kopyala ve
   güncelle: `<title>`, `meta description`, `link rel="canonical"`, Open Graph
   etiketleri, JSON-LD (`SoftwareApplication` + `BreadcrumbList`), breadcrumb,
   `<h1>`, kart içeriği ve "Diğer ürünler" ızgarası.
   Yollar `../../` ile köke çıkar (`../../styles.css`, `../../script.js`).
3. Diğer 6 ürün sayfasındaki "Diğer ürünler" ızgarasına yeni ürünü ekle.
4. `index.html` footer'ındaki **Ürünler** sütununa link ekle
   (aynı sütun her ürün sayfasının footer'ında da var — hepsini güncelle).
5. `sitemap.xml`'e yeni URL'yi ekle, ana sayfadaki JSON-LD `ItemList`'ine de.

Yayına girdikten sonra Search Console → URL Inspection → **Request indexing**.

**Görseller:** ürün ekranları şu an CSS/SVG ile çizilmiş mockup'lar
(`.mock`, `.phone`, `.kpis`, `.bars`, `.gantt`, `.rows`, `.chips` vb.).
Gerçek ekran görüntüsü koymak istersen `pcard__visual` içeriğini
`<img src="assets/urun.png" alt="..." />` ile değiştirmen yeterli.

## Hizmet sayfaları

| Hizmet | URL |
|---|---|
| SAP Business One danışmanlığı | `/hizmetler/sap-business-one-danismanlik/` |
| SAP Business One add-on geliştirme | `/hizmetler/sap-business-one-add-on-gelistirme/` |
| SAP Business One entegrasyonu | `/hizmetler/sap-business-one-entegrasyon/` |

Her hizmet sayfasında kapsam kartları, süreç adımları, açıklama metni, SSS
(`<details>`) ve ilgili ürünler var. JSON-LD: `Service` + `BreadcrumbList` +
`FAQPage`. Ana sayfadaki hizmet kartlarındaki "Detaylı bilgi →" linkleri ve tüm
sayfaların footer'ındaki **Hizmetler** sütunu bu sayfalara gider.

Yeni hizmet sayfası eklerken: sayfayı kopyala, `sitemap.xml`'e, `llms.txt`'ye,
tüm footer'lara ve ana sayfa JSON-LD'sindeki `hasOfferCatalog`'a ekle.

## SSS
Ana sayfada `#sss` bölümü var. Soru eklerken hem görünen `<details>` bloğunu hem
de `<head>` içindeki `FAQPage` JSON-LD'sini güncelle; ikisi birebir aynı olmalı.

## SEO notları
- Kanonik alan adı **www'suz**: `https://serrabilisim.com`. `www` buraya 301
  yönleniyor. Tüm `canonical` ve `sitemap.xml` URL'leri www'suz yazılır.
- Her sayfanın kendine ait `<title>`, `meta description`, `canonical` ve tek bir
  `<h1>`'i olmalı.
- Ana sayfada `Organization` (logo, kurucu, iletişim, hizmet kataloğu) +
  `WebSite` + `ItemList` + `FAQPage`, ürün sayfalarında `SoftwareApplication` +
  `BreadcrumbList`, hizmet sayfalarında `Service` + `BreadcrumbList` + `FAQPage`
  JSON-LD'si var.
  Değiştirdikten sonra https://search.google.com/test/rich-results ile kontrol et.
- Her sayfanın `og:image` ve `twitter:image` etiketi `assets/og/<slug>.png`
  görseline bakar (ana sayfa: `home.png`). Yeni sayfa eklersen görselini de ekle.
- Dahili linkler kökten başlar (`/`, `/#urunler`, `/hizmetler/...`); `index.html`
  yazma.

## Yerelde açmak
Linkler kökten (`/`) başladığı için siteyi küçük bir sunucuyla aç:

```
python -m http.server 8000
```

Sonra tarayıcıda http://localhost:8000 adresine git.

## Yayınlama (GitHub Pages)
Depo **public** olmalı, site kaynağı deponun kökü.

Depo → **Settings → Pages → Build and deployment → Source: Deploy from a branch**
→ Branch: `main`, klasör: `/ (root)` → **Save**.

Her `git push` sonrası site birkaç dakika içinde güncellenir.
