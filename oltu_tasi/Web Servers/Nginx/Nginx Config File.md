#nginx
### Nginx Giriş
##### Tanım:
+ Nginx, çok yönlü bir web sunucusu olarak kullanılır ve birçok farklı amaç için konfigüre edilebilir. İşte Nginx'in başlıca kullanım alanları:
	1. **Web Sunucusu**: Nginx, statik içerik (HTML, CSS, JS dosyaları) sunmak için kullanılır. HTTP ve HTTPS isteklerini işleyerek web sitelerinin temel sunucu rolünü üstlenir.
	2. **Ters Proxy (Reverse Proxy)**: Nginx, istemci isteklerini arka plandaki başka sunuculara yönlendirmek için ters proxy olarak yapılandırılabilir. Bu, yük dengelemesi (load balancing) ve güvenlik (örneğin, gizleme ve IP adreslerini maskeleme) için yaygındır.
	3. **Yük Dengeleyici (Load Balancer)**: Nginx, gelen istekleri birden fazla sunucuya dağıtarak yük dengeleme işlevi görür. Bu, sunucu kaynaklarını daha verimli kullanmaya ve yüksek trafikli uygulamalarda daha yüksek performans sağlamaya yardımcı olur.
	4. **HTTP Önbellekleme (Caching)**: Nginx, dinamik içerikleri cache'leyerek istemcilere daha hızlı sunabilir. Bu, özellikle trafiği yoğun olan web sitelerinde performansı artırmak için kullanılır.
	5. **API Gateway**: Mikroservis mimarilerinde, Nginx genellikle API isteklerini yönetmek, yönlendirmek ve güvenlik politikalarını uygulamak için bir API gateway olarak kullanılır.
	6. **Medya Streaming**: Nginx, video ve ses gibi medya içeriklerini HTTP üzerinden akış (streaming) hizmeti sunmak için de kullanılabilir.
+ Nginx, Rus geliştirici **Igor Sysoev** tarafından geliştirildi.
+ Nginx açık kaynak olarak 2004 de bırakıldı yani duyruldu.

##### 10K Problemi:
+ Web sunucularında "10K problemi" (10,000 connections problem), bir web sunucusunun aynı anda çok sayıda (örneğin, 10.000) istemci bağlantısını idare etmesi sırasında karşılaşılan performans ve verimlilik sorunlarına verilen isimdir.
+ Geleneksel web sunucuları, her bir istemci bağlantısı için ayrı bir işlem veya iş parçacığı (thread) oluşturur.
+ Bu yöntem düşük sayıda bağlantı için etkili olsa da, bağlantı sayısı arttıkça aşağıdaki sorunlara yol açar:
###### 1. Yüksek Bellek Tüketimi:
- Her yeni bağlantı, web sunucusunda bir işlem veya iş parçacığı oluşturur. Bu süreç, bellekte önemli bir yer kaplar.
- 10.000 bağlantı olduğunda, bu işlemler ve iş parçacıkları sistemin RAM'ini hızla tüketebilir ve bellek tükenmesi veya yavaşlamalar meydana gelebilir.
###### 2. CPU Yükü:
- Her işlem veya iş parçacığı için işlemci zamanı ayrılması gerekir.
- 10.000 veya daha fazla bağlantı olduğunda, işlemci bu iş parçacıklarının yönetimiyle meşgul olur, bu da sunucunun performansını düşürür ve yanıt sürelerini uzatır.
##### Nginx ve 10K Problemi:
- Nginx gibi modern web sunucuları bu problemi çözmek için **asenkron, olay tabanlı bir mimari** kullanır.
- Bu mimaride, her bir bağlantı için yeni bir iş parçacığı ya da işlem oluşturulmaz. Bunun yerine, bir olay döngüsü içerisinde I/O (girdi/çıktı) işlemleri yönetilir.
- Bu sayede aynı anda on binlerce bağlantı etkin bir şekilde işlenebilir. Böylece, kaynak kullanımı optimize edilir ve **10K problemi** ortadan kaldırılır.
- Asenkron mimarinin avantajları şunlardır:
	- **Daha Az Bellek Tüketimi**: Tüm bağlantılar tek bir işlem ya da sınırlı sayıda iş parçacığı üzerinden yönetilir.
	- **Daha İyi Performans**: İşlemci kaynakları verimli kullanılır, çünkü I/O işlemleri non-blocking şekilde (engellenmeyen) gerçekleşir.
	- **Daha Yüksek Bağlantı Kapasitesi**: On binlerce hatta yüz binlerce eşzamanlı bağlantı yönetilebilir.

##### HTTP Sunucu Yeteneği Olarak:
Nginx ayrıca şunları da yapabilir;
+ Proxy sunucu email için(IMAP, POP3, ve SMTP)
+ Reverse proxy
+ Load Balancer HTTP, TCP ve UDP sunucuları için

##### Nginx vs Apache:

> [!CAUTION]
> + Nginx, HTTP sunucusu olmasının yanı sıra **mail proxy** yeteneği de sunar. SMTP, IMAP ve POP3 protokollerini destekler ve bu sayede e-posta sunucuları için bir ters proxy (reverse proxy) olarak kullanılabilir.
> + **Ancak;** Apache'nin kendisi doğrudan bir e-posta proxy sunucusu olarak kullanılmaz, çünkü Apache esasen bir HTTP sunucusudur ve web tabanlı içerikleri sunmak için tasarlanmıştır. Ancak, Apache'nin modül tabanlı yapısı sayesinde e-posta trafiği ile ilgili bazı işlemleri desteklemek mümkündür, fakat bu genellikle bir proxy sunucusu görevini üstlenmek anlamına gelmez.

###### 1. Mimari Yapı:
+ **Nginx**: Nginx, **asenkron ve olay tabanlı(event-driven)** bir mimari kullanır. Bu mimari, bağlantıları yönetmek için her bağlantı için bir iş parçacığı (thread) oluşturmaz.
+ Bunun yerine, I/O işlemleri bir olay döngüsü içerisinde yönetilir. Bu yaklaşım, düşük bellek ve işlemci kullanımı ile yüksek sayıda eşzamanlı bağlantıyı (concurrent connections) desteklemeyi sağlar.
+ *Nginx tüm istekleri, bu istekler 10.000 veya 100.000 olabilir tek bir işlem(process) tarafından işlenir(ele alınır.)* **İsteklerde(requests) herhangi bir düşme olmaz.**
---
+ **Apache**: Apache, varsayılan olarak **işlem ve iş parçacığı tabanlı(process-driven)** bir mimari kullanır. **Apache, her bir istemci isteği için yeni bir iş parçacığı veya işlem oluşturur.**
+ Bu, düşük sayıda eşzamanlı bağlantı için yeterli olabilir, ancak çok fazla bağlantı olduğunda performans sorunlarına yol açabilir.
+ *Apache her bir istek için ayrı bir işlem(process) oluşturur ve bu process bu belirli istekleri işler(ele alır).* **Eğer aşırı miktarda istek gelirse ve bu istekler işlem(process) sayısını aşarsa istek düşmeleri olur.**
###### 2. Modül Yapısı:
+ **Nginx**, modüler bir yapıya sahiptir ancak modüller, **statik** (derlenmiş) olarak yüklenir.
+ Bu, Nginx’in çalışırken modül yükleme veya kaldırma yeteneğine sahip olmadığı anlamına gelir.
+ Modüller, Nginx’in kaynak kodunu derlerken eklenir ve çıkarılır.
+ **Dinamik modüller** desteği Nginx'e daha sonra eklenmiştir, ancak bu yaklaşım Apache kadar esnek değildir.
---
+ **Apache**, **daha esnek ve dinamik** bir modül yapısına sahiptir.
+ Apache, modülleri çalışırken (runtime) yükleyip çıkarabilen **dynamically loadable modules** desteğine sahiptir.
+ Apache, varsayılan olarak birçok modülle birlikte gelir ve bu modüller `httpd.conf` veya benzeri konfigürasyon dosyalarında tanımlanarak etkinleştirilir ya da devre dışı bırakılır.
###### 3. Performans:
+ **NGINX**: Yüksek sayıda eşzamanlı bağlantıda Nginx daha iyi performans gösterir.
+ Özellikle statik içeriklerin (HTML, CSS, JavaScript gibi) sunulmasında Nginx çok hızlıdır.
+ 
---
+ **Apache**, saatte 1000 veya daha az istek gibi nispeten düşük trafik seviyelerine sahip siteleri barındırırken daha iyi performans gösterir.
+ Apache de düşük performansını nedeni `.htaccess` dosyasını giriş/çıkış(I/O) operasyonlarıdır. Ayrıca, apache tarafından oluşturulan tüm process'ler bu dosyayı(`.htaccess`) okur.
+ `.htaccess` dosyası URL'nin içerikle tam eşleşmesini sağlayacak olan Apache sunucusunun çekirdek dosyasıdır.
###### 4. Statik ve Dinamik İçerik Sunma:
+ **NGINX**: Statik içerik sunma konusunda oldukça hızlıdır, çünkü I/O işlemleri sırasında engellenmez (non-blocking).
+ Ancak, dinamik içerikleri doğrudan işleyemez; bu tür içerikleri PHP-FPM gibi bir dış modülle işleyerek sunar.
+ **Statik İçerik:** Aynı anda 1.000'e yakın bağlantı çalıştırılarak yapılan bir kıyaslama testine göre Nginx, Apache'den 2,5 kat daha hızlı performans gösteriyor.
---
- **Apache:** 
- Dinamik içerikler Apache tarafından doğal olarak ve doğrudan sunulur.

