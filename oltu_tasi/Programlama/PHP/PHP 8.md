#programlama #php
# Php Ortam Kurulumu:

## Nignx ile:

```nginx
    worker_connections 1024;
}

http {
    include mime.types;


    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/phpDers/;

        index index.php index.html;

        location / {
            try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
            include fastcgi.conf;
            fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        }
    }
}
```


## Linux Terminal ile:

### a. Doğrudan Terminalde PHP Kodu Çalıştırma:

+ Terminalde doğrudan PHP kodu çalıştırmak için `php -r` komutunu kullanabilirsiniz.

```shell
php -r 'echo "Merhaba, Dünya!\n";'
```

**Çıktı:**
```shell
Merhaba, Dünya!
```

### b. PHP Dosyasını Çalıştırma:

+ Eğer bir PHP dosyası çalıştırmak istiyorsanız, öncelikle bir PHP dosyası oluşturun. Örneğin, `merhaba.php` adında bir dosya oluşturalım:

```shell
vim merhaba.php
```

**Php kodu:**
```php
<?php
echo "Merhaba, Dünya ;)\n";
?>
```

**Php kodu çalıştırma:**
```shell
php merhaba.php
```
> **Explanation:**
+ terminalde yukarıdaki komutu çalıştırarak PHP dosyasını çalıştırabilirsiniz.

**Çıktı:**
```shell
Merhaba, Dünya ;)
```

### c. PHP'nin Etkileşimli Kabuğunu Kullanma:

+ PHP, etkileşimli bir kabuk (interactive shell) sunar. Bu kabuğu kullanarak doğrudan terminalde PHP kodları yazıp çalıştırabilirsiniz.
+ Etkileşimli kabuğu başlatmak için terminalde aşağıdaki komutu çalıştırın:

```shell
php -a
```


> [!NOTE]
> + PHP'nin etkileşimli kabuğunu başlatır. Burada PHP kodlarınızı yazıp anında çıktılarını görebilirsiniz.
> +  Kabuktan çıkmak için `exit` yazabilir veya `Ctrl + D` tuş kombinasyonunu kullanabilirsiniz.


```php
Interactive shell

php > echo "Merhaba, Dünya";
Merhaba, Dünya
```

### PHP'nin Web Sunucusu Modunu Kullanma:
+ PHP, yerel bir web sunucusu başlatmak için de kullanılabilir. Bu özellik, hızlı bir şekilde PHP uygulamalarını test etmek için kullanışlıdır.
+ Örneğin, `merhaba.php` dosyasını yerel bir web sunucusunda çalıştırmak için aşağıdaki komutu kullanabilirsiniz:

```shell
php -S localhost:8000
```


```shell
php -S 192.168.1.132:8000
```

> **Explanation:**
+ `localhost` ile servis etiğimizde dış makinelerden ulaşım olmamaktadır. Ama makinenin IP(`192.168.1.132`) adresi ile servis yaptığımızda dış makinelerden ulaşılmaktadır.
+ Çünkü, `localhost`'un IP adresi `127.0.0.1` olmaktadır. Bu IP'İ dışarıya açık değildir.
+ Bu komut, `localhost:8000` adresinde bir web sunucusu başlatır. Tarayıcınızda `http://localhost:8000/merhaba.php` veya `http://192.168.1.132/merhaba.php` adresine giderek `merhaba.php` dosyasının çıktısını görebilirsiniz.


> [!CAUTION]
> + `php -S` komutu, `merhaba.php` dosyasının bulunduğu dizinde yani aynı klasörde çalıştırılmalıdır. 

# Php Kod Yazılımı:

## Merhaba Dünya:
**index.php:**
```php
<!DOCTYPE html>

<html>
    <head>
        <meta charset="UTF-8">
        <title>İlk Ders</title>
    </head>
    <body>
        <h1>
            <?php echo "Merhaba PHP";?>
        </h1>
    </body>
</html>
```
> **Explanation:**
+ `index.php` dosyasını nginx uygulaması veya `php -S` komutu ile servis edebiliriz.
+ Browser(tarayıcı), php dosyasını html dosyası gibi yorumlayacaktır.

```mermaid
graph LR
A(Server-Sunucu) --> B(PHP Interpreter) --> C(Browser-tarayıcı)
```

# Değişkenler:


> [!WARNING]
> + Php de değişkenler `case sensitive`'dir yani büyük küçük harf duyarlıdır.
> + Örneğin; `$sayi1 = 12` ile `$Sayi2 = 16` aynı değişken değildir. Çünkü ikinci değişken S ile başlamaktadır. 


### Temel Kullanımı 1:
**index.php:**
```php
<!DOCTYPE html>

<?php
    $title = "Merhaba PHP ;)";  # Değişken tanımlama
?>

<html>
    <head>
        <meta charset="UTF-8">
        <title>İlk Ders</title>
    </head>
    <body>
        <h1>
            <?php echo $title;?> # Değişkeni çağırma
        </h1>
    </body>
</html>
```
> **Explanation:**
+ İki tane php bloğu oluşturduk. İlk php bloğunda değişken tanımladık, ikinci php bloğunda oluşturulan değişken çağrıldı.

### Temel Kullanımı 2:

```php
<?php
    $isim = "Tanju";
    $soyad = "Yücal";

    echo $isim." ".$soyad;
?>
```
> **Explanation:**
+ Değişken yazarken değişkenlerin `$` başladığına dikkat ediniz!
+ Nokta(`.`) işareti değişkenlerdeki `string`'leri birleştirir.

**Php Sunucu Başlatma:**
```shell
php -S 192.168.1.132:8082 variables.php
```
> **Explanation:**
+ Eğer  `variable.php` dosyasını parametre olarak vermezsek `php -S` komutu `index.php` dosyasını bakacaktır.

**GET isteği:**
```http
HTTP/1.1 200 OK
Host: 192.168.1.132:8082
Date: Wed, 05 Feb 2025 14:56:35 GMT
Connection: close
X-Powered-By: PHP/8.1.2-1ubuntu2.20
Content-type: text/html; charset=UTF-8

Tanju Yücal
```

# Yorum Satırı:
+ Yorum satırları, kodunuzu açıklamak veya belirli bölümlerini geçici olarak devre dışı bırakmak için kullanılır.
+ Yorum satırları, PHP yorumlayıcısı tarafından dikkate alınmaz ve kodun çalışmasını etkilemez.

> [!NOTE]
> + Yorumlar, kodun okunabilirliğini artırmak ve diğer geliştiricilere veya gelecekteki kendinize açıklamalar bırakmak için önemlidir.

## Tekli Yorum Satırı:
+ `//` ve `#` ile başlayan yorumlar, sadece o satırı etkiler.


```php
<?php
// Bu bir tek satırlık yorumdur.
echo "Yorum satırı işareti: //";

# Bu da başka bir tek satırlık yorum satırıdır.
echo "Başka yorum satırı işareti: #";
?>
```

## Çoklu Yorum Satırı:

```php
<?php
/*
Değişken isminde boşluk karakteri olmaz!
$sayi 1        => yanlış
$sayi1 = 19;   => doğru
*/
?>
```


# PHP Veri Tipleri:
## 1. Basit (Skaler) Veri Türleri:
+ Bu türler, tek bir değer tutar.
### a. Integer(Tam Sayı):
- Pozitif veya negatif tam sayıları temsil eder. Örnek: `45`, `-12`, `0`, `3`
- Bellekte genellikle 32 veya 64 bit olarak saklanır.

```php
<?php
$sayi = 42;
echo gettype($sayi);    // Çıktı: integer
echo "<br>";
echo var_dump($sayi);   // Çıktı: int(42)
?>
```

### b. Float (Ondalıklı Sayı veya Double):
- Ondalıklı sayıları temsil eder. Örnek: `3.14`, `-0.6`, `4.0`, `3.9`
- Bellekte genellikle 64 bit olarak saklanır.

```php
<?php
$ondalik = 3.14;
echo gettype($ondalik);  // Çıktı: double
echo "<br>"
echo var_dump($sayi);    // Çıktı: float(3.14)
?>
```

### c. String(Metin):
- Metin verilerini temsil eder. 
- Tek tırnak (`'`) veya çift tırnak (`"`) içinde yazılır. Örnek: `"Merhaba Dünya"`, `'PHP'`


```php
<?php
$metin = "PHP Programlama";
echo gettype($metin);     // Çıktı: string
echo "<br>";
echo var_dump($metin);    // Çıktı: string(15) "PHP Programlama"
?>
```

#### c.1. Tek Tırnak(`'`) ile Tanımlama:
+ Tek tırnak içindeki stringler, özel karakterler (örneğin `\n`, `\t`) ve değişkenler genişletilmez (interpolasyon yapılmaz).
+ `Bash Script` ile aynı şekilde kullanılıyor!

```php
<?php
$isim = 'linux';
$metin = 'Merhaba $isim';
echo $metin;               // Çıktı: Merhaba $isim
?>
```

