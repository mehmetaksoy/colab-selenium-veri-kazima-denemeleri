# Google Colab ile Selenium Web Kazıma Denemeleri (Google Scholar Odaklı)

Bu proje, Google Colaboratory (Colab) ortamında `Selenium` kütüphanesini kullanarak web kazıma (web scraping) işlemleri yapma denemelerini içermektedir. Özellikle, `google-colab-selenium` ve `undetected-chromedriver` paketleri aracılığıyla Google Scholar gibi dinamik web sitelerinden veri çekme girişimleri ve temel Selenium testleri bulunmaktadır.

## 🎯 Projenin Amacı

Bu notebook'un temel amaçları şunlardır:
1.  Google Colab ortamında `google-colab-selenium` paketi ile standart bir Selenium WebDriver'ının (Chrome) başarılı bir şekilde başlatılıp temel bir web sitesine (google.com) erişimini test etmek.
2.  Bot tespit mekanizmalarını aşmak amacıyla `undetected-chromedriver` kullanarak Google Scholar'dan "reinforcement learning applications" anahtar kelimesi ile akademik makale metaverilerini (başlık, yazarlar, özet, PDF linki vb.) çekmeyi denemek.
3.  Toplanan verilerin (başarılı bir kazıma senaryosunda) işlenmesi ve yapılandırılmış formatlarda (CSV, JSON) kaydedilmesi için bir altyapı sunmak.

## 🧪 Deneyler ve İçerik

Notebook aşağıdaki ana bölümleri içerir:

1.  **Kütüphane Kurulumu:**
    * `google-colab-selenium[undetected]` ve `fake-useragent` kütüphaneleri kurulur.
    * Ayrıca standart `selenium`, `webdriver-manager`, `undetected-chromedriver` paketleri de kurulur/kontrol edilir.

2.  **Standart Selenium Testi (Google.com):**
    * `google_colab_selenium` kullanılarak standart bir Chrome sürücüsü başlatılır.
    * `google.com` adresine gidilir ve sayfa başlığı alınarak erişim doğrulanır. Bu kısım genellikle başarılı çalışır.

3.  **Google Scholar Kazıma Denemesi (`undetected-chromedriver` ile):**
    * Daha gelişmiş bot tespitlerini aşmak için `undetected-chromedriver` ile headless modda bir Chrome sürücüsü başlatılır.
    * Google Scholar ana sayfasına gidilir.
    * Belirlenen bir anahtar kelime (`reinforcement learning applications`) ile arama yapılır.
    * Arama sonuçları sayfasındaki makale konteynerlerinden veri (başlık, URL, yazar satırı, özet, PDF linki) çekilmeye çalışılır.
    * **Gözlem:** Bu deneme sırasında Google Scholar, erişimi engelleyerek **403 Forbidden** hatası vermiştir. Bu, `undetected-chromedriver`'ın bile her zaman tüm bot tespit sistemlerini aşamayabileceğini göstermektedir.

4.  **Veri İşleme ve Kaydetme (Teorik):**
    * Eğer veri başarıyla çekilebilseydi, toplanan verilerdeki yazar ve yayın yılı bilgilerini ayrıştırmak için bir mantık içerir.
    * İşlenmiş verilerin Pandas DataFrame'e dönüştürülerek CSV ve JSON formatlarında kaydedilmesi hedeflenir. Ancak 403 hatası nedeniyle bu aşamaya veri aktarılamamıştır.

## 🛠️ Kullanılan Teknolojiler ve Kütüphaneler

* **Programlama Dili:** Python
* **Çalışma Ortamı:** Google Colaboratory
* **Ana Kütüphaneler:**
    * `selenium`
    * `google-colab-selenium`: Colab'de Selenium kullanımını kolaylaştırmak için.
    * `undetected-chromedriver`: Bot tespitlerini aşmaya yardımcı olmak için tasarlanmış Chrome sürücüsü.
    * `pandas`: Veri manipülasyonu ve CSV'ye kaydetme için.
    * `json`: Verileri JSON formatında kaydetmek için.
    * `time`, `random`, `uuid`, `re`: Yardımcı işlemler için.

## 🚀 Kurulum ve Çalıştırma

1.  **Google Colab Ortamı:**
    * Bu `Veri_Kazima_GS_basarili.ipynb` dosyasını Google Colab'e yükleyin veya yeni bir notebook oluşturup kodu kopyalayın.
    * Çalışma zamanı türünü GPU veya CPU olarak ayarlayabilirsiniz (bu proje için GPU zorunlu değildir).

2.  **Kütüphane Kurulumu:**
    * Notebook'un başındaki `%pip install ...` komutları gerekli kütüphaneleri kuracaktır.

3.  **Çalıştırma:**
    * Hücreleri sırayla çalıştırın.
    * İlk test (google.com) genellikle başarılı olacaktır.
    * İkinci test (Google Scholar) büyük olasılıkla 403 hatası verecektir. Bu, web sitesinin güvenlik önlemlerinden kaynaklanmaktadır.

## 📊 Sonuçlar ve Gözlemler

* `google-colab-selenium` ile standart Chrome sürücüsü Colab'de başarılı bir şekilde çalıştırılabilmekte ve genel web sitelerine erişim sağlanabilmektedir.
* `undetected-chromedriver` kullanılmasına rağmen, Google Scholar gibi gelişmiş bot tespit mekanizmalarına sahip sitelerden veri kazımak zorlayıcıdır ve erişim engellenebilir (bu çalışmada 403 hatası alınmıştır).
* Başarılı bir kazıma durumunda, notebook verileri çekip işleyerek CSV ve JSON formatlarında kaydetme yeteneğine sahiptir.

## 💡 Olası İyileştirmeler ve Sonraki Adımlar

Google Scholar gibi sitelerden veri kazımak için:
* **Daha Gelişmiş Teknikler:** Daha sofistike proxy yönetimi, kullanıcı davranışı taklit etme, CAPTCHA çözme servisleri gibi yöntemler denenebilir. Ancak bu yöntemler genellikle daha karmaşıktır ve etik hususları beraberinde getirir.
* **Resmi API'ler:** Mümkünse, web sitelerinin sunduğu resmi API'leri kullanmak her zaman daha stabil, güvenilir ve etik bir yoldur. Google Scholar'ın doğrudan bir arama API'si kısıtlıdır veya akademik olmayan kullanımlar için tasarlanmamıştır.
* **Hata Yönetimi ve Dayanıklılık:** 403 gibi hatalar alındığında betiğin daha akıllıca davranması (örn: farklı IP/User-Agent ile tekrar deneme, belirli bir süre sonra tekrar deneme) için geliştirmeler yapılabilir.
* **Sayfalama (Pagination):** Başarılı bir kazıma senaryosunda, arama sonuçlarının birden fazla sayfasını gezmek için sayfalama mantığı eklenmelidir.