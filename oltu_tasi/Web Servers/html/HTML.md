#web 

+ HTML (**HyperText Markup Language**), web sayfaları oluşturmak için kullanılan standart bir işaretleme dilidir.
+ Web tarayıcıları (Chrome, Firefox, Edge gibi) HTML kodlarını yorumlayarak görsel ve etkileşimli web sayfalarına dönüştürür.
+ Günümüzde **HTML5** sürümü kullanılmaktadır ve multimedya (video, ses), form kontrolleri ve semantik etiketler (`<header>`, `<article>`, `<footer>`) gibi modern özellikler içerir.


> [!NOTE]
> **HTML'nin Temel Özellikleri:**
> 1. **Etiket (Tag) Tabanlıdır**: `<html>`, `<head>`, `<body>`, `<p>` gibi etiketlerle yapılandırılır.
> 	- Örnek: `<p>Bu bir paragraftır.</p>`
> 2. **Hipermetin Desteği**: Bağlantılar (`<a>` etiketi) ile diğer sayfalara veya kaynaklara link verilebilir.
> 	- Örnek: `<a href="https://www.google.com">Google'a Git</a>`
> 3. **Platform Bağımsızdır**: Tüm işletim sistemleri ve tarayıcılarla uyumludur.
> 4. **Dinamik İçerik**: JavaScript ve CSS ile etkileşimli ve stilize sayfalar oluşturulabilir.


