# 🕸️ Web Scraper & Data Automation Bot

Bu proje, statik ve dinamik web sayfalarından otomatik olarak yapılandırılmış veri toplamak, bu verileri temizlemek ve doğrudan Google Sheets üzerine aktarmak için geliştirilmiş kapsamlı bir veri toplama (web scraping) botudur. 

Veri mühendisliği süreçlerinin ilk adımı olan "veri toplama ve temizleme" (ETL/Pipeline) işlemlerini otomatize etmek amacıyla tasarlanmıştır.

## 🚀 Özellikler

* **Dinamik ve Statik Sayfa Desteği:** Sadece statik HTML değil, JavaScript ile sonradan yüklenen içerikleri (pop-up'lar, modallar, dinamik kartlar) de başarıyla işler.
* **Akıllı Fallback Mekanizması:** İstekleri önce hızlı olan HTTP protokolü ile dener, sayfa JS tabanlıysa otomatik olarak Headless Browser moduna (Selenium) geçer.
* **Veri Temizleme & Standardizasyon:** Çekilen dağınık verilerdeki (telefon numaraları, e-postalar, web siteleri) düzensizlikleri Regex (Düzenli İfadeler) ile temizler ve standart bir formata sokar.
* **Google Workspace Entegrasyonu:** Toplanan veriler manuel bir işleme gerek kalmadan, Google Sheets API kullanılarak otomatik olarak bulut tabanlı tablolara yazılır veya güncellenir.
* **Hata Yönetimi (Error Handling):** Ağ kopmaları veya DOM değişiklikleri gibi durumlarda uygulamanın çökmesini engelleyen "retry" (yeniden deneme) yapıları içerir.

## 🛠️ Kullanılan Teknolojiler

Bu proje, güçlü ve modern Python kütüphaneleri kullanılarak inşa edilmiştir:

* **[Python 3.x](https://www.python.org/):** Projenin çekirdek dili.
* **[Selenium WebDriver](https://www.selenium.dev/):** JavaScript ile render edilen dinamik web elementleri ile etkileşime geçmek ve tarayıcı otomasyonu sağlamak için.
* **[BeautifulSoup4 (bs4)](https://www.crummy.com/software/BeautifulSoup/bs4/doc/):** DOM ağacında gezinmek ve HTML/XML içeriklerini hızlıca ayrıştırmak (parsing) için.
* **[Requests](https://pypi.org/project/requests/):** Statik sayfalara hızlı HTTP GET/POST istekleri atmak ve oturum (session) yönetimi için.
* **[Google API Client (OAuth2)](https://github.com/googleapis/google-api-python-client):** Verileri doğrudan Google Sheets tablolarına entegre etmek için (Service Account ile yetkilendirilmiş erişim).
* **Regex (`re`):** Karmaşık metin blokları içerisinden e-posta ve telefon numarası gibi spesifik verileri yakalamak için.

## ⚙️ Nasıl Çalışır?

1. Hedef URL'ler taranır ve içerik analizi yapılır.
2. `BeautifulSoup` ve `Selenium` kullanılarak CSS seçicileri üzerinden istenen veri blokları (şirket adı, sektör, e-posta vb.) izole edilir.
3. Ham veriler `html` ve `re` kütüphaneleriyle HTML taglerinden ve gereksiz boşluklardan arındırılır.
4. Benzersiz bir şirket ID'si (`hashlib`) oluşturularak mükerrer (duplicate) kayıtların önüne geçilir.
5. Hazırlanan JSON formatındaki veri seti, Google Sheets API aracılığıyla ilgili sekmeye (tab'a) toplu olarak (batch update) aktarılır.
