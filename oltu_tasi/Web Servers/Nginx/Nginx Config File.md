#nginx
### Nginx Giriş
#### A. Tanım:
+ Nginx, çok yönlü bir web sunucusu olarak kullanılır ve birçok farklı amaç için konfigüre edilebilir. İşte Nginx'in başlıca kullanım alanları:
	1. **Web Sunucusu**: Nginx, statik içerik (HTML, CSS, JS dosyaları) sunmak için kullanılır. HTTP ve HTTPS isteklerini işleyerek web sitelerinin temel sunucu rolünü üstlenir.
	2. **Ters Proxy (Reverse Proxy)**: Nginx, istemci isteklerini arka plandaki başka sunuculara yönlendirmek için ters proxy olarak yapılandırılabilir. Bu, yük dengelemesi (load balancing) ve güvenlik (örneğin, gizleme ve IP adreslerini maskeleme) için yaygındır.
	3. **Yük Dengeleyici (Load Balancer)**: Nginx, gelen istekleri birden fazla sunucuya dağıtarak yük dengeleme işlevi görür. Bu, sunucu kaynaklarını daha verimli kullanmaya ve yüksek trafikli uygulamalarda daha yüksek performans sağlamaya yardımcı olur.
	4. **HTTP Önbellekleme (Caching)**: Nginx, dinamik içerikleri cache'leyerek istemcilere daha hızlı sunabilir. Bu, özellikle trafiği yoğun olan web sitelerinde performansı artırmak için kullanılır.
	5. **API Gateway**: Mikroservis mimarilerinde, Nginx genellikle API isteklerini yönetmek, yönlendirmek ve güvenlik politikalarını uygulamak için bir API gateway olarak kullanılır.
	6. **Medya Streaming**: Nginx, video ve ses gibi medya içeriklerini HTTP üzerinden akış (streaming) hizmeti sunmak için de kullanılabilir.
+ Nginx, Rus geliştirici **Igor Sysoev** tarafından geliştirildi.
+ Nginx açık kaynak olarak 2004 de bırakıldı yani duyruldu.

#### B. 10K Problemi:
+ Web sunucularında "10K problemi" (10,000 connections problem), bir web sunucusunun aynı anda çok sayıda (örneğin, 10.000) istemci bağlantısını idare etmesi sırasında karşılaşılan performans ve verimlilik sorunlarına verilen isimdir.
+ Geleneksel web sunucuları, her bir istemci bağlantısı için ayrı bir işlem veya iş parçacığı (thread) oluşturur.
+ Bu yöntem düşük sayıda bağlantı için etkili olsa da, bağlantı sayısı arttıkça aşağıdaki sorunlara yol açar:
###### 1. Yüksek Bellek Tüketimi:
- Her yeni bağlantı, web sunucusunda bir işlem veya iş parçacığı oluşturur. Bu süreç, bellekte önemli bir yer kaplar.
- 10.000 bağlantı olduğunda, bu işlemler ve iş parçacıkları sistemin RAM'ini hızla tüketebilir ve bellek tükenmesi veya yavaşlamalar meydana gelebilir.
###### 2. CPU Yükü:
- Her işlem veya iş parçacığı için işlemci zamanı ayrılması gerekir.
- 10.000 veya daha fazla bağlantı olduğunda, işlemci bu iş parçacıklarının yönetimiyle meşgul olur, bu da sunucunun performansını düşürür ve yanıt sürelerini uzatır.
#### C. Nginx ve 10K Problemi:
- Nginx gibi modern web sunucuları bu problemi çözmek için **asenkron, olay tabanlı bir mimari** kullanır.
- Bu mimaride, her bir bağlantı için yeni bir iş parçacığı ya da işlem oluşturulmaz. Bunun yerine, bir olay döngüsü içerisinde I/O (girdi/çıktı) işlemleri yönetilir.
- Bu sayede aynı anda on binlerce bağlantı etkin bir şekilde işlenebilir. Böylece, kaynak kullanımı optimize edilir ve **10K problemi** ortadan kaldırılır.
- Asenkron mimarinin avantajları şunlardır:
	- **Daha Az Bellek Tüketimi**: Tüm bağlantılar tek bir işlem ya da sınırlı sayıda iş parçacığı üzerinden yönetilir.
	- **Daha İyi Performans**: İşlemci kaynakları verimli kullanılır, çünkü I/O işlemleri non-blocking şekilde (engellenmeyen) gerçekleşir.
	- **Daha Yüksek Bağlantı Kapasitesi**: On binlerce hatta yüz binlerce eşzamanlı bağlantı yönetilebilir.

#### D. HTTP Sunucu Yeteneği Olarak:
Nginx ayrıca şunları da yapabilir;
+ Proxy sunucu email için(IMAP, POP3, ve SMTP)
+ Reverse proxy
+ Load Balancer HTTP, TCP ve UDP sunucuları için

#### E. Nginx vs Apache:

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

#### F. Statik ve Dinamik İçerik:
###### 1.Statik İçerik:
###### 2.Dinamik İçerik:

#### G. HTTP Requests:


> [!NOTE]
> + **Genel Şablonu:** `http://<host URL><resource URL>`
> + **Örnek:** `https://jsonplaceholder.typicode.com/posts/1/comments` 
> + **Açıklama:** `https://jsonplaceholder.typicode.com` host URL karşılık gelir ve `/posts/1/comments` resouce URL karşılık gelir. 

##### G.1. Request Formatı:
###### G.1.1 Request-line:
+ HTTP protokolünde `Request-Line`, bir HTTP isteğinin ilk satırında yer alır ve istemcinin sunucuya ilettiği isteğin türünü, hedef URL'yi ve HTTP protokol sürümünü içerir.
+ Bu satır, sunucunun ne tür bir işlem yapması gerektiğini anlamasını sağlar ve istemci tarafından gönderilen isteğin amacını özetler.

```http
<HTTP Yöntemi> <URI> <HTTP Sürümü>
```

```http
GET /products HTTP/1.1
```
> **Explanation:**
> 1. **HTTP metodu:** İsteğin türünü belirtir (GET, POST, PUT, DELETE gibi).
> 2. **Request URI:** Kaynağın konumunu belirten URL’yi içerir ve sunucunun hangi kaynağa ulaşması gerektiğini belirtir. (/products veya /api/v1/users)
> 3. **HTTP Sürümü:** Hangi HTTP protokol sürümünün kullanıldığını belirtir (genellikle `HTTP/1.1` veya `HTTP/2`)

###### G.1.2 Zero or More Header:
+ HTTP’de `header` (başlık), istemci ve sunucu arasında veri alışverişi yaparken ek bilgi sağlayan anahtar-değer çiftlerinden oluşan bir bölümüdür.
+ Header, hem HTTP isteklerinde (request) hem de yanıtlarında (response) bulunur ve veri alışverişinin nasıl yapılacağına dair önemli bilgiler içerir.
+ Bu bilgiler, içeriğin türü, yetkilendirme bilgileri, içerik uzunluğu gibi çeşitli detayları kapsar ve HTTP iletişiminin temelini oluşturur.
1. **Genel Header’lar (General Headers)**:  Hem isteklerde hem de yanıtlarda kullanılabilen, genel bağlantı ve aktarım özelliklerini tanımlar. Örnek: `Cache-Control` (önbellekleme ayarlarını belirler), `Connection` (bağlantının açık kalıp kalmaması gerektiğini belirtir).
2. **Request Header:** İstemci tarafından sunucuya gönderilen istekle ilgili bilgileri içerir. Örnek: `Host`: Sunucunun hangi domain için çalıştığını belirtir, `Accept`: İstemcinin kabul ettiği içerik türlerini belirtir (örneğin `application/json`, `text/html`).
3. **Response Header**:  Sunucu tarafından istemciye döndürülen yanıtla ilgili bilgileri içerir. Örnek: `Content-Type`: Yanıtın içeriğinin türünü belirtir (örneğin `text/html`, `application/json`), `Content-Length`: Yanıtın boyutunu belirtir.
4. **Entity Header:** İletinin kendisine, yani içeriğe (örneğin dosya veya belge) dair bilgileri tanımlar. Örnek: `Content-Encoding`: İçeriğin hangi formatta sıkıştırıldığını belirtir (örneğin `gzip`), `Content-Language`: İçeriğin dilini belirtir (örneğin `en` veya `tr`).