#### c.2. Çift Tırnak(`"`) ile Tanımlama:
- Çift tırnak içindeki string'ler, özel karakterler ve değişkenler genişletilir (interpolasyon yapılır).
- `Bash Script` de aynı kullanım geçerlidir.

##### `$variable`:
```php
<?php
$isim = 'ubuntu';
$metin = "Merhaba $isim";
echo $metin;                // Çıktı: Merhaba ubuntu
?>
```

##### `${variable}`:
+ Küme parantezleri (`{}`), değişkenin sınırlarını belirlemek için kullanılır.
+ `{}` (küme parantezleri) kullanmak daha net ve güvenli bir kod yazmanızı sağlar.

```php
<?php
$distro = 'Arch Linux';
$metin = "En sevdiğim linux dağıtımı {$distro}";
echo $metin;
?>
```

##### `${variable}`: Yeni değişken
+ Küme parantezleri (`{}`), değişkenin sınırlarını belirlemek için kullanılır.
+ Bazen değişken adı, string içindeki diğer karakterlerle karışabilir.

```php
<?php
$prefix = 'Fedora';                     // distro değişkeni
$suffix = 'x64';                        // mimari değişkeni
$OS_distro="${prefix}_${suffix}"        // yeni değişken
?>
```
> **Explanation:**
> - Süslü parantezler ile yeni bir değişken oluşturduk.
> - Eğer süslü parantez(`{...}`) kullanmasaydık, `$prefix` değişkenin ve `$suffix` değişkenin nerede başlayıp nerede bittiğini  php yorumlayıcı anlayamızdı.

#### c.3. Heredoc Syntax:
- Uzun metinler için kullanılır. `<<<` ile başlar ve bir tanımlayıcı ile biter. Çift tırnak gibi davranır (değişkenler ve özel karakterler genişletilir).

```php
<?php
$distro = "Arch Linux";   // veya $distro = 'Arch Linux';
$metin = <<<EOT
Favori linux dağıtımım $distro
Linux is Awesome!
EOT;
echo $metin;
?>
```

#### c.4. Nowdoc Syntax:
- Heredoc'a benzer, ancak tek tırnak gibi davranır (değişkenler ve özel karakterler genişletilmez).

```php
<?php
$distro = "Fedora";    // veya $distro = "Fedora";
$metin = <<< 'EOT'
Another favori linux dağıtımım $distro
Linux is Awesome!
EOT;
?>
```

#### c.5. String Karakterlerine Erişim:
- Stringler, dizi gibi indekslenebilir. Karakterlere `[]` ile erişilir.

```php
<?php
$distro = "Linux is Awesome";
echo $distro[0];                // Çıktı: L
echo "<br>";
echo $metin[6];                 // Çıktı: i
?>
```


> [!CAUTION]
> +  PHP 8 de String'in indeks değerin ulaşmada köşeli parantez(`[]`) kullanılır. Eğer süslü parantez(`{}`) hata verecektir.
> + PHP  de String'in indeks değerin ulaşmada köşeli parantez(`[]`) ve süslü parantez(`{}`) kullanılır.


### d. Boolean (Mantıksal Değer):
- `true` (doğru) veya `false` (yanlış) değerlerini temsil eder.
- Genellikle koşul ifadelerinde kullanılır.

```php
<?php
$mantiksal = true;
echo gettype($metin);     // Çıktı: boolean
echo "<br>";
echo var_dump($metin);    // Çıktı: bool(true)
?>
```

## 2. Birleşik (Compound) Veri Türleri:
+ Bu türler, birden fazla değer veya karmaşık veri yapıları tutar.

### a. Array(Dizi):
- Birden fazla değeri bir arada tutar.
- İndeksli (numeric) veya ilişkili (associative) diziler olabilir. Örnek: `[1, 2, 3]`, `["ad" => "Ahmet", "yas" => 25]`

```php

```

## 3. Özel (Special) Veri Türleri:

# PHP operatörleri:

## 1. Nokta(`.`) operatörü:
+ PHP'de nokta (`.`) operatörü, **string birleştirme** (concatenation) işlemi için kullanılır.
+  İki veya daha fazla stringi birleştirmek veya stringlerle diğer veri türlerini (örneğin integer, float, boolean) birleştirmek için kullanılır.

### Nokta Operatörün Kullanımı:
+ İki stringi birleştirmek için kullanılır.
+ String ile diğer veri türlerini birleştirmek için kullanılır.
+ Birden fazla birleştirme işlemi yapılabilir.

### İki Stringi Birleştirme:
```php
<?php
$ad = "Tanju";
$soyad = "Yücal";
echo $ad . " " . $soyad; // Çıktı: Ahmet Yılmaz
?>
```

### String ile Integer Birleştirme:
```php
<?php
$yas = 25;
echo "Yaşınız: " . $yas; // Çıktı: Yaşınız: 25
?>
```

### Birden Fazla Birleştirme:
```php
<?php
$sayi1 = 10;
$sayi2 = 20;
echo "Sayıların toplamı: " . ($sayi1 + $sayi2); // Çıktı: Sayıların toplamı: 30
?>
```

### Değişkenlerle Birleştirme:
```php
<?php
$urun = "Bilgisayar";
$fiyat = 5000;
echo $urun . " fiyatı: " . $fiyat . " TL"; // Çıktı: Bilgisayar fiyatı: 5000 TL
?>
```

### Nokta Operatörü ile Atama:
```php
<?php
$metin = "Merhaba";
$metin .= " Dünya!"; // $metin değişkenine " Dünya!" ekler.
echo $metin; // Çıktı: Merhaba Dünya!
?>
```