> [!TIP]
> Nginx ve Apache dinamik içeriği aynı hızda sunar

###### 5. OS Desteği:
+ **Nginx** en iyi desteğini Unix benzeri sistemlerde çalışır ve Microsoft Windows desteği de vardır. 
+ **Apache** tüm işletim sistemlerinde çalışır; Unix, Linux veya BSD hata Microsoft Windows için tam bir desteği var.
###### 6. Özellik Modelleri:
+ **Nginx**'in 3. parti çekirdek modülleri vardır (dinamik olarak yüklenemez). Nginx, dinamik olarak yükleyemeyeceğiniz binlerce 3.taraf çekirdek(core module) modülüne sahiptir.
+ Eğer nginx içerisine herhangi bir 3.parti modülü eklemeniz gerekiyorsa, o modülü nginx'in binary koduna eklemeniz gerekir.
---
+ **Apache**'nin 60 adet resmi, Açık/Kapalı olarak ayarlanabilen dinamik olarak yüklenebilir modülü vardır.

> [!IMPORTANT]
> + Aynı tür yapılandırmaya sahip makinede Apache ve Nginx'i çalıştırdığınızı ve Apache üzerinde 5000 istek ve Nginx üzerinde de aynı anda 5000 istek olduğunu varsayalım; o zaman Nginx'in Apache ile karşılaştırıldığında sadece %15 Kaynak kullandığını göreceksiniz.
### Reverse Proxy

> [!NOTE]
> + Nginx de tek işlem(process) çalışır.
> + istek(request) ---> nginx ---> 3. part process 



### Return

```nginx
server {
        listen 80 default_server;
        location /ali {
                add_header Content-Type text/plain;
                return 200 "I publish 80 port";
        }
}

server {
        listen 8080 default_server;
        location /ali {
                add_header Content-Type text/plain;
                return 200 "I publish 8080 port";
        }
}
```
> **Explanation:**


### Allow and  Deny IP

```nginx
        location /secure {

                try_files $uri /secure.html;

                allow 192.168.1.4;

                deny all;

        }
```
> **Explanation:**
> + Bu sayfaya sadece 192.168.1.4’den gelen isteklere izin ver (allow 192.168.1.4) tüm diğer ip’den gelen istekleri reddet (deny all ). 

