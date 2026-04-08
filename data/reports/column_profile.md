# Column Profile Report

- Toplam satir sayisi: **28,587**
- Toplam kolon sayisi: **25**
- Kaynak CSV: **C:/Users/Kadir/Desktop/EffortScope/data/raw/customer_support_tickets.csv**

## language
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 2
- Ornek degerler: de | en
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## priority
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 3
- Ornek degerler: high | medium | low
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## queue
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 10
- Ornek degerler: Technical Support | Returns and Exchanges | Billing and Payments | Sales and Pre-Sales | Service Outages and Maintenance
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## tag_1
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 116
- Ornek degerler: Security | Account | Product | Billing | Feature
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## tag_2
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 13 adet (%0.05)
- Benzersiz deger: 256
- Ornek degerler: Outage | Disruption | Feature | Payment | Product
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## tag_3
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 136 adet (%0.48)
- Benzersiz deger: 392
- Ornek degerler: Disruption | Outage | Tech Support | Account | Feedback
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## tag_4
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 3058 adet (%10.7)
- Benzersiz deger: 554
- Ornek degerler: Data Breach | IT | Documentation | Tech Support | Feedback
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## tag_5
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 14042 adet (%49.12)
- Benzersiz deger: 602
- Ornek degerler: Tech Support | Feedback | Compatibility | Disruption | Automation
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## tag_6
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 22713 adet (%79.45)
- Benzersiz deger: 575
- Ornek degerler: Outage | Organization | Tech Support | IT | Microservice
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## tag_7
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 26547 adet (%92.86)
- Benzersiz deger: 427
- Ornek degerler: Tech Support | Campaign | Workflow | Connection | Troubleshooting
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## tag_8
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 28022 adet (%98.02)
- Benzersiz deger: 224
- Ornek degerler: Tech Support | Ink | Maintenance | IT | Healthcare
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## type
- Tip: `str`
- Rol: `categorical`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 4
- Ornek degerler: Incident | Request | Problem | Change
- Yorum: Segmentasyon, Pareto ve operasyonel dagilim analizi icin uygundur.

## complexity_score
- Tip: `float64`
- Rol: `generated_feature`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 1773
- Ornek degerler: 1.506 | 1.291 | 1.196 | 1.341 | 1.5
- Yorum: Notebook icinde turetilmis analitik ozelliktir.

## created_at_clean
- Tip: `datetime64[us]`
- Rol: `generated_feature`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 365
- Ornek degerler: 2025-02-02 | 2025-10-10 | 2025-08-27 | 2025-06-10 | 2025-06-08
- Yorum: Notebook icinde turetilmis analitik ozelliktir.

## created_day_of_week
- Tip: `str`
- Rol: `generated_feature`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 7
- Ornek degerler: Sunday | Friday | Wednesday | Tuesday | Monday
- Yorum: Notebook icinde turetilmis analitik ozelliktir.

## customer_name
- Tip: `str`
- Rol: `generated_feature`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 10
- Ornek degerler: ZenithCare | OrionTel | NovaTech | BlueOrbit | DataBridge
- Yorum: Notebook icinde turetilmis analitik ozelliktir.

## description_length
- Tip: `int64`
- Rol: `generated_feature`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 908
- Ornek degerler: 751 | 544 | 534 | 605 | 677
- Yorum: Notebook icinde turetilmis analitik ozelliktir.

## is_weekend
- Tip: `int64`
- Rol: `generated_feature`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 2
- Ornek degerler: 1 | 0
- Yorum: Notebook icinde turetilmis analitik ozelliktir.

## resolution_time
- Tip: `float64`
- Rol: `generated_feature`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 1509
- Ornek degerler: 8.35 | 13.37 | 14.87 | 13.15 | 14.29
- Yorum: Notebook icinde turetilmis analitik ozelliktir.

## word_count
- Tip: `int64`
- Rol: `generated_feature`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 142
- Ornek degerler: 82 | 76 | 91 | 97 | 74
- Yorum: Notebook icinde turetilmis analitik ozelliktir.

## version
- Tip: `int64`
- Rol: `numeric`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 3
- Ornek degerler: 51 | 52 | 400
- Yorum: Dagilim, korelasyon ve modelleme icin kullanilabilir.

## effort_hours
- Tip: `float64`
- Rol: `target`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 714
- Ornek degerler: 6.54 | 7.05 | 6.44 | 5.73 | 6.94
- Yorum: Tahminleme hedefidir.

## answer
- Tip: `str`
- Rol: `text`
- Eksik deger: 7 adet (%0.02)
- Benzersiz deger: 28580
- Ornek degerler: Vielen Dank für die Meldung des... | Thank you for reaching out, <name>.... | Thank you for your inquiry. Our... | We appreciate you reaching out with... | Thank you for your inquiry. Our...
- Yorum: Metin analizi, NLP ve karmasiklik yorumlari icin kullanilabilir.

## body
- Tip: `str`
- Rol: `text`
- Eksik deger: 0 adet (%0.0)
- Benzersiz deger: 28585
- Ornek degerler: Sehr geehrtes Support-Team,\n\nich... | Dear Customer Support Team,\n\nI am... | Dear Customer Support Team,\n\nI hope... | Dear Customer Support Team,\n\nI hope... | Dear Support Team,\n\nI hope this...
- Yorum: Metin analizi, NLP ve karmasiklik yorumlari icin kullanilabilir.

## subject
- Tip: `str`
- Rol: `text`
- Eksik deger: 3838 adet (%13.43)
- Benzersiz deger: 24749
- Ornek degerler: Wesentlicher Sicherheitsvorfall | Account Disruption | Query About Smart Home System... | Inquiry Regarding Invoice Details | Question About Marketing Agency...
- Yorum: Metin analizi, NLP ve karmasiklik yorumlari icin kullanilabilir.
