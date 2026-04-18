# Notebook Presentation Notes

Bu dokuman, [EffortScope.ipynb](C:/Users/Kadir/Desktop/EffortScope/EffortScope.ipynb) icindeki 20 baslik icin kisa sunum metinleri icerir. Her baslik altinda 4 cumlelik, akici ve sunumda dogrudan kullanilabilecek bir anlatim hazirlanmistir. Metinler "bu adimda ne yapildi, neden yapildi ve ne sonuc verdi" mantigiyla yazilmistir. Istenirse bu yapi daha sonra slayt notu veya konusma metnine donusturulebilir.

## 1. Project Overview

Bu adimda projenin genel amaci ve kapsami tanimlandi. Yardim masasi ticket verileri uzerinden efor, kaynak kullanimi, segmentasyon ve tahminleme calismasi yapilacagi netlestirildi. Veri setinde gercek efor bilgisi olmadigi icin analiz boyunca kullanilacak sentetik ama tutarli bir efor mantigi kurgulandi. Boylece notebook'un geri kalan tum adimlari icin ortak bir cerceve olusturulmus oldu.

## 2. How to Use

Bu bolum notebook'un nasil calistirilacagini anlatiyor. Hucrelerin yukaridan asagiya sirayla calistirilmasi yeterli olacak sekilde akis tasarlandi. Veri setinin manuel olarak yuklenmesine gerek kalmadan KaggleHub uzerinden otomatik indirme mantigi kuruldu. Bu sayede projeyi farkli ortamda acan biri de ayni akisi daha sorunsuz tekrar edebilir.

## 3. Data Loading

Bu adimda veri seti projeye cekildi ve uygun CSV dosyasi otomatik olarak bulundu. Yerel klasore kopyalanan veri uzerinden tekrarlanabilir bir calisma ortami hazirlandi. Boylece kullanilan kaynagin sabit kalmasi ve analizlerin ayni dosya uzerinden ilerlemesi saglandi. Veri yukleme asamasi tamamlandiktan sonra tum sonraki analizler ayni temel tablo uzerinde yapildi.

## 4. Column Mapping Guide

Bu bolumde veri setindeki kolon isimleri otomatik olarak yorumlandi ve anlamli alanlara eslendi. Farkli veri setlerinde isimlendirme degisebilecegi icin esnek bir fallback mantigi kuruldu. Ozellikle aciklama, oncelik, dil ve tarih gibi kritik kolonlar otomatik tespit edildi. Bu adim notebook'u daha dayanikli ve tekrar kullanilabilir hale getirdi.

## 5. Data Cleaning

Bu adimda ham veri daha temiz ve analiz edilebilir hale getirildi. Tekrarlayan kayitlar silindi, bos metinler duzenlendi ve oncelik alanlari ortak etiketlere normalize edildi. Bazi kategorik alanlarda eksik degerler kontrollu bicimde dolduruldu. Boylece veri daha tutarli hale geldi ve sonraki adimlarda hata riski azaltildi.

## 6. Missing Values

Bu bolumde eksik verilerin hangi kolonlarda ve ne oranda bulundugu incelendi. Ozellikle ust seviye tag alanlarinda belirgin eksiklikler oldugu goruldu. Eksik degerlerin dagilimi gorsel olarak da desteklenerek daha net hale getirildi. Bu analiz sayesinde hangi alanlarin guclu, hangilerinin sinirli yorum verecegi anlasildi.

## 7. Outlier Handling

Bu adimda aykiri degerler dogrudan silinmedi, bunun yerine kontrollu bicimde kirpildi. IQR yontemi kullanilarak asiri uc degerlerin analizi bozmasi engellendi. Bu yaklasim veri kaybini azaltirken dagilimin daha dengeli kalmasina yardimci oldu. Ozellikle turetilmis sayisal alanlarda daha saglikli grafik ve model sonucu alinmasi hedeflendi.

## 8. Feature Engineering

Bu bolum projenin en kritik adimlarindan biri oldu cunku yeni analitik alanlar burada uretildi. Metin yogunlugu, zaman bilgisi, musteri segmenti ve sentetik efor mantigi bu asamada kuruldu. `description_length`, `word_count`, `complexity_score`, `created_hour` ve `effort_hours` gibi alanlar analizin omurgasini olusturdu. Boylece ham veri, is etkisi yorumlanabilecek daha anlamli bir veri yapisina donusturuldu.

## 9. NLP Analysis

Bu adimda ticket metinlerinden en sik gecen kelimeler cikartildi ve WordCloud ile gorsellestirildi. Boylece destek taleplerinin hangi konu etrafinda yogunlastigi daha gorunur hale geldi. Metin analizi ayni zamanda complexity yorumunu destekleyen yardimci bir katman sagladi. Bu kisim ileri seviye NLP degil ama proje icin anlamli bir giris seviyesi metin madenciligi ornegi sundu.

## 10. EDA