> [!IMPORTANT]
> + PHP'de stringlerle çalışırken nokta operatörü, metinleri birleştirmenin en temel ve etkili yoludur.
> + Diğer programlama dillerinde (örneğin, JavaScript'te `+` operatörü) string birleştirme farklı şekilde yapılır, ancak PHP'de bu işlem için özel olarak nokta (`.`) operatörü kullanılır.



> [!CAUTION]
> + Nokta operatörü, sadece string birleştirme için kullanılır. Matematiksel işlemlerde kullanılmaz.
> + Eğer birleştirilecek değerler string değilse (örneğin integer, float), PHP otomatik olarak bu değerleri stringe dönüştürür.

## 2. Artı(`+`) operatörü:
+ PHP'de `+` operatörü, **matematiksel toplama işlemi** yapmak için kullanılır. Bu operatör, sayısal değerler (integer, float) üzerinde çalışır ve bu değerleri toplar.
+ Ancak, PHP'de `+` operatörü string birleştirme işlemi için kullanılmaz (string birleştirme için nokta `.` operatörü kullanılır).

### 2.1. İki Integer Sayıyı Toplama:

```php
<?php
$sayi1 = 10;
$sayi2 = 20;
echo $sayi1 + $sayi2; // Çıktı: 30
?>
```
### 2.2. Integer ve Float Sayıyı Toplama:

```php
<?php
$sayi1 = 5;
$sayi2 = 3.5;            // Float Sayı
echo $sayi1 + $sayi2;   // Çıktı: 8.5
?>
```

### 2.3. String ve Sayıyı Toplama:
+ PHP, `string` içinde sayısal bir değer varsa otomatik olarak sayıya dönüştürür.

```php
<?php
$sayi1 = "10"; // String içinde sayısal değer
$sayi2 = 20;
echo $sayi1 + $sayi2; // Çıktı: 30
?>
```

### 2.4. Geçersiz String Durumu:

```php
<?php
$sayi1 = "10abc"; // Geçersiz string
$sayi2 = 20;
echo $sayi1 + $sayi2; // Çıktı: 20 (10abc, 10 olarak kabul edilir)
?>
```
> **Explanation:**
> + Birinci değişken(`$sayi1`) hem sayı hem de alfabeden oluşuyorsa ve ikinci değişken(`$sayi2`) tam sayıdan oluşmak şartı ile birinci değişken(`$sayi1`) 10, ikinci değişken(`$sayi2`) 20 olarak toplanır.


### 2.5. Boolean Değerlerle Kullanım:
+ Boolean değerler (`true` veya `false`) sayısal olarak `1` ve `0` olarak kabul edilir:

# Language Construct:
+ **Dil yapıları (language constructs)**, PHP'nin temel bileşenleri olup, fonksiyon gibi çalışabilen ancak aslında **fonksiyon olmayan** özel komutlardır.

## Özellikleri:
+ **Fonksiyon değildir**, bu yüzden parantez kullanmak zorunlu değildir.
+ PHP’nin kendi sözdizimine (syntax) gömülüdür.
+ **Daha hızlı çalışır** çünkü fonksiyon çağrısı yapmaz.
+ **Bazen birden fazla argüman alabilir (örneğin, `echo`)**.
+ **Bazıları bir değer döndürmez (örneğin, `echo`), bazıları döndürebilir (örneğin, `isset()`)**.

## Fonksiyon ile Dil Yapısı Arasındaki Fark:
1. Fonksiyonlar parantez gerektirir:

```php

```

2. sd


## 1. echo:
+ PHP'de `echo`, **dizileri (array) doğrudan ekrana basamaz**. Bunun nedeni, `echo`'nun yalnızca **string** (metin) veya string'e dönüştürülebilen değerler (sayılar, boolean gibi) ile çalışmasıdır.
+ Diziler ise doğrudan string'e dönüştürülemez.

### Örnek 1: Hata

```php
<?php
$array = [1, 2, 3];    // Basit bir dizi(array) tanımlanmış
echo $array;
?>
```
> **Explanation:**
> + Eğer bir diziyi `echo` ile ekrana basmaya çalışırsanız, PHP şu hatayı verir: PHP Warning:  Array to string conversion in ...
> + Hata mesajı durumu çok güzel açıklamaktadır; dizinin(array), string veri tipine dönüştürülemiyor ...


# Karşılaştırma Operatörleri:



# Koşullu İfadeler:
+ PHP 8'de `if` koşulları, programın belirli bir kod bloğunu yalnızca belirli bir koşul sağlandığında çalıştırmasını sağlayan yapılardır.
+ `if` koşulları, bir mantıksal ifadeyi değerlendirir ve bu ifade `true` (doğru) olduğunda ilgili kod bloğunu çalıştırır. Eğer koşul `false` (yanlış) ise, kod bloğu atlanır.

## if statement:
### Syntax:
```php
if (koşul) {
    // Koşul true ise bu kod bloğu çalışır
}
```

### Örnek 1: 
```php
<?php
$age = 18;

if ($age >= 18) {              // Çıktı: You are an adult.%
	echo "You are an adult.";   
}
?>
```
> **Explanation:**
> + Bu örnekte, `$age` değişkeni 18'e eşit veya büyükse, `echo` ifadesi çalışır ve ekrana "You are an adult." yazdırılır.
> + `php index.php` komutu ile kodu çalıştırdık.

## `if-else` statement:
+ Eğer koşul `false` ise, alternatif bir kod bloğu çalıştırmak için `else` kullanılır.

### Syntax:
```php
if (koşul) {
    // Koşul true ise bu kod bloğu çalışır
} else {
    // Koşul false ise bu kod bloğu çalışır
}
```

### Örnek 1:
```php
<?php
$age = 15;

if ($age >= 18) {             // Çıktısı: You are a minor.%
	echo "You are an adult.";
} else {
	echo "You are a minor.";
}
?>
```
> **Explanation:**
> + Bu örnekte, `$age` değişkeni 18'den küçük olduğu için `else` bloğu çalışır ve ekrana `You are a minor.` yazdırılır.
> + `php index.php` komutu ile kodu çalıştırdık.

## `if-elseif-else` statement:
+ Birden fazla koşulu kontrol etmek için `elseif` kullanılır. Bu yapı, ilk `if` koşulu `false` olduğunda diğer koşulları sırayla kontrol eder.
### Syntax:
```php
if (koşul1) {
    // Koşul1 true ise bu kod bloğu çalışır
} elseif (koşul2) {
    // Koşul2 true ise bu kod bloğu çalışır
} else {
    // Yukarıdaki koşulların hiçbiri true değilse bu kod bloğu çalışır
}
```

### Örnek 1:
```php
<?php
$score = 85;

if ($score >= 90) {          // Çıktısı: 
    echo "Grade A";
} elseif ($score >= 80) {
    echo "Grade B";
} elseif ($score >= 70) {
    echo "Grade C";
} else {
    echo "Grade F";
}
?>
```

> **Explanation:**
> + Bu örnekte, `$score` değişkeni 85 olduğu için ikinci `elseif` koşulu (`$score >= 80`) `true` olur ve ekrana "Grade: B" yazdırılır.

## İç içe `if` statement:

+ `if` koşulları, başka bir `if` koşulunun içine yerleştirilebilir. Buna iç içe `if` yapısı denir.

### Syntax:
```php
if (koşul1) {
    if (koşul2) {
        // Hem koşul1 hem de koşul2 true ise bu kod bloğu çalışır
    }
}
```

### Örnek 1:

```php
<?php
$age = 20;
$hasLicense = true;

if ($age >= 18) {               // Çıktısı: You can drive%
    if ($hasLicense) {
        echo "You can drive";
    } else {
        echo "You are old enough but need a license.";
    }
} else {
    echo "You are too young to drive!";
}
?>
```
> **Explanation:**
> + Bu örnekte, `$age` 18'den büyük ve `$hasLicense` `true` olduğu için ekrana "You can drive." yazdırılır.
> + `php index.php` komutu ile kodu çalıştırdık.

### Ternary Operatör:
+ PHP'de basit `if-else` koşullarını tek satırda yazmak için **ternary operatör** kullanılır.

### Syntax:
```php
koşul ? true_değer : false_değer;
```

### Örnek 1:
```php
<?php
$age = 20;
echo ($age >= 18) ? "Adult" : "Minor";   // Çıktı: Adult%
?>
```
> **Explanation:**
> + Bu örnekte, `$age` 18'den büyük olduğu için ekrana "Adult" yazdırılır.
> + `php index.php` komutu ile kodu çalıştırdık.

## `if` Koşullarında Mantıksal Operatörler:
+ `if` koşullarında birden fazla koşulu birleştirmek için mantıksal operatörler kullanılır:
### And operatör ile:
 + and operatörü  `&&` ile simge edilir, her iki koşul doğru olduğunda `true` verir. 
 
```php
<?php
$age = 20;
$hasLicense = true;

if ($age >= 18 && $hasLicense) {        // Çıktısı: You can drive.%
	echo "You can drive.";
} else {
	echo "You can not drive!";
}
?>
```
> **Explanation:**
> + Bu örnekte, hem `$age` 18'den büyük hem de `$hasLicense` `true` olduğu için ekrana `You can drive.` yazdırılır.
> + `php index.php` komutu ile kodu çalıştırdık.

## Match Expression:
+ PHP 8'de **`match` expression**, `switch` ifadesine benzer bir yapıdır ancak daha güçlü ve güvenli bir alternatif olarak geliştirilmiştir.
+ `match`, **değer döndüren** bir ifadedir ve **katı (strict) karşılaştırma (`===`)** kullanır.

### Örnek 1: Temel Kullanım
```php
<?php
$status = 200;

$message = match($status) {
    200 => "OK",
    404 => "Not Found",
    500 => "Server Error",
    default => "Unknown Status",
};

echo "$message\n";
?>
```

### `match` ile `switch` Arasındaki Farklar:
| Özellik                  | `match`             | `switch`                              |
| ------------------------ | ------------------- | ------------------------------------- |
| **Katı Karşılaştırma**   | `===` kullanır      | `==` kullanır                         |
| **Değer Döndürme**       | Değer döndürür      | Döndürmez, `break` gerekir            |
| **Daha Az Yazım Hatası** | `break` gerektirmez | `break` yazılmazsa hatalı çalışabilir |
| **Tek Satır Kullanım**   | Mümkün              | Daha zor                              |

# Girdi Alma:
+ PHP'de kullanıcıdan girdi almak için farklı yöntemler kullanılabilir.
+ Bu yöntemler, girdinin kaynağına (örneğin, web formları, komut satırı, vs.) bağlı olarak değişir. İşte PHP'de girdi almanın en yaygın yöntemleri:

## 1. Web Formlarından Girdi Almak (POST ve GET Yöntemleri):
+ Web uygulamalarında, kullanıcıdan genellikle HTML formları aracılığıyla girdi alınır.
+ PHP'de bu girdiler `$_POST` ve `$_GET` süper global değişkenleriyle işlenir.


**nginx.conf**
```nginx
user www-data;

worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include mime.types;
    send_timeout 10s;


    server {
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/phpDers/;

        index form.html;

        location / {
            charset utf-8;
            try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
            include fastcgi.conf;
            fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        }
    }

}
```
> **Explanation:**
> 

### Örnek 1: POST Yöntemi:

**form.html**
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>İlk Ders</title>
    </head>
    <body>
        <h1>
            POST ile Veri Girdisi
        </h1>
                <!-- form.html -->
                <form action="process.php" method="post">
                    Name: <input type="text" name="name"><br>
                    Age: <input type="number" name="age"><br>
                    <input type="submit" value="Submit">
                </form>
    </body>
</html>
```
> **Explanation:**
> + `form.html` dosyasını nginx'de `root directifin` parametresi olan dizininde(`/var/www/html/phpDers/`) oluşturuyoruz.

**process.php**
```php
<?php
// process.php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = $_POST['name'];
    $age = $_POST['age'];

    echo "Name: " . htmlspecialchars($name) . "<br>";
    echo "Age: " . htmlspecialchars($age);
}
?>
```
> **Explanation:**
> + `process.php` dosyasını nginx de `root` direktifin işaret ettiği dizininde(`/var/www/html/phpDers/`) oluşturuyoruz.
> + `$_POST`: Formdan gönderilen verileri alır. Veriler HTTP POST yöntemiyle gönderilir.
> + `htmlspecialchars()`: Güvenlik için kullanıcı girdisini HTML özel karakterlerden temizler.

### Örnek 1: GET Yöntemi:

**form.html**
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>İlk Ders</title>
    </head>
    <body>
        <h1>
            GET ile Veri Girdisi
        </h1>
			<!-- form.html -->
			<form action="process.php" method="get">
			    Search: <input type="text" name="query"><br>
			    <input type="submit" value="Search">
			</form>
    </body>
</html>
```
> **Explanation:**
> + `form.html` dosyasını nginx'de `root` direktifin parametresi olan dizininde(`/var/www/html/phpDers/`) oluşturuyoruz.

