#nginx 

```nginx
location [modifier] [URI] {
  ...
  ...
}
```


+ Location Context, nginx'in istek URI'sini neye göre kontrol etmesi gerektiğini tanımlar.



| Search-Order | Modifier | Description                                                  |     Match-Type     | Stops-search-on-match |
| :----------: | :------: | ------------------------------------------------------------ | :----------------: | :-------------------: |
|     1st      |    =     | The URI must match the specified pattern exactly             |   Simple-string    |          Yes          |
|     2nd      |    ^~    | The URI must begin with the specified pattern                |   Simple-string    |          Yes          |
|     3rd      |  (None)  | The URI must begin with the specified pattern                |   Simple-string    |          No           |
|     4th      |    ~     | The URI must be a case-sensitive match to the specified Rx   | Perl-Compatible-Rx |   Yes (first match)   |
|     4th      |    ~*    | The URI must be a case-insensitive match to the specified Rx | Perl-Compatible-Rx |   Yes (first match)   |
|     N/A      |    @     | Defines a named location block.                              |   Simple-string    |          Yes          |

### Location Context nedir?

**nginx.conf**
```nginx
events {
}

http {

    include mime.types;

    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;
    }
}
```

**GET request:**
```shell
$ curl -X GET -I http://192.168.1.132 
```

>**Explanation:**
>+ Bu config yapısına göre, GET isteği atığımızda `root directive`'in göstermiş olduğu yolu(path) servis edecetir.


> [!TIP]
> + `Location Context` genel itibarı ile `Server Context`'ler içerisinde tanımlanır.
> + `Server Context` içerisinde tanımlanan `Location Context`'leri sırası önemli değildir.

### Location Modifiers:

+ NGINX'te **`location` contextindeki modifier (değiştirici)**, bir `location` bloğunun URL ile nasıl eşleşeceğini belirlemek için kullanılan özel anahtar kelimedir.
+ Modifier, eşleşme türünü ve önceliğini tanımlayarak, gelen bir isteğin hangi `location` bloğuna yönlendirileceğini kontrol eder.
+ `Modifier`'in olması veya olmaması nginx'in `location block` eşleştirme girişim şeklini etkileyecektir.
+ Birden fazla location bloğumuz varsa ve iki location bloğundan fazlası veya birden fazla location bloğu istek URI'nizle eşleşiyorsa, en iyi eşleşme, `modifier` göre belirlenecektir


> [!IMPORTANT]
> + Birden fazla `location` bloğu aynı anda eşleşebilir. NGINX, aşağıdaki sıralamaya göre bir `location` bloğu seçer:
> 1. **Tam eşleşme(`=`):** İlk önce tam eşleşmeler kontrol edilir.
> 2. **Joker önek eşleşmesi(`^~`):** Eğer bir `^~` modifier'lı blok eşleşirse, başka eşleşmeler aranmaz.
> 3. **Düzenli ifade eşleşmeleri(`~`,`~*`):** İlk eşleşen regex bloğu uygulanır.
> 4. **En uzun önek eşleşmesi:**  Eğer yukarıdaki türlerden hiçbirine uymazsa, en uzun eşleşen önek seçilir.
> 5. **Varsayılan (Genel) Eşleşme:** Hiçbir eşleşme bulunmazsa, en genel blok (örn. `/`) uygulanır.

#### 1.None Modifier:
##### Syntax:
```nginx
location [URI] {
	...
	...
}
```

##### Örnek 1:
```nginx
location /no_modifier {
    return 200 "Location Modifier is None";
}
```

---
**GET request**
```shell
$ curl -X GET -i http://192.168.1.132/no_modifier 
```

```shell
$ curl -X GET -i http://192.168.1.132/no_modifier/api
```

```shell
$ curl -X GET -i http://192.168.1.132/no_modifier/api/v1
```

**Curl Çıktıları:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Mon, 18 Nov 2024 14:31:25 GMT
Content-Type: text/plain
Content-Length: 25
Connection: keep-alive