> [!NOTE]
> **HTML Ne Değildir?**
> + Bir programlama dili **değildir** (JavaScript'ten farklı olarak).
> + Tek başına tasarım (CSS) veya dinamik işlevler (JavaScript) sağlamaz, ancak onlarla entegre çalışır.

# HTML5 nedir?

+ HTML5, **HyperText Markup Language (HTML)**'in en son büyük sürümüdür ve web sayfalarının oluşturulması için kullanılan bir işaretleme dilidir.
+ HTML5, önceki HTML sürümlerine göre daha gelişmiş özellikler sunar ve modern web uygulamaları geliştirmeyi kolaylaştırır.

## HTML5'in Özellikleri:
1. **Yeni Semantik Etiketler:**
	+ `<header>`, `<footer>`, `<article>`, `<section>`, `<nav>` gibi etiketler, web sayfalarının yapısını daha anlamlı hale getirir.
2. **Multimedya Desteği:**
	+ `<audio>` ve `<video>` etiketleri sayesinde, harici eklentilere (örneğin, Flash) gerek kalmadan ses ve video oynatma imkanı sağlar.
3. **Canvas ve SVG Desteği:**
	+ `<canvas>` etiketi ile dinamik grafikler ve animasyonlar oluşturulabilir.
	+  **SVG (Scalable Vector Graphics)** desteği ile ölçeklenebilir vektör grafikleri kullanılabilir.
4. **Daha Gelişmiş Form Elemanları:**
	+ Yeni giriş türleri: `<input type="email">`, `<input type="date">`, `<input type="range">` gibi yeni form elemanları gelir.
5. **Yerel Depolama (Local Storage ve Session Storage):**
	+ **localStorage** ve **sessionStorage**, çerezlere (cookies) alternatif olarak veri saklamak için kullanılır.
6. **Daha İyi Javascript API Desteği:**
	+ **Geolocation API**: Kullanıcının konumunu belirleyebilir.
	+ **Drag and Drop API**: Sürükle-bırak işlemleri için destek sunar.
	+ **WebSockets**: Gerçek zamanlı iletişim için daha hızlı bir bağlantı sağlar.

# HTML Taslağı:

```html
<!DOCTYPE html>

<html>
    <head>
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        Hello World!
    </body>
</html>
```

**`<!DOCTYPE html>`**
+ **Ne işe yar?** Belgenin bir **HTML5** dosyası olduğunu tarayıcıya bildirir.
+ **Detay:** Eski HTML sürümlerinde (ör. HTML4) daha karmaşıktı, HTML5 ile bu basit hale geldi.
---
**`<html>...</html>`**
+ **Ne işe yar?** Tüm HTML içeriğini sarmalayan kök (root) elementtir.
+ **`lang` eklenebilir:** Örneğin `<html lang="tr">` sayfanın Türkçe olduğunu belirtir (SEO ve erişilebilirlik için faydalıdır).
---
**`<head>...</head>`**
+ **Ne işe yar?** Sayfanın **görünmeyen** teknik bilgilerini (meta veriler, başlık, CSS/JS bağlantıları) içerir.
+ **Önemli:** Bu kısımda yazılanlar tarayıcıda **görüntülenmez** (`<title>` hariç).
---
**`<title>...</title>`**
+ **Ne işe yarar?** Tarayıcı sekmesinde veya pencerenin başlık çubuğunda görünen metni belirler.
+ **SEO için kritik:** Arama motorları bu metni sayfanın içeriği olarak değerlendirir.
---
**`<body>...</body>`**
+ **Ne işe yarar?** Tarayıcıda **görünen** tüm içerik (metin, resim, videolar vb.) buraya yazılır.


> [!NOTE]
> **Kapama Etiketleri (`</html>`, `</head>`, `</body>`)**
> + **Ne işe yarar?** Açılan her etiketin kapatılması gerekir (HTML5 bazı durumlarda esneklik sağlar, ancak kapatmak en iyi uygulamadır)


> [!TIP]
> + **Boşluklar:** HTML'de fazla boşluk/enterler tarayıcı tarafından **tek boşluk** olarak yorumlanır. Örneğin `Hello World!` arasında 100 boşluk bıraksanız bile tarayıcı 1 boşluk gösterir.
> + **Türkçe Karakterler:** Sayfada Türkçe karakter (ğ, ü, ş vb.) kullanacaksanız `<head>` içine şu meta etiketi eklemelisiniz:
> ```html
> <meta charset="UTF-8">
> ```

# Başlık(header) etiketi:

+ HTML'de başlıklar, **metin içeriğini hiyerarşik olarak düzenlemek** için kullanılan etiketlerdir.
+ Özellikle sayfa yapısını belirlemek, okunabilirliği artırmak ve SEO (Arama Motoru Optimizasyonu) için kritik öneme sahiptirler.

## HTML Başlık Etiketleri(Heading Tags):

+ 6 farklı seviyeden oluşur (`<h1>` en önemli, `<h6>` en az önemli):

|Etiket|Açıklama|Görsel Boyut (Varsayılan)|
|---|---|---|
|`<h1>`|**Ana başlık** (Sayfada genellikle **1 tane** olmalı, SEO için en önemli)|Çok büyük (24px-32px)|
|`<h2>`|Alt başlık (Bölümler)|Büyük (18px-24px)|
|`<h3>`|Alt-alt başlık|Orta (16px-18px)|
|`<h4>`|Daha küçük başlık|Küçük (14px-16px)|
|`<h5>`|Nadiren kullanılır|Daha küçük (12px-14px)|
|`<h6>`|En küçük başlık (Genellikle dipnotlar)|Çok küçük (10px-12px)|

```html
<!DOCTYPE html>

<html>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Linux is Awesome</h1>
        <h2>Linux is Awesome</h2>
        <h3>Linux is Awesome</h3>
        <h4>Linux is Awesome</h4>
        <h5>Linux is Awesome</h5>
        <h6>Linux is Awesome></h6>
        Hello World!
    </body>
</html>
```

**Çıktı:**
![heading tag](images/heading_tag.png)


# Meta Etiketi:

+ `<meta>` etiketi, bir HTML belgesi hakkında **metadata** (üst veri) sağlayan ve genellikle `<head>` bölümünde yer alan bir elementtir.
+ Bu etiket tarayıcılara, arama motorlarına ve diğer web servislerine sayfa hakkında önemli bilgiler iletir.


> [!NOTE]
> **Temel Özellikleri:**
> - *Kendini kapatan etiket(self-closing tag)*: `<meta>` etiketi içerik almaz, tek başına kullanılır.
> - *Tarayıcı/yönlendirme kontrolü*: Sayfa davranışını yönetir.
> - *SEO optimizasyonu*: Arama motorlarına bilgi sağlar.


```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <meta name="description" content="HTML meta etiketi nedir? Meta description nasıl yazılır? SEO için en iyi meta açıklama örnekleri.">
        <meta name="keywords" content="HTML, web geliştirme, frontend, programlama">
        <meta name="author" content="Tanju Yücel, tanju@example.com">                                  <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="refresh" content="30">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <p>
            Linux (telaffuz: Lin-uks); Linux çekirdeğine dayalı, açık kaynak kodlu, Unix benzeri bir işletim sistemi ailesidir. GNU Genel Kamu Lisansı versiyon 2 ile sunulan ve Linux Vakfı çatısı altında geliştirilen bir özgür yazılım projesidir.
        </p>
    </body>
</html
```

## 1. Karakter Kodlaması Belirtme (Zorunlu):

+ `<meta charset="UTF-8">`, bir HTML belgesinin **karakter kodlamasını (character encoding)** tanımlayan temel bir meta etiketidir.
+ Bu etiket, tarayıcıya *Bu sayfadaki metinler UTF-8 standardına göre kodlanmıştır* der.

```html
<meta charset="UTF-8">
```

> [!NOTE]
> **Neden Önemli?**
> 1. *Özel Karakter Desteği* (Türkçe karakterler dahil):
> 	- Doğru: `ğ, ş, ç, ı, ö, ü`
> 	- Yanlış: `ÄŸ, ÅŸ, Ã§, Ã½` (bozuk karakterler)
> 2. *Evrensel Uyumluluk:*
> 	-  Dünyadaki tüm dillerin karakterlerini destekler (Çince, Arapça, Rusça vb.)

## 2. Sayfa Açıklaması (SEO):

+ `<meta name="description">` etiketi, bir web sayfasının içeriğini **kısa ve öz bir şekilde özetleyen** HTML meta etiketidir.
+ Arama motorları (Google, Bing vb.) bu açıklamayı, kullanıcıların arama sonuçlarında sayfanızı daha iyi anlaması için kullanır.

```html
<meta name="description" content="HTML meta etiketi nedir? Meta description nasıl yazılır? SEO için en iyi meta açıklama örnekleri.">
```

## 3. Anahtar Kelimeler(Eski SEO):

+ Bu etiket, bir web sayfasının hangi **anahtar kelimeler** ile ilgili olduğunu belirtmek için kullanılır.
+ Anahtar kelimeler (`keywords`), o sayfanın **konusunu** arama motorlarına anlatmaya yardımcı olurdu.

```html
<meta name="keywords" content="HTML, web geliştirme, frontend, programlama">
```
> **Explanation:**
> + `name="keywords"` → Bu etiketin anahtar kelimeler içerdiğini belirtir.
> + `content="..."` → Virgülle ayrılmış anahtar kelimeler burada yer alır.


> [!CAUTION]
> 🚨 **Modern SEO açısından:**
> + Eskiden (2000’li yılların başında), arama motorları bu etiketi dikkate alıyordu. Ancak artık:
> + **Google ve birçok büyük arama motoru `keywords` etiketini dikkate almıyor.**
> + Çünkü zamanında birçok site, bu etiketi **spam** gibi doldurup kötüye kullandı:
> ```html
> <meta name="keywords" content="para, bedava, kazan, tıkla, para, para, para">
> ```
> + Bu yüzden Google gibi arama motorları, bu etiketi **görmezden** geliyor.

## 4. Web Yazarı:

+ Bu etiket, **web sayfasını kimin yazdığını (yazarını)** belirtmek için kullanılır.

```html
<meta name="author" content="Tanju Yücel">
```
> **Explanation:**
> + `name="author"` → Bu meta etiketinin sayfanın yazarı hakkında bilgi verdiğini söyler.
> + `content="Tanju Yücel"` → Yazarın adı veya yazar hakkında bilgi buraya yazılır.

```html
<meta name="author" content="Tanju Yücel, tanju@example.com">
```
> **Explanation:**
> + İstersen yazarın iletişim bilgisi gibi şeyleri de `content` içine dahil edebilirsin.


> [!WARNING]
> + Kişisel bilgiler bu şekilde herkese açık olur, yani yaygın bir yöntem değildir.
> + SEO etkisi düşüktür.


## 5. Responsive Tasarımın Temeli:

+ Bu meta etiketi, **mobil cihazlarda sayfanın doğru şekilde ölçeklenmesini** sağlayan kritik bir HTML öğesidir.
+ Özellikle responsive (duyarlı) web tasarım için vazgeçilmezdir.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Parametre ve Anlamaları:**

| Parametre       | Değer          | Açıklama                                      |
| --------------- | -------------- | --------------------------------------------- |
| `width`         | `device-width` | Cihazın ekran genişliğine uyum sağlar         |
| `initial-scale` | `1.0`          | Yakınlaştırma olmadan %100 ölçekte başlatır   |
| `minimum-scale` | `0.5`          | Minimum yakınlaştırma seviyesi                |
| `maximum-scale` | `2.0`          | Maksimum yakınlaştırma seviyesi               |
| `user-scalable` | `yes/no`       | Kullanıcının yakınlaştırma yapıp yapamayacağı |

![meta_viewport](meta_viewport.png)

> **Explanation:**
> + `<meta name="viewport" content="...">` etiketi pasif veya aktif ederek nasıl çalıştığını görebilirsiniz. 
# Paragraf Etiketi:

+ HTML'de **`<p>`** (paragraph/paragraf) etiketi, metin içeriğini **paragraf** olarak düzenlemek için kullanılan temel bir blok-level elementidir.
+ Tarayıcılar, `<p>` etiketi içindeki metni otomatik olarak bir paragraf şeklinde (alt ve üst boşluk bırakarak) gösterir.

```html
<!DOCTYPE html>

<html>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
	    <!-- Paragraph Tag -->
        <p>Bu bir paragraf örneğidir. HTML'de metinleri düzenli bloklar halinde göstermek için kullanılır.</p>
    </body>
</html>
```

**Çıktı:**
![p_tag](images/p_tag.png)


> [!NOTE]
> + html de yorum satırı kullanmak için `<!-- Html yorum satırı -->` kullanılır.

## Paragraf Etiketin Özelikleri:

1. **Block-Level Element:**
	+ `<p>` bir satırın tamamını kaplar (yanına başka içerik gelmez, `<span>` gibi inline elementlerden farklıdır).
2. **Otomatik Boşluk:**
	+ Tarayıcılar `<p>` etiketinin öncesine ve sonrasına **margin** ekler (varsayılan CSS: `margin-top: 1em; margin-bottom: 1em;`).
3. **İç İçe Kullanım(nested):**
	+ `<p>` içine başka bir `<p>` **konulamaz** (geçersiz HTML). Ancak diğer etiketler (ör. `<strong>`, `<a>`) eklenebilir:
	```html
	<p> Bir bir <strong>kalın</strong> metin</p>
	```
4. **Semantik Anlam:**
	+ Metnin bir "paragraf" olduğunu tarayıcıya ve arama motorlarına bildirir (erişilebilirlik ve SEO için önemli).


> [!CAUTION]
> **Yaygın Hatalar:**
> - **`<p>` İçine Blok-Level Element Koymak:**
> 	+ Yanlış: `<p><div>Bu div geçersizdir</div></p>`
> 	+ Doğru: `<div><p>Bu paragraf div içinde olabilir</p></div>`


## `<p>` vs `<div>` Farkı:

|Özellik|`<p>`|`<div>`|
|---|---|---|
|**Anlam**|Semantik (paragraf)|Genel amaçlı blok|
|**Varsayılan Stil**|Alt/üst boşluklu|Boşluksuz|
|**Kullanım**|Metin parçaları için|Layout veya gruplama için|

# Hyperlink:

+ Hyperlink (veya **bağlantı**), kullanıcıları bir web sayfasından diğerine, bir dosyaya, e-posta adresine veya sayfa içindeki bir bölüme yönlendiren tıklanabilir öğelerdir.
+ HTML'de `<a>` (anchor) etiketi ile oluşturulur.

##  Önemli Özellikler (Attributes):

+ **Attribute** (öznitelik), HTML etiketlerine **ek özellikler** eklemek için kullanılan yapılardır.
+ Etiketlerin davranışını, görünümünü veya içeriğini kontrol etmeye yararlar.

|Özellik|Açıklama|Örnek Kullanım|
|---|---|---|
|`href`|Hedef URL'yi belirtir (zorunlu).|`href="https://example.com"`|
|`target`|Bağlantının nerede açılacağını belirtir.|`target="_blank"` (yeni sekmede)|
|`title`|Fare üzerine gelindiğinde tooltip gösterir.|`title="Açıklama metni"`|
|`rel`|Güvenlik ve SEO için (ör. `rel="nofollow"`).|`rel="noopener noreferrer"`|
|`download`|Dosyayı indirmeye zorlar.|`download="dosya_adi.pdf"`|
## Örnek 1: Başka bir Sayfaya Link

```html
<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <a href="https://www.youtube.com"
           target="_blank" title="Youtube'a gider"
           >youtube</a>
    </body>
</html>
```

> **Explanation:**
> +  Burada `href` ve `target`, `<a>` etiketinin **attribute**'larıdır.
> + `href="https://www.youtube.com"`: Bağlantıya tıklandığında youtube adresine gider. 
> + `target="_blank"`: bağlantının yeni sekmede açmasını sağlar. 

**Çıktı:**
![anchor](images/anchor.png)

## Örnek 2: Bir html sayfasından başka html sayfasına

**index.html**
```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <a href="linux.html"
           target="_blank" title="Linux Distros"
           >Linux Distros</a>
    </body>
</html>
```

**linux.html**
```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>Linux Distro</title>
    </head>
    <body>
        <h1>Best Linux Distros</h1>
        <p>Debian</p>
        <p>Ubuntu</p>
        <p>Arch Linux</p>
        <p>Gentoo</p>
        <p>Slackware</p>
    </body>
</html>
```
> **Explanation:**
> + `Linux Distros` bağlantısını tıkladığımızda tarayıcı `linux.html` sayfasını yeni sekmede açacaktır. 

# Resim(image) etiketi:

+ **`<img>`** etiketi, bir HTML sayfasına **resim** eklemek için kullanılan **self-closing** (kapanış etiketi olmayan) bir etikettir.
+ Web sayfalarında görsel içerik göstermenin temel yoludur.

##  Önemli Özellikler (Attributes):

| Attribute        | Açıklama                                                                                                                          | Örnek Kullanım             |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| `src`            | Resmin kaynak yolunu belirtir (yerel dosya veya internet URL'si).                                                                 | `src="images/logo.png"`    |
| `alt`            | Resmin alternatif metni (SEO ve erişilebilirlik için zorunlu).                                                                    | `alt="Company Logo"`       |
| `width`/`height` | Resmin genişlik ve yüksekliği (piksel veya % cinsinden).                                                                          | `width="200" height="100"` |
| `title`          | Fare üzerine gelindiğinde gösterilen açıklama.                                                                                    | `title="Detaylı bilgi"`    |
| `loading`        | Resmin yüklenme davranışı (`lazy` ile performans optimizasyonu). Sayfa kaydırıldıkça resim yüklenir (ilk yükleme hızını artırır). | `loading="lazy"`           |
| `srcset`         | DPI veya ekran boyutuna göre farklı resimler belirtme (responsive).                                                               | `srcset="resim-2x.jpg 2x"` |

**index.html:**
```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <img src="linux.jpg"
             width="500px" alt="linux picture"
             title="Linux OS"
        >
    </body>
</html>
```
> **Explanation:**
> + **`src` (source):** Resmin dosya yolunu veya URL'sini belirtir (_zorunlu_).
> + **`alt` (alternate text):** Resim yüklenmezse veya ekran okuyucular için açıklama metni (_erişilebilirlik ve SEO için kritik_).
> + Genellikle resim dosyaları images adını verdiğimiz klasöre koyulur.

**HTML Dizin:**
```shell
nginx-tutorial3 :: www/html/HTML » ls -ltr
```

```shell
total 28
-rw-r--r-- 1 root     root     18328 Feb 25  2022 linux.jpg
-rw-r--r-- 1 root     root       282 Mar 31 22:18 linux.html
-rw-r--r-- 1 www-data www-data   200 Mar 31 23:55 index.html
```
> **Explanation:**
> + `ls -ltr` komut çıktısında görüldüğü üzeri `index.html` ile `linux.png` dosyaları aynı klasörde olduğuna dikkat ediniz.
> + `linux.jpg` resim dosyası yerine istediğiniz resmi kullanabilirsiniz.

# Ses(Audio):

+ **`<audio>`** etiketi, bir web sayfasına **ses dosyası** (müzik, podcast, efekt vb.) eklemek için kullanılan HTML5 elementidir. 
+ Kullanıcıların sesi oynatmasını, duraklatmasını ve ses seviyesini kontrol etmesini sağlar.

## Önemli Özellikler (Attributes):
|Attribute|Açıklama|Örnek Kullanım|
|---|---|---|
|`controls`|Oynatma kontrollerini gösterir (play, pause, volume vb.).|`<audio controls>`|
|`src`|Ses dosyasının yolunu belirtir (alternatif: `<source>` içinde).|`<audio src="muzik.mp3">`|
|`autoplay`|Sayfa yüklendiğinde otomatik oynatır (tarayıcılar genelde engeller).|`<audio autoplay>`|
|`loop`|Sesi döngüye alır (sürekli tekrar eder).|`<audio loop>`|
|`muted`|Ses varsayılan olarak sessizdir.|`<audio muted>`|
|`preload`|Sayfa yüklenirken sesin ne kadar önceden yükleneceğini belirtir.|`<audio preload="auto">`|

## Örnek 1: Temel Kullanım

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <audio controls>
            <source src="./alex-eglair.ogg" type="audio/ogg">
            <source src="./alex-eglair.mp3" type="audio/mpeg">
            Tarayıcınız audio etiketini desteklemiyor.
        </audio>
        
        <audio src="alex-eglair.mp3" controls>

        </audio>
    </body>
</html>
```
> **Explanation:**
> + **`<source>`** ile birden fazla format ekleyerek tarayıcı uyumluluğu sağlanır (MP3, OGG, WAV). Eğer tarayıcınız  `source` etiketi ile belirtilen `ogg` formatı desteklemez ise bir sonraki `source` etiketinde bulunan `mp3` formatını çalıştır. 

**Çıktı:**
![audio](images/audio.png)


> [!NOTE]
> **Yaygın Hatalar:**
> 1. *Format Uyumsuzluğu*:  Tüm tarayıcılar MP3'ü destekler, ancak OGG/WAV için ek `<source>` eklemek gerekebilir.
> 	```html
> 	<source src="muzik.ogg" type="audio/ogg">
> 	<source src="muzik.wav" type="audio/wav">
> 	```
> 2. *`autoplay` Çalışmaması*: Modern tarayıcılar, otomatik oynatmayı **kullanıcı etkileşimi olmadan engeller**.


> [!TIP]
> 1. **Performans için `preload`:**
> 	+ `preload="none"`: Sayfa yüklenirken ses dosyasını yüklemez.
> 	+ `preload="metadata"`: Sadece süre gibi bilgileri yükler.
> 	+ `preload="auto"`: Dosyayı önceden yükler (dikkatli kullanın, bant genişliği tüketir).
> 1. **Tarayıcı Desteği:**
> 	+ MP3 (`audio/mpeg`) -> Tüm tarayıcılar.
> 	+ OGG (`audio/ogg`) -> Firefox, Chrome.
> 	+ WAV (`audio/wav`) -> Yüksek kalite, ancak büyük dosya boyutu.

## Örnek 2: Otomatik Oynatma

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <audio controls autoplay muted loop>
            <source src="./alex-eglair.mp3" type="audio/mpeg">
            Tarayıcınız audio etiketini desteklemiyor.
        </audio>
        <br>
        <audio src="alex-eglair.mp3" controls>

        </audio>
    </body>
</html>
```

**Çıktı:**
![audio_autoplay](images/audio_autoplay.png)

> **Explanation:**
> + Firefox gibi tarayıcılar `autoplay`'i sadece `muted` ile çalıştırır (kullanıcı deneyimi için kısıtlamalar vardır).
> + Chrome temeli tarayıcılar `autoplay` çalışmasını engellemektedir.
> + Yukarıdaki görsel firefox tarayıcısından alınmıştır.

## Örnek 3: Video yükleme davranışı:

+ HTML'deki `<audio>` etiketinde kullanılan `preload` attribute'ü, tarayıcıya ses dosyasını nasıl önceden yüklemesi gerektiğini belirtir.
+ Bu attribute, ağ ve bellek kullanımını optimize etmek için kullanılır.


> [!NOTE]
> **`preload` Değerleri:**
> 1. `none`: Tarayıcı ses dosyasını hiç önceden yüklemez. Kullanıcı `play` butonuna basana kadar ses dosyası indirilmez.
> 2. `metadata`: Sadece dosyanın temel bilgileri (ör. uzunluk, codec bilgisi) yüklenir, ancak ses içeriği indirilmez.
> 3. `auto`: Tarayıcı ses dosyasını tamamen önceden yükleyebilir. Bu, sayfa yüklendiğinde ses dosyasının tamamının indirilmesine neden olabilir.
> 4. (Varsayılan - `preload` belirtilmezse): Tarayıcı kendi kararına göre en uygun yükleme yöntemini seçer.

#### 3.1. `preload=none`

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <audio controls preload="none">
            <source src="./alex-eglair.mp3" type="audio/mpeg">
            Tarayıcınız audio etiketini desteklemiyor.
        </audio>
    </body>
</html>
```

**Çıktı:**
![preload_none](images/preload_none.png)
> **Explanation:**
> + Tarayıcıdan da görüldüğü üzeri tarayıcı her hangi bir ön yükleme yapmamıştır.

#### 3.2. `preload="auto"`

```html
<audio controls preload="auto">
    <source src="./alex-eglair.mp3" type="audio/mpeg">
    Tarayıcınız audio etiketini desteklemiyor.
</audio>
```

**Çıktı:**
![preload_auto](images/preload_auto.png)

> **Explanation:**
> Tarayıcı çıktısından görüldüğü üzeri ses dosyası ve gereken her şey öncesinde yüklenmiş olduğu görünmektedir.

#### 3.3. `preload=metadata`

```html
<audio controls preload="metadata">
    <source src="./alex-eglair.mp3" type="audio/mpeg">
    Tarayıcınız audio etiketini desteklemiyor.
</audio>
```

**Çıktı:**
![preload_metadata](images/preload_metadata.png)
> **Explanation:**
> + Eğer `auto` ile karşılaştırsak sadece dosyanın temel bilgileri (ör. uzunluk, codec bilgisi) yüklenir, ancak ses içeriği yüklenmediğini görebiliriz.


#### 3.4. preload belirtilmezse
+ Eğer `<audio>` etiketinde `preload` attribute'ü belirtilmezse, tarayıcı kendi stratejisine göre en uygun ön yükleme yöntemini seçer.
+ Ancak bu seçim, tarayıcıya ve hatta kullanıcının internet bağlantı hızına bağlı olarak değişebilir.

> [!NOTE]
> **Ne Olur?**
> + Çoğu modern tarayıcı **"preload=metadata"** gibi davranır, yani sadece ses dosyasının uzunluğu ve diğer metadata bilgileri yüklenir ama içeriğin tamamı indirilmez.
> + Bazı tarayıcılar ve durumlara bağlı olarak, tarayıcı **hiçbir şey yüklemeyebilir (preload="none" gibi davranabilir)** ya da ses dosyasının tamamını yükleyebilir (**preload="auto" gibi davranabilir**).
> + Mobil tarayıcılar genellikle bant genişliği tasarrufu yapmak için **"preload=none"** tercih eder.

## `<audio>` vs `<video>` Farkı:
| Özellik           | `<audio>`                          | `<video>`                              |
| ----------------- | ---------------------------------- | -------------------------------------- |
| **Kullanım**      | Sadece ses dosyaları.              | Ses + görüntü.                         |
| **Attribute'lar** | `controls`, `loop`, `muted` ortak. | Ek olarak `poster`, `width`, `height`. |
| **Örnek**         | Müzik çalar, podcast.              | Film, eğitim videosu.                  |

## `src` vs `<source>` Farkı:

| Özellik               | `<audio src="...">`                              | `<audio><source></audio>`         |
| --------------------- | ------------------------------------------------ | --------------------------------- |
| **Çoklu Format**      | ❌ Tek dosya                                      | ✅ Birden fazla format eklenebilir |
| **Hata Mesajı**       | ❌ Yok (boş player)                               | ✅ Özel mesaj yazılabilir          |
| **MIME Tip Belirtme** | ❌ Otomatik algılanır (hatalara açık)             | ✅ `type` ile kesin belirtilir     |
| **Kod Kısalığı**      | ✅ Daha kısa                                      | ❌ Daha uzun                       |
| **Tarayıcı Desteği**  | ⚠️ Sadece belirtilen dosya çalışmazsa hata verir | ✅ En uygun formatı seçer          |

### 1. Doğrudan `src` Kullanımı(Kısa Yol):

```html
<audio src="alex-eglair.mp3" controls></audio>
```
> **Explanation:**
> + *Avantajlar:*
> 	- *Basitlik*: Tek satırda hızlıca ses dosyası ekler.
> 	- *Kısa Kod* : Küçük projeler veya tek format kullanılan durumlar için idealdir.
> + *Dezavantajlar*:
> 	- *Tek  format desteği*: Tarayıcı dosyayı oynatamazsa yedek seçenek sunmaz.
> 	- *Erişilebilirlik eksikliği:* Desteklenmeyen tarayıcılarda sadece boş bir player gösterir(Hata mesajı yok).

### 2. `<source>` Etiketi Kullanımı(Profesyonel Yöntem):

```html
<audio controls>
  <source src="./alex-eglair.mp3" type="audio/mpeg">
  Tarayıcınız audio etiketini desteklemiyor.
</audio>
```
> **Explanation:**
> + *Avantajlar:*
> 	- *Çoklu format desteği:* Birden fazla `<source>` ekleyerek tarayıcı uyumluluğu sağlarsınız
> 	- *Hata yönetimi:* Tarayıcı desteklemiyorsa veya dosya bulunamaz ise alternatif metin gösterir.
> 	- *Net MIME tipi:* `type="audio/mpeg` ile tarayıcıya dosya türünü belirtir(performans avantajı).
> + *Dezavantajı:*
> 	- *Uzun Kod:* Basit senaryolarda gereksiz gelebilir.


# Video:

+ **`<video>`** etiketi, bir web sayfasına **video içeriği** eklemek için kullanılan HTML5 elementidir.
+ Kullanıcıların videoyu oynatmasını, duraklatmasını, sesini kontrol etmesini ve tam ekran yapmasını sağlar.

## Önemli Özellikler(Attributes):

|**Attribute**|**Açıklama**|**Örnek**|
|---|---|---|
|`src`|Video dosyasının yolu (alternatif: `<source>` içinde kullanılır).|`src="film.mp4"`|
|`controls`|Oynatma kontrollerini gösterir (play, ses, tam ekran vb.).|`<video controls>`|
|`width` / `height`|Videoyu belirtilen boyutta gösterir (CSS ile de ayarlanabilir).|`width="800" height="450"`|
|`autoplay`|Sayfa yüklendiğinde otomatik oynatır (tarayıcılar genelde sesi kapalı ister).|`<video autoplay muted>`|
|`loop`|Videoyu döngüye alır (sürekli tekrar eder).|`<video loop>`|
|`muted`|Varsayılan olarak sesi kapalı başlatır.|`<video muted>`|
|`poster`|Video yüklenmeden önce gösterilecek resim (thumbnail).|`poster="resim.jpg"`|
|`preload`|Videoyu önceden yükler (`auto`, `metadata`, `none`).|`preload="metadata"`|

## Örnek 1:  

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
	    <!-- Kısa Yöntem -->
        <video src="Linux_Find.mkv" width="500px"
            controls autoplay>
        </video>
        <br>
        <!-- Profesiyonel Yöntem -->
        <video controls width="500px" autoplay muted>
	        <!-- Firefox mkv uzantısını desteklemiyor -->
            <source src="Linux_Find.mkv" type="video/webm">
            <!-- Firefox mp4 uzantısını destekliyor --> 
            <source src="Go_prog.mp4" type="video/mp4">
        </video>
    </body>
</html>
```

**Çıktı:**
![video_source](images/video_source.png)
> **Explanation:**
> + Kısa yol(`src`) ile Profesyonel Yöntem(`<source>`) arasında fark görülmüyor ama bazı tarayıcılar bazı uzantıları desteklememektedir.
> + `audio` etiketi de olduğu gibi Profesyonel yöntem ile ek  format uzantılı dosyalar ekleyebiliriz. Böylece tarayıcı formatı desteklemez ise bir sonraki formatı çalıştır. 
> + Yani, **`<source>`** ile birden fazla format ekleyerek tarayıcı uyumluluğu sağlanır (MP4, WebM, OGG).



> [!NOTE]
> 1. **Format Uyumsuzluğu:** Tüm tarayıcılar MP4'ü destekler, ancak WebM/OGG için ek `<source>` eklemek gerekebilir.
> 	```html
> 	<source src="Linux_Find.mkv" type="video/webm">
> 	<source src="Go_prog.mp4" type="video/mp4">
> 	```
> 2. **`autoplay` Çalışmaması:** Modern tarayıcılar, otomatik oynatmayı **kullanıcı etkileşimi olmadan engeller** (özellikle sesli videolarda).
> 3. **Erişilebilirlik Eksikliği:** Video içeriği için **altyazı** (`<track>` etiketi) eklemeyi unutmayın:
> 	```html
> 	<track src="altyazi.vtt" kind="subtitles" srclang="tr" label="Türkçe">
> 	```


**Destekleyen Video Formatları:**

|**Format**|**MIME Type**|**Tarayıcı Desteği**|
|---|---|---|
|MP4|`video/mp4`|Tüm modern tarayıcılar (H.264).|
|WebM|`video/webm`|Firefox, Chrome, Edge.|
|OGG|`video/ogg`|Firefox, Opera (eski sürümler).|

## Örnek 2: Otomatik Oynatma

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <video controls width="500px" autoplay muted>
            <source src="Go_prog.mp4" type="video/mp4">
        </video>
    </body>
</html>
```

> **Explanation:**
> + `autoplay` ve `muted` attribute'leri ile sayfa yüklendiğinde video otomatik olarak başlıyor.
> + Chrome ve Firefox gibi tarayıcılar `autoplay`'i sadece `muted` ile çalıştırır.

## Örnek 4:  Döngü

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
	    <!-- loop: Video bittiğinde tekrardan başlar -->
        <video controls width="500px" autoplay muted loop>
            <source src="Linux_Find.mkv" type="video/webm">
            <source src="Go_prog.mp4" type="video/mp4">
        </video>
    </body>
</html>
```
> **Explanation:**
> + `autoplay` ve `muted` attribute'lerini kullanmaksızın da `loop` attribute'ü kullanılır ama genellikle bu üç attribute birlikte kullanılır.

## `preload` attribute:

| Değer      | Ne yapar?                               | Ne zaman kullanılır?                                        |
| ---------- | --------------------------------------- | ----------------------------------------------------------- |
| `none`     | Hiçbir şey yüklemez                     | Veri tasarrufu isteniyorsa                                  |
| `metadata` | Sadece video bilgilerini yükler         | Süre/thumbnail göstermek ama içeriği indirmemek isteniyorsa |
| `auto`     | Gerekirse tamamını bile önceden indirir | Video büyük ihtimalle oynatılacaksa                         |
### Örnek 5: `preload="none"`

+ Video hiç önceden yüklenmez.
+ **Ne zaman kullanılır?** Kullanıcı oynat butonuna basmadan video yüklenmesin istiyorsanız.

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <video controls width="500px" preload="none">
            <source src="Linux_Find.mkv" type="video/webm"> <!-- 1.Durum -->
            <source src="Go_prog.mp4" type="video/mp4"> <!-- 2.Durum -->
        </video>
    </body>
</html>
```
> **Explanation:**
> + Eğer tarayıcı 1.Durum'u desteklemez ise 2.Durumu çalıştırır. Çünkü tüm tarayıcılar `mp4` formatını destekler.


**Çıktı:**

![video_preload_none](video_preload_none.png)

> **Explanation:**
> + Çıktıda da gördüğümüz gibi video ne indirilmiş ne de yüklenmiştir. Çünkü, `preload="none"` olarak ayarlanmıştır.

### Örnek 6: `preload="metadata"`

+ **Ne zaman kullanılır?** Video hakkında bilgi göstermek istiyor ama içeriği hemen indirmek istemiyorsanız.

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <video controls width="500px" preload="metadata">
            <source src="Linux_Find.mkv" type="video/webm">
            <source src="Go_prog.mp4" type="video/mp4">
        </video>
    </body>
</html>
```

**Çıktı:**

![video_preload_metadata](video_preload_metadata.png)

> **Explanation:**
> + Bu çıktı da görüldüğü üzeri video'un sadece temel bilgiler(süre, çözünürlük gibi) yüklenir. *İçerik indirilmez.*

### Örnek 7: `preload="auto"`

+ **Ne zaman kullanılır?** Kullanıcının videoyu oynatma ihtimali yüksekse ve akıcı bir deneyim isteniyorsa.

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <video controls width="500px" preload="auto">
            <source src="Linux_Find.mkv" type="video/webm">
            <source src="Go_prog.mp4" type="video/mp4">
        </video>
    </body>
</html>
```

**Çıktı:**

![video_preload_auto](images/video_preload_auto.png)

> **Explanation:**
> + Tarayıcı videonun ne kadarını önceden yükleyeceğine kendi karar verir. Hatta tamamını da indirebilir.
> + Video ortalarına hızlıca gittiğimizde bekleme olmadığını gözlemleyebilirsiniz.

### Örnek 8: `preload` belirtilmezse

+ Tarayıcı **kendi varsayılanına göre davranır.**
+ Genellikle `preload="metadata"` gibi davranır ama bu, cihaz ve tarayıcıya göre değişebilir.
-  Mobil tarayıcılar genellikle veri tasarrufu için **hiçbir şey yüklememeyi** tercih eder (yani `none` gibi davranır).

## Özet:
- `<video>` etiketi, **web sayfalarına video eklemenin standart yoludur**.
- **`controls`** ile kullanıcı etkileşimi sağlanır.
- Çoklu format desteği için **`<source>`** kullanın.
- Otomatik oynatma (`autoplay`) için **`muted`** gerekebilir.
- Mobil uyumluluk için **CSS ile boyutlandırma** yapın.

## Metin Biçimlendirme:

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <p>Bu Normal Bir Yazı</p>
        <p>Bu <b>Kalın</b> Bir Yazı</p>
        <p>Bu <strong>Kalın</strong> Bir Yazı</p>
        <p>Bu <i>İtalik</i> Bir Yazı</p>
        <p>Bu <em>İtalic</em> Bir Yazı</p>
        <p>Bu <big>Büyük</big> Bir Yazı</p>
        <p>Bu <small>Küçük</small> Bir Yazı</p>
        <p>Bu <sub>Alt Sembol</sub> Bir Yazı</p>
        <p>Bu <sup>Üst Sembol</sup> Bir Yazı</p>
        <p>Bu <ins>Altı Çizili</ins> Bir Yazı</p>
        <p>Bu <del>Üstü Çizili</del> Bir Yazı</p>
        <p>Bu <mark>Fosforlu</mark> Bir Yazı</p>
    </body>
</html>
```

**Çıktı:**

![text_formating](images/text_formating.png)

### 1. `<b>` ve `<strong>` Etiketleri Arasındaki Farklar:

+ `<b>` ve `<strong>` etiketleri her ikisi de metni kalın (bold) göstermek için kullanılsa da, temel farkları vardır.

**Semantik(Anlamsal) Fark**

|`<b>` Etiketi|`<strong>` Etiketi|
|---|---|
|**Sadece görsel kalınlaştırma** yapar|**Metne güçlü vurgu/anlam** katar|
|Semantik önemi yoktur|Semantik önemi vardır|
|Sadece biçimlendirme amaçlıdır|İçeriğin önemini belirtir|
|Ekran okuyucular için fark yaratmaz|Ekran okuyucular vurguyu farklı okuyabilir|

### 2. `<i>` ve `<em>` Etiketleri Arasındaki Farklar:

+ `<i>` ve `<em>` etiketleri her ikisi de metni italik (eğik) göstermek için kullanılsa da, temel farkları vardır.

**Semantik(Anlamsal) Fark:**

|`<i>` Etiketi|`<em>` Etiketi|
|---|---|
|**Sadece görsel italikleştirme** yapar|**Metne vurgu/anlam** katar|
|Semantik önemi yoktur|Semantik önemi vardır|
|Sadece biçimlendirme amaçlıdır|İçeriğin vurgulanmasını sağlar|
|Ekran okuyucular için fark yaratmaz|Ekran okuyucular vurguyu farklı tonlama ile okuyabilir|

# Listeler:

+ HTML'de listeler, web sayfalarında bilgileri düzenli ve okunabilir bir şekilde sunmak için kullanılan temel bir yapıdır. Üç ana liste türü bulunur:
## 1. Sırasız Liste(Unordered Lists):

+ Öğelerin belirli bir sırası önemli olmadığında kullanılır.
+ Her bir liste öğesi genellikle bir madde işareti (disk, daire, kare vb.) ile işaretlenir.
+ `<ul>` etiketi listenin başlangıcını ve `</ul>` etiketi listenin sonunu belirtir.
+ Her bir liste öğesi `<li>` (list item) etiketi içine alınır.

### Örnek 1: Temel Kullanım

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Popüler Programlama Dilleri:</h1>
        <ul>
            <li>Python</li>
            <li>Javascript</li>
            <li>Python</li>
            <li>java</li>
            <li>C programlama</li>
        </ul>
    </body>
</html>
```

**Çıktı:**

![unordered_lists](unordered_lists.png)

### Örnek 2: `style Attribute`

+ CSS ile madde işaretlerinin görünümünü değiştirebilirsiniz:

```html
<ul style="list-style-type: disc;"> <!-- Varsayılan (dolu daire) -->
  <li>Disk stili</li>
</ul>

<ul style="list-style-type: circle;"> <!-- İçi boş daire -->
  <li>Çember stili</li>
</ul>

<ul style="list-style-type: square;"> <!-- Kare -->
  <li>Kare stili</li>
</ul>

<ul style="list-style-type: none;"> <!-- İşaretsiz -->
  <li>İşaretsiz</li>
</ul>
```

### Örnek 3: nested list

+ Sırasız listeleri **iç içe(nested)** kullanabilirsiniz:

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Popüler Programlama Dilleri:</h1>
        <ul>
            <li>Linux OS
                <ul>
                    <li>Ubuntu</li>
                    <li>Arch Linux</li>
                    <li>Fedora</li>
                </ul>
            </li>
            <li>Windows</li>
            <li>Mac OS</li>
        </ul>
    </body>
</html>
```

## 2. Sıralı Liste(Ordered Lists ):

+ Sıralı listeler, numaralı veya belirli bir sıraya göre düzenlenmiş listeler oluşturmak için kullanılır.
+ Her liste öğesi `<li>` (list item) etiketi ile tanımlanır.

### Örnek 1: Temel Kullanım

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Best Operating System:</h1>
        <ol>
            <li>Ubuntu</li>
            <li>Manjora</li>
            <li>Fedora</li>
            <li>Linux Mint</li>
            <li>Arch Linux</li>
        </ol>
    </body>
</html>
```

**Çıktı:**

![ordered_list](ordered_list.png)

### Örnek 2: `type` attribute Kullanımı:

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Best Operating System:</h1>
        <ol type="A">
            <li>Ubuntu</li>
            <li>Manjora</li>
            <li>Fedora</li>
            <li>Linux Mint</li>
            <li>Arch Linux</li>
        </ol>
    </body>
</html>
```

**Çıktı:**

![ordered_list_types](ordered_list_types.png)

+ `<ol>` element'in `type attribute`'ün alabileceği seçenekleri: 

```html
<ol type="A">
  <li>Büyük harfler (A, B, C)</li>
</ol>

<ol type="a">
  <li>Küçük harfler (a, b, c)</li>
</ol>

<ol type="I">
  <li>Roma rakamları (I, II, III)</li>
</ol>

<ol type="i">
  <li>Küçük Roma rakamları (i, ii, iii)</li>
</ol>
```

### Örnek 3:  `start` attribute Kullanımı

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Best Operating System:</h1>
        <ol start="3">
            <li>Ubuntu</li>
            <li>Manjora</li>
            <li>Fedora</li>
            <li>Linux Mint</li>
            <li>Arch Linux</li>
        </ol>
    </body>
</html>
```

> **Explanation:**
> + Liste `start` attribute sayesinde 1 ile değil 3 ile başlayacaktır. 

### Örnek 4: `reversed` attribute Kullanımı

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Best Operating System:</h1>
        <ol reversed>
            <li>Ubuntu</li>
            <li>Manjora</li>
            <li>Fedora</li>
            <li>Linux Mint</li>
            <li>Arch Linux</li>
        </ol>
    </body>
</html>
```

> **Explanation:**
> + `reversed` attribute ile liste 1'den 6'a sıralanmayacaktır. Bunun yerine 6'dan 1'e doğru bir sıralama olacaktır.
> + `reversed` Türkçe karşılığı da *tersine çevrilmiş* 

### Örnek 5: İç İçe Sıralı Listeler

+ Sırasız listeleri iç içe(`nested list`) kullanabilirsiniz:

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Best Operating System:</h1>
        <ol type="A">
            <li>
                Compiled Programming:
                <ol>
                    <li>C programming</li>
                    <li>Golang</li>
                    <li>Java</li>
                </ol>
            </li>
            <li>
                Interpreted Programming:
                <ul>
                    <li>Python</li>
                    <li>Javascript</li>
                    <li>PHP</li>
                </ul>
            </li>
        </ol>
    </body>
</html>
```

## 3. Açıklama Listesi:

+ Açıklama listeleri, terimleri ve onlara ait açıklamaları listelemek için kullanılan özel bir HTML listeleme yöntemidir.
+ Genellikle sözlük tarzı içerikler, tanımlamalar veya anahtar-değer çiftleri göstermek için idealdir.

### Örnek 1: Temel Kullanımı

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Programming Languages</h1>
        <dl>
            <dt>Python</dt>
            <dd>Python is a programming language that lets you work quickly
            and integrate systems more effectively.</dd>

            <dt>Javascript</dt>
            <dd>JavaScript (JS) is a lightweight interpreted (or just-in-time compiled)
             programming language with first-class functions.</dd>
             
            <dt>PHP</dt>
            <dd>A popular general-purpose scripting language that is especially suited
             to web development.</dd>
             
            <dt>Java</dt>
            <dd>Java is a programming language and computing platform first released by 
            Sun Microsystems in 1995.</dd>
            
            <dt>Mojo</dt>
            <dd>Mojo is an innovative, high-performance programming language designed for
             writing systems-level code for AI workloads.</dd>
        </dl>
    </body>
</html>
```

**Çıktı:**

![description_list](images/description_list.png)


> [!NOTE]
> **Elementler ve Anlamları:**
> 1. **`<dl>`** (Description List): Açıklama listesinin ana kapsayıcısı
> 2. **`<dt>`** (Description Term): Tanımlanacak terim
> 3. **`<dd>`** (Description Details): Terimin açıklaması

### Örnek 2: Çoklu Açıklamalar

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Programming Languages</h1>
        <dl>
            <dt>HTML</dt>
            <dd>Web sayfalarının yapısını oluşturur</dd>
            <dd>1991'de Tim Berners-Lee tarafından oluşturuldu</dd>

            <dt>JavaScript</dt>
            <dd>Web sayfalarına dinamik davranış ekler</dd>
        </dl>
    </body>
</html>
```

> **Explanation:**
> + `HTML` için iki tane açıklama mevcut iken, `JavaScript` için yalnızca bir açıklama vardır. 
> + Yani, `HTML` için çoklu açıklama yazılmıştır.

### Örnek 3: nested list

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Programming Languages</h1>
        <dl>
            <dt>Frontend</dt>
            <dd>
                <dl>
                    <dt>HTML</dt>
                    <dd>Structure</dd>

                    <dt>CSS</dt>
                    <dd>Design</dd>

                    <dt>Progamming</dt>
                    <dd>JavaScript</dd>
                </dl>
            </dd>
        </dl>
    </body>
</html>
```

**Çıktı:**

![nested_description_list](images/nested_description_list.png)

# Tablolar:

+ Tablolar, verileri satırlar ve sütunlar halinde düzenli bir şekilde göstermek için kullanılan HTML elementleridir.
+ Temel tablo yapısı `<table>` etiketi ile oluşturulur.


> [!NOTE]
> **Tablo Elementleri:**
> 1. **`<table>`**: Tablonun ana kapsayıcısı
> 2. **`<tr>`** (Table Row): Tablo satırı
> 3. **`<th>`** (Table Header): Başlık hücresi (varsayılan olarak kalın ve ortalanmış)
> 4. **`<td>`** (Table Data): Normal veri hücresi

## Temel Tablo attribute'leri:


> [!NOTE]
> **HTML5 ile Kaldırılan Özellikler:** Bu attribute'ler HTML5 ile artık desteklenmemektedir(CSS Kullanılmalıdır.)
> + `align`
> + `bgcolor`
> + `cellpadding`
> + `cellspacing`
> + `width`
> + `height`
> + `border`

### 1. `<table>` attribute'leri:

+ **border**: Tablo kenarlık kalınlığı (piksel cinsinden)

```html
<table border="1">
```

+ `border attribute` kullanmak yerine aşağıdaki gibi CSS özelliğini(property) kullanınız! 

```css
border 1px solid black;
```

---
+ **cellpadding**: Hücre içi boşluk (piksel)

```html
<table cellpadding="5">
```

+ Bir hücrenin içeriği ile sınırı arasındaki boşluğu tanımlar. Bu özellik(attribute) artık kullanılmıyor: Bunu kullanmak yerine, `<th>` ve `<td>` öğelerine `padding` CSS özelliğini(property) uygulayın.(Kaynak: [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/padding))

```css
padding: 1em;
```

---
+ **cellspacing**: Hücreler arası boşluk (piksel)

```html
<table cellspacing="3">
```

+ İki hücre arasındaki boşluğun boyutunu tanımlar. Bu özellik(attribute) artık kullanılmıyor: Bunu kullanmak yerine, `<table>` öğesinde border-spacing CSS özelliğini(property) ayarlayın..(Kaynak: [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/border-spacing)

```css
border-spacing: 5;
```

---
+ **width**: Tablo genişliği (piksel veya yüzde)

```html
<table width="100">
```

+ Specifies the width of the table. Bunun yerine `width` CSS özelliğini(property) kullanın, çünkü bu nitelik(attribute) kullanım dışıdır.

```css
width: 100px;
```


> [!CAUTION]
> + Hiçbir HTML standardı `<table>` etiketi için `height` (yükseklik) özelliğini içermese de, bazı tarayıcılar `height` niteliğini(attribute) standart dışı bir şekilde yorumlayarak desteklemektedir.
> + Birimsiz değer, piksel cinsinden minimum mutlak yüksekliği ayarlar.
> + Yüzde değeri olarak ayarlanırsa, minimum tablo yüksekliği ana konteynerin(`parent container`) yüksekliğine göreli olacaktır.
> + Bunun yerine min-height CSS özelliğini(property) kullanın, çünkü bu nitelik(attribute) kullanım dışıdır.
> + Kaynak: [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/table)

---

+  **align**: Tablo hizalaması (left|center|right) (CSS ile yapılması önerilir)

```html
<table align="right">
```

+ Tablonun üst element(`parent element`) içindeki yatay hizalamasını belirtir. Olası numaralandırılmış(`enumerated`) değerler sol, merkez ve sağdır.
+ Bunun yerine `margin-inline-start` ve `margin-inline-end` CSS özelliklerini kullanın, çünkü bu öznitelik(attribute) kullanım dışıdır.

```css
margin-inline-start: 20px;
```

---

+ **bgcolor**: Arkaplan rengi (CSS ile yapılması önerilir)

```html
<table bgcolor="red">
```

+ Tablonun arka plan rengini tanımlar. Değer bir HTML rengidir; ya  [6-digit hexadecimal RGB code](https://developer.mozilla.org/en-US/docs/Web/CSS/hex-color) yada [color keyword](https://developer.mozilla.org/en-US/docs/Web/CSS/named-color)
+ Diğer CSS `<color>` değerleri desteklenmiyor. Bunun yerine background-color CSS özelliğini kullanın, çünkü bu öznitelik kullanım dışıdır.

```css
background-color: red;
```

---
### 2. `<tr>`, `<td>`, `<th>` attribute'leri:



## Örnek 1: attribute'ler kullanımı

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <h1>Açılış Saatleri</h1>
        <table bgcolor="black" width="560">
            <tr bgcolor="grey">
                <th width="80">Pazartesi</th>
                <th width="80">Salı</th>
                <th width="80">Çarşamba</th>
                <th width="80">Perşembe</th>
                <th width="80">Cuma</th>
                <th width="80">Cumartesi</th>
                <th width="80">Pazar</th>
            </tr>
            <tr align="center"
                bgcolor="lightgrey">
                <td>9-5</td>
                <td>9-5</td>
                <td>9-5</td>
                <td>9-5</td>
                <td>9-5</td>
                <td>Kapalı</td>
                <td>Kapalı</td>
            </tr>
        </table>
    </body>
</html>
```

> **Explanation:**
> + **align**: Tablo hizalaması (left|center|right) (CSS ile yapılması önerilir)
> + **bgcolor**: Arkaplan rengi (CSS ile yapılması önerilir)
> + **width/height**: Hücre genişlik/yükseklik (CSS ile yapılması önerilir)

**Çıktı:**

![table](images/table.png)

# `span` etiketi:

+ `<span>` etiketi, HTML'de **metin veya belge içindeki belirli bir bölümü işaretlemek** için kullanılan satır içi (inline) bir elementtir.

> [!NOTE]
> **Temel Özellikleri:**
> - Satır içi elementtir (blok oluşturmaz)
> - Kendi başına görsel bir değişiklik yapmaz.
> - CSS ve JavaScript ile kullanılmak üzere tasarlanmıştır.
> - Diğer elementleri gruplamak için idealdir


# `div` etiketi:

+ `<div>` (division - bölüm) etiketi, HTML'de **içerik blokları oluşturmak** için kullanılan temel bir blok-level (blok düzeyinde) elementtir.

> [!NOTE] Title
> **Temel Özellikleri:**
> + Blok-level elementtir (yeni satırda başlar ve tüm genişliği kaplar).
> + Kendi başına görsel bir değişiklik yapmaz.
> + Sayfa düzeni ve CSS/JavaScript ile kullanım için tasarlanmıştır.
> + Diğer elementleri gruplamak için idealdir


> [!CAUTION]
> 1. `<div>` semantik anlam taşımaz (HTML5'te genel amaçlı kapsayıcıdır).
> 2. Gereksiz yere çok fazla div kullanımı ("div soup") kod okunabilirliğini azaltır.
> 3. CSS sınıflarıyla birlikte kullanıldığında en etkilidir.
> 4. Mümkün olduğunda semantik HTML5 elementleri tercih edilmelidir.

## `div` etiketi vs `span` etiketi karşılaştırılması:

|Özellik|`<div>`|`<span>`|
|---|---|---|
|**Görüntü Tipi**|Blok (block)|Satır içi (inline)|
|**Varsayılan**|Yeni satır başlatır|Hiçbir stil uygulamaz|
|**Kullanım**|Büyük içerik blokları|Metin içinde küçük bölümler|

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <title>
            İlk Sayfam
        </title>
    </head>
    <body>
        <span style="background-color: red;"
            >This element is inline</span>
        <div style="background-color: green;"
            >This element is block-level</div>
    </body>
</html>
```

**Çıktı:**

![span_vs_div](images/span_vs_div.png)

# Iframe:

+ `<iframe>` (Inline Frame), bir HTML belgesi içinde başka bir HTML belgesini gömmenizi sağlayan bir HTML elementidir.
+ "Çerçeve içinde çerçeve" anlamına gelir ve web sayfalarına harici içerik eklemek için yaygın olarak kullanılır.
+ Bir HTML iframe, bir web sayfasını bir web sayfası içerisinde görüntülemek için kullanılır.(Kaynak: [w3school](https://www.w3schools.com/HTML/html_iframe.asp))


> [!NOTE]
> **Nitelikleri(Attributes):**
> - **src**: Eklenecek sayfanın URL'sini belirtir.
> - **width**: Çerçevenin genişliği (piksel veya yüzde olarak).
> - **height**: Çerçevenin yüksekliği (piksel veya yüzde olarak).
> - **frameborder**: Çerçeve kenarlığını gösterir/gizler (0 veya 1).
> - **scrolling**: Kaydırma çubuklarını ayarlar ("yes", "no", "auto").

### Örnek 1: Dışarıdan

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <meta name="description" content="HTML meta etiketi nedir? Meta description nasıl yazılır? SEO için en iyi meta açıklama örnekleri.">
        <meta name="keywords" content="HTML, web geliştirme, frontend, programlama">
        <meta name="author" content="Tanju Yücel, tanju@example.com">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="refresh" content="30">
        <title>
            Iframe Kullanımı
        </title>
    </head>
    <body>
        <iframe
            src="https://www.example.com/"
            frameborder= "1"
            width="500" height="400"
        ></iframe>
    </body>
</html>
```

**Çıktı:**

![iframe](images/iframe.png)


### Örnek 2: İçeriden

**nginx.conf**

```nginx
user www-data;
worker_processes auto;

events {
	worker_connections 1024;
}

http {
	include mine.types;

	server {
		listen 8080;
		server_name 192.168.1.132;

		root /var/www/html/HTML;

		index index.html;

		location / {
			try_files $uri $uri/ =404;
		}

		location /reklam {
			alias /var/www/html/HTML;
			index ad.html;
		}
	}
}
```

**index.html**

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <meta name="description" content="HTML meta etiketi nedir? Meta description nasıl yazılır? SEO için en iyi meta açıklama örnekleri.">
        <meta name="keywords" content="HTML, web geliştirme, frontend, programlama">
        <meta name="author" content="Tanju Yücel, tanju@example.com">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="refresh" content="30">
        <title>
            Iframe Kullanımı
        </title>
    </head>
    <body>
        <!-- Aynı klasör içerisinde 1 -->
        <iframe
            src="ad.html"
            frameborder= "1"
            width="500" height="400"
        ></iframe>
        <br>
        <!-- Nginx'in Farklı Location Context'inden 2 -->
        <iframe
            src="http://192.168.1.132:8080/reklam/"
        ></iframe>
    </body>
</html>
```

> **Explanation:**
> 1. `index.html` dosyası ile `ad.html` aynı klasörde bulunmaktadır.
> 2. nginx'in başka bir `location context`'inden yayınlan URI, `iframe` içerisinde kullanabiliriz.


**Mevcut dizin**

```shell
ls -ltr
```

**ls Çıktısı:**

```shell
total 243592
-rw-r--r-- 1 root     root         18328 Feb 25  2022 linux.jpg
-rw-r--r-- 1 root     root         69947 Apr  1 17:47 index.html.1
-rw-rw-r-- 1 ottoman  ottoman    2836968 Apr  1 17:57 alex-eglair.mp3
-rw-rw-r-- 1 ottoman  ottoman  159115728 Apr  3 16:02 Linux_Find.mkv
-rw-rw-r-- 1 ottoman  ottoman   87372446 Apr  3 16:39 Go_prog.mp4
-rw-r--r-- 1 root     root           282 Apr  3 17:18 linux.html
-rw-r--r-- 1 root     root           477 Apr 28 12:45 ad.html
-rw-r--r-- 1 www-data www-data       708 Apr 28 13:48 index.html
```

> **Explanation:**
> + Çıktıyı incelersek `index.html` dosyası ile `ad.html` dosyası aynı klasör olduğu görülmektedir. 

**ad.html**

```html
 <!DOCTYPE html>

<html lang=tr>
        <head>
                <meta charset="UTF-8">
                <meta name="description" content="HTML meta etiketi nedir? ">
                <meta name="keywords" content="HTML, web geliştirme, frontend, programlama">
                <meta name="author" content="Tanju Yücel, tanju@example.com">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>
                        Reklam Sitesi
                </title>
        </head>
        <body style="background-color: aqua;">
                <h1>Bu arabayı al</h1>
        </body>
</html>
```

**Sitenin Görünümü:**

![iframe2](images/iframe2.png)



> [!CAUTION]
> **Güvenlik Notları:**
> + `<iframe>` kullanırken güvenlik risklerine dikkat edin.
> +  Güvenmediğiniz sitelerden içerik gömme
> + `sandbox` özelliğini kullanarak gömülü içeriğin yetkilerini kısıtlayın
> + Clickjacking saldırılarına karşı `X-Frame-Options` header'ını kontrol edin

# Button Etiketi:

+ HTML'de `<button>` etiketi, kullanıcıların tıklayabileceği etkileşimli bir düğme (buton) oluşturmak için kullanılır.
+ Bu düğmeler formları göndermek, iletişim kutularını açmak veya JavaScript fonksiyonlarını tetiklemek gibi çeşitli işlevler(fonksiyonlar) gerçekleştirebilir.
+ `<button>` etiketi tıklanabilir bir düğmeyi tanımlar.


> [!TIP]
> + Tarayıcılara ne tür bir Button olduğunu söylemek için, `<button>` öğesi için her zaman type özniteliğini(attribute) belirtin.


> [!NOTE]
> + `<button>` öğesinin içine metin (ve  `<i>`, `<b>`, `<strong>`, `<br>`, `<img>` vb. etiketler) koyabilirsiniz.
> + `<input>` elemanı ile oluşturulmuş bir buton ile bu mümkün değildir!

## `<button>` vs `<input type="button">`:

### `<button>` Etiketi:
 
 + **İçerik olarak zengin öğeler alabilir**: `<button>` etiketinin içine **metin**, diğer HTML etiketleri (örneğin `<i>`, `<b>`, `<strong>`, `<br>`, `<img>`) ve hatta başka bileşenler koyabilirsiniz.

```html
<button>
    <i class="fa fa-check"></i> Kaydet <!-- İkonlu buton -->
    <br>
    <small>Tıklayarak onay verirsiniz</small>
</button>
```

###  `<input type="button">`:

+ **Sadece düz metin alabilir**: `<input>` elementiyle oluşturulan butonların **`value`** özelliği vardır, ama içine başka HTML etiketleri veya satır atlama (`<br>`) gibi öğeler ekleyemezsiniz.

```html
<input type="button" value="Kaydet"> <!-- Sadece metin -->
```

+ Eğer `value` kısmına HTML kodu yazarsanız, tarayıcı onu metin olarak gösterir (örneğin `<b>Kalın</b>` yazarsanız, etiketler görünür).


> [!NOTE]
> + **`<button>`** → Daha esnek, içine HTML öğeleri yerleştirilebilir.
> + **`<input type="button">`** → Sadece düz metin (`value` ile) kabul eder, görsel özelleştirme sınırlıdır.


## Button Türleri:

### 1. submit button:

+ Form verilerini sunucuya gönderir.

```html
<button type="submit">Gönder</button>
```

### 2. reset button:

+ Formdaki tüm alanları varsayılan değerlerine sıfırlar.

```html
<button type="reset">Sıfırla</button>
```

### 3. Normal Button:

+ Varsayılan davranışı yoktur, genellikle JavaScript ile kullanılır.
+ Html Events da `onclick` özniteliğinde sık sık kullanılır.

```html
<button type="button">Tıkla</button>
```

## Öznitelikleri(Attributes):

|Özellik|Açıklama|
|---|---|
|`type`|Düğme türünü belirtir (`submit`, `reset` veya `button`)|
|`disabled`|Düğmeyi devre dışı bırakır|
|`autofocus`|Sayfa yüklendiğinde düğmeye otomatik odaklanır|
|`form`|Düğmenin ilişkili olduğu formun ID'sini belirtir|
|`formaction`|Form verisinin gönderileceği URL'yi geçersiz kılar|
|`formmethod`|Form gönderme metodunu belirtir (GET, POST)|
|`name`|Form gönderildiğinde kullanılacak isim|
|`value`|Form gönderildiğinde kullanılacak değer|


> [!NOTE]
> 1. **Global Attributes:**
> 	- `<button>` etiketi HTML'deki [Global Attribute](https://www.w3schools.com/tags/ref_standardattributes.asp)'leri de destekler.
> 2. **Event Attributes:**
> 	- `<button>` etiketi HTML'deki [Event Attributes](https://www.w3schools.com/tags/ref_eventattributes.asp)'leri de destekler.


# input Etiketi:



# Form:

+ HTML'de `<form>` etiketi, kullanıcıların web sayfası üzerinden veri girebileceği ve bu verileri sunucuya gönderebileceği interaktif alanlar oluşturmak için kullanılır.
+ Formlar, web'in en temel etkileşim araçlarından biridir.

## Örnek 1: Temel Kullanımı

**nginx.conf**

```nginx
user www-data;
worker_processes auto;

events {
	worker_connections 1024;
}

http {
	include mine.types;

	server {
		listen 8080;
		server_name 192.168.1.132;

		root /var/www/html/HTML;

		index index.html;

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

> **Explanation:**
> + **Hatırlatma:** `fastcgi_pass` parametre karşılığını `sudo find / -name '*fpm.sock'` komut ile buluyoruz.

**index.html**

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <meta name="description" content="HTML meta etiketi nedir?">
        <meta name="author" content="Tanju Yücel, tanju@example.com">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>
            Iframe Kullanımı
        </title>
    </head>
    <body>
        <h3> Form 1: label </h3>
        <form action="kayit.php" method="POST">
            <label for="user_name">Ad:</label><br>
            <input type="text" name="user_name" id="user_name"><br>
            <label for="user_surname">Soyadı:</label><br>
            <input type="text" name="user_surname" id="user_surname"><br><br>
            <input type="submit" value="Gönder">
            <!-- <button type="submi"t value="Send">Gönder</button> -->
            <input type="reset" value="Sıfırla">
        </form>
        <hr>
        <h3> Form 2: placeholder </h3>
        <form action="kayit.php" method="POST">
            <input type="text" name="user_name" placeholder="Adınız"
             ><br><br>
            <input type="text" name="user_surname" placeholder="Soyadınız"
            ><br><br>
            <button type="submit" value="Send"><b>Gönder</b></button>
            <button type="reset"><i>Sıfırla</i></button>
        </form>
    </body>
</html>
```

> **Explanaiton:**
> 1. **Form 1: label**
> 	- Yönlendirmeyi `label` etiketi ile yaptık
> 	- Gönder butonunu `input` etiketi ile yaptık ama dikkat ederseniz `Gönder` yazısını üzerinde şekillendirme yapmıyoruz.
> 	- Form verisini  sunucudaki `kayıt.php` backend'ine gönderiyoruz. Bu için `form`'un `action` özniteliğini(attribute) kullanıyoruz.
> 	- `label` etiketi ile `input`etiketini birleştirmek için `label` etiketinin `for` özniteliği ile `input` etiketinin `id` özniteliği eşit olmalıdır.
> 	- *Sıfırla:* `input` etiketi ile yazılmış olan sıfırla butonu girilen verileri siler.
> 2. **Form 2: placeholder**
> 	- Yönlendirmeyi `input` etiketinin `placeholder` attribute ile yapıyoruz.
> 	- Gönder butonunu için `button` etiketi kullanıyoruz. Eğer dikkat ederseniz Gönder yazısını `b` etiketi ile daha kalın hale getiriyoruz.
> 	- Yine backend'e göndermek için `form` etiketin `action` özniteliğini kullanıyoruz.
> 	- *Sıfırla:* `button` etiketi ile yazılmış olan sıfırla butonu girilen verileri siler.

**Backend:**

```php
<?php
// Form verilerini al
$userName = $_POST['user_name'];
$userSurname = $_POST['user_surname'];

// Veritabanına kaydetme işlemi (örnek amaçlı basit bir işlem)
// Gerçek bir uygulamada burada veritabanı bağlantısı ve SQL sorguları kullanılır.
echo "Kullanıcı Adı: " . htmlspecialchars($userName) . "<br>";
echo "Kullanıcı Soyadı: " . htmlspecialchars($userSurname) . "<br>";
echo "Kayıt işlemi başarılı!";
?>
```

> **Explanation:**
> + `$_POST`, PHP'de HTTP POST metoduyla gönderilen verileri almak için kullanılan önceden tanımlanmış (süper global) bir dizidir.
> + `$_POST`, *değerleri `form` etiketi içerisindeki `input` etiketinin `name` özniteliğinden(attribute) çekmektedir.*
> + `htmlspecialchars()`, PHP'de özel karakterleri HTML varlıklarına dönüştüren bir fonksiyondur. Bu, XSS (Cross-Site Scripting) gibi güvenlik açıklarını önlemek için kullanılan önemli bir fonksiyondur.

**Görünüm:**

![form](images/form.png)


## Örnek 2: Kullanıcı ve Parola

```nginx
user www-data;
worker_processes auto;

events {
	worker_connections 1024;
}

http {
	include mine.types;

	server {
		listen 8080;
		server_name 192.168.1.132;

		root /var/www/html/HTML;

		index index.html;

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

**index.html**

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <meta name="description" content="HTML meta etiketi nedir?">
        <meta name="author" content="Tanju Yücel, tanju@example.com">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>
            Form Kullanımı
        </title>
    </head>
    <body>
        <h3>Kullanıcı Girişi:</h3>
        <form action="backend.php" method="POST">
            <input type="text" name="user_name" placeholder="Adınız">
            <br><br>
            <input type="password" name="user_password" placeholder="Şifreniz">
            <br><br>
            <button type="submit" value="Send"><b>Gönder</b></button>
        </form>
    </body>
</html>
```
> **Explanation:**
> + form yapımızda iki tane girdimiz var; birincisi *kullanıcı isimi* ikincisi ise *kullanıcı şifresi* 
> + Sunucuda olan `backend.php` dosyasına gönderip çalıştırıyoruz.


**backend.php**

```php
<?php
// Gönderilen veri POST isteği gönderildiğini garantiliyoruz.
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Formdan gelen veriyi al
    $user_name = $_POST['user_name'];
    $user_passwd =  $_POST['user_password'];

    $user_passwd_hash = password_hash(
        $user_passwd, PASSWORD_DEFAULT
    );

    // Basit Kontrol
    if (!empty($user_name) && !empty($user_passwd)) {
        echo "Kullanıcı Adı: " . htmlspecialchars($user_name);
        # echo "<br>Şifre: [Güvenlik nedeniyle gösterilmiyor]";
        if ( password_verify($user_passwd, $user_passwd_hash) ) {
            echo "<br>Şifre Doğru..." . $user_passwd_hash;
        }
    } else {
        echo "Lütfen tüm alanları doldurun!";
    }
}
?>
```


**POST isteği:**

```shell
 curl -i -X POST -F "user_name=ottoman" -F "user_password=1234"  http://192.168.1.132:8080/backend.php
```

```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sat, 03 May 2025 13:20:20 GMT
Content-Type: text/html; charset=UTF-8
Transfer-Encoding: chunked
Connection: keep-alive

Kullanıcı Adı: ottoman<br>Şifre Doğru: $2y$10$InRep4TpHIfjigfa9DqSBeIJm3mNEiyPq5KveeUyjgOdEusY0cuB.
```

## Örnek 3: Form verisini dosyaya yazma

**nginx.conf:**

```nginx
user www-data;

worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include mime.types;
	server {
	    listen 8080;
	    server_name 192.168.1.132;

	    root /var/www/html/phpDers1;

	    index index.html;

	    location / {
	        try_files $uri $uri/ =404;
	    }

	    location ~ \.php$ {
	        include fastcgi.conf;
	        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
	        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
	    }
	}
}
```

**index.html**

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <meta name="description" content="HTML meta etiketi nedir?">
        <meta name="author" content="Tanju Yücel, tanju@example.com">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>
            Form Kullanımı
        </title>
    </head>
    <body>
        <h3>Dosyaya Yazma:</h3>
        <form action="save_file.php" method="POST">
            <input type="text" name="user_name" placeholder="Adınız">
            <br><br>
            <input type="email" name="user_email"
                pattern="[A-Za-z0-9]+@linux.com"
                placeholder="E-Postanız">
            <br><br>
            <button type="submit" value="Send"><b>Gönder</b></button>
        </form>
    </body>
</html>
```
> **Explanation:**
> + 

**backend.php**

```php
<?php
//
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Formdan gelen veriyi al
    $user_name = $_POST['user_name'] ?: ' _ ';
    $user_email = $_POST['user_email'] ?: "No Given Email";

    $user_name = strip_tags(trim($user_name));
    $user_email = strip_tags(trim($user_email));

    // echo gettype($user_name) . "\n";

    $file = fopen('/var/www/html/backend/save_users.txt', 'a');
    if ($file) {
        fwrite($file, "$user_name : $user_email\n");
        fclose($file);
        echo 'İşlem Başarılı';
        //
        header("Location: thank_you.html");
        exit;
    } else {
        echo 'Bir hata oluştu';
    }
}
?>
```

> **Explanation:**
> + `$_SERVER[...]`: 
> + `$_POST`:
> + 

**Yazılacak Dosya:**

```shell
cd /var/www/html; sudo mkdir backend
```

```shell
sudo chown -R www-data:www-data /var/www/html/backend
```

```shell
sudo chmod 755 /var/www/html/backend 
```


> [!CAUTION]
> + `www-data` kullanıcısın yazma işleminin yapabilmesi için gerekli izinleri vermemiz gerekmektedir.
> + Aksi takdirde nginx `access.log` ve `error.log` dosyalarına hata mesajı olarak `permission denied` yazılacaktır.
> ```log
> ==> error.log <==
2025/05/08 17:31:10 [error] 27608#0: *348 FastCGI sent in stderr: "PHP message: PHP Warning:  fopen(/var/www/html/backend/save_users.txt): Failed to open stream: Permission denied in /var/www/html/phpDers1/save_file.php on line 13" while reading response header from upstream, client: 192.168.1.106, server: 192.168.1.132, request: "POST /save_file.php HTTP/1.1", upstream: "fastcgi://unix:/run/php/php8.1-fpm.sock:", host: "192.168.1.132:8080", referrer: "http://192.168.1.132:8080/"
> ```


**Dosyayı İzleme:**

+ backend tarafında olan `backend.php` programın dosyaya yazma işlemini canlı olarak takip etmek istersek;
+ Linux `tail` komutun ve `-f` parametresi ile `save_users.txt` dosyasını canlı olarak takip edebiliriz.

```shell
tail -f /var/www/html/backend/save_users.txt
```


**İstemci Tarafı:**

```shell
 curl -i -X POST -F "user_name=ottoman" -F "user_email=tanjuyuca@linux.com"  http://192.168.1.132:8080/save_file.php
```

```http
HTTP/1.1 302 Found
Server: nginx/1.27.2
Date: Tue, 06 May 2025 15:46:16 GMT
Content-Type: text/html; charset=UTF-8
Transfer-Encoding: chunked
Connection: keep-alive
Location: thank_you.html

İşlem Başarılı
```

**Tarayıcı Çıktısı:**

![form_write_file](images/form_write_file.png)

## Örnek 4: Form verisini Database yazma:

**Senaryo:** 
+ nginx üzerinden servis yapacağız. 
+ *Frontend* tarafında `<input type=text ...> ` ve `<input type=date ...>` etiketlerini kullanacağız. 
+ *Backend* tarafında PHP ile PostgreSQL'e bağlanacağız ve PHP ile PostgreSQL'e veri girişi yapacağız.
+ Database tarafında `linus_d` veritabanına manuel olarak `members2` adında tablo oluşturacağız.

### Nginx:

**nginx.conf:**

```nginx
user www-data;

worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include mime.types;
	server {
	    listen 80;
	    server_name 192.168.1.132;

	    root  /var/www/html/connectPostgreSQL;

	    index index.html;

	    location / {
	        try_files $uri $uri/ =404;
	    }

	    location ~ \.php$ {
	        include fastcgi.conf;
	        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
	        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
	    }
	}
}
```

### Veritabanı: PosgreSQL

```shell
sudo -u tanju -i psql -d linus_d
```

+ `linus_d` veritabanın da `members2` adında tablo oluşturuyoruz.

```sql
 CREATE TABLE members2 (
mem_ID SERIAL PRIMARY KEY,
mem_name VARCHAR(255),
mem_user_date DATE,
mem_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP);
```

### Frontend:

**index.html:**

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <meta name="description" content="HTML meta etiketi nedir?">
        <meta name="author" content="Tanju Yücel, tanju@example.com">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>
            Form ve PostgreSQL
        </title>
    </head>
    <body>
        <h3>PostgreSQL Veritabanına Yazma:</h3>
        <form action="index.php" method="POST">
            <input type="text" name="user_name" placeholder="Adınız" required>
            <br><br>
            <input type="date" name="user_date">
            <br><br>
            <button type="submit" value="Send"><b>Gönder</b></button>
        </form>
    </body>
</html>
```

> + Gönder butonunu `<button type="submit" value="Send"><b>Gönder</b></button>` etiketine alternatif olarak
> + `<input type="submit" value="Gönder">` kullanılabilir. Fakat `<b>` etiketi kullanılamayacaktır.

### Backend:

**connect_postgres:**

```php
<?php
try {
    $database_psql = new PDO (
        "pgsql:host=192.168.1.132;
        port=5432;
        dbname=linus_d;
        user=tanju;
        password=1234tyod"
    );
} catch (PDOException $e) {
    echo $e->getMessage();
}
?>
```

**index.php:**

```php
<?php
    require_once "connect_postgres.php";

//
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Formdan gelen veriyi al
    $user_name = $_POST['user_name'] ?: ' _ ';
    $user_date = $_POST['user_date'] ?: "No Given Email";

    $user_name = strip_tags(trim($user_name));
    $user_date = strip_tags(trim($user_date));

    $database_psql->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_SILENT);

    $result = $database_psql->prepare(
        "INSERT INTO members2(mem_name, mem_user_date) VALUES (?, ?);"
    );

    // execute fonksiyonun true veya false değeri döner.
    $bool_result = $result->execute(
        [ $user_name, $user_date]
    );

    // $bool_result değişkenine true dönerse if bloğu çalışır.
    // Eğer false dönerse else bloğu çalışır.
    if ($bool_result) {
        echo "Veri ekleme başarılı...";
    } else {
        print_r($result->errorinfo());
        echo "Veri ekleme başarısız!";
    }
}
```

### İstemci:

![form_date](images/form_date.png)


> [!CAUTION]
> + Eğer `form` ile `radio` verilerini `backend` sunucusuna göndermek isterseniz, mutlaka `input` etiketinin `value` özniteliğini mutlak yazmanız gerekmektedir.
> ```html
> <input type="radio" nama="user_gender" id="m_gender" value="male">
> <input type="radio" nama="user_gender" id="f_gender" value="female">
> ``` 


# HTML Events:

## Mouse Events:

### 1. `onclick()`:

+ onclick, element üzerinde fare tıklandığında tetiklenir.

#### Örnek 1: Button ile

```html
<!DOCTYPE html>

<html lang=tr>
    <head>
        <meta charset="UTF-8">
        <meta name="description" content="HTML meta etiketi nedir?">
        <meta name="author" content="Tanju Yücel, tanju@example.com">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>
            Iframe Kullanımı
        </title>
    </head>
    <body>
        <button type="button" onclick="click_func()">Tıkla</button>
        <p id="changeText">Press Button</p>
        <script>
            function click_func() {
                document.getElementById("changeText")
                            .innerHTML="Button is pressed!"
            }
        </script>
    </body>
</html>
```


