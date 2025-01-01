#nginx 


## 1.add header:
### 1.1. Cache-Control:
```nginx
add_header Cache-Control: max-age=120
```
> **Explanation:**
>  + max-age isteği yönergesi, bir kaynağın önbelleğe alınmış bir kopyasının süresinin dolması için gereken süreyi saniye cinsinden tanımlar.
>  + Yanıtın belirli bir süre (saniye cinsinden) önbelleğe alınmasını belirtir
>  + 120 saniye sonra ==tarayıcı== kendi önbellekten almayarak tekrardan sunucudan istek yapacaktır.


```nginx
add_header Cache-Control: no-cache
```
> **Explanation:**
> + no-cache directive, tarayıcının bir yanıtı önbelleğe alabileceği ancak önce bir kaynak sunucuya bir doğrulama isteği göndermesi gerektiği anlamına gelir.
> + no-cache yönergesinde, tarayıcı önbelleğe almıyor anlama gelmesin, bu yönergede ==önbellekleme yapmaktedır.==

```nginx
add_header Cache-Control: no-store
```
> **Explanation:**
> + Yanıt, hiçbir zaman önbelleğe alınmamalıdır. Her istek yapıldığında sunucudan çekiliyor.
> + Bu ayar geneliikle hasas veriler için kullanılır. Örneğin; kişisel banka detayları için
> + Server veya Client tarafında önbellek depolaması yapmayacak

```nginx
add_header Cache-Control: Public
```
> **Explanation:**
> + Bir kaynak herhangi bir önbellek tarafından önbelleğe alınabilir. Örneğin; ortadaki bir sunucuda olabilir, sunucunun kendisi veya tarayıcı tarafında da olabilir.
> + Yanıt, herhangi bir önbellek tarafından önbelleğe alınabilir.

```nginx
add_header Cache-Control: Private
```
> **Explanation:**
> + Yanıt sadece istemciye özel olarak önbelleğe alınabilir, proxy önbelleklerinde tutulmamalıdır.
> + Ortadaki sunucu önbelleğe almayacaktır.

### 1.2. X-Current-Time:
+ **Tanım:** Kullanıcı tarafından tanımlanan bir özel başlıktır.
+ **Amaç:** Sunucunun yerel saatine veya kullanıcı tarafından belirlenen özel bir saat bilgisini istemciye iletmek için kullanılır.
+ **Format:** Kullanıcının belirlediği herhangi bir format olabilir, ancak genellikle `$time_local` veya `$date_local` gibi değişkenlerden türetilir.

**nginx.conf:**
```nginx
events {
}

http {

    include mime.types;

    log_format specialLog '$remote_addr -> [$date_local] '
                          'body_bytes_sent değeri: $body_bytes_sent'
                          ' - $connection_requests';

    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;

        access_log /var/log/nginx/access-special.log specialLog;
        access_log /var/log/nginx/access.log;

        location /variable {
            add_header X-Current-Time $date_local;
            return 200 "the current time is: $date_local\n";
        }
    }
}
```


```nginx
add_header X-Current-Time $date_local;
```

> **Explanation:**
> + `location context` ve kaynak URI(`/variable`) içerisinde `add_header directive` ile `X-Current-Time` başlığı istemciye gönderilmektedir. 

**GET isteği:**
```shell
curl -X GET -i http://192.168.1.132/variable
```

**Curl Çıktısı:**
```http
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Wed, 04 Dec 2024 12:30:47 GMT
Content-Type: text/plain
Content-Length: 57
Connection: keep-alive
X-Current-Time: Wednesday, 04-Dec-2024 15:30:47 +03

The current time is: Wednesday, 04-Dec-2024 15:30:47 +03
```
> **Explanation:**
> `add-header directive` sayesinde `X-Current-Time` header(başlığını) çıktıda görebiliryoruz.

> [!IMPORTANT]
> + **`X-` ile başlayan başlıklar:** Kullanıcı tanımlı veya özel başlıkları ifade eder. Örneğin; `X-Current-Time` 
> + Bu tür başlıklar HTTP standartlarında yer almaz ama yaygın bir uygulamadır.
> + `date header` : HTTP/1.1 protokolü tarafından tanımlanan standart bir başlıktır. Sunucunun yanıtını oluşturduğu UTC (Koordinatlı Evrensel Zaman) zaman dilimindeki tarihi ve saati gösterir.

##### Date ile X-Current-Time Farkları:

+ **`Date`:** Varsayılan olarak eklendiği için çoğu durumda yeterlidir. İstemciler için güvenilir ve standart bir tarih/saat kaynağıdır.
+ **`X-Current-Time`:** Yerel saat dilimine ihtiyaç duyulan özel uygulamalarda veya hata ayıklama amacıyla kullanılabilir. Örneğin:

|Özellik|`Date` Başlığı|`X-Current-Time` Başlığı|
|---|---|---|
|**Standart mı?**|Evet (HTTP protokolünün bir parçası)|Hayır (özel bir başlık)|
|**Otomatik mi?**|Evet (Nginx gibi sunucular ekler)|Hayır (kullanıcı tanımlamalı)|
|**Zaman Dilimi**|Her zaman UTC (GMT)|Yerel saat dilimi kullanılabilir|
|**Amaç**|Yanıt oluşturma zamanı|Özel bilgi veya yerel zaman|
|**Kapsam**|Tüm HTTP istemcileri|Özel ihtiyaçlara bağlı|

---
## 2.client_body_buffer_size:

```nginx
client_body_buffer_size 10M
```
> **Explanation:**
> client’dan post isteğini gönderildiğinde buffer da tutulacağı boyut miktarını belirliyor.Bu, sunucunun tek seferde 10 MB'a kadar olan request body verilerini geçici olarak belleğe almasına izin verir.


---
## 3.server_tokens:

### 3.1.server_token on:

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

        server_tokens on;
        access_log /var/log/nginx/access.log;

        location /video {
            return 200 "Enjoy the movie!!!!";
        }

    }
}
```

**GET isteği:**
```shell
curl -X GET -i 192.168.1.132/video
```

**Curl Çıktısı:**
```http
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Sat, 28 Dec 2024 11:58:35 GMT
Content-Type: text/plain
Content-Length: 19
Connection: keep-alive