Location Modifier is None%
```

> **Explanation:**
> + Üç `curl` komutun çıktısı aynı ve http 200 kodun başarılı olduğunu göstermektedir. 
> + Modifier belirtilmezse, bu durumda belirtilen pattern, istek URL'sinin başlangıcıyla (önek olarak - prefix match) eşleşir.
> + *Örneğin*, `/api` pattern'i `http://192.168.1.132/api/v1` veya `http://192.168.1.132/api` ile eşleşir.
> + *Varsayılan olarak kullanılır.*

##### Örnek 2: Bir Dizin İçin

```nginx
location /no_modifier/ {
    return 200 "Location Modifier is None and for directory";
}
```
> **Explanation:**
> + **Uyarı:** Yukarıdaki `Örnek 1`'den farklı olarak `/` eklenmiştir.

---
**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/no_modifier/ 
```

```shell
$ curl -X GET -i http://192.168.1.132/no_modifier/linux
```

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Tue, 19 Nov 2024 17:19:35 GMT
Content-Type: text/plain
Content-Length: 30
Connection: keep-alive

Location Modifier is None and for directory%
```
> **Explanation:**
> + Bu URI'lar http 200 kodu vermektedir yani başarılır.


---

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/no_modifier
```

**Curl çıktısı:**
```shell
HTTP/1.1 404 Not Found
Server: nginx/1.27.2
Date: Tue, 19 Nov 2024 17:43:19 GMT
Content-Type: text/html
Content-Length: 153
Connection: keep-alive

<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.27.2</center>
</body>
</html>
```
> **Explanation:**
> + Fakat forward slash'ı(`/`) kaldırdığımızda http 404 kodu dönmektedir.

##### Örnek 3: En uzun önek eşleşmesi:

```nginx
location /static/distro/ubuntu.png {
    return 200 "longest url and exact match";
}
```
> **Explanation:**
> + Tam `URI` yolunu vermiştir ve bu en uzun önektir.

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/static/distro/ubuntu.png 
```
> **Explanation:**
> + Bu `location context` çalıştırabilmemiz için IP'den sonra tam yolunu vermemiz gerekmektedir.

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Tue, 19 Nov 2024 18:44:41 GMT
Content-Type: image/png
Content-Length: 27
Connection: keep-alive

longest url and exact match%
```
> **Explanation:**
> + 

#### 2.Tam Eşleşme(`=`):
+ Bu modifier, istek URL'sinin belirtilen pattern ile **tam olarak eşleşmesi** gerektiğini belirtir.
+ **En yüksek önceliğe** sahiptir. Eğer bir tam eşleşme bulunursa, diğer eşleşmeler kontrol edilmez.
+ İngilizce karşılığı: `Exact Match`

##### Syntax:
```nginx
location = [URI] {
	...
	...
}
```

##### Örnek 1:
```nginx
location = /exact_match {
    return 200 "Lcoation Modifier is Exact Match(=)";
}
```

---
**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/exact_match
```

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Mon, 18 Nov 2024 13:13:49 GMT
Content-Type: text/plain
Content-Length: 35
Connection: keep-alive

Lcoation Modifier is Exact Match(=)%
```
> **Explanation:**
> + Yalnızca `http://192.168.1.132/exact_match` isteği bu blokla eşleşir.
> + Http 200 kodu ile başarılı olduğunu anlayabiliriz.

---
**GET requests:**
```shell
$ curl -X GET -i http://192.168.1.132/exact_match/
```

```shell
$ curl -X GET -i http://192.168.1.132/about?foo=bar
```

**Curl Çıktıları:**
```shell
HTTP/1.1 404 Not Found
Server: nginx/1.27.2
Date: Mon, 18 Nov 2024 13:19:33 GMT
Content-Type: text/html
Content-Length: 153
Connection: keep-alive

<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.27.2</center>
</body>
</html>
```

> **Explanation:**
> + `http://192.168.1.132/about/` veya `http://192.168.1.132/about?foo=bar` gibi isteklerle eşleşmez.
> + Http 404 kodu(*sunucu istek kaynağını bulamıyor*) ile başarısız olduğunu anlayabiliriz.
> + Her iki `curl` komut da aynı hata mesajını verecektir.