**Request Header:**
```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html
```

**Response Header:**
```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 1024
Set-Cookie: sessionId=abc123; HttpOnly
```

###### G.1.3. Empty-line:
+ HTTP protokolünde önemli bir yapısal rol oynar. İstemci veya sunucu, başlıklar ve gövde arasında bir ayrım yapabilmek için bu satırı kullanır.
+ Bu satır olmazsa, protokol başlıkların sonunu ve gövdenin başlangıcını doğru bir şekilde ayıramaz, bu da iletişimin bozulmasına veya yanlış yorumlanmasına yol açabilir.
###### G.1.4. body:
+ Bir HTTP isteği veya yanıtının asıl içeriğini, yani başlıklarda (header) belirtilen veri türüne göre istemciye veya sunucuya gönderilmesi amaçlanan veriyi barındıran bölümdür.

> [!TIP]
> + Her HTTP isteğinin bir gövdesi olmak zorunda değildir.
> + Örneğin, `GET` isteğinde genellikle gövde bulunmaz, çünkü `GET` yalnızca sunucudan veri almak için kullanılır.
> + Gövde içeren istekler genellikle `POST`, `PUT`, veya `PATCH` gibi sunucuya veri göndermeyi veya güncellemeyi amaçlayan isteklerde bulunur.

##### G.2. GET Request: 
 + **GET** metodu, HTTP protokolünde bir kaynağı (genellikle bir web sayfası veya API verisi) sunucudan istemek için kullanılan en yaygın HTTP yöntemidir.
 + GET isteği, sunucudan veri almak amacıyla kullanılır ve veriyi yalnızca okunur olarak elde etmeyi amaçlar; yani, sunucuya veri göndermek veya sunucu üzerinde bir değişiklik yapmak amacıyla kullanılmaz.


> [!TIP]
> + **İstek Gövdesi (Request Body) Yoktur**
> + GET istekleri genellikle bir gövde içermez. Tüm gerekli veriler, URL yoluna veya sorgu parametrelerine (query string) eklenir.

###### GET Request Atma:
```shell
$ curl -i -X GET www.example.com
```
> **Explanation:**
> + `curl` komut ile `www.example.com` sitesine bir `GET` isteği atmış bulunuyoruz.
> + `-X` parametresi ile istek türünü belirleyebiliriz. 
> + Ayrıca `-X` parametresin uzun yazılışı: `--request`

##### G.3. POST Request:
+ **POST** isteği, HTTP protokolünde sunucuya veri göndermek veya sunucu üzerinde bir işlem yapmak için kullanılan bir HTTP metodudur.
+ POST istekleri, genellikle yeni bir kaynak oluşturmak veya sunucu üzerinde bir değişiklik yapmak amacıyla kullanılır.
+ Örneğin, bir kullanıcı kayıt formunu göndermek veya yeni bir ürün eklemek için POST isteği yapılır.


> [!TIP]
> + **Gövde (Request Body) vardır**
> + POST isteğinde veri, HTTP başlıklarının ardından gelen gövde (body) kısmında yer alır. Gövdeye eklenen veri, form verisi, JSON, XML veya diğer formatlarda olabilir.

```shell
$ curl -X POST https://jsonplaceholder.typicode.com/todos \
-H "Content-Type: application/json" \
-d '{"userId": 1, "title": "linux is awesome", "id": 2}'
```
> **Explanation:**
> + `https://jsonplaceholder.typicode.com` test amaçlı **POST** isteği atabileceğiniz ücretsiz sitedir.
> + `-H` parametresi ile `Content-Type: application/json` header'ı ekliyoruz
> + `-d` parametresi ile de siteye veri yani data gönderiyoruz.

##### G.4. PUT Request:
+ **PUT** isteği, belirli bir kaynağı **oluşturmak** veya **güncellemek** için kullanılır.
+ PUT, gönderilen veriyi sunucuda tanımlı bir kaynağın **üzerine yazmak** için kullanılır.
+ Örneğin, bir kullanıcının bilgilerini güncellemek için PUT isteği gönderildiğinde, o kullanıcının tüm mevcut bilgileri gelen verilerle değiştirilir.

```shell
$ curl -X PUT https://jsonplaceholder.typicode.com/posts/1 \
-H "Content-Type: application/json" \
-d '{"userId": 1, "id": 3, "title": "linux is awesome", "body": "ubuntu"}'
```
> **Explanation:**
> + `https://jsonplaceholder.typicode.com` test amaçlı **PUT** isteği atabileceğiniz ücretsiz sitedir.
> + `-H` ve `-d` parametreleri yukarıda açıklanmıştır.

| Özellik             | PUT                                             | POST                                               |
| ------------------- | ----------------------------------------------- | -------------------------------------------------- |
| **Amaç**            | Kaynak oluşturma veya güncelleme                | Yeni kaynak oluşturma veya veri gönderme           |
| **Idempotent**      | Evet (aynı veri tekrar gönderilirse sonuç aynı) | Hayır (aynı veri tekrar gönderilirse farklı sonuç) |
| **Kaynak**          | Var olan kaynağı tamamen günceller              | Yeni kaynak yaratır veya mevcut kaynağa veri ekler |
| **Kullanım Örneği** | Mevcut kullanıcı bilgilerini güncelleme         | Yeni kullanıcı kaydı oluşturma                     |

> [!TIP]
> + **PUT**, genellikle belirli bir kaynağın güncellenmesi için tercih edilirken, **POST** yeni bir kaynak oluşturma durumunda daha uygun bir seçimdir.

##### G.5. DELETE Request:
+ **DELETE** isteği, sunucudaki belirli bir kaynağı **silmek** için kullanılan bir HTTP metodudur.
+ Bu istekle sunucuya gönderilen kaynağın kimliği veya konumu belirtilir ve sunucu, bu kaynağı sistemden kaldırır. Örneğin, bir kullanıcıyı, kaydı veya dosyayı silmek için kullanılabilir.


> [!NOTE]
> + **DELETE Request’in Özellikleri**
> + **Silme İşlemi:** DELETE isteği genellikle bir veri kaynağını, örneğin bir kullanıcı veya ürün kaydını, veritabanından veya sunucudan kaldırır.
> + **Yanıt Kodu:** Başarılı bir silme işlemi sonrası sunucu genellikle 200 (OK) veya 204 (No Content) yanıt kodu döner. Eğer kaynak bulunamazsa 404 (Not Found) yanıtı dönebilir.

```shell
$  curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
```