Bu bolumde verinin genel profili tanimlayici istatistiklerle ve temel grafiklerle incelendi. Efor dagilimi ve oncelik dagilimi gibi temel desenler burada goruldu. Hangi kategorilerin daha sik geldigi ve eforun nasil bir yapida dagildigi daha net hale geldi. Bu adim sonraki ozel analizlerin hangi yone gitmesi gerektigine dair ilk resmi verdi.

## 11. Pareto Analysis

Bu adimda toplam eforun musteriler arasinda nasil dagildigi Pareto mantigi ile incelendi. Amac, toplam kaynagin buyuk kisminin az sayida musteri uzerinde toplanip toplanmadigini gormekti. Grafik sonucunda bazi musteri gruplarinin toplam efor icinde daha baskin paya sahip oldugu goruldu. Bu bulgu kaynak planlama ve musteri bazli SLA degerlendirmesi icin onemli bir temel sagladi.

## 12. Workload Heatmap and Seasonality

Bu bolumde is yukunun hem gun hem de saat bazinda nasil toplandigi heatmap ile gosterildi. Ayni zamanda aylik ticket hacmi incelenerek mevsimsellik benzeri trendler izlendi. Boylece talep yogunlugunun zamana esit dagilmadigi daha net ortaya kondu. Bu adim operasyonel kapasite planlama icin dogrudan kullanilabilecek bir gorus sagladi.

## 13. Boxplot by Work Type

Bu adimda is turu veya kuyruk bazinda efor dagilimi kutu grafikleri ile incelendi. Hangi kategorilerde ortanca eforun yuksek oldugu ve hangi alanlarda aykiri degerlerin arttigi goruldu. Bu, bazi is tiplerinin digerlerine gore daha degisken veya daha maliyetli oldugunu gostermeye yardimci oldu. Boylece kok neden analizi tarafinda daha somut bir kategori bazli bakis elde edildi.

## 14. Clustering

Bu bolumde musteri bazli segmentasyon yapmak icin KMeans algoritmasi kullanildi. Musteriler ortalama efor, cozum suresi, complexity ve ticket hacmi gibi degiskenlerle gruplandirildi. Sonucta bazi segmentlerin sistematik olarak daha yuksek destek maliyeti olusturdugu goruldu. Bu adim, tum musterilere ayni operasyonel yaklasimin uygun olmayabilecegini gosterdi.

## 15. Regression Modeling

Bu adimda sentetik `effort_hours` hedef degiskeni tahmin edilmeye calisildi. Veri egitim ve test olarak ayrildi, kategorik alanlarda One-Hot Encoding uygulandi ve modelleme akisi pipeline yapisina alindi. Boylece daha profesyonel ve tekrar edilebilir bir tahminleme akisi kurulmus oldu. Bu kisim projenin makine ogrenmesi boyutunu olusturdu.

## 16. Model Comparison

Bu bolumde farkli regresyon modelleri ayni veri uzerinde karsilastirildi. MAE, RMSE ve R2 gibi metriklerle hangi modelin daha iyi performans verdigi olculdu. Modellerin sonuclari yan yana gosterilerek karar sureci daha seffaf hale getirildi. Boylece sadece model kurmakla kalinmadi, en uygun model secimi de veriyle desteklenmis oldu.

## 17. Feature Importance

Bu adimda en iyi modelin hangi degiskenlere daha fazla agirlik verdigi incelendi. Ozellikle complexity, metin yogunlugu ve zaman sinyallerinin efor uzerindeki etkisi daha somut goruldu. Bu analiz modelin neden o sonucu verdigini yorumlamayi kolaylastirdi. Boylece proje sadece tahmin yapan degil, aciklanabilir bir yapiya da yaklasti.

## 18. Insights

Bu bolumde teknik analiz sonuclari is diliyle yorumlandi. En yogun gunler, en maliyetli kategoriler, en fazla efor tuketen musteriler ve en guclu iliskiler burada bir araya getirildi. Bulgular sadece grafik olarak birakilmadi, yonetsel anlam tasiyacak sekilde yazili hale getirildi. Bu kisim projenin karar destek degerini en net gosteren bolumlerden biri oldu.

## 19. Recommendations

Bu adimda analiz bulgulari dogrudan aksiyon onerilerine donusturuldu. Complexity bazli uzman yonlendirme, gun-saat bazli kapasite planlama ve yuksek eforlu segmentlere ozel SLA tasarimi on plana cikarildi. Her onerinin arkasina veriyle desteklenen bir gozlem baglandi. Boylece notebook sadece analiz yapan degil, iyilestirme onerisi sunan bir is cikti haline geldi.

## 20. Executive Summary

Bu bolum tum calismanin kisa bir yonetici ozeti olarak tasarlandi. Projenin amaci, veri kaynagi, ana bulgulari ve en onemli operasyonel etkileri burada tek yerde toplandi. Teknik detaylari bilmeyen bir yonetici bile bu ozet ile projenin ne kazandirdigini hizlica anlayabilir. Sunumun kapanisinda kullanmak icin en uygun bolumlerden biri de burasi oldu.