##### Örnek 2:
+ Eğer hem `None Location Context` hem de` Exact Match Location Context` aynı URI sahipse, nginx nasıl davranır?
**nginx.conf**
```nginx
http {

    include mime.types;

    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;

        location /contactUs {
            return 200 "None Modifier prefix match";
        }

        location = /contactUs {
            return 200 "Exact Modifier";
        }

    }
}
```
> **Explanation:**
> + İki tane location context mevcut ve her ikisi de aynı kaynağı(`/contactUs`) göstermektedir. 

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/contactUs
```

**Çıktı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sat, 23 Nov 2024 20:55:02 GMT
Content-Type: text/plain
Content-Length: 14
Connection: keep-alive

Exact Modifier%
```
> **Explanation:**
> + Çıktıdan da anlaşılacağı üzeri ikinci location çalışmıştır. Bunun sebebi exact modifier, none modifier'dan daha üst önceliğe sahip olmasıdır.

---

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/contactUs/linux
```

**Çıktı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sat, 23 Nov 2024 21:15:40 GMT
Content-Type: text/plain
Content-Length: 26
Connection: keep-alive

None Modifier prefix match%
```
> **Explanation:**
> + `/contactUs` kaynağından sonra bir `/linux` adında kaynak daha verilmiştir. Bunun sonucu olarak None modifier location blok çalışmıştır.
> + Çünkü, exact location blok adı üzerinde tam eşleşme ister. Aksi takdirde çalışmaz fakat none modifer ise eşleşme olabilmesi için `/contactUs` kaynağı olması yeterlidir.

---

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/contac
```

**Çıktı:**
```shell
HTTP/1.1 404 Not Found
Server: nginx/1.27.2
Date: Sat, 23 Nov 2024 21:39:21 GMT
Content-Type: text/html
Content-Length: 153
Connection: keep-alive

<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.27.2</center>
</body>
</html>
```
****
> **Explanation:**
> + `/contac` kaynağı ile istek yaptığımızda hem `exact modifier` ile hem de `none modifier` ile bir eşleşme olmadığını görebiliyoruz.
> + Çünkü, `exact modifier` sadece `/contactUs` bakarken `none modifier` ise `/contactUs` ile başlamasını bakıyordu. Fakat her ikisinde de uyuşmamaktadır.

#### 3.Regex Eşleşme:


> [!WARNING]
> + `Location Context` de `regex` kullanabilmek için;
> + Debian temeli işletim sistemlerinde `sudo apt install libpcre3 libpcre3-dev` ve REHL temeli işletim sistemlerinde `sudo dnf install pcre pcre-devel` komutu ile kütüphaneler kurulması gerekir.
> + Eğer kaynak kodundan derleme ile nginx kurulumu yapıyorsanız, `--with-pcre` modülü eklemeniz gerekmektedir.
> + `nginx -V` komut ile hangi modüllerin yüklü olduğunu görebiliriz.


##### 3.1.Regex Case Sensitive(`~`):
##### Syntax:
```nginx
location ~ [URI] {
	...
	...
}
```
> **Explanation:**
> + Temel taslağın sunmakta ve   tilda(~) URI küçük harf veya büyük harf duyarlığına bakar.
> + Yani URI, *linux* olanla *Linux* olan aynı değildir.

##### Örnek 1:
```nginx
location ~ \.(png|gif) {
	return 200 "Location Modifier is Regex Case Sensitive Match";
}
```

> **Explanation:**
> tilda(~) ifadesi : ==case sensitive regular expression== yani küçük büyük harfe duyarlı ve düzenli ifadeleri dikkate almaktadır. `\` backslash *nokta işaretinin* özel anlama gelmesini durduruyor. Yani Regex de *nokta işareti* her hangi bir karaktere karşılık geliyor. 
> [[Nginx Directives#Cache-Control|Cache-Control no-store]] bakınız. 


**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/linux.png  
```

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Mon, 18 Nov 2024 14:51:01 GMT
Content-Type: image/png
Content-Length: 47
Connection: keep-alive

Location Modifier is Regex Case Sensitive Match%
```
> **Explanation:**
> + Location context, regex yapıda `png` veya `gif` uzantılı dosyaları arayacaktır ve `linux.png` bu istenen duruma uygun olduğu için 200 kodu verecektir.

---
**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/linux.gif
```

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Mon, 18 Nov 2024 14:51:11 GMT
Content-Type: image/gif
Content-Length: 47
Connection: keep-alive

