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
| Günlük harcama | Tavanı olan, gün gün girilen | Nakit olanı çıkarır |
| Kart | Limit, borç, taksitler | Sadece o döngüde ödenen kısmı çıkarır |

**Biriken bölümü iki sütunludur:** solda kalan borç, sağda bu döngüde ödenecek tutar. Sağ sütunu boş bırakırsan satır "2. döngü", "3. döngü" diye saymaya başlar ve uyarı çıkar. Ertelenen kalemin kaç aydır ertelendiğini görmek bunun tek amacı.

**Tavan nakit ve kart olarak ikiye bölünür.** Harcama bölümünün altındaki tablodan ikisini ayrı girersin; toplam ikisinin toplamıdır. Kart satırı yalnızca bir kart eklenmişse görünür.

Belirleyici olan toplamdır. Nakit payını aşıp kart payından artırdıysan toplam hâlâ tutuyorsa uyarı çıkmaz — ilgili satır sarıya döner, o kadar. Kırmızı uyarı yalnızca toplam tavan aşılınca gelir, iki taraf birbirinden ödünç alabilir.

**Üstteki büyük rakam** kalan günler için günlük harcama limiti: kalan toplam tavan ÷ kalan gün, ödeme yöntemi fark etmeksizin. Harcadıkça aşağı iner, harcamadığın gün yukarı çıkar. Toplam tavan aşılırsa eksiye düşer ve kırmızıya döner. Altındaki satır nakit ve kart paylarının ayrı ayrı nerede olduğunu gösterir.

Bilinçli olarak "planın önünde/gerisindesin" gibi bir tempo göstergesi yok. Öyle bir oran ancak döngünün ilk gününden itibaren her harcama kaydedilirse doğru olur; bir gün atlandığında program bunu "harcamadı" sayar ve yanıltır.

**Kart ayrı bir havuzdur.** Hem günlük harcamalarda hem sabit giderlerde nakit mi kartla mı ödediğini seçersin. Kartla ödenen şey o ayın nakdinden düşmez — kartın limitinden düşer ve bir sonraki döngünün "bu ay ödenecek" satırına geçer. Alt özette iki rakam durur: *Kalan (nakit)* ve *karta binen*.

Sabit gider satırlarındaki seçim ancak bir kart eklenmişse görünür. Karta bağlanan sabit gider her döngüde kartı yeniden yükler — faturan karttan otomatik ödeniyorsa gerçekte de böyle olur. O satırın tutarı bölüm toplamından çıkar, parantezin altında *+6.000 kartta* diye ayrı gösterilir.

Kart bölümü iki parçadır. Üstte **limit**: büyük rakam şu an harcayabileceğin tutar, altında dönem başı boşta olan ve bu dönem harcanan. Altta **ödeme**: bu ay ödenecek, ödedim, gelecek ay ödenecek, sonraki aylara kalan.

Üç alanı sen girersin, yanlarında `sen gir` etiketi vardır: kartın toplam limiti, dönem başında bankada boşta görünen tutar, ve ekstrendeki ödenecek tutar. Boşta rakamını girmen gerekir çünkü uygulama senin ondan önceki borcunu bilemez. Geri kalan satırlar hesaplanır: karta binen her şey boştadan düşer, ödeme yaptıkça geri açılır, hesaplanan değer bir sonraki döngüye devreder. Banka ile uyuşmazsa alanı elle düzeltirsin.

`ödedim` tek istisnadır: oraya yazdığın tutar nakit Kalan'dan düşer, çünkü kart borcunu nakitle ödersin.

Harcama bölümünün başlığında bir **varsayılan** seçimi var. Çoğu şeyi kartla alıyorsan oraya kartı koyarsın; her girişte tek tek seçmen gerekmez. Tek seferlik istisnada form üstünden nakde çevirirsin, ekledikten sonra kendi varsayılanına döner.

Taksitli alışverişte taksit sayısını girersin. O döngüye bir taksit biner, kalanı sonraki döngülere otomatik dağılır. Limitte ise tutarın tamamı bloke görünür — bankalar da böyle yapar.

Asgari ödeme tutarı bilinçli olarak yok. Asgari ödemek kalan bakiyeye faiz işletir ve borcu büyütür; ekranda hedef gibi durmasını istemedim.

**Yeni döngü öncekinden devralır.** Sabit kalemler, girişler, tavan, kart ayarları ve ödenmemiş biriken bakiyeler otomatik taşınır; günlük harcama listesi sıfırlanır. Arada kullanmadığın aylar olduysa devir en son kullandığın döngüyü bulur (12 aya kadar geriye bakar).

Devir **kopyalamadır**: aylar birbirinden bağımsızdır, birinde yaptığın değişiklik diğerini etkilemez. Tek istisna kart ve biriken borçlardır; onlar zincirleme devam eder.

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
const CACHE = "dongu-v9";
```

satırındaki sürüm numarası bir artırılmalı (`dongu-v8`, sonra `v9`…). Yoksa cihazlar eski sürümü göstermeye devam eder.
