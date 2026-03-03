 Temel Sınıf Yapıları ve Veri Modelleri
Sistem, dört ana sınıf etrafında yapılandırılmıştır. Her sınıf, kütüphane ekosistemindeki belirli bir varlığı veya işlevi temsil eder.

----Kitap Sınıfı----
Kitap nesneleri, sistemin temel veri birimleridir.
Özellikler: Ad, yazar, sayfa sayısı, basım yılı ve durum.
Kapsülleme (Encapsulation): Kitap adı __ad şeklinde gizli (private) bir öznitelik olarak tanımlanmıştır. Bu veriye erişim get_ad() metodu ile sağlanır.
Durum Yönetimi: Her kitabın varsayılan durumu "Müsait" olarak atanır ve ödünç verme işlemlerine göre set_durum() metodu ile güncellenir.

Üye ve Yönetici Sınıfları
Sistemde iki tip kullanıcı tanımı bulunmaktadır:
Uye (Standart): İsim, numara ve rol bilgilerini içerir. Ödünç alınan kitaplar odunc adlı bir listede tutulur.
Yonetici (Admin): Uye sınıfından türetilmiştir (Kalıtım). Standart üye özelliklerine ek olarak "Yönetim" departmanına otomatik atanır ve sistemden kitap silme yetkisine sahiptir.

Kütüphane Sınıfı
Tüm kitap envanterini yöneten merkezi sınıftır. Kitap ekleme, listeleme, arama ve silme fonksiyonlarını barındırır.

--------------------------------------------------------------------------------
----Operasyonel İş Akışları ve Fonksiyonlar----
Yazılımın işleyişi, belirli kurallar ve doğrulama mekanizmaları çerçevesinde gerçekleşmektedir.

Kitap Ödünç Alma ve İade Süreci
İşlemler islem metodu üzerinden "al" veya "ver" parametreleri ile yönetilir:
Ödünç Alma: Kitabın durumu "Müsait" ise işlem başarılı olur; kitabın durumu "Ödünç verildi" olarak güncellenir ve üyenin listesine eklenir.
İade Etme: Üyenin kendi listesinde bulunan bir kitap, kütüphaneye geri teslim edildiğinde durumu tekrar "Müsait" haline getirilir.

2.2. Yönetici Yetkileri ve Güvenlik
Sistemde kritik işlemler (kitap silme gibi) rol tabanlı bir kontrole tabidir.
Bir kitabın sistemden tamamen silinebilmesi için işlemin bir Yonetici nesnesi tarafından tetiklenmesi gerekir.
Yönetici silme işlemi sırasında kütüphane veri tabanında (listesinde) kitabın varlığı kontrol edilir ve işlem sonucunda bilgilendirme mesajı verilir.

--------------------------------------------------------------------------------

----Kullanıcı Arayüzü ve Sistem Seçenekleri----
Sistem, sekiz ana seçenekten oluşan bir yönetim paneli sunar.

1-Kitap Ekle
Kitap bilgilerini (ad, yazar, sayfa, yıl) sisteme kaydeder.

2-Üye Ekle
Standart veya Yönetici statüsünde yeni kullanıcı oluşturur.

3-Listele
Kütüphanedeki tüm kitapları ve güncel durumlarını gösterir.

4-Kitap Ödünç Ver
Belirlenen üyeye kitap tahsisi yapar.

5-Kitap İadesi
Üyenin üzerindeki kitabı sisteme geri kazandırır.

6-Bilgi
Üyenin profil bilgilerini ve sahip olduğu kitap sayısını gösterir.

7-Sil (Admin)
Sadece yöneticilerin erişebildiği kitap silme fonksiyonu.

8-Çık
Program döngüsünü sonlandırır.

--------------------------------------------------------------------------------

4. Teknik Kayda Değer Detaylar ve Hata Yönetimi
Veri Tipi Kontrolü: Kitap ekleme sırasında sayfa sayısı ve yıl gibi alanlar için try-except bloğu kullanılarak sayısal veri girişi zorunlu tutulmuştur. Geçersiz girişlerde sistem hata mesajı verir.
Arama Optimizasyonu: Kitap aramalarında büyük/küçük harf duyarlılığını ortadan kaldırmak için lower() fonksiyonu kullanılmaktadır.
Nesne Temsili: __str__ metodu sayesinde kitap nesneleri yazdırıldığında kullanıcıya anlamlı bir formatta ('Kitap Adı' - Yazar (Yıl) [Durum]) bilgi sunulmaktadır.
Üyelik Doğrulaması: İşlemlerden önce üyenin sistemde kayıtlı olup olmadığı, döngüsel bir kontrol ve bayrak (bulundu = True) mekanizması ile teyit edilmektedir.

--------------------------------------------------------------------------------
