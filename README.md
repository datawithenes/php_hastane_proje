
# PHP ile Detaylı Hastane Yönetim Sistemi (HMS)

Bu proje, PHP ile geliştirilmiş bir **Hastane Yönetim Sistemi** (HMS) uygulamasıdır. Bitirme çalışmam olarak sunduğum bu projeyi, kullanıcıların yönetici, doktor ve hasta olarak giriş yapabileceği bir hastane sistemi şeklinde tasarladım. Kullanıcılar şifrelerini MD5 ile şifreleyerek sisteme giriş yapabilirler. Admin paneli üzerinden doktor ve hasta işlemleri yapılabilir, IP adresleri takip edilebilir.

## Proje Özeti

Bu sistem aşağıdaki temel özelliklere sahip bir hastane yönetim sistemidir:

- **Admin Paneli**: Admin, sistemdeki doktor ve hasta bilgilerini yönetebilir, yeni kayıtlar ekleyebilir ve mevcut kayıtları silebilir.
- **Doktor ve Hasta Girişi**: Doktorlar ve hastalar sisteme giriş yapabilir.
- **Şifreleme**: Kullanıcı şifreleri MD5 ile şifrelenir ve güvenli giriş için şifreler MD5 ile çözülüp girilebilir.
- **IP Takibi**: Admin panelinde, her kullanıcı (doktor ve hasta) için IP adresleri takip edilebilir.

## Proje Özellikleri

- **Kullanıcı Türleri**: 
  - **Admin**: Admin paneline erişim sağlar, doktor ve hasta yönetimi yapabilir.
  - **Doktor**: Kendi profilini görebilir ve hastalarla ilgili işlemler yapabilir.
  - **Hasta**: Kendi profilini görebilir, sağlık bilgilerini güncelleyebilir.
  
- **Veritabanı**: MySQL veritabanı kullanılarak hastaların, doktorların ve admin bilgileri saklanır.
  
- **Güvenlik**: Şifreler MD5 algoritması ile şifrelenmiştir.

## Gereksinimler

Bu projeyi çalıştırabilmek için aşağıdaki yazılımlara ihtiyacınız vardır:

- PHP (v7.4 veya üzeri)
- MySQL veya MariaDB
- Apache veya Nginx (web sunucusu)
- phpMyAdmin (veritabanı yönetimi için opsiyonel)
- Web tarayıcısı (Chrome, Firefox, vb.)

## Kurulum

### 1. Veritabanı Kurulumu

1. PHPMyAdmin veya başka bir MySQL yönetim aracı kullanarak bir veritabanı oluşturun. Bu örnekte veritabanı adı **hms** olarak kullanılacaktır.
2. Veritabanı oluşturduktan sonra, proje klasöründeki `hms.sql` dosyasını **phpMyAdmin** veya MySQL komut satırı aracılığıyla içeri aktarın.

   ```bash
   mysql -u root -p hms < hms.sql
   ```

### 2. Proje Dosyalarını Sunucuya Yükleme

1. **PHP ve MySQL sunucusu** üzerinde bir dizin oluşturun (örneğin `hms_project`).
2. Proje dosyalarını bu dizine yükleyin veya kopyalayın.

### 3. Web Sunucusunun Yapılandırılması

- Eğer Apache kullanıyorsanız, aşağıdaki gibi bir yapılandırma dosyası oluşturabilirsiniz.
- Eğer başka bir web sunucusu kullanıyorsanız, uygun yapılandırmayı yapın.

**Apache için örnek `.htaccess` dosyası**:

```apache
RewriteEngine On
RewriteBase /

# URL yönlendirme (SEO dostu URL'ler için)
RewriteRule ^(.*)$ index.php/$1 [L]
```

### 4. Veritabanı Bağlantısını Yapılandırma

Projede yer alan `config.php` dosyasını açın ve veritabanı bağlantı bilgilerinizi aşağıdaki gibi düzenleyin:

```php
<?php
$servername = "localhost";
$username = "root";
$password = "";  // Veritabanı şifreniz
$dbname = "hms";  // Kullanılacak veritabanı adı

// Veritabanı bağlantısı
$conn = new mysqli($servername, $username, $password, $dbname);

// Bağlantıyı kontrol et
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

### 5. Sisteme Giriş

- Admin paneline giriş için `admin` kullanıcı adı ve şifresi ile giriş yapabilirsiniz.
- Diğer kullanıcılar için, doktor ve hasta kayıtları oluşturulabilir. Şifreler MD5 ile şifrelendiğinden, şifrelerinizi **MD5 Encrypt-Decrypt** siteleri yardımıyla çözebilirsiniz.

### 6. Sistem Kullanımı

- **Admin Paneli**: Admin kullanıcıları, doktorları ve hastaları yönetebilir. IP takibi ve kayıt işlemleri admin panelinden yapılabilir.
- **Doktor Paneli**: Doktorlar, kendilerine ait bilgileri görüntüleyebilir ve hastalarla ilgili işlemler yapabilir.
- **Hasta Paneli**: Hastalar, kendi sağlık bilgilerini güncelleyebilir ve geçmiş kayıtları görüntüleyebilir.

## Şifreleme ve Güvenlik

Bu projede kullanıcı şifreleri MD5 algoritması ile şifrelenmiştir. Giriş yaparken şifrelerinizi MD5 ile çözmeniz gerekecektir. 

- **Örnek MD5 Şifre Çözme**: Şifrenizi MD5 ile çözüp admin, doktor veya hasta olarak giriş yapabilirsiniz. Şifrelerinizi çevrimiçi MD5 şifre çözme araçları kullanarak çözebilirsiniz.

## Örnek Kullanıcılar

- **Admin Girişi**:
  - Kullanıcı Adı: `admin`
  - Şifre: `admin_password` (MD5: `21232f297a57a5a743894a0e4a801fc3`)
  
- **Doktor Girişi**:
  - Kullanıcı Adı: `doctor1`
  - Şifre: `doctor_password` (MD5: `c4ca4238a0b923820dcc509a6f75849b`)

- **Hasta Girişi**:
  - Kullanıcı Adı: `patient1`
  - Şifre: `patient_password` (MD5: `8ad8757baa8564dc136c1e07507f4a2b`)

## Katkı Sağlama

Bu projeye katkı sağlamak isterseniz, lütfen şu adımları takip edin:

1. Bu projeyi forkladığınızda kendi dalınızı oluşturun.
2. Yeni özellikler veya hata düzeltmeleri ekleyin.
3. Pull request oluşturun.

## Lisans

Bu proje [MIT Lisansı](LICENSE) altında lisanslanmıştır.


