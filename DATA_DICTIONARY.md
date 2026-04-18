# Data Dictionary

**Proje:** Yardim Masasi Efor ve Kaynak Kullanimi Veri Analitigi  
**Proje Kodu:** PRJIC20260203  
**Kaynak Veri Dosyasi:** `data/raw/customer_support_tickets.csv`  
**Toplam Ham Satir Sayisi:** `28,587`  
**Sozluk Kapsami:** Ham veri alanlari ve notebook icinde uretilen analitik alanlar

## Amac

Bu dokuman, projede kullanilan veri alanlarinin ne ifade ettigini, hangi tipte tutuldugunu ve analizde nasil kullanildigini resmi bir teslim artefakti olarak aciklar.

Alanlar iki ana gruba ayrilmistir:

- `Raw`: Kaynak veri setinden dogrudan gelen alanlar
- `Generated`: Notebook icinde feature engineering ile uretilen alanlar

## Sentetik Alanlarin Ozeti

Bu projede en kritik nokta sudur: butun `Generated` alanlar ayni seviyede degildir. Bazilari ham veriden dogrudan turetilmis yardimci ozelliklerdir, bazilari ise sentetik veya simule edilmis alanlardir.

### Ham veriden turetilen ama sentetik olmayan alanlar

- `description_length`
- `word_count`
- `complexity_score`
- `is_weekend`

### Sentetik veya simule edilen alanlar

- `effort_hours`
- `resolution_time`
- `customer_name`
- `created_at_clean`
- `created_day_of_week`
- `created_hour`
- `created_month`
- `created_month_name`
- `month_period`

Bu ikinci grup, gercek operasyon verisi olmadigi icin notebook icinde analitik demonstrasyon amaciyla uretilmistir. Bu alanlara dayanan bulgular, gercek KPI olcumu degil prototip yorum olarak okunmalidir.

## Alanlar

Bu bolum daha rahat okunabilsin diye gruplandirilmis durumda. Once ham veri alanlari, sonra notebook icinde uretilen alanlar verilir.

### Hizli Ozet

| Grup | Icerik | Ne Ise Yarar? |
| --- | --- | --- |
| Metin alanlari | `subject`, `body`, `answer` | Talep icerigini anlamak, NLP yapmak |
| Operasyon alanlari | `type`, `queue`, `priority`, `language`, `version` | Is akisini, onceligi ve segmentleri incelemek |
| Etiket alanlari | `tag_1` ... `tag_8` | Teknik konu ve alt kategorileri okumak |
| Turetilmis alanlar | `description_length` ... `resolution_time` | Efor, zaman, segmentasyon ve modelleme yapmak |

### 1. Ham Metin Alanlari

| Alan | Tip | Ne Anlama Gelir? | Ornek | Analizde Kullanim |
| --- | --- | --- | --- | --- |
| `subject` | `str` | Musteri talebinin kisa basligi | `Account Disruption` | Baslik bazli NLP, konu yorumu, karmasiklik sinyali |
| `body` | `str` | Talebin detayli aciklama metni | Serbest metin | `word_count`, `description_length`, `complexity_score`, WordCloud |
| `answer` | `str` | Destek ekibinin verdigi yanit metni | Serbest metin | Yardimci metin analizi, cevap yapisi inceleme |

### 2. Ham Operasyon Alanlari

| Alan | Tip | Ne Anlama Gelir? | Ornek | Analizde Kullanim |
| --- | --- | --- | --- | --- |
| `type` | `str` | Ticket veya is kaydinin tipi | `Incident`, `Request`, `Problem`, `Change` | Is turu bazli dagilim, boxplot, kok neden analizi |
| `queue` | `str` | Talebin yonlendirildigi destek kuyrugu | `Technical Support` | Operasyonel segmentasyon, teknik alan bazli yorum |
| `priority` | `str` | Talebin oncelik seviyesi | `low`, `medium`, `high` | Efor iliskisi, boxplot, tahminleme modeli |
| `language` | `str` | Talebin dili | `en`, `de` | Dil bazli dagilim ve segmentasyon |
| `version` | `int64` | Veri setindeki surum veya kayit varyanti | `51`, `52`, `400` | Yardimci sayisal profil, korelasyon, modelleme |

### 3. Ham Etiket Alanlari

Bu alanlar ticket'in teknik veya konu bazli alt siniflarini gosterir. `tag_1` en dolu ve en kullanisli etiket alanidir. `tag_5` sonrasinda eksik oranlari belirgin bicimde artar.

