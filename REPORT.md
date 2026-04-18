# EffortScope ? Helpdesk Effort & Resource Analytics

EffortScope, customer support ticket verilerini kullanarak destek operasyonlarinda eforu gorunur hale getirmeyi amaclayan bir analiz projesidir. Proje; ticket hacmi, icerik karmasikligi, musteri segmentleri ve oncelik seviyesi gibi sinyalleri bir araya getirerek hem analitik icgoru uretir hem de efor tahminleme yaklasimini gosterir.

Bu proje ozellikle su problemi hedefler: destek ekipleri cogu zaman hangi ticket turlerinin daha maliyetli oldugunu, hangi musteri segmentlerinin daha fazla kaynak tukettigini ve hangi donemlerde kapasite baskisi olustugunu sistematik bicimde goremez. EffortScope bu gorunurlugu saglayarak kaynak planlama, SLA yonetimi ve surec iyilestirme kararlarini veriyle destekler.

## Kullanilan Veri Seti

Projede Kaggle uzerindeki `tobiasbueck/multilingual-customer-support-tickets` veri seti kullanilmistir. Veri seti cok dilli musteri destek ticket'lari icerir ve tipik olarak su bilgileri barindirir:

- ticket aciklama metni (`body`)
- konu basligi (`subject`)
- yanit metni (`answer`)
- oncelik (`priority`)
- ticket tipi (`type`)
- dil (`language`)
- etiket alanlari (`tag_1` ... `tag_8`)

Veri setinin kritik siniri, gercek `effort_hours` veya dogrulanmis cozum suresi icermemesidir. Bu nedenle projede analitik gosterim amaciyla sentetik fakat tutarli hedef degiskenler turetilmistir.

## Feature Engineering

### `effort_hours`
- Ana hedef degiskendir.
- Ticket aciklamasindaki kelime sayisi, priority agirligi ve kontrollu rastgele gurultu ile uretilmistir.
- Destek operasyonundaki is yukunu temsil eden sentetik ama yorumlanabilir bir hedef sunar.

### `resolution_time`
- `effort_hours` ile iliskili ikinci operasyonel gostergedir.
- Ticket cozum suresi benzeri bir cikti ureterek zaman boyutunu gorunur kilar.

### `description_length`
- Aciklama metninin karakter uzunlugunu olcer.
- Daha uzun ticket'larin daha fazla inceleme gerektirebilecegini gosteren temel sinyaldir.

### `word_count`
- Aciklama metnindeki kelime sayisini olcer.
- Ticket yogunlugunu sayisal hale getirir ve sentetik efor olusumunda dogrudan etkilidir.

### `complexity_score`
- `description_length`, `word_count` ve priority bilgisinden turetilmistir.
- Ticket karmasikligini tek bir skorda toplar.

### `customer_name`
- Veri setinde gercek musteri adi olmadigi icin sentetik kurumsal musteri etiketi uretilmistir.
- Musteri bazli segmentasyon ve kaynak tuketim farklarini okumayi saglar.

### `created_day_of_week`
- Tarih bilgisinden veya kontrollu simulasyondan uretilmistir.
- Talebin haftanin hangi gunlerinde yogunlastigini gosterir.

### `created_hour`
- Ticket'in gun icindeki acilis saatini gosterir.
- Gun-saat yogunluk heatmap'i ve vardiya planlama yorumlari icin kullanilir.

### `created_month_name`
- Tarih bilgisinden turetilen aylik kategoridir.
- Mevsimsellik ve aylik talep trendi analizinde kullanilir.

### `is_weekend`
- Ticket'in hafta sonu acilip acilmadigini belirten ikili degiskendir.
- Hafta ici ve hafta sonu yuklerini karsilastirmaya yardimci olur.

## Analiz

### Eksik Veri Analizi
Kolon profili, ust seviye tag alanlarinda belirgin eksiklik oldugunu gostermektedir. En dikkat cekici eksikler `tag_8` (%98.02), `tag_7` (%92.86), `tag_6` (%79.45) ve `tag_5` (%49.12) kolonlarinda gorulmustur. Bu durum ileri seviye etiketleme disiplininin tum kayitlarda korunmadigini gosterir.

### Musteri Bazli Efor Dagilimi
En yuksek ortalama efor tuketen musteriler arasinda `PeakLogistics`, `AtlasWorks` ve `ZenithCare` yer almaktadir. KMeans segmentasyonu da bazi musteri kumelerinin sistematik olarak daha yuksek ortalama efor uretebildigini gostermistir.

### Complexity vs Effort Iliskisi
`complexity_score` ile `effort_hours` arasindaki korelasyon `0.8574` seviyesindedir. Bu guclu pozitif iliski, ticket karmasikligi arttikca operasyonel eforun da anlamli sekilde arttigini gosterir.

### Yogunluk Gunleri
Haftalik dagilimda en yuksek ticket hacmi `Wednesday` gununde gorulmustur (`4,175` ticket). Hafta sonu ortalama eforu ile hafta ici ortalama efor birbirine cok yakindir; bu da hacim dagilimi farkli olsa bile birim ticket zorlugunun buyuk fark gostermedigini dusundurur.

### Mevsimsellik ve Gun-Saat Yogunlugu
Notebook'a eklenen gun-saat heatmap'i, destek talebinin sadece gun bazinda degil saat bazinda da belirli bloklarda toplandigini gorunur hale getirmektedir. Aylik trend grafigi ise yil icinde bazi aylarin digerlerine gore daha yuksek ticket hacmi uretebildigini gostererek mevsimsellik yorumunu guclendirir.