Location Modifier is Regex Case Sensitive Match%
```
> **Explanation:**
> + Yukarıdaki gibi regex yapısında `png` veya `gif` uzantılı dosyaları URL'e girildiğinde bu location context çalışacaktır.

---
**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/linux.jpg
```

**Curl Çıktısı:**
```shell
HTTP/1.1 404 Not Found
Server: nginx/1.27.2
Date: Mon, 18 Nov 2024 16:00:28 GMT
Content-Type: text/html
Content-Length: 153
Connection: keep-alive

<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.27.2</center>
</body>
</html>
```
> **Explanation:**
> + Eğer `linux.jpg` gibi uzantısı `jpg` olan bir URI isteği yaptığımızda location context'deki regex'e uygun olmadığı için bu location context'e girmeyecek ve hata verecektir.

---

> [!WARNING]
> + Eğer `curl -X GET -i http://192.168.1.132/linux.PNG` gibi bir istek atarsak bu istek sonucunda bize bir 404 kodu dönecektir.
> + Çünkü, uzantısı(`.PNG`) location context'deki yapıya uygun olmasına rağmen uzantı büyük harf ile yazıldığı için bu location context'e girmeyecektir.

##### Örnek 2:
+ `Server Context` içerinde 2 tane `Location Context` mevcuttur. Biri `none modifier` diğeri ise `regex case sensitive match` ve her ikisinde aynı kaynağı göstermektedir.

**nginx.conf:**
```nginx
events {
}

http {

    include mime.types;

    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;

        location /contactUs {
            return 200 "None Modifier prefix match";
        }

        location ~ /contactUs {
            return 200 "Regex Case Sensitive Modifier";
        }

    }
}
```
> **Explanation:**
> + `Server Context` de None modifier Location Context ve Regex Case Sensitive Modifier Location Context olmak üzeri iki tane Location blok bulunmaktadır.

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/contactUs 
```

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sun, 24 Nov 2024 08:48:23 GMT
Content-Type: text/plain
Content-Length: 29
Connection: keep-alive

Regex Case Sensitive Modifier%
```
> **Explanation:**
> + Çıktıdan da anlaşıldığı üzeri iki `location context`'den `Regex Case Senitive Modifier` gelmiştir.
> + Çünkü, nginx'e göre Regex Modifier'lar none modifier'dan daha önce önceliğe sahip. Yani eğer location context'de aynı kaynak var ise önce regex modifier çalıştırılır.

---

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/CONTACTUS 
```

**Curl Çıktısı:**
```shell
HTTP/1.1 404 Not Found
Server: nginx/1.27.2
Date: Sun, 24 Nov 2024 09:37:04 GMT
Content-Type: text/html
Content-Length: 153
Connection: keep-alive

<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.27.2</center>
</body>
</html>
```
> **Explanation:**
> + Hem nono modifier hem de regex case sensitive modifier büyük-küçük harf duyarlı olduğu için her iki location bloğuna girmedi.

##### 3.2.Regex Case Insensitive(`~*`):
###### Syntax:
```nginx
location ~* [URI] {
	...
	...
}
```
> **Explanation:**
> + Büyük/küçük harf duyarsızdır.

###### Örnek 1:
```nginx
location ~* \.(png|gif) {
	return 200 "Location Modifier is Regex Case Sensitive Match";
}
```
> **Explanation:**
> + Eğer dikkat ederseniz `Regex Case Sensitive Eşleşme` ile aynı `regex` yapısını kullandık ama `~*` ifadesi ile ek küçük büyük harf duyarlılığını ortadan kaldırdık.

**GET requests:**
```shell
$ curl -X GET -i http://192.168.1.132/linux.png
```

```shell
$ curl -X GET -i http://192.168.1.132/linux.PNG
```

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Mon, 18 Nov 2024 18:48:03 GMT
Content-Type: image/png
Content-Length: 47
Connection: keep-alive

Location Modifier is Regex Case Sensitive Match%
```
> **Explanation:**
> + Uzantısı `png` ve uzantısı `PNG` olan iki URI istek yaptığımızda aynı sonucu alıyoruz.
> + Çünkü, `~*` ifadesi küçük harf ve büyük harf duyarlığını ortadan kalırıyor.

