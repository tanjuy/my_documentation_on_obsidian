
# 1. Laravel Yükleme:

## 1.1. PHP Yükleme:

```shell
sudo apt install php php-fpm php-xml php-curl
```

## 1.2. Composer Yükleme:

#### 1.2.1. Linux Depolarından:

```shell
sudo apt-get install composer 
```

#### 1.2.2. Composer Sitesinden:

```shell

```

# 2. Laravel Projesi Oluştur:

+ Laravel projesini oluşturmanın iki yolu vardır;
## Yöntem 1:

```shell
composer global require laravel/installer
```


> [!NOTE]
> + `laravel/installer` kaldırmak için;
> ```shell
> composer global remove laravel/installer
> ```

+ Sonrasında `~/.config/composer/vendor/bin` yolunu PATH'e eklemelisin;

**bashrc için:**

```shell
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.bashrc
```

+ Ayarlar geçerli olabilmesi için:

```shell
source ~/.bashrc
```

**zshrc için:**

+ Eğer **Zsh** kullanıyorsan (`echo $SHELL` çıktısı `/bin/zsh` ise), aşağıdaki komutu `.zshrc` için uygula:

```zsh
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.zshrc
```

+ Ayarlar geçerli olabilmesi için:

```shell
source ~/.zshrc
```


> [!CAUTION]
> + Yeni bir terminal açınız ve `laravel -V` komutunu veriniz.
> + Eğer `Laravel Installer 5.2.1` veriyorsa başarılı bir şekilde yüklenmiştir.


+ Yeni bir proje oluştur;

```shell
laralvel new proje
```

## Yöntem 2: Composer ile Proje oluşturma:

+ Yeni bir proje oluştur;

```shell
composer create-project laravel/laravel proje
```

## Yönetm 1 vs Yöntem 2:

### 1. `laravel new proje`

+ Bu komut **Laravel Installer** aracılığıyla proje oluşturur.


> [!NOTE]
> **Avantajları:**
> + Laravel dosyalarını **önbellekten** çok daha hızlı indirir.
> + Laravel'ın **en güncel sürümünü** kullanır.
> + İndirme sırasında `composer create-project`'e göre **daha az zaman** harcar.


> [!TIP]
> **🔧 Gereksinim:**
> + `composer global require laravel/installer` komutuyla kurulan `laravel` komut satırı aracı gerekir.
> + `PATH`'e `~/.config/composer/vendor/bin` eklenmiş olmalı.

### 2. `composer create-project laravel/laravel proje`

+ Bu komut Laravel projesini **doğrudan GitHub’daki kaynak koddan ve Composer üzerinden** indirir.


> [!NOTE]
> + Laravel Installer kurulu olmasa bile çalışır.
> + `--prefer-dist` gibi Composer seçenekleriyle özelleştirilebilir.
> + Daha çok **kontrollü ve Composer uyumlu** bir kurulum sağlar.


> [!TIP]
> ❗️ Dezavantajı:
> + Genellikle Laravel Installer’a göre daha **yavaş** çünkü her dosya yeniden indiriliyor.


| Özellik                               | `laravel new`                   | `composer create-project`     |
| ------------------------------------- | ------------------------------- | ----------------------------- |
| Hız                                   | Çok hızlı (önbellekli)          | Daha yavaş                    |
| Laravel Installer gerekir mi?         | Evet                            | Hayır                         |
| Sürüm kontrolü                        | En güncel sabit sürüm           | Belirli sürüm verilebilir     |
| Internet bağlantısına ihtiyacı        | İlk seferde evet, sonra daha az | Her zaman internetten indirir |
| Özelleştirilebilirlik (composer flag) | Hayır                           | Evet (örneğin `--no-dev`)     |


> [!NOTE]
> **🎯 Hangi Durumda Hangisini Kullanmalıyım?**
> + **Hızlıca proje başlatmak** istiyorsan → `laravel new proje-adi`
> + **Laravel Installer kurulu değilse** → `composer create-project laravel/laravel proje-adi`
> + **Sürüm kontrolü veya özelleştirme** gerekiyorsa → `composer create-project laravel/laravel:^10.0 proje-adi`

# 3. Yayınlama(Deploy):

## A. Geliştrime(Development):

```shell
ls -la proje
```

**ls çıktısı:**

