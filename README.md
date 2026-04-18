# EffortScope – Helpdesk Effort & Resource Analytics

EffortScope, customer support ticket verilerini kullanarak destek operasyonlarinda eforu, kaynak kullanimini ve musteri segmentlerini analiz eden bir veri bilimi projesidir. Proje; metin yogunlugu, oncelik seviyesi, zaman sinyalleri ve musteri bazli farkliliklar uzerinden hem analitik icgoru uretir hem de efor tahminleme yaklasimini gosterir.

## 30 Saniyede Proje

### Bu proje ne yapiyor?

- Gercek support ticket metinleri ve operasyon kolonlari uzerinden EDA, NLP, segmentasyon ve tahminleme akisi kuruyor.
- Ticket yogunlugu, complexity, priority ve segment farklarini gorunur hale getiriyor.
- Helpdesk analizi icin tekrar calistirilabilir bir notebook ornegi sunuyor.

### Bu proje ne yapmiyor?

- Gercek operasyonel `effort_hours` veya dogrulanmis `resolution_time` tahmini yapmiyor.
- Gercek musteri kimligi, gercek zaman damgasi veya gercek SLA verisi uzerinden calismiyor.
- Uretildigi haliyle production-ready bir karar motoru oldugunu iddia etmiyor.

## Sentetik Alan Uyarisi

Asagidaki alanlar ham veri setinden gelmez; notebook icinde analitik demonstrasyon amaciyla uretilir veya simule edilir:

- `effort_hours`
- `resolution_time`
- `customer_name`
- `created_at_clean`
- `created_day_of_week`
- `created_hour`
- `created_month`
- `created_month_name`
- `month_period`

## Proje Amaci

Bu proje su sorulara veri odakli cevap uretmeyi hedefler:

- Hangi ticket tipleri daha yuksek operasyonel efor gerektiriyor?
- Hangi musteri segmentleri daha fazla kaynak tuketiyor?
- Haftanin hangi gunlerinde ticket yogunlugu artiyor?
- Ticket complexity seviyesi eforu nasil etkiliyor?

## Veri Seti

Projede Kaggle uzerindeki `tobiasbueck/multilingual-customer-support-tickets` veri seti kullanilmistir.

Veri seti tipik olarak su alanlari icerir:

- `body`
- `subject`
- `answer`
- `priority`
- `type`
- `language`
- `tag_1` ... `tag_8`

Veri setinde gercek `effort_hours` bulunmadigi icin proje kapsaminda sentetik ama tutarli hedef ve destekleyici feature'lar uretilmistir. Bu nedenle proje, gercek operasyonel performans olcumunden cok analitik prototip ve demonstrasyon niteligindedir.

## Turetilen Ana Kolonlar

- `effort_hours`: Ana hedef degisken, sentetik efor modeli
- `resolution_time`: Eforla iliskili sentetik cozum suresi
- `description_length`: Ticket aciklamasinin karakter uzunlugu
- `word_count`: Ticket aciklamasindaki kelime sayisi
- `complexity_score`: Aciklama yogunlugu ve priority bazli karmasiklik skoru
- `customer_name`: Musteri bazli segmentasyon icin sentetik kurumsal etiket
- `created_day_of_week`: Ticket'in haftanin hangi gunune dustugu
- `created_hour`: Gun ici is yukunun hangi saatlerde toplandigini gosterir
- `created_month_name`: Aylik talep yogunlugu ve mevsimsellik analizi icin kullanilir
- `is_weekend`: Hafta sonu bayragi

## Notebook Kapsami

`EffortScope.ipynb` icinde su adimlar yer alir:

- KaggleHub ile otomatik veri indirme
- Kullanilan CSV'yi proje klasorune kopyalama
- Kolon esleme ve fallback mekanizmasi
- Veri temizleme ve eksik veri analizi
- Feature engineering
- NLP analizi
- EDA, musteri bazli Pareto, gun-saat heatmap, aylik trend ve is turu boxplot
- KMeans ile musteri segmentasyonu
- Regresyon modelleme ve model karsilastirma
- Feature importance, insights, oneriler ve executive summary

## Modelleme

Kullanilan modeller:

- Linear Regression
- Random Forest
- Gradient Boosting

Kullanilan metrikler:

- MAE
- RMSE
- R2

Son stabil notebook sonucuna gore en iyi model **Gradient Boosting** olmustur.

- MAE: yaklasik `0.335`
- RMSE: yaklasik `0.400`
- R2: yaklasik `0.910`

Bu performans, modelin tanimlanan sentetik efor mantigini basarili bicimde ogrendigini gosterir. Ancak `effort_hours` sentetik olarak uretildigi icin sonuclar gercek operasyonel performansin birebir temsili olarak degil, analitik demonstrasyon olarak yorumlanmalidir.

Teknik not: RMSE compatibility helper was used to support different scikit-learn versions.

## Ana Bulgular

- `complexity_score` ile `effort_hours` arasinda guclu pozitif iliski vardir.
- Uzun ve detayli aciklamalar daha yuksek efor gerektirir.
- Priority seviyesi arttikca ortalama efor da artar.
- En yuksek ticket hacmi `Wednesday` gununde gorulmustur.
- Aylik trend ve gun-saat heatmap'i, talep yogunlugunun zaman icinde dengeli dagilmadigini gosterir.
- Bazi musteri segmentleri digerlerine gore daha yuksek ortalama efor tuketmektedir.

## Oneriler

1. Complexity bazli uzman yonlendirme uygulanmali.
2. Gun bazli kapasite planlama ile yogunluk gunleri dengelenmeli.
3. Yuksek efor tuketen segmentler icin SLA ve otomasyon stratejileri gelistirilmeli.

## Proje Yapisi

- `EffortScope.ipynb`: Ana analiz notebook'u
- `DATA_DICTIONARY.md`: Ham ve turetilmis alanlar icin resmi veri sozlugu
- `REPORT.md`: Teknik ve is odakli proje raporu
- `data/raw/customer_support_tickets.csv`: Yerel veri kopyasi
- `data/reports/column_profile.csv`: Kolon ozet raporu
- `data/reports/column_profile.md`: Kolon bazli markdown aciklamalari
- `data/reports/column_profile.html`: Kolon profilinin HTML gorunumu
- `data/reports/dataset_preview.csv`: Ilk 100 satirlik veri onizlemesi
- `data/reports/column_missingness.png`: Eksik veri gorseli
- `data/reports/column_uniques.png`: Benzersiz deger sayisi gorseli
