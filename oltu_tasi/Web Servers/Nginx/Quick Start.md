#nginx 

##### 1. Nginx Kurulumu:

> [!CAUTION]
> + *Nginx kurulum* ve *Config dosya ayarları* **Ubuntu 22.04** üzerinde gerçekleştirilmektedir.


```shell
$ sudo apt install nginx
```
> **Explanation:**
> + `apt` paket yöneticisi kullanılarak nginx kurulumu yapılıyoruz.
> + Alternatif kurulum için [[Nginx Config File#Nginx Kurulumu|Nginx Kuruluma]] bakınız.


> [!NOTE]
> + Nginx'in config dosyası `/etc/nginx` dizinde mevcuttur. 
> + Nginx'in log dosyları da `/var/log/nginx` dizininde mevcuttur.

##### 2. Durum Kontrolü
```shell
$ sudo systemctl status nginx.service
```
Veya

```shell
$ ps aux | grep nginx
```
> **Explanation:**
> + Nginx'in kurulup kurulmadığını ve düzgün çalışıp çalışmadığını kontrol edebilirsiniz.

##### 3. İstek Atma:
```shell
$ curl -i http://192.168.1.129/
```
> **Explanation:**
> + Kurmuş olduğumuz nginx sunucuya `curl`  ile `GET` isteği yapıyoruz.
> + Bu işlemi tarayıcının bar'ına yazılarak da yapılabilir.

##### 4. Log Dosyasından İzleme:
```shell
$ tail -f /var/log/nginx/*
```
> **Explanation:**
> + `tail` komut ve `-f` parametresi ile nginx'in log dosyalarını canlı bir şekilde izleyebiliyoruz.
> + `/var/log/nginx/` dizini altında `access.log` ve `error.log` adında iki dosya mevcuttur.
> + Yukarıda yaptığımız `GET` istekleri buradaki `access.log` dosyasına yazılacaktır.

**Tail Komut Çıktısı:**
```shell
==> /var/log/nginx/error.log <==
2024/10/06 19:27:09 [notice] 19962#19962: signal process started

==> /var/log/nginx/access.log <==
192.168.1.106 - - [06/Oct/2024:19:27:16 +0000] "GET / HTTP/1.1" 200 396 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:131.0) Gecko/20100101 Firefox/131.0"
192.168.1.106 - - [06/Oct/2024:19:27:44 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:131.0) Gecko/20100101 Firefox/131.0"
```

+ **error.log:** nginx servisini yeniden başlatıldığını söylemektedir. (`sudo nginx -s reload`)
+ **access.log:**  nginx servisine 2 `GET` isteğin yapıldığını *ilk olarak* nginx, 200 response code aldığını görünüyor. Çünkü ilk istek olduğu için. 
	+ *İkinci istekte* ise nginx, 304 response code alındığı görünmektedir. 
	+ Çünkü tarayıcı, nginx'in statik içerğini önbelleğe alındığını nginx bildirmiştir(**If-Modified-Since**) ve 
	+ nginx, statik içerikte değişiklik olup olmadığına bakmıştır(**Last-Modified**) sonuç olarak; istek de bir değişiklik olmadığıdır.(Kısa açıklama)


### Statik İçerikleri Yayınlama:

**Site Dizini**
```shell
$ mkdir -p /var/www/html
```
> **Explanation:**
> + Eğer linux sisteminizde bu dizin yapısı yok ise `mkdir` komut ile oluşturuyoruz.
> + Çünkü statik web sitemizi bu dizine atacağız.

**nginx.conf backup:**
```shell
$ sudo cp -v /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
```


> [!IMPORTANT]
> + `/etc/nginx/nginx.conf` dosyasında yapılan değişiklerin aktif olabilmesi için;
> + `nginx -t` komut ile config dosyasının syntax(söz dizimi) kontrolü yapıyoruz.
> + `nginx -s reload` komut ile de config dosyasın aktif olmasını sağlıyoruz.
#### 1.Basit nginx.conf:
**nginx.conf**
```nginx
events {
}

http {
    server {
        # Virtual Host
        
        listen 80;
        server_name 192.168.1.134;

        root /var/www/html/bloggingtemplate/;
    }
}
```

> **Explanation:**
> 1. **listen directive:**  Sunucunun içerisinde ilk olarak web sitesini dinlemek istediğimiz port yer alır.
> 2. **server_name directive:** Bu belirli isteğin hangi belirli sunucuda işleneceğini tanımlamak için `server_name` tanımlamamız gerekiyor.
> 3. **root directive:** Bundan sonra hangi dosya sisteminin hangi konumu okuyacağını belirlemek için kök hakkını tanımlamanız gerekir.


> [!NOTE]
> +  Eğer `/var/www/html` yapısında dizin yolunuz yok ise `mkdir -p /var/www/html` komut ile oluşturabilirsiniz.
> + `bloggingtemplate` adlı dosyayı indirmek için [link](https://www.100utils.com/download/course-files-for-youtube-course-complete-nginx-training/)


**Nginx Servisi**
```shell
$ sudo nginx -s reload
```
> **Explanation:**
> + **Alternatif Komut:** `sudo systemctl reload nginx.service` 
> + Eğer `reload` yerine `sudo systemctl restart nginx.service` sinyali gönderirsek; nginx önce durdurulur daha sonra başlatılır 


**İstek Gönderme**
```shell
$ curl -X GET -I http://192.168.1.132/assets/js/bootsnav.js
```
> **Explanation:**
> + `/assets/js/bootsnav.js` gibi URL uzantılarını nginx'ın log dosyasında alabilirsiniz.
> + nginx log dosyaları için: `tail -f /var/log/nginx/*`

**Çıktı**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sun, 10 Nov 2024 09:02:24 GMT
Content-Type: text/plain
Content-Length: 27843
Last-Modified: Wed, 06 Nov 2024 14:05:18 GMT
Connection: keep-alive
ETag: "672b779e-6cc3"
Accept-Ranges: bytes
```
> **Explanation:**
> + `curl` komut yerine tarayıcı ile de yapabilirsiniz.
> + `HTTP/1.1 200 OK`**:** Durum Kodu `200` vermektedir ayrıca `tail -f /var/log/nginx/access.log` dosyasında aynı durum kodunu göstermektedir.
> + `Server: nginx/1.27.2`**:** Sunucuda çalışan nginx'in versiyonunu vermektedir.
> + `Date: Sun, 10 Nov 2024 09:02:24 GMT`**:** HTTP Date başlığı, sunucunun istemciye yanıt gönderdiği zamanı belirtir. Nginx gibi sunucular, istemciye gönderilen yanıtlara otomatik olarak `Date` başlığını ekler. Nginx’te bu başlık üzerinde özel bir ayar yapmaya gerek yoktur, çünkü Nginx bu başlığı varsayılan olarak ekler. Ayrıca UTC saat dilimine göre yazar. `timedatectl` komut ile UTC zaman dilimini görebilirsiniz.(`Date: Sun, 10 Nov 2024 09:51:06 GM`)
> + `Content-Type: text/plain` **:**  Sunucu tarafında nginx.conf dosyasında mime type yazılmadığı için nginx tüm dosyaları uzantısı ne olursa olsun tarayıcıya varsayılan olarak `text/plain` olarak okunmasını istemektedir.
> + `Content-Length: 27843` **:** Gönderilen dosya boyutun 27843 byte olduğunu göstermektedir.
> + `Last-Modified: Wed, 06 Nov 2024 14:05:18 GMT` **:**  Bu  mevcut tarihi `/var/www/html/` dizini içerisinde bulunan dosya tarihinden almaktadır. Eğer `ls -ltr /var/www/html/bloggingtemplate` komutunu çalıştırsanız değiştirileme tarihlerin aynı olduğunu görebilirsiniz.  

#### 2.Type Context ekleme:
**ngnix.conf**
```nginx
events {
}

http {

    types {
        text/html html;
        text/css  css;
        application/javascript js;
    }

    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;
    }
}
```
> **Explanation:**
> + Eğer dikkat ederseniz bir öncekinde farklı olarak `types context` eklendiğini görebilirsiniz
> + Ayrıca sadece html, css ve javascript için tip bildirimi yapılmıştır.


**İstek Gönderme**
```shell
$ curl -X GET -I http://192.168.1.132/assets/js/bootsnav.js
```

**Çıktı**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sun, 10 Nov 2024 14:51:04 GMT
Content-Type: application/javascript
Content-Length: 27843
Last-Modified: Sun, 10 Nov 2024 14:50:53 GMT
Connection: keep-alive
ETag: "6730c84d-6cc3"
Accept-Ranges: bytes 
```
> **Explanation:**
> + nginx.conf dosyasına `type context` ekleyip içerisine `application/javascript js;` directive yazdığımızda `Context-Type` header'ı `text/plain`'den `application/javascript` değiştiğini görebiliriz.
> + Böylelikle tarayıcı bu dosyayı(`bootsnav.js`) javascript dosyası olarak değerlendirip ona göre çalıştıracaktır.
> + Diğer header'lar bir önceki olan Basit nginx.conf da anlatılmıştır.


**İstek Gönderme**
```shell
$ curl -X GET -I http://192.168.1.132/assets/css/animate.css
```

**Çıktı**
```shell
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sun, 10 Nov 2024 15:38:55 GMT
Content-Type: text/css
Content-Length: 51840
Last-Modified: Wed, 06 Nov 2024 14:05:18 GMT
Connection: keep-alive
ETag: "672b779e-ca80"
Accept-Ranges: bytes
```
> **Explanation:**
> + Aynı durum `css` uzantılı dosyalara içinde geçerlidir. tek farklı js değil de css olmasıdır.

#### 3.mime.types Dosyasını Ekleme:
+ Nginx’in dosya türlerini (MIME türleri) tanımladığı bir yapılandırma dosyasıdır.
+ Bu dosya, Nginx’in hangi dosya türüne hangi **MIME türünü** atayacağını belirler.
+ Bir dosya türü için doğru MIME türü atamak, istemcinin (tarayıcı veya uygulama) dosyayı nasıl işlemesi gerektiğini anlamasına yardımcı olur.

```nginx
events {
}

http {

    # types {
    #   text/html html;
    #   text/css  css;
    #   application/javascript js;
    # }
    include mime.types;

    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;
    }
}
```
> **Explanation:**
> + `type context` mime.types adlı dosya içerisine aktarıyoruz. Ayrıca `mime.types` dosyası `nginx.conf` dosyası ile aynı dizinde yani klasörde bulunmaktadır.
> + Eğer `mime.type` dosyası `nginx.conf` ile aynı dizine bulunmaz ise `mime.type` dizinin tam yolunu vermek zorundayız.
> + `include` directive bir config dosyasına başka bir config dosyası dahil eder. Zaten `include` türkçe karşılığı dahil etmektir.
> + `mime.types` dosyası nginx ile birlikte gelmektedir ve `/etc/nginx/mime.types` dizine de bulunmaktadır.


```shell
$ curl -X GET -I http://192.168.1.132/assets/css/bootstrap.min.css
```

```shell
$ curl -X GET -I http://192.168.1.132/assets/images/clients/c6.png
```

```shell
$ curl -X GET -I http://192.168.1.132/assets/js/jquery.appear.js
```

```shell
$ curl -X GET -I http://192.168.1.132/assets/images/portfolio/p1.jpg
```
> **Explanation:**
> + `Content-Type` header(başlığı) dosya uzantılarına uygun olarak verecektir.

#### 4.Port Değiştirme:
+ Tarayıcıalar(Browsers) varsayılan olarak 80 ve 443 portlarını dinlemektedir ve IP adresi veya domian'den sonra port numarasını yazmamıza gerek yoktur. Fakat bunun haricindeki port ile isteklerde yaptığımızda port numarasını bildirmemiz gerekmektedir.
**nginx.conf**
```nginx
events {
}

http {
    include mime.types;

    server {
        # Virtual Host
        listen 8080;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;
    }
}
```

**İstek Atma**
```shell
$ curl -X GET -I http://192.168.1.132:8080
```
> **Explanation:**
> + `listen directive` 80 portundan 8080 portuna almış bulunuyoruz. Nginx gelen istekleri 80 portundan değil de 8080 portundan dinlemeye başlayacaktır.
> + Eğer fark ederseniz nginx 80 portunu dinlerken `curl` komutuna port bildiriminde bulunmamıştık. Ama nginx 8080 portunu dinlediğine de yani varsayılan değerden farklı port verildiğinde port numarası belirtilmesi gerekir.


#### 5.Location Context:


