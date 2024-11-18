#nginx 
```nginx
location [modifier] [URI] {
  ...
  ...
}
```

> [!INFO] Bilgi
> Location bloğunun genel şablonu

### Location Modifiers:

+ NGINX'te **`location` contextindeki modifier (değiştirici)**, bir `location` bloğunun URL ile nasıl eşleşeceğini belirlemek için kullanılan özel anahtar kelimedir.
+ Modifier, eşleşme türünü ve önceliğini tanımlayarak, gelen bir isteğin hangi `location` bloğuna yönlendirileceğini kontrol eder.


> [!IMPORTANT]
> + Birden fazla `location` bloğu aynı anda eşleşebilir. NGINX, aşağıdaki sıralamaya göre bir `location` bloğu seçer:
> 1. **Tam eşleşme(`=`):** İlk önce tam eşleşmeler kontrol edilir.
> 2. **Joker önek eşleşmesi(`^~`):** Eğer bir `^~` modifier'lı blok eşleşirse, başka eşleşmeler aranmaz.
> 3. **Düzenli ifade eşleşmeleri(`~`,`~*`):** İlk eşleşen regex bloğu uygulanır.
> 4. **En uzun önek eşleşmesi:**  Eğer yukarıdaki türlerden hiçbirine uymazsa, en uzun eşleşen önek seçilir.
> 5. **Varsayılan (Genel) Eşleşme:** Hiçbir eşleşme bulunmazsa, en genel blok (örn. `/`) uygulanır.

#### 1.None Modifier:
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
> + Modifier belirtilmezse, bu durumda belirtilen pattern, istek URL'sinin başlangıcıyla (önek olarak) eşleşir.
> + *Örneğin*, `/api` pattern'i `http://192.168.1.132/api/v1` veya `http://192.168.1.132/api` ile eşleşir.
> + *Varsayılan olarak kullanılır.*


#### 2.Tam Eşleşme(`=`):
+ Bu modifier, istek URL'sinin belirtilen pattern ile **tam olarak eşleşmesi** gerektiğini belirtir.
+ **En yüksek önceliğe** sahiptir. Eğer bir tam eşleşme bulunursa, diğer eşleşmeler kontrol edilmez.
+ İngilizce karşılığı: `Exact Match`

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


#### 3.Regex Eşleşme:
##### 3.1.Regex Case Sensitive Eşleşme:
###### Syntax:
```nginx
location ~ [URI] {
	...
	...
}
```
> **Explanation:**
> + Temel taslağın sunmakta ve   tilda(~) URI küçük harf veya büyük harf duyarlığına bakar.
> + Yani URI, *linux* olanla *Linux* olan aynı değildir.

###### Örnek 1:
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

##### 3.2.Regex Case Insensitive Eşleşme:
```nginx
location ~* [URI] {
	...
	...
}
```
> **Explanation:**
> + Büyük/küçük harf duyarsızdır.


#### 4.Joker Eşleşmesi(`^~`):
###### Syntax:
```nginx
location ^~ [URI] {
	...
	...
}
```
> + **Önek eşleşmesidir**, ancak düzenli ifadelerden (regex) önce değerlendirilir.
> + Eğer bir `^~` modifier'lı blok eşleşirse, regex eşleşmeleri kontrol edilmez.

###### Örnek 1: 
```nginx
location ^~ /static/ {
    root /var/www/static;
}
```