#### H. HTTP Response Kodları:
+ HTTP'de **Response Code** (Yanıt Kodu), bir istemcinin (örneğin, tarayıcı veya başka bir istemci uygulaması) sunucuya yaptığı isteğe sunucunun verdiği yanıtın durumunu bildiren üç haneli sayısal bir koddur.
+ Bu kodlar, istemcinin isteğinin başarılı olup olmadığını, bir hata meydana gelip gelmediğini veya başka bir işlem yapılması gerekip gerekmediğini belirtir.
+ Üç haneli tam sayıdan oluşmaktadır ve ilk hanesi kodun sınıfını tanımlar.
##### 1xx(info) - Bilgilendirme Yanıtı:
+ *İstek alındı ve işlem sürüyor*. Genellikle çok yaygın kullanılmaz.
+ **100 Continue:** İstemci, isteğe devam edebilir.
##### 2xx(success) - Başarılı Yanıtlar:
+ İstek başarıyla tamamlanmıştır.
+ **200 OK:** İstek başarıyla işleme alındı ve yanıt verildi.
+ **201 Created:** İstek başarılı ve yeni bir kaynak oluşturuldu (genellikle POST isteğinde).
##### 3xx(redirection) - Yönlendirme Yanıtları:
+ İstemcinin isteği başka bir kaynağa yönlendirilmelidir.
+ **301 Moved Permanently:** İstenen kaynak kalıcı olarak başka bir konuma taşındı.
+ **302 Found:** İstenen kaynak geçici olarak başka bir konuma taşındı.
+ **304 Not Modified:** Kaynakta herhangi bir değişiklik yok, bu nedenle yeniden indirilmesine gerek yok (genellikle önbellekleme için kullanılır).
##### 4xx(Client Error) - İstemci Hataları:
+ İstemcinin yaptığı istekte hata vardır.
+ **400 Bad Request:** Geçersiz istek, sunucu isteği işleyemiyor.
+ **401 Unauthorized:** Yetkilendirme gerekiyor, ancak sağlanmamış.
+ **403 Forbidden:** İstemcinin kaynağa erişim izni yok.
+ **404 Not Found:** İstenen kaynak sunucuda bulunamadı.
##### 5xx(Server Error) - Sunucu Hataları:
+ *Sunucu isteği işleyemediği durumlarda oluşur.*
+ **500 Internal Server Error:** Sunucuda beklenmeyen bir hata oluştu.
+ **502 Bad Gateway:** Sunucu, başka bir sunucudan geçersiz bir yanıt aldı.
### Reverse Proxy

> [!NOTE]
> + Nginx de tek işlem(process) çalışır.
> + istek(request) ---> nginx ---> 3. part process 


### Nginx Kurulumu:

#### A. Debian Temeli İşletim Sistemleri:
```shell
$ sudo apt install nginx
```
> **Explanation:**
> + Ubuntu ve Debian işletim sistemlerinde *nginx* kurulumunu `apt` paket yöneticisi tarafından yapar.

+ Eğer apt paket yöneticisi ile kurulum yaparsanız, *nginx* ile birlikte kurulacak paketler;
```shell
fontconfig-config fonts-dejavu-core libdeflate0 libfontconfig1 libgd3 libjbig0 libjpeg-turbo8 libjpeg8 libnginx-mod-http-geoip2 libnginx-mod-http-image-filter libnginx-mod-http-xslt-filter libnginx-mod-mail libnginx-mod-stream libnginx-mod-stream-geoip2 libtiff5 libwebp7 libxpm4 nginx-common nginx-core
```

---
#### B. REHL Temeli İşletim Sistemleri:

```shell
$ sudo yum install nginx
```

+  Yüklediğimiz *nginx*'in çalıştığını veya çalışmadığını kontrol edelim;

> [!WARNING]
> + `yum` paket yöneticisi yüklediği paket veya uygulamaları varsayılan olarak çalıştırmaz. Çalıştırma işlemini kullanıcıya bırakır. 

```shell
$ ps aux | grep nginx
```
> **Explanation:**
> + 

```sh
$ sudo systemctl enable --now nginx.service
```
> **Explanation:**
> + `systemctl` aracı ile `nginx` sevisini hem aktif(`--now`) hem de sistem yeniden başladığında aktif(`enable`) olmasını sağlıyoruz. 

```sh
$ sudo systemctl status nginx
```
> **Explanation:**
> + Tekrardan `systemctl` ile nginx servisini kontrol etiğimiz de  servisin  çalıştığını görebiliriz.

```sh
$ firewall-cmd --add-service=http --permanent
```

```sh
$ firewall-cmd --add-service=https --permanent
```

> **Explanation:**
> +  REHL temeli işletim sistemlerinde  `firewalld deamon` çalışır. nginx de `80 port` kullanır Bu yüzden `80 port`'una izin vermemiz gerekmektedir.
> + Nginx https bağlantıları için 443 portu kullanır. Güvenlik duvarı tarafında bu porta izin vermemiz gerekmektedir.

```sh
$ firewall-cmd --reload
```
> **Explanation:**
> + Firewalld deamond da yapılan değişikliklerin geçerli olabilmesi için bu komutu çalıştırıyoruz.

---
#### C. Kaynak Koddan Derleme:

+ nginx derleme işlemini yapabilmemiz için nginx source code indirmemiz gerekmektedir.
+ Kaynak kodu indirme  [link](https://nginx.org/en/download.html) gitmek için tıkayınız.
+ Derleme işlemini `Mainline version` ile sürdüreceğiz. `nginx-1.27.2` bağlantının adresini kopyalıyoruz.

```sh
$ wget https://nginx.org/download/nginx-1.27.2.tar.gz
```


> [!CAUTION]
> + Eğer paket yöneticileri(`apt, yum...`) ile yüklediğimizde nginx'e modül(*3.part modül veya özel modül*) dahil edemiyoruz. Bu yüzden nginx kaynak koddan yüklemede modül yükleme imkanı vermektedir. 
> + Kaynak kod üzerinde derleme işlemi işletim sisteminden bağımsız yapar. Yani ubuntu üzerinde yapılan işlemler almalinux üzerinde de aynı şekilde olur.

```sh
$ tar -zxvf nginx-1.27.2.tar.gz            # Çıktı: nginx-1.27.2
```
> **Explanation:**
> + Hem arşivlenmiş(tar) hem de sıkıştırılmış(gz) dosya `tar`  ve parametreleri ile çıkarma işlemini yapıyoruz.

```shell
$ cd nginx-1.27.2; ls -l
```

**Çıktı:**
```shell
total 860
-rw-r--r--. 1 ottoman ottoman 328790 Oct  2 18:30 CHANGES
-rw-r--r--. 1 ottoman ottoman 503040 Oct  2 18:30 CHANGES.ru
-rw-r--r--. 1 ottoman ottoman   5215 Oct  2 18:13 CODE_OF_CONDUCT.md
-rw-r--r--. 1 ottoman ottoman   4049 Oct  2 18:13 CONTRIBUTING.md
-rw-r--r--. 1 ottoman ottoman   1319 Oct  2 18:13 LICENSE
-rw-r--r--. 1 ottoman ottoman  14220 Oct  2 18:13 README.md
-rw-r--r--. 1 ottoman ottoman    787 Oct  2 18:13 SECURITY.md
drwxr-xr-x. 6 ottoman ottoman   4096 Oct 11 02:28 auto
drwxr-xr-x. 2 ottoman ottoman    168 Oct 11 02:28 conf
-rwxr-xr-x. 1 ottoman ottoman   2611 Oct  2 18:13 configure
drwxr-xr-x. 4 ottoman ottoman     72 Oct 11 02:28 contrib
drwxr-xr-x. 2 ottoman ottoman     40 Oct 11 02:28 html
drwxr-xr-x. 2 ottoman ottoman     21 Oct 11 02:28 man
drwxr-xr-x. 9 ottoman ottoman     91 Oct  2 18:13 src
```
> **Explanation:**
> + İndirdiğimiz nginx kaynak kodlarını ekran yazdırıyoruz.

##### C.1. Debian Temeli OS:
```sh
$ sudo apt install build-essential
```

```sh
$ sudo apt install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev make
```
> **Explanation:**
> + `PCRE library`, `build-essential` ile birlikte gelmemektedir.

---
##### C.2. REHL Temeli OS:
```sh
$ sudo yum install groupinstall "Development Tools"
```
> **Explanation:**
> + Nginx'i kaynak koddan(`source code`) derleme(`compile`)  yapılabilmesi için işletim sistemlerine bağlı olarak bazı araçların yüklenmesi gerekmektedir.
> + `PCRE library`, `Development Tools` içerisinde gelmektedir. 

```sh
$ sudo yum list installed pcre pcre-devel zlib zlib-devel openssl openssl-devel make
```
> **Explanation:**
> + `list installed` komutu ile hangi kütüphanelerin yüklü olduğunu teyit edebilirsiniz.

```sh
$ sudo yum install pcre pcre-devel zlib zlib-devel openssl openssl-devel make
```
> **Explanation:**
> + Bir çok kütüpahane `Development Tools` ile gelmektedir fakat Eğer eksik komut ile karşılaşırsanız bu kütüphaneleri yükleyebilirsiniz.

---
##### C.3. OS'dan Bağımsız İşlemler:

###### C.3.1 Configure İşlemi:
> [!CAUTION]
> + Aşağıdaki komutu indirmiş olduğunuz `nginx source code` içerisinde çalıştırınız.

```sh
$ sudo ./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module
```

> **Explanation:**
> + Nginx configure etme işlemini başlatabiliriz: `configure` komutun alacağı parametreler [link](https://nginx.org/en/docs/configure.html) de mevcuttur.
> + `sudo ./configure --help` komut ile `configure` komutun alacağı parametreleri terminal üzerinde ekranda listeleyebiliriz.
> + İşlem tamamlandığında `Makefile` dosyası oluşacaktır.

###### C.3.2. Make işlemi:
```shell
$ sudo make
```

> **Explanation:**
> + Kodu derlemek için `make` komutunu çalıştırıyoruz.
> + Eğer böyle bir çıktı görüyorsanız; `make[1]: Leaving directory '/home/ottoman/nginx-1.27.2'` işlem tamamlanmıştır.

```shell
$ sudo make install
```

> **Explanation:**
> + Nginx yüklemesi yapmak için bu komutu çalıştırıyoruz.

```shell
$ nginx -v                 # Çıktı: nginx version: nginx/1.27.2
```

> **Explanation:**
> + nginx versiyonunu veriyorsa nginx'niz hayırlı olsun kurulum başarılı.

###### C.3.3 Nginx Çalıştırma:
```shell
$ sudo nginx 
```

> **Explanation:**
> + Yüklemiş olduğumuz nginx uygulamasını başlatacaktır.

```sh
$ sudo ps aux | grep nginx
```
> **Explanation:**
> + Nginx'in çalıştığını teyit etmek için ve çıktı bize bir master ve bir de worker process'leri ekrana verecektir.

**Nginx yeniden başlatma:**
```shell
$ sudo nginx -s reload                                # 1
```

```shell
$ sudo /usr/bin/kill -s HUB <nginxProcessID>          # 2
```
> **Explanation:**
> 1. `nginx` programı `-s` parametresi ile kendi process'ini yeniden başlatma sinyali gönderiyoruz.
> 2. Linux'ta "HUP" sinyali, "Hang Up" anlamına gelir. "Hang Up" türkçe anlamı telefonu kapatmak anlamına gelir. Sinyal numarası olarak 1 (SIGHUP) ile temsil edilir.
> 	+ **Bir terminal kapandığında**: Bir kullanıcı SSH üzerinden bağlanıp terminalden çıkış yaparsa, bağlı işlemlere SIGHUP sinyali gönderilir. Bu sinyal, işlemin terminalle bağlantısının kesildiğini belirtir.
> 	+ **Yeniden başlatma (reload)**: Bazı daemon veya servisler için SIGHUP sinyali, yapılandırma dosyalarının yeniden yüklenmesi (reload) anlamına gelir. Örneğin, Nginx veya Apache gibi web sunucuları yapılandırma değişikliklerinden sonra bu sinyalle yeniden başlatılabilir, böylece tam anlamıyla durdurulup yeniden başlatılmadan değişiklikler uygulanır.


```sh
$ curl -i http://192.168.1.132
```
> **Explanation:**
> + `curl` komut ile `GET` isteği yaptığımızda bize nginx'in varsayılan web sitesi geri dönmesi gerekir.
> + Bu `GET` isteğini her hangi bir tarayıcı ile de yapılabilir.

##### C.4. Nginx Servis Oluşturma:

> [!IMPORTANT]
> + Servis oluşturma işletim sistemlerinde bağımsızdır fakat hangi servis yöneticisini kullanmasına bağlıdır.
> + Burada kullanılan servis yöneticisi **systemd** olacaktır. Bundan dolayı hem debian hem de REHL temeli OS de aynıdır.

###### nginx.service dosyası:
```shell
$ vim /lib/systemd/system/nginx.service
```

```systemd
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/var/run/nginx.pid
ExecStartPre=/usr/bin/nginx -t
ExecStart=/usr/bin/nginx
# ExecReload=/usr/bin/nginx -s reload
ExecReload=/usr/bin/kill -s HUP $MAINPID
ExecStop=/usr/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```
> **Explanation:**
> 1. **Description:** servis bağlatıldığında log dosyalarına() söyle bir çıktı veriyor;
> 	+ Starting The NGINX HTTP and reverse proxy server...
> 	+ Started The NGINX HTTP and reverse proxy server...
> 2. 

```shell
$ sudo systemctl daemon-reload
```
> **Explanation:**
> + systemd manager configuration yeniden yükleyecektir.
> + Yeni bir systemd servis dosyası eklediğinizde ya da mevcut bir servis dosyasında değişiklik yaptığınızda, `systemctl daemon-reload` çalıştırarak systemd'nin bu değişiklikleri okumasını sağlamanız gerekir.

```shell
$ sudo systemctl enable --now nginx.service
```
> **Explanation:**
> + /etc/systemd/system/multi-user.target.wants/nginx.service.

### Nginx Modülleri:


> [!NOTE]
> + Modülleri nginx'i kaynak koddan derlerken kullanılır;
> + Genel şeması: `configure --module1 --module2 --module3 ...`

###### 1. --sbin-path modülü:
+ nginx yürütülebilir dosyasının adını ayarlar. Bu ad yalnızca kurulum sırasında kullanılır. Varsayılan olarak dosya `prefix /sbin/nginx` olarak adlandırılır.([nginx.com](https://nginx.org/en/docs/configure.html))
+ derleme ve kurulum sürecinde Nginx’in ikili (binary) dosyasının sistemde nereye yükleneceğini belirlemek için kullanılır.(chatgpt)
+ Bu seçenek, Nginx’in çalıştırılabilir dosyasının (genellikle `/usr/sbin/nginx`) tam yolunu tanımlamanıza olanak tanır.
**Örnek Kullanım:**
```shell
$ ./configure --sbin-path=/usr/bin/nginx
```
###### 2. --conf-path modülü:
+ nginx.conf yapılandırma dosyasının adını ayarlar. Eğer gerek duyulur ise nginx farklı bir yapılanadırma dosyası ile başlatılabilir; `nginx -c configFile` ile bul işlem yapılabilir.([nginx.com](https://nginx.org/en/docs/configure.html))
+ Nginx'in ana yapılandırma dosyasının (configuration file) sistemde nerede bulunacağını belirtmek için kullanılır.
**Örnek Kullanım:**
```shell
$ ./configure --conf-path=/etc/nginx/nginx.conf
```

###### 3. --error-log-path modülü:
+ Birincil derece hatanın, uyarıların ve tanılama dosyasının adını ve dizin yolunu ayarlar. Yükleme sonrasında `error_log` yönergesi(directive) ile `nginx.conf` dosyasında dosyanın adı ve dizin yolu değiştirilebilir.([nginx.com](https://nginx.org/en/docs/configure.html))
+ Nginx'in hata günlüklerinin (error log) nereye yazılacağını belirlemek için kullanılır.
+ **Amaç:** Sunucudaki hataların kolayca izlenebilmesi ve teşhis edilmesi için kullanılır.

**Örnek Kullanım:**
```shell
$ ./configure --error-log-path=/var/log/nginx/error.log
```

###### 4. --http-log-path modülü:
+ HTTP sunucusunun birincil istek günlük dosyasının adını ve dizin yolunu ayarlar. Yükleme sonrasında `access_log` yönergesi(directive) ile `nginx.conf` dosyasında dosyanın adı ve dizin yolu değiştirilebilir. Varsayılan olarak dosya `prefix/logs/access.log` olarak adlandırılır. ([nginx.com](https://nginx.org/en/docs/configure.html))
+ HTTP isteklerinin günlüklerinin (access log) hangi dosyada tutulacağını belirlemek için kullanılır.
+ **Amaç:** Web sunucusuna yapılan HTTP isteklerinin kaydını tutmak, trafik analizleri ve hata ayıklama için önemlidir.

**Örnek Kullanım:**
```shell
$ ./configure --http-log-path=/var/log/nginx/access.log
```

###### 5. --with-pcre module:
+ PCRE kütüphanesinin kullanımını zorlar.([nginx.com](https://nginx.org/en/docs/configure.html))
+ Perl Compatible Regular Expressions (PCRE) kütüphanesinin Nginx'e dahil edilmesini sağlar. 
+ PCRE, düzenli ifadeleri (regex) kullanarak metin eşleme ve işleme işlemleri yapar ve Nginx’in gelişmiş özelliklerinden bazıları için gereklidir.


> [!CAUTION]
> + Nginx'te kullanılan regex ifadeleri Perl regex ile yüksek oranda uyumludur. 
> + Bu, Nginx kullanıcılarının Perl'deki regex özelliklerini büyük ölçüde kullanabilmelerini sağlar.
> + PCRE, birçok programlama dili ve araç tarafından desteklenir çünkü Perl regex sözdizimi oldukça güçlü ve esnektir.
> + Bu modülü kullanabilmek için; *REHL* işletim sistemlerinde `pcre pcre-devel` ve *debian* temeli işletim sistemlerinde `libpcre3 libpcre3-dev` kütüphanelerin kurulu olması gerekmektedir.


**Örnek Kullanım:**
```shell
$ ./configure --with-pcre
```

**Kullanım Alanı:**
```nginx
location ~ ^/images/(.*)\.(jpg|jpeg|png)$ {
    # İstek "/images/" ile başlayan ve ".jpg", ".jpeg", ".png" ile biten URL'ler için
    # Yapılacak işlemler
}

```
> **Explanation:**
> + nginx `pcre` kütüphanesini eklenmesi ile yukarıda görülen nginx de  `regex` yapısını kullanabiliyoruz.
###### 6. --pid-path modülü:
+ Ana process'in process ID depolayacak olan nginx.pid dosyasının adını ve dizin yolunu ayarlar. Nginx derleme sonrasında `pid` yönergesini(directive) kullanarak `nginx.conf` dosyasında dosya adı ve dizin yolu değiştirilebilir. ([nginx.com](https://nginx.org/en/docs/configure.html))
+ Nginx'in **Process ID (PID)** dosyasının nerede saklanacağını belirtmek için kullanılır.
+ PID dosyası, çalışan Nginx sürecinin kimliğini (process ID) içerir. Bu dosya, Nginx sürecini izlemek, yönetmek ve gerektiğinde yeniden başlatmak veya durdurmak için kullanılır.
+ **Amaç:** Nginx’i başlatmak, durdurmak veya yeniden başlatmak için PID dosyası kullanılır. Özellikle sistem yöneticileri, bu dosyayı kullanarak süreçlerin ID'sini bilip doğru işlemler yapabilir.(chatgpt)

**Örnek Kullanım:**
```sh
$ ./configure --pid-path=/var/run/nginx.pid
```
###### 7. --with-http_ssl_module modülü:
+ HTTP sunucusuna [HTTPS protokol desteği](https://nginx.org/en/docs/http/ngx_http_ssl_module.html) ekleyen bir modülün oluşturulmasını sağlar.Bu modül varsayılan olarak derlenmez. Bu modülü derlemek ve çalıştırmak için OpenSSL kütüphanesi gereklidir.([nginx.com](https://nginx.org/en/docs/configure.html))
+ Nginx'in **SSL/TLS** (Secure Sockets Layer / Transport Layer Security) desteğiyle derlenmesini sağlar. SSL/TLS, web trafiğini şifreleyerek güvenli iletişim kurmanıza olanak tanır ve HTTPS protokolünün temelini oluşturur.


> [!CAUTION]
> + `with-http_ssl_module` kullanabilmek için;
> + REHL işletim sistemleri de `openssl openssl-devel` kütüphaneleri
> + Debian temeli işletim sistemlerin de `libssl-dev` kütüphanesi kurulu olması gerekmektedir. 

**Örnek Kullanım:**
```sh
$ ./configure --with-http_ssl_module
```
### Nginx Config Dosyası:

+ **nginx configuration file is the heart of nginx web server**

> [!NOTE]
> + Eğer debian temelli işletim sistemlerinde `apt` paket yöneticisini kullanarak nginx kurduysanız `nginx config` dosyası `/etc/nginx` dizinde mevcut olacaktır.

+ `nginx.conf`, NGINX'in çalışma şeklini belirleyen direktiflerin bulunduğu ana konfigürasyon dosyasıdır.

#### A.Simple ve Block Directive:
##### A.1.Simple Directive:
+  Bir modülün isimi boşlukla ayrılmış parametre sonu noktalı virgüle(`;`) bitiyorsa buna **simple directive** denir.
+ Simple directive anahtar-değer çifti formunda tanımlanan her hangi birşey.
###### Örnek:
```nginx
worker_processes auto;
```
> **Explanation:**
> + `worker_processes` modülün isimi ardından bir boşluk daha sonrasında `auto` parametresi en son olarak da noktalı virgül(`;`) gelmektir. Fakat parametre kullanılmıştır.
> + İşte bu yapıdaki directive'ler *simple directive* diyoruz.
##### A.2.Block Directive:
+ Simple directive ile aynı ama nginx'in alacağı komutları süslü parantez(`{...}`) ile çevreler.
+ Eğer Block Directive içerisine her hangi bir directive alırsa artık bu yapıya **context** denir.
###### Örnek:
```nginx
http {                          # 1
    server {                    # 2 
        listen 80;
        server_name example.com;

        location / {           # 3
            root /var/www/html;
            index index.html;
        }
    }
}
```
> **Explanation:**
> 1. `http` bir block directive ama içerisinde hem simple directive hem de block directive içerdiği için block directive yerine **context** deyiceğiz.
> 2. `server` bir context diyoruz çünkü içerisinde directive'ler bulunmaktadır.
> 3. `location` da yukarıdaki tanım uygun olarak bir context'dir.
> 4. Kaynak: [Configuration File’s Structure](https://nginx.org/en/docs/beginners_guide.html)

#### B.`nginx.conf` Dosyasın Genel Yapısı:
+ NGINX yapılandırma dosyası, hiyerarşik bir yapıya sahiptir ve genellikle dört ana bloktan oluşur:
1. **Main Context**
2. **Event Context**
3. **HTTP Context**
4. **Server Context**
5. **Location Context**
###### `nginx.conf` Genel Şablonu:
```nginx
# Main Context
...
events {
	# Event Context
	...
}
http {
	# Http Context
	upstream backend_server {
		# Upstream Context
	}
	...
    server {
	    # Server Context
	    ...
        location / {
	        # Location Context
            ...
        }
    }
}
```


> [!NOTE]
> + `include` directive'i bir dosyayı bulunduğu dosyaya dahil eder. Kısacası bir dosya dahil etmek isteniyorsa `include` directive kullanılır.

###### 1. Main Context:
+ **Konum:** `nginx.conf` dosyasının en üst düzeyinde bulunur.
+ **Amaç:** NGINX'in genel çalışma ayarlarını belirler. Bu ayarlar tüm `server` ve `location` blokları için geçerlidir.
+ main context'in bir diğer adı da *global context* denir. Ayırca küme parantezi`{...}` içermeyen tek context'dir.
+ *Temel düzeyde tüm uygulamayı etkileyen detayları yapılandırmak(config etmek) için kullanılır.*

```nginx
user www-data;                                   # 1
worker_processes auto;                           # 2
pid /run/nginx.pid;                              # 3
include /etc/nginx/modules-enabled/*.conf;       # 4
```
> **Explanation:**
> 1. NGINX süreçlerini çalıştıracak kullanıcı ve grup.
> 2. NGINX'in çalıştıracağı worker process'lerin sayısını belirler.
> 	+ **auto:** kaç işlemci var ise o kadar worker process oluşturur.
> 3. nginx'in çalışmış olduğu process ID'yi verir.


> [!CAUTION]
> + Bazı directive'ler main context'inde ayarlanması gerekmektedir Örneğin;
> + `user www-data`: worker process'leri çalıştıracak kullanıcı(user) ve grup(group)
> + `worker_processes 4`: çalıtırılacak olan worker sayısı
> + `pid /run/nginx.pid`: ana process'in PID'yi kayıt edecek dosya ve konumu

###### 2. Events Context:
+ **Konum**: Main context içinde yer alır.
+ **Amaç**: NGINX'in olay (event) modelini ve bağlantı yönetimini ayarlar.
```nginx
events {
    worker_connections 768;                 # 1
    # multi_accept on;
}
```
> **Explanation:**
> 1. `worker_connections`: Her `worker process` aynı anda açabileceği maksimum bağlantı sayısı.

###### 3. Http Context:
+ **Konum**: Main context içinde yer alır.
+ **Amaç:** NGINX'in **HTTP protokolü** ile nasıl çalışacağını belirleyen ayarların yapıldığı bölümdür. Örneğin, **gzip sıkıştırma**, **keep-alive bağlantı süresi**, ve **log formatları** gibi genel HTTP özelliklerini yapılandırır.
+ Http context, programın HTTP veya HTTPS bağlantılarını nasıl işleyeceğini tanımlamak için gerekli tüm yönergeleri ve diğer bağlamları içerecektir.
+ nginx config dosyasında en uzun context `http context`'dir.

```nginx
http {
    # Basic Settings
    sendfile on;                                 # 1

    include /etc/nginx/mime.types;               # 2
    default_type application/octet-stream;

    # SSL Settings
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
    ssl_prefer_server_ciphers on;

    # Logging Settings
    access_log /var/log/nginx/access.log;         # 3
    error_log /var/log/nginx/error.log;           # 3

    # Gzip Settings
    gzip on;                                      # 4

    # Virtual Host Configs
    include /etc/nginx/conf.d/*.conf;             # 5
    include /etc/nginx/sites-enabled/*;           # 5
}
```
> **Explanation:**
> 1. `sendfile`: Dosya gönderme optimizasyonunu etkinleştirir.
> 2. `mime type` ile dosya tiplerini `nginx.conf` dahil edilir.
> 3. `Log` dosyaların  nereye yazılacağını belirliyor.
> 4. `gzip` ile dosya sıkıştırılıp gönderiliyor.
> 5. `server context` tanımlanmış  dizinler `nginx.conf` dahil ediliyor.

###### 4. Server Context:
+ **Konum**: HTTP context içinde yer alır.
+ **Amaç**: Belirli bir sunucu (domain) için ayarları tanımlar. Her `server` bloğu, farklı bir domain veya IP için yapılandırılabilir.

```nginx
server {
    listen 80;                          # 1
    listen [::]:80;                     # 2

    server_name example.com;            # 3

    root /var/www/example.com;          # 4
    index index.html;                   # 5

    location / {                        # 6
        try_files $uri $uri/ =404;
    }
}
```
> **Explanation:**
> 1. `listen directive`: Sunucunun dinleyeceği IP adresi ve port. Burada dinlenen port 80 dinleniyor. *IP versiyonu versiyon IP4 olmaktadır.*
> 2. Yine `listen` directive kullanılmaktadır ama *IP versiyonu IP6 versiyonudur*.
> 3. `server_name directive`: Sunucunun adını (domain) belirtir. 
> 4. `root directive`: Web dosyalarının bulunduğu dizin.
> 5. `index directive`: Varsayılan olarak sunulacak dosya.
> 6. `location context`: URL yollarına göre istekleri yönlendirir.


> [!IMPORTANT]
> + Nginx’te **virtual host (sanal ana bilgisayar)**,
> + aynı sunucuda birden çok web sitesinin veya alan adının barındırılmasını sağlayan bir yapılandırma tekniğidir.
> + Her bir virtual host, `server` blokları kullanılarak yapılandırılır ve her blok, belirli bir alan adına veya bağlantı noktasına göre ayrılır.
> + Böylece, Nginx gelen istekleri doğru siteye yönlendirir ve her bir alan adı için farklı ayarlar yapılabilir.
> + Bu özellik, paylaşımlı sunucularda veya farklı siteler için gereklidir.

**Virtual Host Örnek:**
```nginx
http {
    server {
        listen 80;
        server_name example.com;
        root /var/www/example;
        index index.html;
    }

    server {
        listen 80;
        server_name example.org;
        root /var/www/example_org;
        index index.html;
    }
}
```
> **Explanation:**
> + `example.com` ve `example.org` alan adları aynı Nginx sunucusunda barındırılır.
> + Her `server` bloğu, kendi kök dizinini (`root`) ve ayarlarını içerir. Böylece, gelen istekler belirtilen alan adına göre ilgili dizine yönlendirilir.
> + Sonuç olarak 2 tane `virtual host` mevcuttur.

###### 5. Location Context:
+ **Konum**: Server context içinde yer alır.
+ **Amaç**: Belirli bir URL yoluna gelen isteklerin nasıl işleneceğini tanımlar. Örneğin, belirli dosya türleri için özel işlemler yapılabilir veya belirli dizinlere istekler yönlendirilebilir.
+ `location context` içerinde bir veya birden fazla `location context` tanımlayabiliriz.

```nginx
server {
    listen 80;                          # 1
    listen [::]:80;                     # 2

    server_name example.com;            # 3

    root /var/www/example.com;          # 4
    index index.html;                   # 5

    location /linux {                   # 6
		index linux.html;  
        root /var/www/html;             # 7
    }
}
```
> **Explanation:**
> 7. En basit `location` tanımı yapıyoruz. Konun anlaşılabilmesi için;
- `vim /var/www/linux.html` komut ile basit bir html dosyası oluşturduk. 	
- `curl -i http://192.168.1.129/linux/` komut veya tarayıcı ile `GET` isteği yaptığımızda nginx bize `/var/www/linux/linux.html` içreğini bize gönderecektir.
- `index directive` :  nginx programının `/var/www/linux/` dizininde `linux.html` dosyasına bakmasını söylemektedir. 
-  Yukarıdaki config dosyasında kullanılan `try_files` directive buradaki `location` context içeriği ile aynı işi yapar ama daha gelişmiş özelikleri mevcuttur.

###### 6. Upstream Context:
+ Nginx'te **upstream context**, birden fazla sunucunun yük dengelemesi (load balancing) için ayarlandığı bir context'dır.
+ upstream context bir veya birden fazla server IP'ler veya domain'ler bulunur.(Upstream Sunucular)
+ Genellikle, `proxy_pass` direktifiyle birlikte kullanılarak gelen isteklerin belirli bir sunucu grubuna yönlendirilmesi sağlanır.
+ Yük dengeleme yapılırken, istekler sunucular arasında dağıtılır.

**Örnek:**
```nginx
upstream backend_servers {
    server server1.example.com;
    server server2.example.com;
}

server {
    location / {
        proxy_pass http://backend_servers;
    }
}
```
> **Explanation:**
> + `proxy_pass` komutu ile gelen istekleri `backend_servers` upstream'ında bulunan sunucular gönderiyoruz.
> + Temel olarak `load balancing` yani yük dengeleme işlemi yapıyoruz. Yük dengeleme olarak denmek isten mevcut sunucuya gelen isteklerin belirli bir algoritma ile `upstream`'daki sunuculara dağıtmaktır.
> + nginx varsayılan olarak `load balancing` de `round-robin` kullanmaktadır.
> + `Load Balancing` konusunda daha detaylı anlatılacaktır.

> [!WARNING]
> + Upstream context, http context içerisine yerleştirilmelidir. Server context'in de dış kısmında bulunmalıdır.

###### 7.Mail Context:
+ Mail context main context yani global context içerisinde tanımlanır.

###### Final nginx.conf:
+ `/etc/nginx/nginx.conf` dosyasını en basit hali;

```nginx
# Main Context
user www-data;                                   # 1
worker_processes auto;                           # 2
pid /run/nginx.pid;                              # 3
include /etc/nginx/modules-enabled/*.conf;       # 4

events {
	# Event Context
    worker_connections 768;                 # 1
    # multi_accept on;
}
http {
	# Http Context
    # Basic Settings
    sendfile on;                                 # 1

    include /etc/nginx/mime.types;               # 2
    default_type application/octet-stream;

    # SSL Settings
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
    ssl_prefer_server_ciphers on;

    # Logging Settings
    access_log /var/log/nginx/access.log;         # 3
    error_log /var/log/nginx/error.log;           # 3

    # Gzip Settings
    gzip on;                                      # 4

    # Virtual Host Configs
    include /etc/nginx/conf.d/*.conf;             # 5
    include /etc/nginx/sites-enabled/*;           # 5
}
```

+ `/etc/nginx/sites-enabled/default` dosyası;
+ `include /etc/nginx/sites-enabled/*` directive ile aşağıdaki config dosyası da dahil olacaktır.

```nginx
server {
    listen 80;                          # 1
    listen [::]:80;                     # 2

    server_name example.com;            # 3

    root /var/www/example.com;          # 4
    index index.html;                   # 5

    location /linux {                   # 6
		index linux.html;  
        root /var/www/html;             # 7
    }
}
```

### Nginx Variables:



### Nginx Directives:
#### Listen directive:
+ **Amaçı:** IP için `adres` ve `port` veya UNIX-domain soket için `path` istekleri hangi sunucuların kabul edeceğini ayarlar.
###### 1.İsim tabanlı sanal sunucular:
+ nginx ilk olarak isteğin hangi sunucuda işleneceğine karar verir. Bütün üç sanal sunucunun `*:80` portunu dinlediği basit bir yapılandırmayla başlayalım:

```nginx
server {
    listen      80;
    server_name example.org www.example.org;
    ...
}

server {
    listen      80;
    server_name example.net www.example.net;
    ...
}

server {
    listen      80;
    server_name example.com www.example.com;
    ...
}
```

+ bu nginx yapılandırma(config) da nginx, isteğin hangi sunucuya yönlendirileceğini belirlemek için yalnızca isteğin başlık alanı olan “Host”u test eder.
+ Eğer değeri herhangi bir sunucu adıyla uyuşmuyorsa veya istek bu başlık alanını hiç içermiyorsa, nginx isteği bu port için varsayılan sunucuya yönlendirecektir.
+ Varsayılan sunucu ilk sunucudur — bu nginx'in standart varsayılan davranışıdır.
+ Hangi sunucunun varsayılan olacağını, listen yönergesindeki default_server parametresiyle açıkça belirleyebilirsiniz:

```nginx
server {
    listen      80 default_server;
    server_name example.net www.example.net;
    ...
}
```


> [!WARNING]
> + `default_server` parametresi 0.8.21 sürümünden beri mevcuttur. Daha önceki sürümlerde `default` parametrenin kullanılması gerekirdi.
> + Varsayılan sunucunun, sunucu adının değil, *dinleme portunun* bir özelliği olduğunu unutmayın. 

**Kaynak:**
1. [nginx.org](https://nginx.org/en/docs/http/ngx_http_core_module.html#listen)
2. [How nginx processes a request](https://nginx.org/en/docs/http/request_processing.html)

#### Root Directive:

#### Server_name Directive:


> [!IMPORTANT]
> 1. nginx, client'dan aldığı istekleri önce dinlenen port(`listen`) numarasına ve daha sonra `server_name` ile tanımlanmış `virtual server` alana iletir. 
> 2. nginx, tarayıcıdan gelen `Host header` bakar  ve daha sonra `server_name` ile aynı olan `virtual server` bölgesine yönlendirir.


##### 1.Server_name:
##### 2.Server_name ve Host header:
+ NGINX'te `server_name` direktifi ile **HTTP Host header** arasında doğrudan bir ilişki vardır.
+ Bu ilişki, NGINX'in birden fazla sanal sunucuyu (virtual server) nasıl yönettiğini ve doğru sunucu bloklarını (server blocks) nasıl eşlediğini belirler.
###### Temel İlişki:
+ `server_name` directive, gelen istekteki *Host header*'a dayanarak belirli bir *server block* seçmek için kullanılır.
+ HTTP protokolünde, istemciler (örn. tarayıcılar), isteğin hedef domain adını *Host header* içinde sunucuya gönderir.
+ NGINX, gelen isteği işlerken Host header'daki değerle `server_name` direktifini karşılaştırır ve eşleşen bir *server block* bulmaya çalışır.
---
###### Nasıl Çalışır?
 **1.İstemciden Gelen İstek:**
```http
GET / HTTP/1.1
Host: www.example.com
```
> **Explanation:**
> + İstemci(Client) bir domain'e HTTP isteği gönderir.

**2.Nginx Yapılandırması:**
```nginx
server {
    server_name www.example.com;
    root /var/www/example;
}

server {
    server_name www.another.com;
    root /var/www/another;
}
```
> **Explanation:**
> + NGINX, konfigürasyondaki `server_name` direktifleriyle *Host header*'daki değeri eşleştirir.

**Eşleşme:**
+ Host header `www.example.com` ise, NGINX bu istek için ilk `server` bloğunu seçer.
---
###### Detaylı Eşleşme Kuralları:
+ NGINX, gelen istek için doğru `server block`u seçerken belirli bir sırayla kontrol yapar:

**1.Direk Eşleşme:**
```nginx
server {
	listen 80;
    server_name www.example.com;
}
```
> **Explanation:**
> + Host header'daki değer, `server_name` direktifindeki herhangi bir değerle tam eşleşirse, o `server block` seçilir.
> + Host header: `www.example.com` → Bu blok seçilir.

---
**2.Joker Karakter Eşleşmesi(Wildcard Matching):**
```nginx
server {
	listen 80;
    server_name *.example.com;
}
```
> **Explanation:**
> + `server_name`'de joker karakterler (`*`) kullanılabilir:
> + `*.example.com`: `foo.example.com`, `bar.example.com` gibi alt alan adlarını eşleştirir.
> + `example.*`: `example.com`, `example.org` gibi son ekleri eşleştirir.
> + Host header: `sub.example.com` → Bu blok seçilir.

---
**3.Düzenli İfade Eşleşmesi(Regex Matching):**
```nginx
server {
	listen 80;
    server_name ~^www\.(.+)\.com$;
}
```
> **Explanation:**
> + `server_name`'de düzenli ifadeler kullanılabilir.
> + Host header: `www.example.com` → Bu blok seçilir.
> + *Uyarı:* Eğer dikkat  regex kullanabilmemiz için domain başına `~^` işareti koymamız gerekmektedir.

---
**4.Varsayılan Server Block(Default Server):**
```nginx
server {
    listen 80 default_server;
    server_name _;
}
```
> **Explanation:**
> + Hiçbir `server_name` eşleşmiyorsa, **varsayılan server block** kullanılır.
> + Bir server block, `default_server` olarak işaretlenebilir.
> + Bu blok, Host header eşleşmese bile çalışır.

---
###### Host Header ile server_name Örneği:
```nginx
server {
	listen 80;
    server_name www.example.com;
    root /var/www/example;
}

server {
	listen 80;
    server_name www.test.com *.test.com;
    root /var/www/test;
}

server {
    listen 80 default_server;
    server_name _;
    root /var/www/default;
}
```
> **Explanation:**
> + `Host: www.example.com` => ilk blok seçilir(exact name)
> + `Host: api.test.com` => İkinci blok seçilir(Wildcard name)
> + `Host: unknown.com`  => Üçüncü blok seçilir. (Varsayılan server block)

> [!IMPORTANT]
> + `server_name` ile Host header, doğru `server block`u seçmek için birbiriyle ilişkilidir.
> + Eşleşme sırası:
> 	1. Tam Eşleşme(exact name)
> 	2. Wildcard Eşleşme (Wildcard name)
> 	3. Regex Eşleşme
> 	4. Varsaylan Server Block(`default_server`)

**Ek Kaynak:** [Resmi Sitesi](https://nginx.org/en/docs/http/server_names.html)
#### Return directive:

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
> 


#### Allow and  Deny IP

```nginx
        location /secure {

                try_files $uri /secure.html;

                allow 192.168.1.4;

                deny all;

        }
```
> **Explanation:**
> + Bu sayfaya sadece 192.168.1.4’den gelen isteklere izin ver (allow 192.168.1.4) tüm diğer ip’den gelen istekleri reddet (deny all ). 



### Nginx Contexts:

#### Types Context:

#### Location Context:
+ NGINX'te **`location` context**, gelen bir HTTP isteğinin **URL yolu** (path) temelinde nasıl işleneceğini tanımlayan bir context'dir.
+ **`server` context** içinde yer alır ve gelen isteklere göre farklı davranışlar sergilemek için kullanılır.
+ Örneğin, bir URL'nin hangi dosyayı sunacağını, hangi proxy sunucusuna yönlendirileceğini veya hangi kuralın uygulanacağını belirtmek için kullanılır.
+ Location Block'lar Server Block'ların (veya diğer konum blokları) içerisinde yaşar ve istek URI'sinin nasıl işleneceğine karar vermek için kullanılır.
+ Location Context içerinde Location Context oluşturabiliyoruz ve buna `nested Location context` denir
##### Syntax:
```nginx
location [optional_modifier] [URI] {
	...
}
```
> **Explanation:**
> + 


**Kaynak:** [Best Tutorial - 2:32](https://www.youtube.com/watch?v=NwijBVfiK_o)
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
>  + [[Nginx location#Örnek 1| location_1]] 

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
```http
GET /resim.jpg HTTP/1.1
Host: example.com
```
> **Explanation:**
> İstemci, belirli bir kaynağı (örneğin, bir web sayfası veya resim dosyası) almak için caching sunucusuna bir istek gönderir. Bu istekte `If-Modified-Since` başlığı genellikle yer almaz, çünkü istemci kaynağı henüz önbelleğe almadı.

2. **Caching Sunucunun Yanıtı:**
```http
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
```http
GET /resim.jpg HTTP/1.1
Host: example.com
If-Modified-Since: Wed, 21 Oct 2023 07:28:00 GMT
```
> **Explanation:**
> İstemci aynı kaynağı tekrar almak istediğinde, caching sunucusuna yeni bir GET isteği gönderir. Bu istek genellikle `If-Modified-Since` başlığını içerir ve daha önce aldığı `Last-Modified` tarihini içerir.

#### 2. Caching Sunucu ve Orijinal Sunucu Arasında İletişim
1. **Caching Sunucusunun Öncelikli Yanıtı:**
```http
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 12345

... (cached image data) ...
```
> **Explanation:**
> Caching sunucusu, istemciden gelen isteği aldığında, önbelleğinde bulunan verinin `Last-Modified` tarihini kontrol eder. Eğer istemcinin `If-Modified-Since` tarihinden daha yeni bir veri varsa, caching sunucusu doğrudan istemciye `200 OK` yanıtıyla birlikte önbellekteki veriyi döner.

2. **Orijinal Sunucuya İstek Gönderme:**
```http
GET /resim.jpg HTTP/1.1
Host: example.com
If-Modified-Since: Wed, 21 Oct 2023 07:28:00 GMT
```

> **Explanation:**
> + Eğer caching sunucusu, istemciden gelen `If-Modified-Since` başlığının tarihinden daha eski bir veri bulursa veya ilgili kaynak önbellekte mevcut değilse, caching sunucusu bu başlıkla birlikte orijinal sunucuya bir istek gönderir.
> + Orijinal sunucu, istekte belirtilen tarihten itibaren kaynağın değişip değişmediğini kontrol eder.

```http
HTTP/1.1 304 Not Modified
```
> **Explanation:**
>  Eğer kaynak belirtilen tarihten sonra değişmemişse, orijinal sunucu `304 Not Modified` yanıtı döner. Bu durumda caching sunucusu, önbelleğindeki veriyi yeniden kullanarak istemciye bir yanıt gönderir.

```http
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
> 1. .png uzantlı dosyaları kapsamaktadır. Ayrıca  tilda(~): küçük büyük harf duyarlığı vardır. Bakınız: [[Nginx location#Regex Case Sensitive Eşleşme|Regex Case Sensitive Eşleşme]] 
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

