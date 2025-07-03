# 🧠 BlogStore | AI Destekli Makale Platformu

BlogStore, Entity Framework Core ve .NET Core teknolojileri kullanılarak geliştirilen, **AI destekli**, modern bir makale platformudur. Katmanlı mimari yapısıyla sürdürülebilir, güvenli ve ölçeklenebilir bir yapı sunar.

---

## 🗂️ Katmanlı Mimari Yapısı

Proje, SOLID prensiplerine uygun olarak **katmanlı mimari** ile geliştirilmiştir:

- **Presentation Layer**: Kullanıcı arayüzü (UI) katmanıdır. MVC mimarisiyle sayfaların görüntülenmesini sağlar.
- **Entity Layer**: Veritabanı tablolarını temsil eden sınıfları içerir.
- **Data Access Layer**: Entity Framework Core kullanarak veri işlemlerini gerçekleştiren katmandır. Repository desenine uygun şekilde yapılandırılmıştır.
- **Business Layer**: Uygulamanın iş mantığını barındırır. Validasyon ve iş kuralları burada tanımlanır.

---

## ⚙️ Entity Framework Özelleştirmeleri

- `Include()` gibi metotlarla ilişkili veriler çekildi.
- Senaryolara özgü LINQ sorguları yazılarak filtreli veri çekimi sağlandı.
- Performans ve kod okunabilirliği artırıldı.

---

## 💬 Akıllı Yorum Sistemi (AI Destekli)

Yorumlarda toksik içerikleri tespit etmek için **ToxicBERT** modeli entegre edilmiştir.  
Model Türkçede sınırlı başarı sağladığı için yorumlar önce İngilizceye çevrilip sonra analiz edilmiştir.

Kullanılan modeller:

- `Helsinki-NLP/opus-mt-tr-en` → Türkçe yorumları İngilizceye çevirir.
- `unitary/toxic-bert` → Yorumun toksik olup olmadığını analiz eder.

Bu sayede kullanıcılar **küfür, hakaret, saldırı** içeren yorumlar yapamaz.

---

## 📡 AJAX ile Dinamik Yorum Sistemi

- Login olmayan kullanıcılar yorum alanını göremez, bunun yerine **giriş yapma bağlantısı** görünür.
- Login olan kullanıcılar yorum yazabilir.
- Yorumlar AJAX üzerinden iletilir ve sayfa yenilemeden listeye eklenir.
- Toksik içerik kontrolü başarıyla yapılır, toksik yorumlar engellenir.

---

## 🔒 Slug Kullanımı ile URL Güvenliği

Makalelere ulaşımda `id` yerine **slug** yapısı kullanılmıştır.  
Bu sayede hem **URL manipülasyonları** önlenmiş hem de **SEO uyumluluğu** sağlanmıştır.

Örnek:/Makale/Detay/yapay-zeka-nedir ✅

---

## 🔐 Identity ile Kullanıcı Yönetimi

- ASP.NET Core Identity kullanılarak giriş/kayıt işlemleri gerçekleştirildi.
- `AppUser` entity’si üzerinden kullanıcı bilgileri tutuldu ve genişletildi.
- Kullanıcı, profilini güncelleyebilir; güncelleme sonrası güvenlik nedeniyle sistemden çıkış yapılır.

---

## 📚 Entity Yapısı ve İlişkiler

**Entity'ler:**

- `AppUser`: Kullanıcı bilgilerini içerir.
- `Article`: Makale içeriklerini barındırır.
- `Category`: Makalelerin ait olduğu kategoriler.
- `Tag`: Makalelere etiket atamak için kullanılır.

**İlişkiler:**

- Bir **AppUser**, birçok **Article** yazabilir.
- Her **Article**, bir **Category**ye aittir.
- **Article** ve **Tag** arasında çoklu ilişki kurulmuştur.
- Yorumlar da article üzerinden kullanıcıya bağlıdır.

---

## 📊 Admin Paneli Özellikleri

### Dashboard

- Kategorilere göre makale sayısı **chart** şeklinde gösterilir.
- Son yüklenen 4 makale listelenir.
- Kullanıcının makalelerine yapılan son 5 yorum gösterilir.

### Makale Listem

