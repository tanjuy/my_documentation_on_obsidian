#nginx 

## 1.client_body_buffer_size:

```nginx
client_body_buffer_size 10M
```
> **Explanation:**
> client’dan post isteğini gönderildiğinde buffer da tutulacağı boyut miktarını belirliyor.Bu, sunucunun tek seferde 10 MB'a kadar olan request body verilerini geçici olarak belleğe almasına izin verir.

---
## 1.add header:
### 1.1. Cache-Control:
```nginx
add_header Cache-Control: max-age=120
```
> **Explanation:**
>  + max-age isteği yönergesi, bir kaynağın önbelleğe alınmış bir kopyasının süresinin dolması için gereken süreyi saniye cinsinden tanımlar.
>  + Yanıtın belirli bir süre (saniye cinsinden) önbelleğe alınmasını belirtir
>  + 120 saniye sonra ==tarayıcı== kendi önbellekten almayarak tekrardan sunucudan istek yapacaktır.

---
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