Enjoy the movie!!!!
```
> **Explanation:**
> + `server_tokens on` durumunda yaptığımızda `curl` komutun çıktısından da(`Server: nginx/1.27.2`) anlaşılacağı üzeri, nginx'in versiyon bilgisini vermektedir. 

**Nmap:**
```shell
nmap -p 80,443 -sV 192.168.1.132
```

**Nmap Çıktıs:**
```shell
Starting Nmap 7.80 ( https://nmap.org ) at 2024-12-28 15:04 +03
Nmap scan report for 192.168.1.132
Host is up (0.0017s latency).

PORT    STATE  SERVICE VERSION
80/tcp  open   http    nginx 1.27.2
443/tcp closed https

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.53 seconds
```
> **Explanation:**
> + `nmap`'in `-sV` parametresi ile versiyon kontrolünde  `80/tcp  open   http    nginx 1.27.2` 
> + nginx'in versiyonu görünmektedir.


### 3.2.server_token off:

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

        server_tokens on;
        access_log /var/log/nginx/access.log;

        location /video {
            return 200 "Enjoy the movie!!!!";
        }

    }
}
```

**GET isteği:**
```shell
curl -X GET -i 192.168.1.132/video
```

**Curl Çıktısı:**
```http
HTTP/1.1 200 OK
Server: nginx
Date: Sat, 28 Dec 2024 12:08:26 GMT
Content-Type: text/plain
Content-Length: 19
Connection: keep-alive

Enjoy the movie!!!!
```
> **Explanation:**
> + `server_token off` durumunda olunduğunda;
> + `curl` komut çıktısında göründüğü üzeri `Server: nginx` sadece adı mevcut versiyonu görünmemektedir.

**Nmap:**
```shell
nmap -p 80,443 -sV 192.168.1.132
```

**Nmap Çıktıs:**
```shell
Starting Nmap 7.80 ( https://nmap.org ) at 2024-12-28 15:09 +03
Nmap scan report for 192.168.1.132
Host is up (0.0017s latency).

PORT    STATE  SERVICE VERSION
80/tcp  open   http    nginx
443/tcp closed https

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.46 seconds
```
> **Explanation:**
> + `nmap` çıktısında da `80/tcp  open   http    nginx` versiyonu görünmemektedir.

---

## 4.log_format directive:

+ **`log_format`** direktifi, sunucunun **erişim logları (access logs)** için kullanılan özel bir günlük formatını tanımlamak amacıyla kullanılır.
+ Günlük dosyaları(`log files`), gelen HTTP istekleriyle ilgili çeşitli bilgileri kaydetmek için kullanılır ve bu bilgiler, performans analizi, hata ayıklama veya trafik izleme için önemli bir kaynaktır.

**Syntax:**
```nginx
log_format <format_name> <format_string>;
```
+ `<format_name>` : Log formatına bir ad verir. Bu ad, daha sonra ilgili `access_log` direktifinde kullanılabilir.
+ **`<format_string>`**: Log girdisinin içeriğini ve düzenini tanımlar. Nginx'in çeşitli değişkenlerini kullanarak günlük girdisini özelleştirebilirsiniz.

> [!WARNING]
> + `log_format directive`'i `http context` içerisinde yazılmalıdır aksi takdirde hata alırsınız.
> + Örneğin; `server context` içerisinde tanımladığımızda `2025/01/01 09:33:54 [emerg] 3417#0: "log_format" directive is not allowed here in /etc/nginx/nginx.conf:17` hata vermektir.

### Popular Değişkenler:

| Değişken               | Açıklama                                                  |
| ---------------------- | --------------------------------------------------------- |
| **`$remote_addr`**     | İstemcinin IP adresi.                                     |
| **`$remote_user`**     | İstemcinin kimlik doğrulama adı (varsa).                  |
| **`$time_local`**      | Yerel sunucu zamanı.                                      |
| **`$time_iso8601`**    | ISO 8601 formatında zaman.                                |
| **`$request`**         | HTTP isteği (örneğin: `GET /index.html HTTP/1.1`).        |
| **`$status`**          | HTTP yanıt durum kodu (örneğin: `200`, `404`).            |
| **`$body_bytes_sent`** | Yanıt gövdesinin bayt cinsinden boyutu.                   |
| **`$request_time`**    | İstek işleme süresi (saniye).                             |
| **`$http_referer`**    | Referer başlığı (isteğin geldiği kaynak).                 |
| **`$http_user_agent`** | Tarayıcı bilgisi (User-Agent başlığı).                    |
| **`$scheme`**          | İstek protokolü (örneğin: `http` veya `https`).           |
| **`$server_name`**     | Hangi sunucu bloğunun isteği işlediği.                    |
| **`$upstream_addr`**   | İsteğin yönlendirildiği backend sunucunun adresi (proxy). |

### Örnek 1:
**nginx.conf:**
```nginx
events {
}

http {
    include mime.types;

    log_format specialLog 'Client IP: $remote_addr' '$remote_user [$time_local] '
                          'Request-line: "$request" ' 'Status Code: $status '
                          'Body bytes sent: $body_bytes_sent ' '"$http_referer" '
                          'Http user agent: "$http_user_agent"';
    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;

        access_log /var/log/nginx/special_on_access.log specialLog;  # <---

        location /userdata {
            return 200 "User data is published!!!";
        }
    }
}
```

> **Explanation:**
> + `log_format directive` de kullanmış olduğumuz gömülü değişkenlerimiz;
> + `$remote_addr`: İstek yapan istemcinin IP adresi.
> + **`$remote_user`**: İstemci tarafından sağlanan kimlik doğrulama adı (varsa).
> + **`$time_local`**: İsteğin işlendiği yerel sunucu zamanı.
> + **`$request`**: HTTP isteği (örneğin: `GET /index.html HTTP/1.1`).
> + **`$status`**: HTTP durum kodu (örneğin: `200`, `404`).
> + **`$body_bytes_sent`**: İstemciye gönderilen yanıt gövdesinin boyutu (bayt olarak).
> + **`$http_referer`**: İsteğin geldiği kaynak sayfa (referer).
> + **`$http_user_agent`**: İstemcinin tarayıcı bilgisi (User-Agent).

**GET isteği:**
```shell
curl -X GET -i http://192.168.1.132/userdata
```

**Curl Çıktısı:**
```http
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Wed, 01 Jan 2025 09:08:13 GMT
Content-Type: text/plain
Content-Length: 25
Connection: keep-alive

User data is published!!!
```

**Log Dosyası**
```shell
tail -f /var/log/nginx/special_on_acces.log /var/log/nginx/error.log
```

**Tail Çıktısı:**
```log
==> special_on_access.log <==
Client IP: 192.168.1.106 - - [01/Jan/2025:12:08:13 +0300] Request-line: "GET /userdata HTTP/1.1" Status Code: 200 Body bytes sent: 25 "-" Http user agent: "curl/8.10.1"
```
> **Explanation:**
> + Eğer dikkat ederseniz `curl komut` ile `GET` isteği atığımızda  `nginx.conf` dosyasında `log_format directive` ile düzenlediğimiz şekilde log dosyasına yazdırıldı.
> + Lütfen çıktıyı `nginx.conf` dosyasındaki `log_format directive` ile bu log dosyasındaki çıktıyı karşılaşıtırınız.

### Örnek 2: json format
**nginx.conf:**
```nginx
events {
}

http {
    include mime.types;

    log_format specialLog escape=json '{'
        '"time":"$time_iso8601",'
        '"remote_addr":"$remote_addr",'
        '"request-line":"$request",'
        '"status":"$status",'
        '"body_bytes_sent":"$body_bytes_sent",'
        '"http_referer":"$http_referer",'
        '"http_user_agent":"$http_user_agent"'
    '}';

    server {
        # Virtual Host
        listen 80;
        server_name 192.168.1.132;

        root /var/www/html/bloggingtemplate/;

        access_log /var/log/nginx/special_on_access.log specialLog;  # <---

        location /userdata {
            return 200 "User data is published!!!";
        }
    }
}
```
> **Explanation:**
> + Bu format, log verilerini JSON olarak kaydeder ve log analizi için kullanımı kolaylaştırır.
> + **`escape=json`**: Özel karakterlerin JSON uyumlu bir şekilde kaçış karakteriyle işlenmesini sağlar.
> + `/var/log/nginx/special_on_access.log` : Günlük dosyasının kaydedileceği yer.
> + `specialLog` : Kullanılacak log formatının adı.

**GET isteği:**
```shell
curl -X GET -i http://192.168.1.132/userdata 
```
**Curl Çıktısı:**
```http
HTTP/1.1 200 OK
Server: nginx/1.27.2
Date: Wed, 01 Jan 2025 10:32:34 GMT
Content-Type: text/plain
Content-Length: 25
Connection: keep-alive

User data is published!!!
```

**Log Dosyası:**
```shell
tail -f /var/log/nginx/special_on_access.log /var/log/nginx/error.log
```

**Tail Çıktısı:**
```json
==> special_on_access.log <==
{"time":"2025-01-01T14:18:08+03:00","remote_addr":"192.168.1.106","request-line":"GET /userdata HTTP/1.1","status":"200","body_bytes_sent":"25","http_referer":"","http_user_agent":"curl/8.10.1"}
```
> **Explanation:**
> + `tail` komut bize hem `special_on_access.log` hem de `error.log` dosyalarını okumaktadır. Ama odak noktamız `access log` olduğu için sadece `special_on_access` dosyasını yazdık.

**Json Formatter**
```json
{
  "time": "2025-01-01T13:32:34+03:00",
  "remote_addr": "192.168.1.106",
  "request-line": "GET /userdata HTTP/1.1",
  "status": "200",
  "body_bytes_sent": "25",
  "http_referer": "",
  "http_user_agent": "curl/8.10.1"
}
```
> **Explanation:**
> + `curl` komutu ile GET isteği atığımızda `nginx.conf` dosyasında `log_format directive` ile düzenlenmiş yapıda log dosyasına json formatında yazılmıştır.
> + `json formatter` ile daha düzenli bir görünüm kazandırmış oluyoruz.
## 5.Access_log directive:
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

        location /userdata {
            access_log /var/log/nginx/access_userdata.log;  # <---
            return 200 "User data is published!!!";
        }
    }