**process.php**
```php
<?php
// process.php 
if ($_SERVER["REQUEST_METHOD"] == "GET") {
    $query = $_GET['query'];

    echo "You searched for: " . htmlspecialchars($query);
}
?>
```
> **Explanation:**
> + `process.php` dosyasını nginx de `root` direktifin işaret ettiği dizininde(`/var/www/html/phpDers/`) oluşturuyoruz.
> + `$_GET`: URL üzerinden gönderilen verileri alır. Veriler HTTP GET yöntemiyle gönderilir.

## 2. Komut Satırından Girdi Almak (CLI):
+ PHP, komut satırından çalıştırıldığında kullanıcıdan girdi almak için `fgets(STDIN)` veya `readline()` fonksiyonlarını kullanabilir.

### Örnek 1: `fgets(STDIN)` ile Girdi Almak
```php
<?php
echo "Enter your name: ";
$name = fgets(STDIN);     // Kullanıcıdan Girdi Alır.
echo "Hello, ".trim($name)."\n"; // // trim() ile boşlukları temizle
?>
```
# Döngüler(loops):
+  PHP 8'de **loop** (döngü) yapıları, belirli bir işlemi tekrarlamak için kullanılır. PHP'de temel olarak dört tür döngü bulunur:
## 1. For Döngüsü:

+ `for` döngüsü, genellikle bir başlangıç değeri(`start`), bir koşul(`condition`) ve bir artış/azalış(`increase/decrease`) adımı içerir.  Bu yapı, döngünün kaç kez çalışacağını kontrol etmek için idealdir.

### Syntax:
```php
for (start; condition; increase/decrease) {
	loop code block
}
```
> **Explanation:**
> 1. **start:** Döngü başlamadan önce bir kez çalıştırılır. Genellikle bir sayaç değişkeni(`counter variable`) tanımlanır (örneğin, `$i = 0`).
> 2. **condition:** Her iterasyondan(`iteration`) önce kontrol edilir. Koşul doğru (`true`) olduğu sürece döngü devam eder.
> 3. **increase/decrease:** Her iterasyondan(`iteration`) sonra çalıştırılır. Genellikle sayaç değişkenini(`counter variable`) artırır veya azaltır (örneğin, `$i++`).


> [!NOTE]
> + for döngüleri PHP'deki en karmaşık döngülerdir. C'deki muadilleri gibi davranırlar.

### Örnek 1:  Temel Kullanımı

```php
<?php
for ($i = 0; $i < 5; $i++) {
	echo "Number: $i\n";
}
?>
```
> **Explanation:**
> - `$i = 0`: Sayaç değişkeni(`counter variable`) `0` olarak başlatılır.
> - `$i < 5`: Koşul, `$i` değeri `5`'ten küçük olduğu sürece döngü devam eder.
> `$i++`: Her iterasyondan(`iteration`) sonra `$i` değeri `1` artar.

### Örnek 2:  Geriye Doğru Sayma

```php
for ($i = 10; $i > 0; $i--) {
	echo "Number: $i\n";
}
```
> **Explanation:**
> - `$i = 10`: Sayaç değişkeni(`counter variable`) `10` olarak başlatılır.
> - `$i > 0`: Koşul, `$i` değeri `0`'dan büyük olduğu sürece döngü devam eder.
> - `$i--`: Her iterasyondan(`iteration`) sonra `$i` değeri `1` azalır.

### Örnek 3: Birden Fazla Değişken ile
+ `for` döngüsünde birden fazla değişkeni aynı anda kontrol edebilirsiniz.

```php
for ($i = 0, $j = 10; $i < 10, $j > 0; $i++, $j--) {
    echo "i: $i, j: $j\n";
}
```
> **Explanation:**
> + `$j > 0` çıkarırsak aynı çıktı verecektir. Çünkü `for` döngüsü ` $i < 10` koşulu sağladığı sürece  çalışacaktır. 
> + `for ($i = 0, $j = 10; $i < 10; $i++, $j--) ` döngüsü yukarıdaki ile aynı çıktıyı verecektir.
> + `$i = 0, $j = 10`: İki değişken başlatılır.
> + `$i < 10`: Koşul, `$i` değeri `10`'dan küçük olduğu sürece döngü devam eder.
> + `$i++, $j--`: Her iterasyondan(`iteration`) sonra `$i` artar ve `$j` azalır.

### Örnek 4: Dizi Üzerinde `for` döngüsü

```php
<?php
$fruits = ['Elma', 'Muz', 'Portakal', 'Çilek'];

for ($i = 0; $i < count($fruits); $i++) {
    echo "Meyve: " . $fruits[$i] . "\n";
}
?>
```
> **Explanation:**
> + `count()` fonksiyonu, bir dizideki eleman sayısını veya bir nesnedeki özellik sayısını döndüren yerleşik bir fonksiyondur.


## 2. While Döngüsü:
+ PHP 8'de `while` döngüsü, belirli bir koşul doğru olduğu sürece kod bloğunu tekrar tekrar çalıştıran bir döngü yapısıdır.
### Syntax:

```php
while (condition) {
	loop code block
}
```
> **Explanation:**
> + Döngü, belirtilen **koşul (condition)** `true` olduğu sürece çalışmaya devam eder. Koşul `false` olduğunda döngü sona erer.

### Örnek 1: Temel Kullanımı

```php
<?php
$counter = 1;

while ($counter <= 5) {
    echo "Sayı: $counter\n";
    $counter++;
}

?>
```
> **Explanation:**
> - `$counter = 1`: Sayaç değişkeni `1` olarak başlatılır.
> - `$counter < 5`: Koşul, `$counter` değeri `5`'ten küçük olduğu sürece döngü devam eder.
> - `$counter++`: Her iterasyondan(`iteration`) sonra `$counter` değeri `1` artar.


> [!WARNING]
> + `counter++`  yorum satırı yaparsak `while` döngüsü sonsuz bir döngüye girecektir.
> + Çünkü, `$counter <= 5` her zaman doğru olacağı için sonsuz döngüde olacaktır.
> + Bu tür durumlardan kaçınmak için döngü içinde koşulu değiştirecek bir ifade kullanılmalıdır.

### Örnek 1: Array

```php
<?php
$prog_lang = ['PHP', 'Python', 'Javascript', 'Java'];
$index = 0;

while ($index < count($prog_lang)) {
    echo "Program Language: ".$prog_lang[$index++]."\n";
}
?>
```
> **Explanation:**
> - `count($meyveler)`: Dizinin uzunluğunu alır.
> - `$index < count($meyveler)`: Koşul, dizinin tüm elemanları üzerinde dolaşana kadar devam eder.
> - `$index++`: Her iterasyondan(`iteration`) sonra `$index` değeri `1` artar.


> [!TIP]
> `while` Döngüsünün Avantajları:
> - **Esneklik**: Koşulun ne zaman sonlanacağı dinamik olarak belirlenebilir.
> - **Kontrol Kolaylığı**: Özellikle koşulun başlangıçta bilinmediği durumlarda kullanışlıdır.
> - **Okunabilirlik**: Koşulun başlangıçta kontrol edilmesi, kodun daha anlaşılır olmasını sağlar.

## 3. Do-while Döngüsü:
+ PHP 8'de **`do-while` döngüsü**, bir koşul doğru (`true`) olduğu sürece tekrarlanacak işlemler için kullanılan bir döngü türüdür.


> [!TIP]
> + `while` döngüsünden farklı olarak, `do-while` döngüsü **koşulu döngünün sonunda kontrol eder**.
> + Bu nedenle, `do-while` döngüsü **en az bir kez çalışır**, koşul baştan yanlış (`false`) olsa bile.

### Syntax:
```php
do {
    // Koşul doğru olduğu sürece çalışacak kodlar
} while (condition);
```
> **Explanation:**
> - **do**: Döngü bloğu, koşul kontrol edilmeden önce bir kez çalıştırılır.
> - **while (koşul)**: Döngü bloğu çalıştıktan sonra koşul kontrol edilir. Koşul doğru (`true`) olduğu sürece döngü tekrarlanır.

### Örnek 1: Temel Kullanımı:
```php
<?php
$i = 0;

do {
    echo "Sayı: $i\n";
    $i++;              // Her döngüde sayı artar.
} while ($i < 5);
?>
```
> **Explanation:**
> + Eğer `$i = 6` yaparsak ekrana `0` yazar ve durur. Çünkü koşul sağlanmaz ise en az bir kez çalışır.

### Örnek 2: Kullanıcı Girişi Kontrolü