## HTTP Cache Control header
``` nginx
user www-data;
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include mime.types;

    server {
        server_name 192.168.1.125;

        root /var/www/html/bloggingtemplate/;

        location / {
            try_files $uri $uri/ =404;
        }

        location ~ \.(png) {           # location_1
            try_files $uri $uri/ =404;
            add_header Cache-Control no-store;
        }
    }
}
```
> **Explanation:**
>  + [[Nginx Directives#Cache-Control|Cache-Control]]  başlığında açıklanmış
>  + [[Nginx location modifier#Örnek 1| location_1]] 

![Cache-Control no-store](images/cache_control_no_store.png)
## HTTP If-Modified-Since:
> [!INFO] Bilgi:
> + if-modified-since sadece istemci(client) tarafında mevcuttur. Server tarafında mevcut değildir.  nginx yapılandırma dosyasında yapılandırmayı desteklememektedir.
> + Her istek gönderen istemci(client) bu başlığı yani header'ı (if-modified-since) eklenmeli istek içerisine
> + if-modified-since birkez eklendiğinde istek(request) önbellekleme sunucularına(caching servers) gider. caching server backend uygulama sunucusu ile tekrar kontrol eder ve dosyalar ile beraber son değiştirilmiş tarihini gönderir belirli bir formata: *Last-Modified: Wed, 20 Aug 2020 15:26:38 GMT*
> 	1. Eğer uygulama sunucusunda bir değişiklik olmadıysa, uygulama sunucusu caching server'e 304 kodu(Not Modified) gönderir.
> 	2. Eğer bir uygulama sunucusunda bir değişiklik var ise ve istek yapılan tarih ile uygulama sunucusundaki tarih uyuşmazsa, uygulama sunucusu dosyalar ile birlikte 200 kodunu gönderir.
> 	3. Caching server güncellenmiş içeriği istemcilerine(client) gönderecektir.

> [!INFO] Bilgi: Nasıl Çalışır: Tarayıcı - Sunucu
> 1. **İlk İstek:** Bir istemci sunucudan bir kaynağı ilk kez indirdiğinde, sunucu genellikle yanıtla birlikte `Last-Modified` başlığını gönderir. Bu başlık, kaynağın en son ne zaman değiştirildiğini belirtir.
> 2. **Sonraki İstekler:** İstemci, bu kaynağı daha sonra tekrar indirmek istediğinde, isteğe `If-Modified-Since` başlığını ekler ve bu başlığa sunucunun daha önce belirttiği `Last-Modified` tarihini yazar. İstemcinin isteği şu şekilde olabilir:
> ```
>GET /resim.jpg HTTP/1.1
   Host: example.com
   If-Modified-Since: Wed, 21 Oct 2023 07:28:00 GMT
>```
>3. Sunucu Cevabı:
> 	+ Eğer kaynak belirtilen tarihten sonra değiştirilmediyse, sunucu `304 Not Modified` yanıtını döner. Bu durumda istemci, kaynağı yeniden indirmek yerine önbelleğindeki mevcut versiyonu kullanabilir.
> 	+ Eğer kaynak belirtilen tarihten sonra değiştirilmişse, sunucu `200 OK` yanıtıyla birlikte güncellenmiş kaynağı döner.

#### 1. İstemci ve Caching Sunucu Arasında İletişim
1. **İlk İstek:**
```
GET /resim.jpg HTTP/1.1
Host: example.com
```
> **Explanation:**
> İstemci, belirli bir kaynağı (örneğin, bir web sayfası veya resim dosyası) almak için caching sunucusuna bir istek gönderir. Bu istekte `If-Modified-Since` başlığı genellikle yer almaz, çünkü istemci kaynağı henüz önbelleğe almadı.

2. **Caching Sunucunun Yanıtı:**
```
HTTP/1.1 200 OK
Last-Modified: Wed, 21 Oct 2023 07:28:00 GMT
Content-Type: image/jpeg
Content-Length: 12345

... (image data) ...
```
> **Explanation:**
> + Caching sunucusu, isteği orijinal sunucuya iletir. Orijinal sunucu, kaynağı döndürür ve `Last-Modified` başlığını içerir.
> + Caching sunucusu, bu yanıtı alır ve hem istemciye iletir hem de yanıtı önbelleğe kaydeder.

3. **Sonraki İstekler:**
```
GET /resim.jpg HTTP/1.1
Host: example.com
If-Modified-Since: Wed, 21 Oct 2023 07:28:00 GMT
```
> **Explanation:**
> İstemci aynı kaynağı tekrar almak istediğinde, caching sunucusuna yeni bir GET isteği gönderir. Bu istek genellikle `If-Modified-Since` başlığını içerir ve daha önce aldığı `Last-Modified` tarihini içerir.

#### 2. Caching Sunucu ve Orijinal Sunucu Arasında İletişim
1. **Caching Sunucusunun Öncelikli Yanıtı:**
```
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 12345

... (cached image data) ...
```
> **Explanation:**
> Caching sunucusu, istemciden gelen isteği aldığında, önbelleğinde bulunan verinin `Last-Modified` tarihini kontrol eder. Eğer istemcinin `If-Modified-Since` tarihinden daha yeni bir veri varsa, caching sunucusu doğrudan istemciye `200 OK` yanıtıyla birlikte önbellekteki veriyi döner.

2. **Orijinal Sunucuya İstek Gönderme:**
```
GET /resim.jpg HTTP/1.1
Host: example.com
If-Modified-Since: Wed, 21 Oct 2023 07:28:00 GMT
```

> **Explanation:**
> + Eğer caching sunucusu, istemciden gelen `If-Modified-Since` başlığının tarihinden daha eski bir veri bulursa veya ilgili kaynak önbellekte mevcut değilse, caching sunucusu bu başlıkla birlikte orijinal sunucuya bir istek gönderir.
> + Orijinal sunucu, istekte belirtilen tarihten itibaren kaynağın değişip değişmediğini kontrol eder.

```
HTTP/1.1 304 Not Modified
```
> **Explanation:**
>  Eğer kaynak belirtilen tarihten sonra değişmemişse, orijinal sunucu `304 Not Modified` yanıtı döner. Bu durumda caching sunucusu, önbelleğindeki veriyi yeniden kullanarak istemciye bir yanıt gönderir.

```
HTTP/1.1 200 OK
Last-Modified: Wed, 22 Oct 2023 10:12:00 GMT
Content-Type: image/jpeg
Content-Length: 12567

... (new image data) ...
```
> **Explanation:**
>  Eğer kaynak değişmişse, orijinal sunucu güncellenmiş içeriği `200 OK` yanıtıyla birlikte döner. Caching sunucusu bu yeni veriyi önbelleğe alır ve istemciye iletir.

>[!CAUTION] Dikkat:
>Last-Modified(sunucu tarafı) başlığı ve If-Modified-Since(client tarafı) *tarihi* nereden aldığını göstermektedir:

![Last-Modified ve If-Modified-Since](Pictures/If-Modified-Since.png)

## WhiteList Server to NGINX
> **Konu Amaçı:** sunucuyu nginx'te nasıl beyaz listeye alabileceğimizi göreceğiz. Yani Web siteniz belirli sayfaları herkese açık olmamalı örneğin; web sitenizin admin panel gibi son kullanıcıya açık olmamalı. Web sitesinde bazı sayfaları kullanıcılar kısıtlamamız gerekiyor.

###### Örnek 1: En basit gösterimi - whitelistIP
```nginx
user www-data;
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include mime.types;

    server {
        server_name 192.168.1.125;

        root /var/www/html/bloggingtemplate/;

        location / {
            try_files $uri $uri/ =404;
        }

        location ~ \.(png) {                           # 1
            try_files $uri $uri/ =404;
            allow 192.168.1.104;                       # 2
            deny all;                                  # 2
        }
    }
}
```
> **Explanation:**
> 1. .png uzantlı dosyaları kapsamaktadır. Ayrıca  tilda(~): küçük büyük harf duyarlığı vardır. Bakınız: [[Nginx location modifier#Regex Case Sensitive Eşleşme|Regex Case Sensitive Eşleşme]] 
> 2. location context alanına bakarsak allow directive 192.168.1.104'lu IP'ye izin verirken deny directive tüm diğer IP'lere engellemektedir.
> Eğer 192.168.1.125'li IP'den giriş yaparsak, log dosyası bunu gösterir:
 `192.168.1.103 - - [22/Aug/2024:14:56:47 +0300] "GET /assets/images/clients/c5.png HTTP/1.1" 403 153 "http://192.168.1.125/" "Mozilla/5.0 (iPhone; CPU iPhone OS 14_7_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148"`
> Log dosyasında göründüğü gibi png uzantlı dosyaya **403 hata** kodunu vermektedir.

###### Örnek 2: Nginx'e whiteListIP dahil etme
```nginx
user www-data;
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include mime.types;

    server {
        server_name 192.168.1.125;

        root /var/www/html/bloggingtemplate/;

        location / {
            try_files $uri $uri/ =404;
        }

        location ~ \.(png) {
            try_files $uri $uri/ =404;
            include /etc/nginx/whiteListIP;        # 1
            deny all;
        }
    }
}
```

###### Örnek 2.1: whiteListIP dosyası
```nginx
allow 127.0.0.1;                    # 2
# allow 192.168.1.0/24;

allow 192.168.1.104;
```
> **Explanation:**
> 1. [[Nginx Config File#Örnek 1 En basit gösterimi - whitelistIP|Örnek 2]] deki ile aynı ama IP'leri nginx config dosyasına yazmaya başlarsak dosyanın karmaşıklığı artar Diğer yandan Yukarıdaki whiteListIP dosyasına yazarak ve bu dosyayıda yukarıdaki nginx config(Örnek 2) dosyasına dahil ederek daha düzenli bir yapı oluşturabiliriz.
> 2. whiteListeIP dosyasına izin vermek istedğiniz IP'leri yazabilirsiniz.

>[!CAUTION]
> *Allow veya Deny directive'leri* kullanılarak giriş verilmeyen sayfalar `403 kod hatası(403 Forbidden)`  vermektedir. Bunun anlamı sayfa kaynaklarını olmadığı değil. Buraya kullanıcıları erişim yetkisin olmadığın bilgisini verir.


## Kaynaklar Erişimi Kısıtlama - Limit Access on Resources

