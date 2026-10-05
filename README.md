# Sprung

Türkçe konuşanlar için 30 günlük yoğun Almanca başlangıç programı. Telefona kurulan, internetsiz de çalışan kişisel bir web uygulaması (PWA).

Program "30 günde akıcılık" iddiası taşımaz. Amaç, 30 gün içinde mevcut seviyeden mümkün olan en yüksek pratik iletişim seviyesine çıkmak ve sonrasında sürecek bir çalışma düzeni kurmaktır.

## Yaklaşım

Yöntem, yoğun diplomatik dil eğitiminden (ör. FSI) çıkarılabilen genel ilkelerle modern dil öğrenme araştırmalarının ortak noktalarına dayanır:

- **Görev odaklı öğrenme:** Her gün gerçek bir iletişim görevi etrafında kurulur: tanışma, sipariş, yol sorma, randevu.
- **Kalıplarla kelime:** Kelimeler tek başına değil, cümle içinde öğrenilir.
- **Aktif hatırlama:** Cevap gösterilmeden önce Türkçeden Almancaya kendin üretirsin.
- **Aralıklı tekrar:** Kalıplar 1, 3, 7, 14 ve 30 gün aralıklarla geri gelir.
- **Shadowing:** Konuşmacıyı yarım saniye geriden, aynı ritim ve tonlamayla sesli takip edersin.
- **Geç düzeltme:** Önce cevabını tamamlarsın; fark sonra kelime kelime gösterilir ve hata defterine yazılır.

Ortada "gizli istihbarat yöntemi" yok. Kullanılan ilkeler belgelenmiş ve bilinen ilkeler.

## Günlük oturum (yaklaşık 60 dakika)

| Blok | 1. gün | 2. gün ve sonrası |
|---|---|---|
| Seviye testi | 20 dk | – |
| Tekrar | – | 10 dk |
| Yeni kalıplar ve aynı gün hatırlama | 20 dk | 15 dk |
| Dinleme ve shadowing | 15 dk | 20 dk |
| Üretim (çeviri ve kişisel sorular) | – | 10 dk |
| Gramer (örneklerle) | – | 5 dk |
| Gün 0 ses kaydı | 5 dk | – |

1. günde tekrar bloğu yok, çünkü henüz tekrar edilecek bir şey yok. Seviye testinde bilinemeyen kalıplar 2. günün tekrar destesine eklenir.

Program günü, oturum bitirildikçe ilerler; atlanan bir takvim günü içerik kaçırmana yol açmaz. Tekrar zamanları ise takvime göre hesaplanır.

## Fazlar

| Günler | Faz | Odak |
|---|---|---|
| 1–7 | Temel | Tanışma, aile, günlük rutin, kafe, alışveriş, yol, randevu |
| 8–14 | Günlük hayat | Rol yapma ağırlıklı senaryolar |
| 15–21 | Spontane | Ezber dışı anlatım |
| 22–30 | Gerçek hayat | Simülasyonlar ve 30. gün değerlendirmesi |

Uygulamada 1–7. günlerin içeriği hazır. Sonraki haftalar, performansa göre hazırlanan içerik paketleriyle eklenir. İlerleme ekranı sonraki faza hazır olup olmadığını gösterir. Bunun için kartların en az %80'inin en az bir kez tutulmuş, son 3 günün doğruluğunun da en az %75 olması gerekir.

## Kurulum

1. Repodaki dosyaları GitHub Pages ile yayınla: **Settings > Pages > Deploy from a branch > main / (root)**.
2. Yayınlanan adresi iPhone'da Safari ile aç, **Paylaş > Ana Ekrana Ekle**'ye dokun.
3. Uygulamayı ana ekrandan aç ve **Ayarlar**'da *Sesi test et* ile *Mikrofonu test et*'e bas.

Almanca ses yoksa iPhone'da **Ayarlar > Erişilebilirlik > Seslendirilen İçerik > Sesler** bölümünden Almanca bir ses indir.