```shell
total 392
drwxr-xr-x 12 www-data www-data   4096 Jun  9 13:51 .
drwxr-xr-x  3 www-data www-data   4096 Jun  9 13:51 ..
drwxr-xr-x  7 www-data www-data   4096 Jun  9 13:51 app
-rwxr-xr-x  1 www-data www-data   1686 Jun  9 13:51 artisan
drwxr-xr-x  3 www-data www-data   4096 Jun  9 13:51 bootstrap
-rw-r--r--  1 www-data www-data   1882 Jun  9 13:51 composer.json
-rw-r--r--  1 www-data www-data 299059 Jun  9 13:51 composer.lock
drwxr-xr-x  2 www-data www-data   4096 Jun  9 13:51 config
drwxr-xr-x  5 www-data www-data   4096 Jun  9 13:51 database
-rw-r--r--  1 www-data www-data    258 Jun  9 13:51 .editorconfig
-rw-r--r--  1 www-data www-data   1146 Jun  9 13:51 .env
-rw-r--r--  1 www-data www-data   1095 Jun  9 13:51 .env.example
-rw-r--r--  1 www-data www-data    186 Jun  9 13:51 .gitattributes
-rw-r--r--  1 www-data www-data    243 Jun  9 13:51 .gitignore
-rw-r--r--  1 www-data www-data    248 Jun  9 13:51 package.json
-rw-r--r--  1 www-data www-data   1134 Jun  9 13:51 phpunit.xml
drwxr-xr-x  2 www-data www-data   4096 Jun  9 13:51 public
-rw-r--r--  1 www-data www-data   4109 Jun  9 13:51 README.md
drwxr-xr-x  5 www-data www-data   4096 Jun  9 13:51 resources
drwxr-xr-x  2 www-data www-data   4096 Jun  9 13:51 routes
drwxr-xr-x  5 www-data www-data   4096 Jun  9 13:51 storage
drwxr-xr-x  4 www-data www-data   4096 Jun  9 13:51 tests
drwxr-xr-x 40 www-data www-data   4096 Jun  9 13:51 vendor
-rw-r--r--  1 www-data www-data    263 Jun  9 13:51 vite.config.js
```


```
cd proje; php artisan serve
```

> + `laravel new proje` ile oluşturduğumuz  dosya içerisine girmemiz gerekmektedir.
> + Eğer yukarıdaki çıktıyı incelerseniz `artisan` adında çalıştırılabilen dosyayı göreceksiniz!

**Çıktı:**

```shell

   INFO  Server running on [http://127.0.0.1:8000].

  Press Ctrl+C to stop the server

```

> + `http://127.0.0.1:8000` anlamı local yani bilgisayarın kendi yani iç ağ sisteminde yayına açacaktır.
> + Diğer bilgisayarlardan bu ağ ulaşamazsınız.
> + laravel'in çalıştığı makinede `localhost:8000` veya `127.0.0.1:8000` adresini tarayıcı girdiğinizde laravel'in `welcome.blade.php` sayfası gelecektir. 

+ Eğer diğer bilgisayarlarında bu ağ ulaşmasını yani diğer bilgisayarlarda yayınlamak isterseniz;

```shell
php artisan serve --host=192.168.1.132 --port=8000
```

> + `--host` parametresi ile bilgisayarın açık olan bir ara yüz(`interface`) ağınız yazabilirsiniz.
> + `--port` parametresi ile hangi port dinleneceğiniz ayarlayabilirsiniz.

**Çıktı:**

```shell

   INFO  Server running on [http://192.168.1.132:8000].

  Press Ctrl+C to stop the server

```

> + Tarayıcı gidip `http://192.168.1.132:8000` adresini girdiğinizde laravel'in `welcome.blade.php` sayfası gelecektir.

## B. Üretim(Production):


> [!CAUTION]
> 1. `laravel new proje` komutunu `ottoman` adlı home dizininde `proje` dosyasını oluşturuyoruz,
> 2. `cp -v /home/ottoman/proje /var/www/html/laravelDers` komutu ile `/var/www/html/laravelDers` dizinine kopyalıyoruz
> 3.  `sudo chown -R www-data:www-data /var/www/html/laravelDers/proje` 
> 	+ `proje` dizinin sahibini `www-data` yapıyoruz. Çünkü nginx kullanıcısı `www-data`'dır. Böylelikle nginx bu klasörü okurken izin ile ilgili sorunlar yaşamaz.

### Nginx:

**nginx.conf:**

```nginx
events {
    worker_connections 1024;
}

http {
    include mime.types;

	server {
        listen 8081;
        server_name 192.168.1.132;

        root /var/www/html/laravelDers/proje/public;

        index index.php;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
                include fastcgi.conf;
                fastcgi_pass unix:/run/php/php8.1-fpm.sock;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
	}
}
```

####  `$query_sting` nginx değişkeni:

##### Örnek 1:

+ Eğer kullanıcı tarayıcıdan şunu çağırırsa:

```
http://example.com/search?q=kitaplar&page=2
```

> + Buradaki `?q=kitaplar&page=2` kısmı — işte bu kısım **query string**'dir.
> + Anlamı: `$query_string = q=kitaplar&page=2`

##### 🎯 Laravel’in Nginx konfigürasyonunda:

```nginx
try_files $uri $uri/ /index.php?$query_string;
```

> 1.  İstenen dosya veya klasör varsa onu getir (`$uri`, `$uri/`)
> 2. Yoksa istek `index.php`'ye yönlendirilsin,
> 3. Ve varsa **sorgu parametreleri (`$query_string`) kaybedilmeden** `index.php`'ye iletilsin.
> 	+ Yani Laravel’in `Route::get()` gibi rotaları bu veriye erişebilir.


> [!TIP]
> + Eğer bu olmasaydı, URL’deki `?q=kitaplar` gibi veriler Laravel’e **hiç ulaşmazdı**, dolayısıyla `Request::query('q')` gibi ifadeler **boş** dönerdi.

##### Örnek 2: Laravel'de Query String'i Alma Yöntemleri

+ Tarayıcıdan şöyle bir URL isteği geldiğini düşünelim:

```bash
http://localhost:8000/arama?q=kitaplar&page=2
```

> Bu URL’de:
> + `/arama` → route (yol)
> + `?q=kitaplar&page=2` → query string (sorgu dizgisi)

**A) `Request` Sınıfı ile:**

```shell
sudo vim /var/www/html/laravelDers/proje/routes/web.php
```


```php
use Illuminate\Http\Request;

Route::get('/arama', function (Request $request) {
    $kelime = $request->query('q');
    $sayfa = $request->query('page');

    return "Arama kelimesi: $kelime - Sayfa: $sayfa";
});
```

+ GET isteği atıyoruz.

```shell
 curl "http://192.168.1.132:8081/arama?q=kitaplar&page=2"
```

+  curl komutun GET cevabı.

```shell
Arama kelimesi: kitaplar - Sayfa: 2
```
### Apache:


# MVC(Model-View-Controller):

+ Laravel'de **MVC (Model-View-Controller)**, uygulamanın yapısını düzenlemek ve kodun daha okunabilir, sürdürülebilir olmasını sağlamak için kullanılan bir yazılım mimarisidir.
+  Laravel, bu mimariyi temel alarak geliştirilmiş bir PHP framework'üdür.

## 1. Model(Veri Katmanı):

+ Veritabanı işlemlerini yönetir.
+ Veri ekleme, silme, güncelleme ve sorgulama işlemleri burada yapılır.
+ Veritabanı işlemleri model aracılığıyla yapılır.
+ Laravel’de her model genellikle bir veritabanı tablosuna karşılık gelir.
+ **Dizin Yolu:** `/var/www/html/laravelDers/proje/app/Models`

## 2. View:

+ Kullanıcıya gösterilen arayüzü (HTML, Blade şablonları) temsil eder.
+ Dinamik verileri göstermek için kullanılır.
+ HTML, CSS, JavaScript gibi şeyler burada yer alır.
+ Laravel'de genellikle `resources/views` klasöründe bulunur ve **Blade** şablon motoru kullanılır.
+ **Dizin Yolu:** `/var/www/html/laravelDers/proje/resources/views`
## 3. Controller:

+ Kullanıcıdan gelen istekleri işler.
+ Model ile veri alışverişi yapar ve sonucu View'e gönderir.
+ **Dizin Yolu:** `/var/www/html/laravelDers/proje/app/Http/Controllers`

## MVC Akışı(Laravel'de Nasıl Çalışır?)

1. **Kullanıcı** bir URL'ye istek gönderir (örneğin `/users/1`).
2. **Route** (`routes/web.php`), bu isteği ilgili **Controller** metoduna yönlendirir.

	```php
	Route::get('/users/{id}', [UserController::class, 'show']);
	```

3. **Controller**, **Model**'den veriyi çeker.
4. **Model**, veritabanı işlemlerini gerçekleştirir.
5. **Controller**, aldığı veriyi **View**'e gönderir.
6. **View**, kullanıcıya HTML olarak render edilir.

```shell
tree -L 1 proje
```

**Çıktı**

```shell
.
├── app
├── artisan
├── bootstrap
├── composer.json
├── composer.lock
├── config
├── database
├── package.json
├── phpunit.xml
├── public
├── README.md
├── resources
├── routes
├── storage
├── tests
├── vendor
└── vite.config.js
```

# web.php

## Örnek 1: String Dönüş