+ `do-while` döngüsü, kullanıcıdan geçerli bir girdi alınana kadar tekrarlanacak işlemler için idealdir.

```php
<?php
do {
    $input = readline('Please, enter a number(1-10 arası): ');
} while ($input < 1 || $input > 10);

echo "Geçerli Sayı: $input\n";
?>
```
> **Explanation:**
> - Kullanıcıdan bir sayı girmesi istenir.  Girilen sayı `1` ile `10` arasında değilse, döngü tekrarlanır.
> - Geçerli bir sayı girildiğinde döngü sonlanır ve sonuç yazdırılır.


> [!TIP]
> - **En Az Bir Kez Çalışır**: Koşul baştan yanlış olsa bile döngü bloğu bir kez çalışır.
> - **Kullanıcı Etkileşimi**: Kullanıcıdan girdi alınması veya belirli bir koşul sağlanana kadar işlem yapılması gereken durumlarda kullanışlıdır.
> - **Esneklik**: Koşulun döngü sonunda kontrol edilmesi, bazı senaryolarda daha uygun olabilir.

## 4. Foreach Döngüsü:

# Array (Dizi):

+ PHP 8'de **array** (dizi), birden fazla değeri tek bir değişkende saklamak için kullanılan bir veri yapısıdır.
+ Diziler, farklı veri türlerini (string, integer, float, object, vs.) içerebilir ve bu değerlere anahtarlar (key) veya indeksler (index) aracılığıyla erişilebilir.
+ PHP'de diziler iki türde olabilir:
	1. **İndeksli Diziler**: Değerler sıralı bir şekilde saklanır ve her bir değere bir indeks numarası ile erişilir.
	2. **Associative Diziler**: Değerler, anahtar-değer çiftleri şeklinde saklanır. Her bir değere bir anahtar (key) ile erişilir.


## 1. İndeksli Diziler:

### Örnek 1:
```php
<?php
$fruits = ['Elma', 'Muz', 'Portakal'];
echo "$fruits[0] \n";    // Çıktı: Elma
echo "$fruits[1] \n";    // Çıktı: Muz
?>
```

## 2. Associative Dizi:

```php
<?php
$person = [
    'name' => 'Tanju',
    'department' => 'Biology',
    'city' => 'İstanbul'
];

echo $person['name'] . "\n";
echo $person['department'] . "\n";
?>
```

## 3. Çok Boyutlu Dizi:
+ **İndeksli dizini** içerisinde **associate diziler** oluşturduk.

```php
<?php
$students = [
    ['name' => 'Ali', 'not' => 85],
    ['name' => 'Veli', 'not' => 90]
];

echo $students[0]['name'] . "\n";
echo $students[1]['not'] . "\n";
?>
```

# Fonksiyonlar:

## Built-in Fonksiyonlar:
+ PHP'nin çekirdek kütüphanesinde bulunur ve herhangi bir ek kurulum veya eklenti gerektirmeden doğrudan kullanılabilir.
### 1. String Fonksiyonlar:
#### 1. strlen fonksiyonu:
+ Bir dizgenin (string) uzunluğunu bayt cinsinden hesaplar.


> [!CAUTION]
> + Bu fonksiyon, dizge içindeki karakter sayısını değil, dizgenin bellekte kapladığı bayt sayısını döndürür.
> + Bu özellikle, çok baytlı karakter kodlamaları (örneğin UTF-8) kullanıldığında önemlidir.

##### Sözdizimi:
```php
$length = strlen($string)
```
> **Explanation:**
> - `$string`: Uzunluğu hesaplanacak dizge. 
> - `$length`: Dizgenin bayt cinsinden uzunluğu.

##### Temel Kullanımı:
```php
<?php
$string = "Merhaba Dünya";
echo strlen($string);       // Çıktı: 13 (UTF-8'de "Merhaba Dünya" 14 bayttır)
?>
```


> [!IMPORTANT]
> + `strlen` fonksiyonu, dizge içindeki karakter sayısını değil, bayt sayısını döndürür.
> + Özellikle UTF-8 gibi çok baytlı karakter kodlamalarında, bir karakter birden fazla bayt ile temsil edilebilir.
> +  Bu nedenle, karakter sayısını bulmak için `mb_strlen` gibi çok baytlı karakter fonksiyonlarını kullanmak daha doğru olacaktır.

#### 2. mb_strlen fonksiyonu:

```php
<?php
$string = "Merhaba Dünya";
echo mb_strlen($string, 'UTF-8');
?>
```


> [!WARING]
> + `mb_strlen` fonksiyonun kullanabilmesi için `mbstring` adındaki dinamik kütüphaneni yüklenmesi gerekir.
> + Debian temeli işletim sistemlerinde `sudo apt install php8.1-mbstring` komutu ile kurabilirsiniz.
> + REHL temeli işletim sistemlerinde `sudo yum install php-mbstring` komut ile kurulumu gerçekleştirebilirsiniz.
> + Bu işlemlerin etkin olabilmesi için gerekli servisleri yeniden başlatmanız gerekir. Örneğin; nginx için `php-fpm`, `apache` için `httpd` veya `apache2` ve  windows için  `XAMPP/WAMP` kontrol paneli gibi servisler yeniden başlatılmalıdır.

#### 3. str_word_count:

##### Syntax:

```php
str_word_count(string $string, int $format = 0, ?string $characters = null): mixed
```
> **Explanation:**
> 1. **`$string`**: Kelimeleri sayılacak veya işlenecek dizge. 
> 2. **`$format`** (isteğe bağlı): Fonksiyonun nasıl sonuç döndüreceğini belirler. Varsayılan değer `0`'dır. Olası değerler:
> 	- `0`: Kelime sayısını döndürür (varsayılan).
> 	- `1`: Dizge içindeki kelimeleri bir dizi olarak döndürür.
> 	- `2`: Kelimelerin dizge içindeki konumlarını (indislerini) bir ilişkisel dizi olarak döndürür.
> 3. **`$characters`** (isteğe bağlı): Kelime olarak kabul edilecek ek karakterleri belirtir. Örneğin, tire (`-`) veya kesme işareti (`'`) gibi karakterlerin kelime parçası olarak kabul edilmesini sağlar.

##### Örnek 1: Kelime Sayısını Bulma (`$format = 0`):

```php
<?php
$string = "Linux is Awesome. I always use Arch Linux";
$wordCount = str_word_count($string);
echo $wordCount;         // Çıktı: 8
?>
```
> **Explanation:**
> + Eğer kelime sayısını bulmak istiyorsak `format = 0` parametresini yazmak zorunda değiliz.
> + `str_word_count($string, 0)` ile `str_word_count($string)` aynı görevi görür.


##### Örnek 2: Kelimeleri Dizi Olarak Alma (`$format = 1`):
```php
<?php
$string = "Linux is Awesome. I always use Arch Linux";
$wordCount = str_word_count($string, 1);
print_r($wordCount);         // Çıktı: 8
?>
```

#### 4. strtolower:
- PHP'de `strtolower` fonksiyonu, bir dizgeyi (string) küçük harflere dönüştürmek için kullanılır.
- Bu fonksiyon, dizge içindeki tüm büyük harfleri küçük harflere çevirir ve sonucu döndürür.
- Özellikle metin işlemlerinde büyük-küçük harf duyarsız karşılaştırmalar yapmak veya metni standart bir formata getirmek için kullanışlıdır.
##### Syntax:

```php
strtolower(string $string): string
```
> **Explanation:**
> - **Parametreler:** `$string`: Küçük harflere dönüştürülecek dizge.
> - **Dönüş Değeri:** Dizgenin küçük harflere dönüştürülmüş hali.

##### Örnek 1: Temel Kullanımı:
```php
<?php
$string = "HELLO WORLD";
echo strtolower($string);     // Çıktısı: hello world
?>
```


> [!WARNING]
> + **Türkçe Karakter Problemi:**
> + `strtolower`, ASCII karakterleri için optimize edilmiştir. `strtolower`: ASCII karakterleri için hızlı ve etkilidir. Türkçe karakterleri de destekler, ancak yerel ayarlara bağlıdır.
> + UTF-8 gibi çok baytlı karakter kodlamaları için `mb_strtolower` kullanmak daha doğru sonuçlar verir. `mb_strtolower`: Çok baytlı karakter kodlamaları (UTF-8 gibi) için daha uygundur. Türkçe karakterlerle çalışırken daha güvenilirdir.

#### 5. mb_strtolower:
+ `mb_strtolower`, PHP'de çok baytlı (multibyte) karakter kodlamalarını (örneğin UTF-8) destekleyen bir fonksiyondur.
+ Bu fonksiyon, bir dizgeyi (string) küçük harflere dönüştürürken, çok baytlı karakterleri (Türkçe karakterler, Çince, Japonca vb.) doğru bir şekilde işler.


> [!TIP]
> + Özellikle UTF-8 gibi karakter kodlamaları kullanıldığında, `strtolower` yerine `mb_strtolower` kullanmak daha güvenilir sonuçlar verir.

