# Para Döngüsü

Maaş gününden maaş gününe çalışan kişisel bütçe takibi. Tek sayfa, kurulum yok, sunucu yok, hesap yok. Bütün veriler tarayıcının kendi deposunda durur.

Kağıt üzerinde tutulan aylık bütçe defterinin dijital karşılığı: aynı blok yapısı, aynı ara toplamlar, üstüne günlük harcama takibi ve devreden borç sayacı.

## Ne yapar

**Döngü ayın 1'inde değil, seçtiğin günde başlar.** Maaşın ayın 7'sinde yatıyorsa döngü 7'sinde açılır, ertesi ayın 6'sında kapanır. Ayarlar'dan 1–28 arası herhangi bir gün seçilebilir.

**Bölümler serbest.** Dört tip var, istediğin kadarını istediğin adla ekleyebilirsin:

| Tip | Ne için | Toplama etkisi |
|---|---|---|
| Giriş | Maaş, ek gelir | Ekler |
| Sabit gider | Kira, kredi, fatura | Çıkarır |
| Biriken | Devreden borç, ertelenen ödeme | Çıkarır (sadece o ay ayrılan kısım) |
| Günlük harcama | Tavanı olan, gün gün girilen | Çıkarır |

**Biriken bölümü iki sütunludur:** solda kalan borç, sağda bu döngüde ödenecek tutar. Sağ sütunu boş bırakırsan satır "2. döngü", "3. döngü" diye saymaya başlar ve uyarı çıkar. Ertelenen kalemin kaç aydır ertelendiğini görmek bunun tek amacı.

**Üstteki büyük rakam** kalan günler için günlük harcama limiti. Çubuktaki dikey çizgi bugün olman gereken yeri gösterir; çubuk çizgiyi geçtiyse plandan öndesin, renk sarıya döner. Ay sonunu beklemeden görürsün.

**Yeni döngü öncekinden devralır.** Sabit kalemler ve ödenmemiş biriken bakiyeler otomatik taşınır, günlük harcama listesi sıfırlanır.

## Dil

Arayüz Türkçe ve İngilizce. Ayarlar → Dil → TR / EN. Seçim kaydedilir, uygulama o dille açılır.

Dil değişimi sadece arayüz metinlerini etkiler. Senin yazdığın bölüm adları ve kalem etiketleri (Maaş, Kredi, Ceza…) senin verindir, olduğu gibi kalır — istersen elle değiştirirsin. Sayı biçimi dile uyar: Türkçede `45.000`, İngilizcede `45,000`.

## Kurulum

Dosyaları bir GitHub Pages reposuna yükle, Settings → Pages → Deploy from a branch → main / root.

- **iPhone:** Safari'de adresi aç → Paylaş → Ana Ekrana Ekle. Tam ekran açılır, çevrimdışı çalışır.
- **Bilgisayar:** Chrome/Edge'de adres çubuğundaki yükle ikonu. Kendi penceresinde açılır.

## Veri

Veriler `localStorage`'da, sadece o cihazda. Sunucuya hiçbir şey gitmez, bu repoda hiçbir rakam yoktur.

Bunun iki sonucu var:

1. **Telefon ve bilgisayar ayrı veri tutar.** Aktarmak için Ayarlar → "Yedeği indir" / "Yedeği yükle".
2. **Tarayıcı verisi temizlenirse kayıt gider.** Ayda bir yedek almak yeterli.

## Dosyalar

| Dosya | Görevi |
|---|---|
| `index.html` | Uygulamanın tamamı — HTML, CSS, JS, ikonlar tek dosyada |
| `sw.js` | Service worker; çevrimdışı çalışmayı sağlar |
| `manifest.webmanifest` | Uygulama adı, ikon, tam ekran ayarı |
| `icon-512.png` | Ana ekran ikonu |

Bağımlılık yok, derleme adımı yok. `index.html` doğrudan tarayıcıda açılır.

## Güncelleme

`index.html` değiştirildiğinde `sw.js` içindeki

```js
const CACHE = "dongu-v1";
```

satırındaki sürüm numarası artırılmalı (`dongu-v2`). Yoksa cihazlar eski sürümü göstermeye devam eder.
