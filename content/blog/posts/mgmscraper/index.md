---
title: "MGMScraper: MGM Verilerine Hızlı ve Programatik Erişim"
date: 2025-06-02T00:00:00.000Z
tags: ["python", "web scraping"]
categories: ["Meteoroloji", "Yazılım"]
description: "Türkiye Meteoroloji Genel Müdürlüğü (MGM) verilerine asenkron, hızlı ve yeniden kullanılabilir erişim sağlayan açık kaynak Python kütüphanesi."
author: mhmmdlsubasi
draft: true
cover:
  image: cover.png
sidebar:
  groups:
    - title: "MGMScraper Hakkında"
      items:
        - title: "GitHub"
          icon: "github"
          url: "https://github.com/mhmmdlsubasi/MGMScraper"
          domain: "github.com"
          description: "Kaynak kodları"

        - title: "PyPI"
          url: "https://pypi.org/project/mgmscraper"
          domain: "pypi.org"
          description: "Python kütüphanesi"
---

# 🚀 Giriş

Meteorolojik verilerle çalışan her geliştirici ve araştırmacının bildiği bir gerçek var: **MGM'nin web sitesinden manuel veri çekmek tam bir işkence!** Saatlerce tarayıcıda tıklama, kopyala-yapıştır döngüsü, tutarsız formatlar... Tanıdık geliyor mu?

İşte tam bu sorunu çözmek için **MGMScraper**'ı geliştirdim. Bu Python kütüphanesi ile Türkiye Meteoroloji Genel Müdürlüğü'nün tüm verilerine sadece birkaç satır kodla ulaşabilirsiniz.

## ⚡ Neden MGMScraper?

### Önce - Sonra: Geleneksel Yöntem vs MGMScraper

❌ **Eskiden:**

- MGM sayfalarında gezin
- İstasyon kodlarını tek tek ara
- Verileri elle kopyala
- Excel’de birleştir
- Formatlarla uğraş
- Saatler harcandı, sadece birkaç günlük veri alındı

✅ **Şimdi MGMScraper ile:**

- Tek bir Python fonksiyon çağrısı
- Tüm veriler JSON formatında hazır
- Saniyeler içinde işlem tamam

```python
import asyncio
from mgmscraper import HttpClient, ObservationService

async def main():
    async with HttpClient() as session:
        obs_service = ObservationService(session)
        istanbul_data = await obs_service.get_by_province_plate(34)

        for station in istanbul_data:
            print(f"{station['istNo']}: {station['sicaklik']}°C")

asyncio.run(main())
```

**Sonuç:** 10 saniyede tüm İstanbul istasyonlarının verileri elinde!

# 🌐 Meteorolojik Veriye Programatik Erişimin Önemi

**Günümüzde meteorolojik veriye erişim**, özellikle araştırma ve yazılım geliştirme süreçlerinde kritik öneme sahip. Ancak bu verilere tarayıcı üzerinden ulaşmak, zaman alıcı ve tekrarlanabilirlikten uzak bir süreçtir. Çoğu zaman, veriyi elle çekmek, analiz etmek ve birleştirmek çok fazla iş gücü gerektirir. Bu gibi durumlar, özellikle büyük veri setleriyle çalışırken, ciddi zaman kayıplarına neden olabilir.

Bu nedenle, **MGMScraper** adlı Python kütüphanesini geliştirdim. Amacım, **Türkiye Meteoroloji Genel Müdürlüğü**'nün (mgm.gov.tr) web sitesinde sunulan meteorolojik verilere hızlı, kolay ve yeniden kullanılabilir bir şekilde erişim sağlamaktır. Bu araç, veriyi doğrudan **programatik** bir şekilde çekmek ve analiz etmek isteyen araştırmacılar ve yazılımcılar için güçlü bir çözüm sunmaktadır.

# 🎯 MGMScraper'ın Temel Özellikleri

**MGMScraper**, **asenkron** ve **modüler** yapısıyla dikkat çeker. Python'un popüler `aiohttp` kütüphanesini kullanarak, yüksek performanslı, paralel veri çekimi yapılmasını sağlar. Proje, farklı veri kaynaklarını ve API'leri bir araya getirerek, veri çekme sürecini kolaylaştırır. İşte projenin öne çıkan özellikleri:

✅ **Asenkron yapı:** `aiohttp` ile yüksek performanslı veri çekimi. Bu, birden fazla istek gönderilirken, her birinin sırasıyla beklenmeden işlem yapılmasına olanak tanır. Bu sayede, yüzlerce istasyon verisini bile saniyeler içinde, programınızı kilitlemeden çekebilirsiniz.  
✅ **Modüler tasarım:** Farklı meteorolojik veri servislerine ve sayfalara kolayca entegre olabilen modüler bir yapı. Bu sayede farklı veri türlerine yönelik sorgulamalar rahatlıkla yapılabilir.  
✅ **Yeniden kullanılabilirlik:** Kullanıcılar, sadece birkaç satır kod ile istedikleri veriyi çekebilir. Veri çekme süreci, parametrelerle özelleştirilebilir.  
✅ **Kapsamlı API**: İstasyon bilgileri, anlık gözlemler, tahminler, istatistikler ve radar görüntüleri.  
✅ **Rate limiting:** Sunucu kaynaklarını korumak için yapılandırılabilir istek sınırlaması.  
✅ **Hata yönetimi:** MGM sunucularına anlık erişim sorunları veya geçici ağ hataları durumunda, MGMScraper pes etmez! Akıllı 'exponential backoff' mekanizması sayesinde, istekleri otomatik olarak artan aralıklarla yeniden deneyerek veri kaybını en aza indirir.  
✅ **Lisans:** Açık kaynak MIT lisansı. Bu, kullanıcıların projeyi özgürce kullanabilmesini ve geliştirmesini sağlar.
✅ **Minimal bağımlılık:** Sadece `aiohttp` ve `beautifulsoup4`.

# 🔧 Kullanım Alanları

- Hava durumu uygulamaları
- İklim veri analizi
- Araştırma projeleri
- Meteorolojik veri görselleştirme
- IoT projelerinde hava durumu entegrasyonu

# 🏗️ Projenin Teknik Yapısı

Projenin temelinde, **MGM web sitesindeki veri erişim noktalarını (API endpoint'leri)** anlamak ve bu verilere doğru parametrelerle erişmek bulunuyor. Bunun için, MGM'nin sunduğu verilerin yapısını çözümlemek adına **HTTP trafiği** analiz edilmiştir. Bu analiz sayesinde, veri çekerken kullanılan endpoint'ler ve parametreler belirlenmiştir.

Projede **aiohttp** kütüphanesinin yanı sıra, Python'un standart kütüphaneleri de kullanılarak veri işleme ve hata yönetimi sağlanmıştır.

# 💻 Örnek Kullanım

MGMScraper, özellikle **JSON** veya **XML** formatındaki verileri işleyerek, bu verileri doğrudan Python veri yapıları haline dönüştürür. Kullanıcılar, bu verileri kolayca analiz edebilir, görselleştirebilir ve daha ileri düzey çalışmalar yapabilirler. Aşağıda MGMScraper ile veri çekme süreci basit bir örnekle açıklanmıştır:

```python
import asyncio
from mgmscraper import HttpClient, ObservationService

async def main():
    async with HttpClient() as session:
        obs_service = ObservationService(session)
        istanbul_weather = await obs_service.get_by_province_plate(34)

        for station in istanbul_weather:
            print(f"{station['istNo']}: {station['sicaklik']}°C")

asyncio.run(main())
```

Yukarıdaki örnekte, **ObservationService** sınıfı kullanılarak belirli bir istasyon için son gözlem verisi çekilmiştir. Bu süreç tamamen asenkron şekilde gerçekleştirilir ve veriler **verimli** bir şekilde toplanır.

# 📦 Hızlı Kurulum

```bash
pip install mgmscraper
```

# 🤝 Projeye Göz Atın ve Katkıda Bulunun

MGMScraper ile projelerinize zaman kazandırın. Yıldız verin ⭐, katkıda bulunun veya hemen kendi uygulamanızda kullanmaya başlayın!

🔗 **GitHub**: https://github.com/mhmmdlsubasi/mgmscraper  
🔗 **PyPI**: https://pypi.org/project/mgmscraper  
📚 **Dokümantasyon**: Detaylı kullanım örnekleri README'de mevcut

Bu proje, Türkiye'deki geliştiricilerin meteorolojik verilere daha kolay erişmesini sağlamak amacıyla geliştirildi. Geri bildirimlerinizi ve katkılarınızı bekliyorum! 🤝