##### mb_strtolower syntax:
```php
mb_strtolower(string $string, ?string $encoding = null): string
```
> **Explanation:**
> + **Parametreler:** 
> + `$string` Küçük harflere dönüştürülecek dizge.
> + `$encoding` (isteğe bağlı): Karakter kodlamasını belirtir. Varsayılan değer `null`'dur ve bu durumda içsel karakter kodlaması (internal encoding) kullanılır. Genellikle `UTF-8` kullanılır.
> + **Dönüş Değeri:** Dizgenin(string) küçük harflere dönüştürülmüş hali.


> [!TIP]
> + PHP'de `mb_strtolower` fonksiyonunun önündeki **`mb_`** öneki, bu fonksiyonun **"multibyte"** (çok baytlı) karakter kodlamalarını desteklediğini belirtir.
> + `mb`: "Multibyte" kelimesinin kısaltmasıdır.
> + **Multibyte:** Bir karakterin birden fazla bayt ile temsil edildiği karakter kodlamalarını ifade eder. Örneğin, UTF-8, UTF-16, Shift_JIS gibi kodlamalar çok baytlıdır.

##### Örnek 1: Temel Kullanımı:
```php
<?php
$string = "MERHABA DÜNYA";
echo mb_strtolower($string, 'UTF-8');    // Çıktısı: merhaba dünya
?>
```

#### 6. strtoupper fonksiyonu:
#### 7. mb_strtoupper fonksiyonu:

#### 8. trim fonksiyonu:
+ PHP 8'de `trim()` fonksiyonu, bir string'in başındaki ve sonundaki boşlukları (veya belirtilen diğer karakterleri) kaldırmak için kullanılır.
+ Bu fonksiyon, özellikle kullanıcı girdilerini temizlerken veya veri işleme sırasında sıkça kullanılır.
##### trim syntax:
```php
trim(string $string, string $characters = " \n\r\t\v\x00"): string
```
> **Explanation:**
> + **Parametreler:**
> + **$string**: Boşlukları veya belirtilen karakterleri kaldırmak istediğiniz string
> + **$characters** (isteğe bağlı): Kaldırılmasını istediğiniz karakterleri belirtebileceğiniz bir string. Varsayılan olarak şu karakterleri kaldırır:
> 	- Boşluk ( )
> 	- Yeni satır, newline (`\n`)
> 	- Satır başı (`\r`)
> 	- Sekme, tab (`\n`)
> 	- Dikey sekme (`\v`)
> 	- Null byte(`\x00`)
> + **Dönen Değer:** 
> 	-  **string**: Başındaki ve sonundaki belirtilen karakterler kaldırılmış olan yeni string.

##### Örnek 1: 

```php
$text = "    Hello, World!     ";
echo $text;                // php>     Hello, World!     
echo trim($text);          // php> Hello, World!
```
> **Explanation:**
> + `php -a` komut ile php'in shell'in de hızlıca test edebilirsiniz.
> + Varsayılan olarak,  `Hello, World!` text'in sağındaki ve solundaki boşlukları kaldırdı. 

```php
$text2 = ">>>Hello, World!<<<";
echo $text2;              // php> >>>Hello, World!<<<
echo trim($text2, "<>");  // php> Hello, World!
```
> **Explanation:**
> + `<` ve `>` işaretleri solunda veya sağında mevcut ise `trim` fonksiyonu kaldıracaktır.
> + Dikkat ederseniz varsayılan dışında simge kullanılmıştır.


### 2. Sayısal(Numeric) Fonksiyonlar:
#### 1. is_int fonksiyonu:
+ PHP 8'de `is_int()` fonksiyonu, bir değişkenin tamsayı (integer) olup olmadığını kontrol etmek için kullanılan bir fonksiyondur.
+ Bu fonksiyon, değişkenin tamsayı türünde olup olmadığını kontrol eder ve eğer değişken bir tamsayı ise `true`, değilse `false` döndürür.
##### Syntax:
```php
bool is_int(mixed $value)
```
> **Explanation:**
> - `$value`: Kontrol edilecek değişken.

##### Örnek 1:
```php
<?php
$number = 12;
$float = 3.14;
$string = "15";

echo var_dump(is_int($number))."<br>";    // Çıktı: bool(true)
echo var_dump(is_int($float))."<br>";     // Çıktı: bool(false)
echo var_dump(is_int($string))."<br>";    // Çıktı: bool(false)
?>
```
> **Explanation:**
> - `$number` değişkeni bir tamsayı olduğu için `is_int($number)` `true` döner.
> - `$float` değişkeni bir ondalıklı sayı (float) olduğu için `is_int($float)` `false` döner.
> - `$string` değişkeni bir string olduğu için `is_int($string)` `false` döner. 



> [!CAUTION]
> + Eğer `is_int` değeri `false` çıktısı oluştursa, ekran çıktı vermez.

#### 2. is_numeric fonksiyonu:

+ PHP 8'de `is_numeric()` fonksiyonu, bir değişkenin sayısal bir değer içerip içermediğini kontrol etmek için kullanılır.
+ Bu fonksiyon, değişkenin bir sayı veya sayısal bir string olup olmadığını kontrol eder. Eğer değişken sayısal bir değer içeriyorsa `true`, içermiyorsa `false` döner.

##### Syntax:
```php
is_numeric(mixed $value): bool
```
> **Explanation:**
> + **Parametre:**
> 	- **$value**: Kontrol edilecek değişken. Bu bir string, integer, float veya başka bir türde olabilir.
> + **Dönen Değer:**
> 	- **bool**: Değişken sayısal bir değer içeriyorsa `true`, içermiyorsa `false`.

##### Örnek 1:
```php
<?php
$var1 = 33;
$var2 = '33';
$var3 = '33fsd';
$var4 = 'abc';
$var5 = 33.5;
$var6 = '33.5';
$var7 = '0x4A';   // Hexadecimal (PHP 8'de sayısal kabul edilmez)
$var8 = '1e4';    // Bilimsel gösterim (sayısal kabul edilir)

echo var_dump(is_numeric($var1));        // bool(true)
echo var_dump(is_numeric($var2));        // bool(true)
echo var_dump(is_numeric($var3));        // bool(false)
echo var_dump(is_numeric($var4));        // bool(false)
echo var_dump(is_numeric($var5));        // bool(true)
echo var_dump(is_numeric($var6));        // bool(true)
echo var_dump(is_numeric($var7));        // bool(false)
echo var_dump(is_numeric($var8));        // bool(true)
?>
```


> [!CAUTION]
> + PHP 8'de `is_numeric()` fonksiyonu, **hexadecimal** (örn. `0x4A`) ve **binary** (örn. `0b101010`) stringleri artık sayısal olarak kabul **etmez**.
> + Bu, PHP 7'ye kıyasla bir değişikliktir. PHP 7'de bu tür stringler sayısal kabul ediliyordu, ancak PHP 8'de bu davranış kaldırıldı.
> + - `is_numeric()`, boş string (`""`) veya boşluk karakterleri içeren stringler için `false` döner.


> [!NOTE]
> **Ne Zaman Kullanılır?**
> - Kullanıcı girdilerinin sayısal olup olmadığını kontrol ederken.
> - Matematiksel işlemler yapmadan önce bir değişkenin sayısal olup olmadığını doğrulamak için.
> - Veritabanına veya başka bir sisteme sayısal veri göndermeden önce veriyi doğrulamak için.

#### 3. is_float fonksiyonu:
+ PHP 8'de `is_float()` fonksiyonu, bir değişkenin **float** (kayan noktalı sayı) türünde olup olmadığını kontrol etmek için kullanılır.
+  Eğer değişken float türündeyse `true`, değilse `false` döner.
##### Syntax:

```php
is_float(mixed $value): bool
```
> **Explanation:**
> + **Parametre:**
> 	- **$value**: Kontrol edilecek değişken. Bu bir float, integer, string veya başka bir türde olabilir.
> + **Dönen Değer:**
> 	- **bool**: Değişken float türündeyse `true`, değilse `false`.

##### Örnek 1:

```php
<?php
$var1 = 42;                // integer - tam sayı
$var2 = 42.5;              // float - ondalıklı sayı
$var3 = "42.5";            // string (sayısal string)
$var4 = 'abc';             // string (sayısal olmayan)
$var5 = true;
$var6 = null;

var_dump(is_float($var1));    // bool(false)
var_dump(is_float($var2));    // bool(true)
var_dump(is_float($var3));    // bool(false) - string olduğu için
var_dump(is_float($var4));    // bool(false)
var_dump(is_float($var5));    // bool(false)
var_dump(is_float($var6));    // bool(false)
?>
```

> [!CAUTION]
> - `is_float()` sadece **float türündeki değişkenler** için `true` döner.
> - **String içinde yazılmış float değerler** (örn. `"42.5"`) için `false` döner, çünkü bunlar string türündedir.
> - **Integer değerler** için `false` döner, çünkü bunlar float değildir.
> - **Boolean**, **null** veya **array** gibi diğer türler için de `false` döner.