### Is Turu Bazli Dagilim
Is turu veya kuyruk bazli boxplot analizi, bazi kategorilerde ortanca eforun daha yuksek oldugunu ve dagilimin daha genis oldugunu gostermektedir. Bu durum, belirli is tiplerinin daha degisken operasyonel maliyet urettigine isaret eder.

### Segmentasyon (KMeans)
`KMeans (n_clusters=4)` ile yapilan musteri segmentasyonu, ortalama efor, ortalama cozum suresi, complexity, ticket sayisi ve hafta sonu orani gibi degiskenler uzerinden yapilmistir. Sonuclar, bazi segmentlerin digerlerine gore daha pahali destek profili tasidigini gosterir.

## Modelleme

Projede uc farkli regresyon yaklasimi denenmistir:

- Linear Regression
- Random Forest
- Gradient Boosting

Kullanilan performans metrikleri:

- **MAE**: Ortalama mutlak hata
- **RMSE**: Buyuk hatalara daha duyarli kok ortalama kare hata
- **R2**: Hedef degisken varyansinin ne kadar aciklandigi

Son stabil notebook ciktilarina gore en iyi model **Gradient Boosting** olmustur:

- MAE: `0.335`
- RMSE: `0.400`
- R2: `0.910`

Gradient Boosting'in one cikmasinin nedeni, dogrusal olmayan iliskileri ve feature etkilesimlerini daha iyi yakalayabilmesidir. Linear Regression ve Random Forest da rekabetci sonuclar vermistir; bu da uretilen hedef yapisinin hem dogrusal hem de etkile?imli sinyaller tasidigini gosterir.

Model teknik olarak guvenilir gorunse de kritik yorum aynidir: `effort_hours` sentetik olarak uretilmistir. Bu nedenle model, gercek operasyonun birebir tahmin motoru olarak degil, analitik yaklasimin uygulanabilirligini gosteren bir demonstrasyon olarak degerlendirilmelidir.

Teknik not: RMSE compatibility helper was used to support different scikit-learn versions.

## Bulgular

- Uzun ve detayli aciklamaya sahip ticket'lar daha yuksek efor gerektirir.
- `complexity_score` ile `effort_hours` arasinda guclu pozitif iliski vardir.
- Priority seviyesi yukselince ortalama efor artar.
- Ticket hacmi haftanin belirli gunlerinde yogunlasir; en yuksek hacim `Wednesday` gunundedir.
- Musteri bazli Pareto analizi, toplam eforun bazi musteri gruplarinda yogunlastigini gosterir.
- Gun-saat heatmap'i ve aylik trend grafigi, zaman bazli kapasite planlamanin gerekli oldugunu destekler.
- Bazi musteri segmentleri digerlerine gore daha yuksek ortalama efor ureterek orantisiz kaynak tuketir.
- Ust seviye tag alanlarindaki eksiklik, ileri kategorik raporlamayi sinirlandirmaktadir.

## Oneri 1 ? Complexity Bazli Uzman Yonlendirme
- Problem: Karmasik ticket'lar standart akista gereksiz zaman kaybina neden olabilir.
- Veriyle gozlem: `complexity_score` ile `effort_hours` arasinda guclu iliski vardir.
- Cozum: Complexity esigi asan ticket'lar ilk asamada uzman ekip veya ikinci seviye kuyruga yonlendirilmelidir.
- Etki: Cozum suresi kisalir, tekrar islem orani duser.

## Oneri 2 ? Gun Bazli Kapasite Planlama
- Problem: Ticket hacmi haftaya esit dagilmamaktadir.
- Veriyle gozlem: En yuksek hacim `Wednesday` gununde gorulmustur; gun-saat heatmap'i de belirli zaman bloklarinda yogunlasma oldugunu gostermektedir.
- Cozum: Vardiya ve back-up kapasite planlari gun ve saat bazli hacim desenine gore optimize edilmelidir.
- Etki: Backlog birikimi ve SLA sapmasi riski azalir.

## Oneri 3 ? Yuksek Eforlu Segmentler Icin SLA Gozden Gecirme
- Problem: Tum musteri segmentleri operasyon uzerinde ayni yuku olusturmamaktadir.
- Veriyle gozlem: Bazi segmentler sistematik olarak daha yuksek ortalama efor uretmektedir.
- Cozum: Yuksek efor tuketen segmentler icin SLA, self-service icerikleri ve surec otomasyonu birlikte yeniden tasarlanmalidir.
- Etki: Destek maliyeti daha ongorulebilir hale gelir.

## Executive Summary

EffortScope, musteri destek operasyonlarini efor ve kaynak kullanimi acisindan gorunur kilmak icin gelistirilmis bir analiz projesidir. Kaggle tabanli cok dilli ticket verisi uzerinde metin yogunlugu, priority, musteri segmenti ve zaman sinyalleri kullanilarak sentetik bir efor modeli kurulmustur.

Ana bulgular sunlardir:

- complexity arttikca effort belirgin bicimde artmaktadir
- bazi musteri segmentleri daha yuksek kaynak tuketmektedir
- ticket hacmi haftanin belirli gunlerinde ve belirli saat bloklarinda yogunlasmaktadir
- aylik trend analizi mevsimsellik yorumunu desteklemektedir
- en iyi model Gradient Boosting olmustur

Is etkisi acisindan proje; kapasite planlama, uzman yonlendirme ve segment bazli SLA tasarimi icin daha guclu bir analitik temel sunmaktadir. Ancak hedef degisken sentetik oldugu icin sonuclar, gercek operasyonel performans vaadi olarak degil karar destek ve analitik prototip olarak degerlendirilmelidir.