Sesli cevap vermek için iPhone'a Almanca klavye ekle: **Ayarlar > Genel > Klavye > Klavyeler**. Ardından cevap kutusunda Almanca klavyeye geçip dikte tuşunu kullan.

Menü adları iOS sürümüne göre değişebilir.

## Haftalık döngü: içerik paketleri

1. **Ayarlar > Haftalık dökümü kopyala**'ya bas. Doğruluk oranları, en sık hatalar, en çok unutulan kartlar ve serbest cevaplar panoya kopyalanır.
2. Dökümü bir dil modeline, örneğin Claude'a yapıştır. Döküm, sonraki haftanın paketini hangi şemayla isteyeceğini de içerir.
3. Gelen JSON'u **Ayarlar > İçerik paketi** alanına yapıştır ve *Paketi ekle*'ye bas.

Paket şeması:

```json
{
  "version": 1,
  "days": [
    {
      "day": 8,
      "title": "Türkçe başlık",
      "titleDe": "Almanca başlık",
      "task": "Günün görevi",
      "grammar": { "title": "…", "points": ["…"], "examples": [{ "de": "…", "tr": "…" }] },
      "chunks": [{ "id": "d8-01", "de": "…", "tr": "…", "alt": ["kabul edilen diğer doğru cevaplar"] }],
      "dialogue": { "title": "…", "speakers": { "A": "…", "B": "…" }, "lines": [{ "s": "A", "de": "…", "tr": "…" }] },
      "produce": [{ "id": "d8-p1", "tr": "…", "de": "…", "alt": [] }],
      "questions": [{ "id": "d8-q1", "q": "…", "tr": "…", "model": "…" }]
    }
  ]
}
```

Zorunlu alanlar şunlar: `day`, `title`, `task`, `chunks` (her birinde `id`, `de`, `tr`) ve `dialogue.lines` (her birinde `de`). Aynı gün numarasıyla eklenen paket, öncekinin yerine geçer.

## Veri ve gizlilik

- İlerleme, kartlar, hatalar ve cevaplar yalnızca cihazdaki tarayıcı hafızasında (localStorage) tutulur. Ses kayıtları IndexedDB'de durur.
- Hiçbir veri sunucuya gönderilmez. Analitik ya da takip yok.
- **Ayarlar > Yedeği kopyala** ile ilerlemeni metin olarak alıp bir yere kaydedebilirsin. Ses kayıtları yedeğe dahil değil.
- Safari site verilerini temizlemek ya da uygulamayı ana ekrandan silmek ilerlemeyi silebilir. Bunları yapmadan önce yedek al.
- Uygulama kodu ve ders içeriği bu repoda herkese açık. Örnek cümlelerde kurgusal bir karakter kullanılıyor.

## Dosyalar

| Dosya | Görevi |
|---|---|
| `index.html` | Uygulamanın tamamı: arayüz, mantık ve 1. hafta içeriği |
| `sw.js` | Çevrimdışı çalışma için service worker (önce ağ, sonra önbellek) |
| `manifest.webmanifest` | Ana ekran uygulaması tanımı |
| `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` | İkonlar |

Derleme adımı ya da dış bağımlılık yok. Güncellemek için yeni `index.html`'i yüklemek yeterli. Service worker önce ağa baktığı için yeni sürüm, internete bağlıyken bir sonraki açılışta gelir.

## Bilinen sınırlar

- Telaffuz otomatik ölçülmez. Kayıtlarını modelle karşılaştırmak ve dikte ipucu yalnızca kaba bir geri bildirim verir.
- Dinleme sentetik sesle yapılır. Doğal konuşma melodisi için gerçek kayıtlarla desteklemek gerekir.
- Serbest cevaplar uygulama içinde düzeltilmez; düzeltme haftalık dökümle gelir.
- Almanca içerik yapay zekâyla yazıldı ve anadil kontrolünden geçmedi.
- Ses sentezi ve kayıt, cihaza ve tarayıcıya bağlıdır. iPhone'da ana ekran modunda ilk kullanımda test edilmeli.