### 3. Array(Dizi) Fonksiyonu:
#### array_sum fonksiyonu:
+ PHP 8'de `array_sum` fonksiyonu, bir dizideki tüm değerlerin toplamını hesaplar.
+ Bu fonksiyon, dizideki sayısal değerleri toplar ve sonucu döndürür. 
+ Eğer dizi içinde sayısal olmayan değerler varsa (örneğin stringler), bu değerler toplama işlemine dahil edilmez (yani `0` olarak kabul edilir)

##### Syntax:
```php
array_sum(array $array): int|float
```
> **Explanation:**
> - `$array`: Toplanacak değerleri içeren dizi.
> - Dönüş değeri: Dizideki sayısal değerlerin toplamı (`integer` veya `float` olarak).

##### Örnek 1: Temel Kullanım

```php
<?php
$numbers = [1, 2, 3, 4, 5];           // Array(Dizi)

$sum = array_sum($numbers);
echo "Result: $sum\n";                // Çıktı: 15
?>
```

##### Örnek 2: Sayısal olmayan Değerler

```php
<?php
$mixed = [1, 2, 'hello', 3, 'world', 4.5];
$sum = array_sum($mixed);
echo $sum;         // Çıktı: 10.5 ("hello" ve "world" toplama dahil edilmez)
?>
```

> [!NOTE]
> - `array_sum` fonksiyonu, dizideki tüm değerlerin sayısal olup olmadığını kontrol etmez. Sayısal olmayan değerler toplama işlemine dahil edilmez.
> - Eğer dizideki tüm değerler integer ise, sonuç integer olarak döner. Eğer en az bir tane float değer varsa, sonuç float olarak döner.

##### Örnek 3: Associate Dizi

```php
$assoc = ["a" => 1, "b" => 2, "c" => 3];
$sum = array_sum($assoc);
echo $sum;                 // Çıktı: 6
```

## Diğer Fonksiyonlar:
### print_r fonksiyonu:
+ PHP 8'de `print_r`, bir değişkenin (dizi, nesne, string, sayı vb.) insanlar tarafından okunabilir bir şekilde görüntülenmesini sağlayan bir fonksiyondur.


> [!CAUTION]
> + Bu fonksiyon, özellikle **diziler** ve **nesneler** gibi karmaşık veri yapılarını hızlıca incelemek ve hata ayıklamak için kullanılır.

#### Sözdizimi:
```php
<?php
print_r(mixed $value, bool $return = false): mixed
?>
```
> **Explanation:**
> + **Parametreler:**
> + `$value` : Görüntülenecek değişken yani ekran basılacak değişken. Bu bir dizi, nesne, string, sayı vb. olabilir.
> + **`$return`** (isteğe bağlı): Eğer `true` olarak ayarlanırsa, `print_r` sonucu ekrana yazdırmak yerine bir string olarak döndürür. Varsayılan değer `false`'dur.
> + **Dönüş Değeri:**
> + `$return` parametresi `false` ise, sonuç doğrudan ekrana yazdırılır ve `true` döner.
> + `$return` parametresi `true` ise, sonuç bir string olarak döndürülür.

#### Örnek 1: Temel Kullanım

```php
<?php
$array = ["PHP", "Python", "Javascript"];
print_r($array);
?>
```

**Çıktısı:**
```php
Array
(
    [0] => Php
    [1] => Python
    [2] => javascript
)
```

#### Örnek 2: Basit Değişkenler:
```php
<?php
$string = "Linux is Awesome";
print_r($string);
?>
```

#### Örnek 3: Sonucu String Olarak Alma:

```php
<?php
$array = ["PHP", "Python", "Javascript"];
$stringArray = print_r($array, true);
echo $stringArray;                   // 1. Çıktı
echo var_dump($array);               // 2. Çıktı: Veri Tipi: Array
echo var_dump($stringArray);         // 3. Çıktı: Veri Tipi: String
?>
```
> **Explanation:**
> + `print_r` fonksiyonu 2. parametresi ya `false` yada `true` değeri alır. Varsayılan olarak `fasle`'dur. 
> + Eğer `true` değeri ile çalıştırsanız `$array` değişkenin içerisindeki diziyi `string`'e dönüştürüp `$stringArray` değişkenine atar. 
> + `var_dump` fonksiyonu ile veri tiplerini kontrol edebiliriz.

**Çıktısı:**
```php
Array                  // 1. Çıktı
(
    [0] => PHP
    [1] => Python
    [2] => Javascript
)
array(3) {             // 2. Çıktı
  [0]=>
  string(3) "PHP"
  [1]=>
  string(6) "Python"
  [2]=>
  string(10) "Javascript"
}
string(65) "Array    
(
    [0] => PHP
    [1] => Python
    [2] => Javascript
)
"                    // 3. Çıktı
```
> **Explanation:**
> + Çıktı sonuçlarını daha alabilmek için; `php -a` komut ile php'in interaktif kabuk ortamında php kodlarını yazdık;
> + `var_dump` fonksiyonu php de kullanılan verilerin tiplerini ayrıntılı bir şekilde ekran basar.

#### Örnek 4: `print_r` ile `var_dump` Arasındaki Fark:

- `print_r`, daha temiz ve okunabilir bir çıktı sunar. Özellikle diziler ve nesneler için kullanışlıdır.
- `var_dump`, değişkenin türü ve değeri hakkında daha ayrıntılı bilgi verir (örneğin, string uzunluğu, integer değeri vb.). Ancak çıktısı `print_r`'ye göre daha karmaşıktır.

```php
<?php
$prog_lang = ['PHP', 'Python', 'Javascript'];
var_dump($prog_lang);
echo "<br>";
print_r($prog_lang);
?>
```

**Çıktısı:**
```php
array(3) {           // var_dump fonksiyon çıktısı
  [0]=>
  string(3) "PHP"
  [1]=>
  string(6) "Python"
  [2]=>
  string(10) "Javascript"
}
Array              // print_r fonksiyon çıktısı
(
    [0] => PHP
    [1] => Python
    [2] => Javascript
)
```
> **Explanation:**
> - Çıktılar `php -a` komutu ile php kabuk ortamını çalıştırıp php kodları tek tek denenerek alınıştır.
> - `echo` dil yapısı kullanılarak tarayıcıda daha düzgün gürünüm kazandırmak için yazılmıştır.


### count fonksiyonu:
+ PHP 8'de `count()` fonksiyonu, bir dizideki eleman sayısını veya bir nesnedeki özellik sayısını döndüren yerleşik bir fonksiyondur.
#### Syntax:
```php
count(array|Countable $value, int $mode = COUNT_NORMAL): int
```
> **Explanation:**
> - **$value**: Eleman sayısını almak istediğiniz dizi veya `Countable` arayüzünü(`interface`) uygulayan bir nesne.
> - **$mode**: İsteğe bağlı bir parametredir. Varsayılan olarak `COUNT_NORMAL` kullanılır. Eğer `COUNT_RECURSIVE` olarak ayarlanırsa, çok boyutlu dizilerdeki tüm elemanlar sayılır.

#### Örnek 1: Array
```php
<?php
$array = [1, 2, 3, 4, 5];
echo count($array) . "\n";
?>
```
#### Örnek 2: Çok Boyutlu bir dizi
```php
<?php

$array = [
    'a' => [1, 2, 3],
    'b' => [4, 5],
    'c' => [6]
];

echo 'Üst Seviye: '.count($array)."\n";
echo 'Tüm Elemanlar: '.count($array, COUNT_RECURSIVE)."\n";
?>
```
# Fonksiyon Oluşturma:

+ PHP 8'de fonksiyon oluşturmak ve kullanmak oldukça basittir. Fonksiyonlar, belirli bir işlevi gerçekleştirmek için kullanılan kod bloklarıdır
+ Fonksiyonlar, kodunuzu daha modüler, okunabilir ve yeniden kullanılabilir hale getirir.

## 1. Fonksiyon Tanımlama ve Çağırma:
+ Fonksiyonlar, `function` anahtar kelimesi ile tanımlanır. Fonksiyon adı, parametreler ve fonksiyon gövdesi (işlevi gerçekleştiren kod) içerir.

```php
<?php
// Fonksiyon Tanımlama
function greeting() {
    echo "Hello, World\n";
}

// Fonksiyon Çağırma
greeting();            // Çıktı: Hello, World
?>
```

## 2. Parametreli Fonksiyon Oluşturma:

+ Fonksiyonlara parametreler ekleyerek daha esnek hale getirebilirsiniz. Parametreler, fonksiyonun dışarıdan veri almasını sağlar.

```php
<?php
// Parametre ile Fonksiyon Tanımlama
function greeting($name) {
    echo "Hello, $name\n";
}

// Parametre ile Fonksiyon Çağırma
greeting('Tanju');
?>
```

## 3. Varsayılan Parametreli Fonksiyon:

+ Fonksiyon parametrelerine varsayılan değerler atayabilirsiniz. Bu, parametre belirtilmediğinde varsayılan değerin kullanılmasını sağlar.