- Kullanıcının tüm makaleleri listelenir.
- Her makale kart yapısında sunulur.
- "Makaleyi Görüntüle" butonuyla detay sayfasına yönlendirme yapılır.

### Yeni Makale Oluştur

- "Başlık", "Resim URL", "Kategori" ve "İçerik" alanlarıyla yeni makale oluşturulur.

### Profilim

- Kullanıcı bilgilerini güncelleyebilir.
- Güncelleme sonrası oturum sonlandırılır ve kullanıcı tekrar giriş yapar.

---

## 🌍 UI Panel Özellikleri

### Anasayfa

- Platformdaki tüm makaleler listelenir.
- Makaleye tıklanıldığında detayları görüntülenir.
- Yorumlar gösterilir.
- Login kullanıcı yorum yapabilir.
- Toksik yorumlar engellenir.
- Login olmayan kullanıcıya giriş yapma yönlendirmesi yapılır.

### Kategoriler

- Tüm kategoriler listelenir.
- Seçilen kategoriye ait makaleler filtrelenir.

### Yazarlar

- Tüm kullanıcılar/yazarlar listelenir.
- Yazara tıklandığında, o yazarın tüm makaleleri gösterilir.

### Giriş Yap

- Giriş yapan kullanıcı yorum yapabilir ve admin paneline erişebilir.

---

## 🧩 Kod Optimizasyonu: Extension Yapısı

`BusinessLayer > Container > Extension` yapısıyla tüm servis kayıtları merkezi bir dosyada toplandı.

## 🧪 Teknolojiler

- **ASP.NET Core 6.0**  
  Web uygulaması geliştirme için kullanılan modern ve modüler framework.

- **Entity Framework Core**  
  ORM aracı, veritabanı işlemleri için LINQ destekli yapı sunar.

- **SQL Server**  
  Projenin veritabanı altyapısı.

- **ASP.NET Identity**  
  Kimlik doğrulama ve kullanıcı yönetimi için kullanıldı.

- **jQuery & AJAX**  
  Dinamik yorum sistemi ve asenkron işlemler için kullanıldı.

- **Chart.js**  
  Dashboard kısmında makale istatistiklerini grafiksel olarak göstermek için kullanıldı.

- **HuggingFace Transformers**  
  NLP modellerini projeye entegre etmek için kullanıldı.

- **ToxicBERT**  
  Yorumların toksik olup olmadığını analiz eden AI modeli.

- **Helsinki-NLP/opus-mt-tr-en**  
  Türkçe yorumları İngilizceye çevirerek daha doğru toksik analiz yapılmasını sağladı.



# 📸 Fotoğraflar

![newblog001](https://github.com/user-attachments/assets/53b1c2a8-6b60-42d0-a0ac-406b668bb882)
![kategoriler01](https://github.com/user-attachments/assets/0bd34236-6971-4e8f-95fc-6be3a76565d3)
![dashboard01](https://github.com/user-attachments/assets/96b877b0-565c-412f-97f8-352b5d69fbc7)
![yazar02](https://github.com/user-attachments/assets/8430b717-21ea-4c20-9f38-966426e3ce4e)
![Screenshot 2025-07-03 222330](https://github.com/user-attachments/assets/383fc203-2903-4916-9256-afb13d270145)
![Screenshot 2025-07-03 222135](https://github.com/user-attachments/assets/27ece2b4-ceec-420e-abda-b6429558f867)
![Screenshot 2025-07-03 221949](https://github.com/user-attachments/assets/c08bdd01-60b6-44d4-8780-8afcdfe9097d)




![Screenshot 2025-07-03 221318](https://github.com/user-attachments/assets/6708aec7-e9a8-46ef-a6d5-52d5bc9e8346)
![comment1](https://github.com/user-attachments/assets/f1df3125-8b26-4f3f-840e-02ef9b8ebc96)
![bloganasayfa01](https://github.com/user-attachments/assets/8713d869-9be9-4e5f-92cb-119884a2813d)

![semih02](https://github.com/user-attachments/assets/8438cc75-7d53-4162-838b-9fc4b445bb6f)
![semih01](https://github.com/user-attachments/assets/03c772b1-6a14-4a41-8a80-af7de0de8b0d)
![Screenshot 2025-07-03 221726](https://github.com/user-attachments/assets/d983f808-1251-4bc5-9fa1-229e4a010610)