| Alan | Tip | Ne Anlama Gelir? | Ornek | Not |
| --- | --- | --- | --- | --- |
| `tag_1` | `str` | Birincil etiket | `Security`, `Account` | En guclu konu sinyali |
| `tag_2` | `str` | Ikincil etiket | `Outage`, `Feature` | Konu zenginlestirme icin yararli |
| `tag_3` | `str` | Ucuncul etiket | `Disruption`, `Feedback` | Teknik alan gruplamada yardimci |
| `tag_4` | `str` | Dorduncul etiket | `Data Breach`, `IT` | Derin kategori bilgisi verir |
| `tag_5` | `str` | Besincil etiket | `Compatibility`, `Automation` | Ileri analiz icin yararli, eksik orani yuksek |
| `tag_6` | `str` | Altinci etiket | `Microservice`, `IT` | Eksik orani cok yuksek |
| `tag_7` | `str` | Yedinci etiket | `Workflow`, `Connection` | Sinirli kullanim |
| `tag_8` | `str` | Sekizinci etiket | `Maintenance`, `Healthcare` | Sinirli kullanim |

### 4. Notebook Icinde Uretilen Analitik Alanlar

Bu alanlar ham veri setinde yoktur. Analiz, gorsellestirme ve modelleme amaciyla notebook icinde uretilmistir.

| Alan | Tip | Durum | Nasil Uretildi? | Ornek | Analizde Kullanim |
| --- | --- | --- | --- | --- | --- |
| `description_length` | `int64` | Turetilmis | `body` metninin karakter sayisi alinarak | `751` | Metin yogunlugu, complexity sinyali |
| `word_count` | `int64` | Turetilmis | `body` icindeki kelime sayisi hesaplanarak | `82` | Efor modeli, NLP yorumlari |
| `complexity_score` | `float64` | Turetilmis | Metin uzunlugu, kelime sayisi ve `priority` birlestirilerek | `1.506` | Korelasyon, efor analizi, modelleme |
| `created_at_clean` | `datetime64` | Simule / Sentetik | Tarih kolonundan temizlenerek veya simule edilerek | `2025-02-02 13:00:00` | Tum zaman bazli analizlerin temeli |
| `created_day_of_week` | `str` | Simule / Sentetik | `created_at_clean` uzerinden gun adi turetilerek | `Wednesday` | Gun bazli yogunluk, kapasite planlama |
| `created_hour` | `int64` | Simule / Sentetik | `created_at_clean` uzerinden saat bilgisi alinarak | `13` | Gun-saat heatmap, vardiya yorumu |
| `created_month` | `int64` | Simule / Sentetik | `created_at_clean` uzerinden ay numarasi alinarak | `2` | Aylik trend ve mevsimsellik |
| `created_month_name` | `category` | Simule / Sentetik | Ay numarasinin ay ismine cevrilmesiyle | `Feb` | Aylik grafikler ve mevsimsellik yorumu |
| `month_period` | `str` | Simule / Sentetik | Tarihin `YYYY-MM` formatina cevrilmesiyle | `2025-02` | Aylik toplulasma ve raporlama |
| `is_weekend` | `int64` | Turetilmis / Kismen simule | Gun bilgisinden hafta sonu olup olmadigi belirlenerek | `0`, `1` | Hafta ici / hafta sonu karsilastirmasi |
| `customer_name` | `str` | Sentetik | Segmentasyon icin sentetik musteri etiketi atanarak | `ZenithCare` | Musteri bazli Pareto, clustering |
| `effort_hours` | `float64` | Sentetik | Metin yogunlugu + priority + kontrollu noise ile | `6.54` | Ana hedef degisken, Pareto, boxplot, regresyon |
| `resolution_time` | `float64` | Sentetik | `effort_hours` ile iliskili ikinci sentetik metrik olarak | `8.35` | Operasyonel sure yorumu, modelleme |

## Kritik Notlar

- `effort_hours` ve `resolution_time` alanlari ham veri setinden gelmez; notebook icinde analitik demonstrasyon amaciyla uretilir.
- `customer_name` gercek musteri adi degildir; segmentasyon ve Pareto analizi icin sentetik olarak atanir.
- `created_at_clean`, `created_hour`, `created_month`, `created_month_name` ve `month_period` alanlari zaman serisi ve yogunluk analizini desteklemek icin temizlenmis veya simule edilmis zaman bilgisinden uretilir.
- `tag_5` ile `tag_8` arasindaki alanlarda eksik oranlari yuksektir; bu nedenle ileri seviye kategori analizlerinde dikkatli yorumlanmalidir.

## Veri Kalitesi Ozeti

| Baslik | Durum |
| --- | --- |
| Tekrarlayan kayitlar | Notebook icinde temizlenir |
| Eksik veriler | Kolon bazinda incelenir; kritik alanlarda doldurma / normalize etme uygulanir |
| Aykiri degerler | Sayisal turetilmis alanlarda IQR clipping uygulanir |
| Kategorik standardizasyon | `priority` alaninda ortak etiketlere normalize etme yapilir |
| Birim birligi | Efor ve cozum suresi saat bazli yorumlanir |

## Teslim Notu

Bu dosya, proje baslangic kriterlerinde belirtilen "veri setindeki degiskenlerin neyi ifade ettigine dair Data Dictionary hazirlanmasi" maddesini karsilamak uzere olusturulmustur.