```php
<?php
// Varsayılan parametre ile Fonkson Tanımlama
function greeting($name = 'Guest') {
    echo "Hello, $name\n";
}

// Varsayılan parametre ile fonksiyon çağırma
greeting();            // Çıktı: Hello, Guest
// Varsayılan paramtrenin üzerine yazma(override)
greeting('Tanju');     // Çıktı: Hello, Tanju
?>
```

## 4. Değer Döndüren Fonksiyon:

+ Fonksiyonlar, `return` anahtar kelimesi ile bir değer döndürebilir. Bu değer, fonksiyonun çağrıldığı yerde kullanılabilir.

```php
<?php
// Return ile fonksiyon tanımlama
function sum($a, $b) {
    return $a + $b;
}

// Fonskiyonu çağırma ve geri dönen değerini bir değişkene atma
$result = sum(12,13);
echo "Toplam: $result\n";
?>
```

## 5. Çoklu Parametre ve Tür Bildirimi:

+ PHP 8'de fonksiyon parametrelerine ve dönüş değerlerine tür bildirimi (`type hinting`) ekleyebilirsiniz. Bu, fonksiyonun beklenen türde veri almasını ve döndürmesini sağlar.

```php
<?php
// type hinting ile fonksiyon tanımlama
function sum(int $a, int $b): int {
    return $a + $b;
}


$result = sum(10, 12);
echo "Toplam1: $result\n";        // Çıktı: Toplam1: 22

$resultString1 = sum(10, '13');   // "13" integer'a dönüştürülebilir
echo "Toplam2: $resultString1\n"; // Çıktı: Toplam2: 23 

$resultString2 = sum(10, 'abc');  // Fatal error: Uncaught TypeError: sum():
echo "Toplam3: $resultString2\n";
?>
```
> **Explanation:**
> + **Hatanın uzun hali:** `Fatal error: Uncaught TypeError: sum(): Argument #2 ($b) must be of type int, string given, called in ...`  

## 6. Değişken Sayıda Parametre (Variadic Functions):

+ Fonksiyonlara değişken sayıda parametre göndermek için `...` operatörünü kullanabilirsiniz. Bu, tüm parametreleri bir dizi olarak alır.

```php
<?php
function sum(...$number) {
    return array_sum($number);
}

echo sum(1, 2, 3, 4, 5) . "\n";
?>
```
## 7. Anonim Fonksiyonlar(Closure)

+ Anonim fonksiyonlar, isimsiz fonksiyonlardır ve genellikle bir değişkene atanır. Bu fonksiyonlar, özellikle `callback` olarak kullanılır.

```php
<?php
// Anonim Fonksiyonu Tanımlama
$greeting = function($name) {
    echo "Merhaba, ${name}!\n";
};

// Anonim Fonksiyonu Çağırma
$greeting("Tanju");             // Çıktı: Merhaba, Tanju!
?>
```
## 8. Fonksiyonlarda `strict_types` Kullanımı:
+ PHP 8'de `declare(strict_types=1);` kullanarak tür kontrolünü daha katı hale getirebilirsiniz.
+ Bu, fonksiyonlara tam olarak belirtilen türde veri gönderilmesini zorunlu kılar.

```php
// declare(strict_types=1);  // 1. Durum
declare(strict_types=1);     // 2. Durum

function multiple(int $a, int $b) {
    return $a * $b;
}

echo multiple(3, 5) . "\n";
echo multiple(3, '5') . "\n";
?>
```
> **Explanation:**
> 1. **Durum:** Hata vermeden çalışmaktadır. Yani `'5'` string karakterini integer olarak yorumlamaktadır.
> 2. **Durum:**  `declare(strict_types=1)` aktif olduğu için hiç bir şekilde string karakter kabul etmemektedir ve hata fırlatmaktadır. 
> 	+ **Hata:** `Fatal error: Uncaught TypeError: multiple(): Argument #2 ($b) must be of type int, string given, called in ...`


> [!TIP]
> - Tür bildirimi (`type hinting`) ve `strict_types` kullanarak daha güvenli kod yazabilirsiniz.


# Hata Yakalama:

Düzenlenecek!!!!
```php
<?php
declare(strict_types=1);

function hesapMakinesi(float $a, float $b, string $islem): float {
    return match ($islem) {
        '+' => $a + $b,
        '-' => $a - $b,
        '*' => $a * $b,
        '/' => $a / $b,
        default => throw new InvalidArgumentException("Geçersiz işlem: $islem"),
    };
}

// Fonksiyonu çağırma
echo hesapMakinesi(10, 5, '+'); // 15
echo hesapMakinesi(10, 5, '*'); // 50
echo hesapMakinesi(10, 0, '/'); // Warning: Division by zero
?>
```
# php.ini dosyası:
+ `php.ini`, PHP’nin yapılandırma dosyasıdır ve PHP’nin nasıl çalışacağını belirleyen ayarları içerir. PHP çalıştırıldığında, bu dosya okunarak çeşitli yapılandırma seçenekleri belirlenir.
## php.ini'in Temel Görevleri:
- PHP'nin **genel yapılandırmasını** belirler.
- **Bellek kullanımı**, **yükleme süresi**, **dosya yükleme limiti** gibi ayarları yönetir.
- **Hata raporlama ve günlük kaydı (logging)** ile ilgili yapılandırmaları belirler.
- **Oturum yönetimi (session handling)** ve **zaman aşımı (timeout)** sürelerini ayarlar.
- **Genişletmeler (extensions)** ve **modüller** için yapılandırmalar içerir.

## php.ini Dizin Yolu:
+ php.ini dosyasının konumu, sisteminize ve PHP'nin nasıl kurulduğuna bağlıdır:
+ **Linux/macOS (CLI veya Apache/Nginx ile kullanılıyorsa):**

```shell
php --ini | grep 'Loaded Configuration File'
```

veya

```shell
php -i | grep 'Loaded Configuration File'
```

+ **Windows (XAMPP/WAMP gibi ortamlar):** `C:\xampp\php\php.ini` veya `C:\wamp64\bin\php\php.ini`


> [!NOTE]
> + XAMPP, yerel bir bilgisayarda web sunucusu ortamı kurmak ve web uygulamaları geliştirmek için kullanılır.
> + Özellikle PHP tabanlı projeler (örneğin WordPress, Joomla) veya MySQL veritabanı kullanan uygulamalar için idealdir.
> +  XAMPP sayesinde, bir web sunucusunu bilgisayarınızda kolayca çalıştırabilir ve test edebilirsiniz.
> + **X**: Çapraz platform (Windows, Linux, macOS gibi işletim sistemlerinde çalışabilir).
> + **A**: Apache (web sunucusu).
> + **M**: MySQL/MariaDB (veritabanı yönetim sistemi).
> + **P**: PHP (sunucu tarafı programlama dili).
> + **P**: Perl (programlama dili, ancak daha az kullanılır).


## Servisleri Yeniden Başlatma:
+ php.ini dosyasında yapılan değişikliklerin geçerli olması için bazı servisleri(`apache2`,`httpd` veya `php-fpm` gibi) yeniden başlatılması gerekir.
+ **Apache için:**

```shell
sudo systemctl restart apache2   # Debian temeli dağıtımlar
```

```shell
sudo systemctl restart httpd     # RHEL temeli dağıtımlar
```

+ **Nginx ve PHP-FPM için:**

```shell
sudo systemctl restart php-fpm
```

+ **Windows (XAMPP/WAMP için):**  XAMPP/WAMP kontrol panelinden Apache’yi yeniden başlatın.
## php.ini Ayarları:

### 1. display_errors:
+ Eğer `display_errors` değeri **On** olarak ayarlanmışsa, PHP çalışma zamanında oluşan hataları doğrudan tarayıcıya yansıtır. Bu, geliştirme sürecinde hata ayıklamayı kolaylaştırır.

> [!CAUTION]
> - `display_errors = On` **sadece geliştirme ortamlarında kullanılmalıdır.**
> - **Üretim (production) ortamlarında** hata mesajlarını doğrudan ekrana yazdırmak güvenlik riski oluşturur, çünkü sistemle ilgili hassas bilgiler açığa çıkabilir.

**Geliştirme Ortamında:**
```ini
display_errors = On
```

**Production Ortamında:**
```ini
display_errors = Off
log_errors = On                      ; Hataları bir dosyaya kaydet
error_log = /var/log/php_errors.log  ; Günlük dosyasının yolu
```
> **Explanation:**
> + Eğer `display_errors = Off` olarak ayarlandıysa, PHP hataları ekrana yazdırmaz, ancak hata kayıtlarını `error_log` parametresi ile belirlenen dosyaya kaydedebilir. 
> + Yapılan ayarlanın etkin olabilmesi için yukarıda belirtilen servisleri yeniden başlatmayı unutmayız!

### upload_max_filesize:


## post_max_size:

###### Kaynak:
[Yazılımcı Adam](https://www.youtube.com/watch?v=fStgJtE2asI&list=PLvDYObN1J9DJurXmMzoZnpXVQGI6cELmc&index=4)
[Sadık Turan](https://www.youtube.com/watch?v=rdYpMb3BFxI&t=2779s)