```

**GET isteği:**
```shell
curl -X GET -i http://192.168.1.132/userdata
```

**Curl Çıktısı:**
```log
==> /var/log/nginx/access_userdata.log <==
192.168.1.106 - - [29/Dec/2024:18:14:22 +0300] "GET /userdata HTTP/1.1" 200 25 "-" "curl/8.10.1"
192.168.1.106 - - [29/Dec/2024:18:15:28 +0300] "GET /userdata HTTP/1.1" 200 25 "-" "curl/8.10.1"
```

**Log Dizini:**
```shell
nginx-tutorial3 :: /var/log/nginx » ls
access.log access_userdata.log  error.log
```

> **Explanation:**
> + `/userdata` adındaki kaynak URI istek yaptığımızda `/var/log/nginx/` dizini içerisinde farklı log dosyaları olmalarına rağmen `acces_userdata.log` dosyasına yazılmaktadır.
> + Çünkü `location context` içerisinde `access_log directive` ile log dosya yolu belirtmiş bulunmaktadıyız.
> + Log dizinindeki dosyaları nginx'in `access_log directive` oluşturacaktır. 


> [!NOTE]
> + Eğer web sitenizde veya web uygulamanızda farklı işlemler için ayrı dosyalarda log tutmak için `access_log directive`'i çok kullanışlı olacaktır.
> + Örneğin; kullanıcılar için ayrı log dosyası, misafir kullanıcıları için ayrı log dosyası ve kayıt işlemleri için ayrı log dosyası tutmak istediğimizde `access_log directive`'ini kullanabiliriz.

> [!CAUTION]
> + Best Practice olarak;
> + Hata günlüklerini(`error logs`) tek bir dosya da muhafaza etmek,
> + Giriş günlüklerini(`access logs`) ayrı dosyalara dağıtmak;


#### Access_log off:
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

        location /userdata {
            access_log /var/log/nginx/access_userdata.log;
            return 200 "User data is published!!!";
        }

        location /noLog {
            access_log off;  # <---
            return 200 "This resource URI is not logged!";
        }
    }
}
```