```shell
├── routes
│   ├── api.php
│   ├── channels.php
│   ├── console.php
│   └── web.php
```

+ Laravel'de `routes/web.php` dosyası, web arayüzü için rotaları (URL yönlendirmelerini) tanımladığınız ana dosyalardan biridir.
+ Bu dosya, HTTP isteklerini uygulamanızın ilgili controller metodlarına veya doğrudan closure(Anonim) fonksiyonlarına bağlar.


```shell
vim web.php
```

**web.php:**

```php
<?php

use Illuminate\Support\Facades\Route;

/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider and all of them will
| be assigned to the "web" middleware group. Make something great!
|
*/

Route::get('/', function () {
    return view('welcome');
});

Route::get('/linux', function () {
    return "Linux is Awesome!";
    // echo "Linux is Best!"
});

});
```

> + **URL'leri ve İlgili İşlemleri Eşleştirme:** Belirli bir URL'ye (örneğin, `/linux`) ulaşıldığında hangi kodun çalıştırılacağını (yani hangi **controller metodu**'nun çağrılacağını) tanımlarsınız.


```shell
curl -i http://192.168.1.132:8081/linux
```

**Çıktı:**

```http
HTTP/1.1 200 OK
Server: nginx/1.27.2
Content-Type: text/html; charset=UTF-8
Transfer-Encoding: chunked
Connection: keep-alive
Cache-Control: no-cache, private
Date: Tue, 10 Jun 2025 15:02:13 GMT
Set-Cookie: XSRF-TOKEN=eyJpdiI6IjRibUlzTWw2ejhMbVZPemk0WXNUZnc9PSIsInZhbHVlIjoiWjZzZG5YYnJKL0lGSVkxUzZtZExWdUNLdmo1dkFpNGhyS0dLL2hydE1OeVJDMlJmcXFJc0ZnNExMSFNhVGFURnlWMDFidG1uZmo0Vm5zMmdqbFFXbi9Zb2ZTU1pSQ1AwR0h3WnZvZ0hGby84R2Y2bG8yL2pKb1Z3SE9sdnA2bE8iLCJtYWMiOiI5NjhjNjgxZDBiZTExYWZiYjFhMjhiYzliZGFmZTBhYWVjMWMyMjk0MTNjYzg5ZDc0NjcwZWY3NzEyMzZjNzY1IiwidGFnIjoiIn0%3D; expires=Tue, 10 Jun 2025 17:02:13 GMT; Max-Age=7200; path=/; samesite=lax
Set-Cookie: laravel_session=eyJpdiI6Ik1ITTdwR2dxTlQ2UHhadm0vTTROMHc9PSIsInZhbHVlIjoiRjFNL0N6WGUySUxZQTQ1Wm1IbEhGaWlWYzduOUxaemM4WDNsTUIzeDF1ZmJnNGtMaFVoSnk1amlSQmg3Qzlra0NQaVdGQ1JmcnF6S1BxKzlveXlzWGd6RFZnRDFadVhUUmFrZ05kMTQ5Ujl0NlNqQ0tWRHVHbjJHNXh6UDhuQkQiLCJtYWMiOiI0MWMyN2U1ZTg3NjJmN2I4ZTU4YWMxMmFkNzhiMDRhODgwMTQ3ODVhOWVjZjBjMzIwOTBiZDIyZGQyMjVlNWQzIiwidGFnIjoiIn0%3D; expires=Tue, 10 Jun 2025 17:02:13 GMT; Max-Age=7200; path=/; httponly; samesite=lax

Linux is Best!
```

## Örnek 2:  `view()` fonksiyonu

**web.php:**

+ **Dosyanın dizin yolu:** `/var/www/html/laravelDers/proje/routes/web.php` 

```php
<?php

use Illuminate\Support\Facades\Route;

/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider and all of them will
| be assigned to the "web" middleware group. Make something great!
|
*/

Route::get('/', function () {
    return view('welcome');
});

Route::get('/iletisim', function () {
    return view('contact');
});

```


> [!NOTE]
> + `view()` fonksiyonu aslında Laravel'in `helpers.php` dosyasında tanımlanmış **global bir PHP fonksiyonudur**.
> ```shell
> vendor/laravel/framework/src/Illuminate/Foundation/helpers.php
> ```


**contact.blade.php:**

+ **Dosyanın dizin yolu:** `/var/www/html/laravelDers/proje/resources/views/contact.blade.php`

```php
<!DOCTYPE html>

<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>
		İletişim
	</title>
</head>

<body>
	<h2>"İletişim Sayfası view'den gelir"</h2>
</body>

</html>
```

