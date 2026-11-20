# n8n ERP Otomasyonları

Bir üretim firmasının ERP'si etrafında kurulmuş, 15'ten fazla canlı iş akışından oluşan otomasyon platformu. Bildirimler ve onaylar konu bazlı Telegram gruplarından yönetilir. Yorumlama ve soru-cevap işleri yerel LLM (Ollama) ile yapılır.

> Bu depo bir proje vitrinidir. Kaynak kod ve iş akışları paylaşılmamaktadır.

## Otomasyonlar

| Kod | Otomasyon |
|---|---|
| OTM01 | Satış belgesinde varsayılan dışı varyant veya pasif malzeme seçilince uyarı. Kurallar web yönetim sayfasından düzenlenir. |
| OTM02 | Haftalık satış özeti ve LLM yorumu |
| OTM03 | Haftalık üretim planı önerisi: açık siparişler ile stok karşılaştırması, Excel çıktısı |
| OTM04 | Son kullanma tarihi yaklaşan veya geçmiş stok uyarısı (lot bazında, alıcı önerili) |
| OTM05 | **ERP asistanı:** Telegram'da `/sor` ile doğal dilde soru. LLM araç seçer, güvenli SQL çalıştırılır. |
| OTM06 | Mesai dışında güvenlik kamerası hareket bildirimi (fotoğraflı) |
| OTM07 | Tablodan Excel'e aktarım ve düzenlenen Excel'den **onaylı** ERP güncellemesi |
| OTM08 | Üretim personeli takip Excel'i (değişiklik olduğunda güncellenir) |
| OTM09 | Ürün Takip Sistemi (ÜTS) künye, etiket ve belgelerini otomatik indirme |
| OTM10 | Minimum stok için ürün ağacının tüm seviyelerinde bileşen ihtiyacı hesabı |
| OTM11 | Gelen e-fatura ve e-irsaliyeleri ERP web servisiyle alma ve bildirim |
| OTM12 | Sanal POS tahsilat bildirimi ve **ERP'ye otomatik tahsilat fişi.** Cari eşleşme hafızadan, yoksa yapay zekâ önerisi ve Telegram onay düğmesiyle yapılır. |
| OTM13 | Müşteri anketi yanıt bildirimi (advers olaylar öne çıkarılır) |
| OTM14 | ÜTS bildirim hatalarını izleme |
| OTM15 | İhale saat takibi ve fiyatsız kalem kontrolü |
| OTM17 | Mesai içinde iş emrine giriş yapmayan personel uyarısı |
| OTM18 | Vadesi geçmiş alacak arama listesi (FIFO). Düğmelerle görüşme sonucu girilir, gün sonu özeti gönderilir. |

## Mimari ilkeler

- **Salt okunur replika:** Raporlar ana veritabanını değil, okuma replikasını kullanır.
- **Ayrı otomasyon veritabanı:** Kural, log ve durum tabloları `otmNN_` önekiyle ayrı tutulur.
- **Adlandırma standardı:** Klasör, workflow ve tablo adları aynı `OTMnn` koduyla eşleşir.
- **Yardımcı mikro servisler:** Telegram relay, kamera relay, Excel aktarıcı, ÜTS indirici, ERP SOAP istemcisi.
- **İnsan onayı:** ERP'ye yazan akışlar Telegram'daki onay düğmeleriyle ilerler.

## Teknolojiler

`n8n` · `JavaScript` · `Python` · `PostgreSQL` · `Telegram Bot API` · `Ollama (yerel LLM)` · `SOAP` · `Docker`
