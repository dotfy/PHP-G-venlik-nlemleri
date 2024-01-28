### 1. **XSS (Cross-Site Scripting)**

#### Açıklama:
XSS saldırıları, kullanıcıların tarayıcılarında kötü amaçlı betiklerin çalıştırılmasına izin veren bir güvenlik açığıdır.

#### Örnek Kod:
```php
// Kötü kod örneği
echo "Merhaba, " . $_GET['name'] . "!";
```

#### Çözüm:
```php
// Güvenli kod örneği
echo "Merhaba, " . htmlspecialchars($_GET['name'], ENT_QUOTES, 'UTF-8') . "!";
```

#### Açıklama:
`htmlspecialchars()` kullanarak giriş verilerini temizlersiniz, böylece HTML etiketleri çalıştırılamaz hale gelir.

---

### 2. **SQL Enjeksiyonu**

#### Açıklama:
SQL enjeksiyonu, kötü niyetli kullanıcıların SQL sorgularını manipüle etmelerine olanak tanıyan bir güvenlik açığıdır.

#### Örnek Kod:
```php
// Kötü kod örneği
$username = $_POST['username'];
$password = $_POST['password'];
$query = "SELECT * FROM users WHERE username='$username' AND password='$password'";
```

#### Çözüm:
```php
// Güvenli kod örneği
$username = mysqli_real_escape_string($conn, $_POST['username']);
$password = mysqli_real_escape_string($conn, $_POST['password']);
$query = "SELECT * FROM users WHERE username='$username' AND password='$password'";
```

#### Açıklama:
`mysqli_real_escape_string()` kullanarak giriş verilerini temizlersiniz ve SQL sorgularını güvenli hale getirirsiniz. Daha iyi bir seçenek olarak, PDO kullanımını düşünebilirsiniz.

---

### 3. **CSRF (Cross-Site Request Forgery)**

#### Açıklama:
CSRF saldırıları, kullanıcının isteğini kötü niyetli bir şekilde başka bir web sitesinde kullanarak, kullanıcının bilgilerini değiştirmeyi amaçlar.

#### Örnek Kod:
```php
// Kötü kod örneği
echo "<img src='http://example.com/update.php?param1=value1&param2=value2' style='display:none;'>";
```

#### Çözüm:
```php
// Güvenli kod örneği
echo "<img src='http://example.com/update.php?param1=value1&param2=value2&token=" . $_SESSION['token'] . "' style='display:none;'>";
```

#### Açıklama:
Her kullanıcının oturumunda benzersiz bir CSRF belirteci (token) oluşturarak, sadece bu belirteci kullanarak yapılan isteklere izin verirseniz, CSRF saldırılarından korunabilirsiniz.

---

### 4. **Giriş Bilgilerinin Güvenliği**

#### Açıklama:
Parola güvenliğini sağlamak, kullanıcı hesaplarını korumanın temelidir.

#### Örnek Kod:
```php
// Kötü kod örneği
$password = $_POST['password'];

// Güvenli olmayan parola kullanımı
```

#### Çözüm:
```php
// Güvenli kod örneği
$password = password_hash($_POST['password'], PASSWORD_BCRYPT);
```

#### Açıklama:
`password_hash()` fonksiyonu kullanarak parolaları güvenli bir şekilde saklayabilirsiniz. Ayrıca, `password_verify()` ile kullanıcı girişlerini kontrol edebilirsiniz.

---

Bu örnekler, PHP uygulamalarında karşılaşılabilecek güvenlik açıklarını ve bu açıkları nasıl kapatılacağını anlamanıza yardımcı olabilir. Ancak, unutmayın ki güvenlik önlemleri sürekli olarak gözden geçirilmeli ve güncellenmelidir. Yeni güvenlik tehditlerine karşı daima hazır olmalısınız.
