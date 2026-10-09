# FastPDF — PDF araçları, tarayıcında 📄⚡

Birleştir, böl, döndür, filigran ekle, düzenle. **Tüm işlemler tarayıcında** — dosyaların cihazından asla çıkmaz.

Açık kaynak · ücretsiz · kurulum yok · zayıf bilgisayarlar için optimize · offline çalışır.

## Kullanım

`index.html` dosyasını tarayıcında aç — hepsi bu. (Tek dosyalık uygulama: fontlar, kütüphaneler gömülü; `js/` klasöründeki lazy modüller otomatik yüklenir.)

## Araçlar (16 — hepsi yayında)

**Düzenle**
- **Birleştir** — birden fazla PDF'i sıralı şekilde tek dosyada birleştir
- **Böl** — tüm sayfaları ayır ya da aralıklarla böl (1-3, 5, 8-10)
- **Döndür** — sayfaları 90°/180°/270° çevir (tümü veya seçili)
- **Sayfa Sil** — istenmeyen sayfaları aralıklarla sil (1-3, 5)
- **Sayfa Düzenle** — sayfaları yeniden sırala / çoğalt / ters çevir
- **Boş Sayfa Ekle** — A4 boş sayfaları istediğin yere ekle
- **Sayfa Numarası** — alt orta/sağ, üst orta konumlu numaralama

**Dönüştür**
- **Görsel → PDF** — JPG/PNG/WebP'yi sıralı şekilde PDF yap (EXIF temizlemeli)
- **Metin → PDF** — TXT ve Markdown'ı Türkçe karakter destekli PDF yap
- **PDF → Metin** — metin katmanını .txt olarak çıkar (pdf.js, lazy)
- **PDF → Görsel** — sayfaları JPG/PNG yap, ZIP'le toplu indir (pdf.js, lazy)
- **HTML → PDF** — yapıştırılan HTML'i tarayıcının yazdırma motoruyla PDF yap

**Güvenlik & İmza**
- **Filigran** — her sayfaya çapraz metin filigranı (saydamlık ayarlı)
- **İmza** — çizim tahtası veya görsel yükleme ile imza yerleştirme
- **PDF Bilgi** — sayfa sayısı, boyut ve tüm meta verileri gör
- **Meta Düzenle** — başlık, yazar, konu, anahtar kelime değiştir + tam temizleme

## Gizlilik (ürünün kalbi)

- **Ağ erişimi tarayıcıda kilitli:** CSP politikası (`connect-src 'self' blob:`) tüm dış bağlantıları engeller — uygulama istese bile veri gönderemez.
- **Dosyalar yalnız RAM'de:** diske hiçbir şey yazılmaz; sekme kapanınca kaybolur. "Tüm verileri sil" butonu anında temizler.
- **Meta/EXIF temizleme:** Görsel→PDF'te fotoğraf konum (GPS) bilgileri varsayılan olarak temizlenir; "Meta Düzenle"de tüm meta verileri sıfırlama butonu vardır.
- **Analytics yok, çerez yok, izleme yok:** her şey dosyanın içinde; tek depolanan şey tema tercihi.
- **Kendin kanıtla:** DevTools → Ağ sekmesini aç, işlem yap — sıfır istek görürsün.

## Mimari Notu

- **Çekirdek tek dosya** (`index.html`, ~1 MB): tüm hafif araçlar + fontlar + pdf-lib + JSZip gömülü — offline çalışır
- **Lazy motorlar** (`js/`): pdf.js + worker + html2canvas yalnızca ilgili araç açılınca yüklenir — zayıf bilgisayarda ilk yükleme hızı korunur
- **Gizlilik kilidi:** CSP meta etiketi dış ağ erişimini engeller

## GitHub Pages'te Yayınlama

1. Repoyu GitHub'a push et (public).
2. **Settings → Pages** → _Deploy from a branch_ → `main` / `(root)` → Save.
3. `js/` klasörü otomatik servis edilir — ek ayar gerekmez.

## Geliştirme

Kaynak kod, build script ve testler `fastpdf-dev/` klasöründe ayrıca tutulur (bu repo'da değil):

```
fastpdf-dev/src/           → HTML şablon + app.js (kaynak)
fastpdf-dev/src/build.py   → index.html üretici
fastpdf-dev/vendor/        → pdf-lib, jszip (MIT)
fastpdf-dev/test/          → jsdom + Chromium testleri
fastpdf-dev/skills/        → tasarım prensipleri (bencium, MIT)
```

Build + test:

```bash
cd fastpdf-dev
npm install jsdom puppeteer   # bir kez
python3 src/build.py          # ../fastpdf/index.html üretir
node test/smoke.js            # çekirdek işlemler
node test/browser-e2e.js      # gerçek Chromium: 16 aracın uçtan uca testi
```

## Lisans

[MIT](LICENSE) — © 2026 Berke Hazar

pdf-lib (MIT) · JSZip (MIT) · pdf.js (Apache-2.0) · html2canvas (MIT) · Inter & Syne fontları (SIL OFL 1.1)