---

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/linux.jpg 
```

**Curl Çıktısı:**
```shell
HTTP/1.1 404 Not Found
Server: nginx/1.27.2
Date: Tue, 19 Nov 2024 11:34:50 GMT
Content-Type: text/html
Content-Length: 153
Connection: keep-alive

<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.27.2</center>
</body>
</html>
```
> **Explanation:**
> + Location context'de kullanılan regex yapısında `jpg` uzantılı dosyaları bulmadığı için bu URI'e atılan isteğe bağlı olarak bu `location block` çalışmayacaktır.

###### Örnek 2:
+ `Server Context` içerinde  `None modifier location context` ve `regex case insensitive modifier location context` bulunmaktadır.
+ Bu her iki `location context`  URI üzerinde aynı kaynak üzerinde hizmet vermektedir.

**nginx.conf:**
```nginx
events {
}

http {

    include mime.types;

    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;

        location /contactUs {
            return 200 "None Modifier prefix match";
        }

        location ~* /contactUs {
            return 200 "Regex Case Insensitive Modifier";
        }

    }
}
```
> **Explanation:**
> + Yukarıdaki açıklamada olduğu gibi URI üzerinde aynı kaynağa hizmet vermektedir. 
> + Bu durumda nginx nasıl davranır.

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/CONTACTUS 
```

```shell
$ curl -X GET -i http://192.168.1.132/contactUs
```

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sun, 24 Nov 2024 09:55:00 GMT
Content-Type: text/plain
Content-Length: 31
Connection: keep-alive

Regex Case Insensitive Modifier%
```
> **Explanation:**
> + `/CONTACTUS` ve `/contactUs` kaynakları üzerinden istek atığımızda `regex case insensitive modifier` bloğu çalıştı.
> + Çünkü, `regex case insensitive modifier` büyük-küçük harf duyarlığı değildir.


#### 4.Joker Eşleşmesi(`^~`):
+ **`^~` modifier**, URL yolunun belirtilen pattern ile **önek (prefix)** olarak eşleşip eşleşmediğini kontrol eder.
+ Bu eşleşme, düzenli ifadelerle yapılan eşleşmelerden daha yüksek önceliğe sahiptir. Eğer bir `^~` eşleşmesi bulunursa, diğer regex eşleşmeleri değerlendirilmez.


> [!TIP]
> + Performans optimizasyonu için tasarlanmıştır. 
> + Büyük bir düzenli ifade listesi kullanıyorsanız ve bazı URL öneklerini düzenli ifadelere girmeden işlemek istiyorsanız, joker eşleşme kullanışlıdır.

##### Syntax:
```nginx
location ^~ [URI] {
	...
	...
}
```
> + **Önek eşleşmesidir**, ancak düzenli ifadelerden (regex) önce değerlendirilir.
> + Eğer bir `^~` modifier'lı blok eşleşirse, regex eşleşmeleri kontrol edilmez.

##### Örnek 1: 
```nginx
location ^~ /linux.png {
    return 200 "Joker eşleşmesi çalıştırıldı."
}

location ~* \.(png|gif) {
	return 200 "Location Modifier is Regex Case Sensitive Match";
}
```
> **Explanation:**
> + Joker Eşleşmesini daha iyi anlamak için `regex` yapılı location context ile birlikte kullanılmalıdır.
> + En üsteki joker eşlemesi iken bir alttaki ise `regex case insensitive` eşleşme olmaktadır.

**GET request:**
```shell
$ curl -X GET -i http://192.168.1.132/linux.png
```

**Curl Çıktısı:**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Tue, 19 Nov 2024 13:06:37 GMT
Content-Type: image/png
Content-Length: 17
Connection: keep-alive

Joker Eşleşmesi%
```
> **Explanation:**
> + Eğer çıktıyı incelersek joker Eşleşmesi verdiğini görebiliriz.
> + İstek URI hem joker Eşleşmesi hem de `regex case insensitive` karşılamasına rağmen öncelik hakkı joker eşlemesinin daha fazla olmasından dolayı joker eşleşmesinin bulunduğu `location context` çalışmıştır.

