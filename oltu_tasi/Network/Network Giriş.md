## OSI nedir?
+ OSI (Open Systems Interconnection) modeli, bilgisayar ağlarının nasıl çalıştığını açıklayan ve standart hale getirilmiş bir referans modelidir. Bu model, iletişimin daha anlaşılır ve yönetilebilir olmasını sağlamak için 7 farklı katmana bölünmüştür.
+ Her katman, bir ağ iletişimi sırasında gerçekleşen belirli görevleri yerine getirir.

### 1. Physical Layer:
##### 1.1. RJ45:

### 2. Data Link:


### 3. Network:
##### IP: 
+ IP, İngilizce de *Internet Protocol* kısaltmalarından gelir.
+ Paketlerdeki IP adresleri, hedef sisteme ulaşana kadar bunların ağdaki farklı düğümler üzerinden yönlendirilmesine yardımcı olur.

### 4.Transport Layer:
+ İletişimin güvenilirliği, hata kontrolü ve veri akışının düzenlenmesi bu katmanda gerçekleştirilir. TCP ve UDP gibi protokoller bu katmanda çalışır.
##### 4.1. TCP:
+ TCP (Transmission Control Protocol), internetin temel protokollerinden biri olup, verilerin iki bilgisayar arasında *güvenilir* bir şekilde iletilmesini sağlayan bir iletişim *protokolüdür*.
+ *TCP, veri iletiminde güvenliği, veri sıralamasını ve hata kontrolünü sağlar.*
+ TCP'nin çalışma süreci genellikle üç aşamada açıklanır: **üçlü el sıkışması**, **veri iletimi** ve **bağlantı sonlandırma**.
###### 1. Üçlü el sıkışması:
+ TCP, iki cihaz arasında veri iletmeden önce bir bağlantı kurar. Bu süreç üç aşamalı bir el sıkışma ile gerçekleştirilir:
1. **SYN(Synchronization) Paketi Gönderme:** İletişimi başlatan cihaz (istemci), diğer cihaza (sunucu) bir SYN (senkronizasyon) paketi gönderir. Bu paket, istemcinin bağlantı talebinde bulunduğunu belirtir ve istemcinin başlatacağı ilk sıra numarasını içerir.
2. **SYN-ACK (Synchronization-Acknowledgment) Paketi Alma:** Sunucu, SYN paketini aldığında bağlantı isteğini onaylamak için bir SYN-ACK (senkronizasyon-onay) paketi geri gönderir. Bu paket, sunucunun başlatacağı sıra numarasını ve istemcinin SYN isteğine onay verdiğini belirtir.
3. **ACK (Acknowledgment) Paketi Gönderme:** İstemci, SYN-ACK paketini aldığında, son adım olarak sunucuya ACK (onay) paketi gönderir. Bu, istemcinin bağlantıyı onayladığını ve veri iletimi için hazır olduğunu gösterir.
###### 2. Veri iletimi:
1. **Veri Segmentlere Bölünür:** Gönderici taraf, büyük verileri TCP segmentleri adı verilen küçük parçalara böler. Her segmentin başına bir TCP başlığı eklenir ve bu başlık, segmentin sıra numarası ve hata kontrol bilgilerini içerir.
2. **Sıralı Veri İletimi:** Segmentler sırayla alıcıya gönderilir. Alıcı, her bir segmentin doğru sırada olup olmadığını kontrol eder. Eğer bir segment kaybolmuş ya da bozulmuşsa, alıcı bunu fark eder ve kaybolan segmentin tekrar gönderilmesini talep eder.
3. **Onaylama(Acknowledgment):** Alıcı taraf, her başarılı şekilde alınan segment için göndericiye bir ACK paketi gönderir. Bu, alıcının segmenti doğru şekilde aldığını ve bir sonraki segmentin gönderilebileceğini belirtir.
4. **Akış Kontrolü:** TCP, alıcı tarafın kapasitesine göre veri akışını düzenler. Eğer alıcı, gelen veriyi işleyemeyecek kadar yoğun ise, gönderici veri hızını düşürür.
5. **Tıkanıklık Kontrolü:** TCP, ağdaki tıkanıklıkları algılayabilir ve veri iletim hızını ağın durumuna göre ayarlar. Ağ tıkanıklığı olduğunda, TCP daha az veri gönderir ve ağda daha fazla kapasite olduğunda gönderim hızını artırır.
###### 3. Bağlantıyı Sonlandırma:
1. **FIN (Finish) Paketi Gönderme:** 
##### 4.2 UDP:
+ UDP ingilizce de *User Datagram Protocol* olarak bilinir.
+ 

#### 5. Session:

#### Presentation:


### 7.Application Layer:
+ Kullanıcı ile doğrudan etkileşimde olan katmandır. Uygulama yazılımlarının (web tarayıcıları, e-posta istemcileri, FTP istemcileri gibi) ağ üzerinden veri alışverişi yapmasını sağlar.
#### 7.1 HTTP:
+ **HTTP** istemci(client) ve sunucu(server) modeline dayanır. HTTP web istemcisi ve web sunucusu arasında bağlantı kurmak için kullanılır. HTTP web sayfalarındaki bilgileri gösterir.
+ HTTP, istemci tarayıcısı (istek) ile web sunucusu (yanıt) arasında *hipermetin(hypertext)* biçiminde veri aktarımı için kullanılır; **HTTPS**'de de aynı şey geçerlidir; ancak veri aktarımı şifreli biçimde yapılır.
+ HTTP, TCP/IP temeli haberleşme protokolü kullanır.
##### 1.Connectionless Özelliği:
+ HTTP, bağlantısız bir protokoldür, yani bir istemci (örneğin bir web tarayıcısı) sunucuya her istek gönderdiğinde, bu istek için yeni bir bağlantı kurulur.
+ *Sunucu, isteği yanıtladıktan sonra bu bağlantı kapatılır. Bir sonraki istek için tekrar yeni bir bağlantı başlatılır. Bu süreç her istek için tekrar edilir.*
+ Bu özellik, iki taraf arasında kalıcı bir bağlantının kurulmadığı anlamına gelir. İstemci her istek gönderdiğinde, sunucu bir önceki isteği hatırlamaz; her istek ayrı ve bağımsız bir işlem olarak ele alınır.
###### Connectionless Özelliğin İşleyişi:
1. **İstemci isteği başlatır:** Tarayıcı, bir HTTP isteği oluşturur (örneğin bir web sayfasına erişmek için).
2. **Sunucu İsteği alır:** Sunucu bu isteği alır, işleyip yanıtını hazırlar (örneğin istenen web sayfasının HTML'sini gönderir).
3. **Yanıtı Gönderdikten Sonra Bağlantı Kapanır:** Sunucu, yanıtı gönderdikten sonra istemci ile olan bağlantıyı kapatır.
4. **Yeni İstek İçin Yeni Bağlantı:** Eğer istemci yeni bir istek gönderirse (örneğin başka bir sayfaya yönlendirme veya aynı sayfadan bir resim yükleme), bu istek için tekrar yeni bir bağlantı açılır.


> [!IMPORTANT]
> + HTTP/1.0'dan itibaren her istek için yeni bir bağlantı kurulurken, **HTTP/1.1** sürümünde **kalıcı bağlantılar** (persistent connections) kavramı tanıtılmıştır.
> + Bu özellik sayesinde aynı TCP bağlantısı üzerinden birden fazla istek ve yanıt gönderilebilir, bu da performansı artırır.
> + **HTTP/2** ise daha da ileri giderek, aynı bağlantı üzerinden çok sayıda isteği paralel olarak işleyebilir.

##### 2. Media Independent:
+ HTTP'nin "media independent" (medyadan bağımsız) olması, bu protokolün hangi türde içerik veya medya taşındığına bakmaksızın çalışabilmesi anlamına gelir. Yani HTTP, ilettiği verilerin ne olduğunu bilmez ya da anlamaz; sadece veriyi taşır.
+ Bu veri, bir HTML sayfası, bir resim, bir video, bir ses dosyası veya başka bir format olabilir.
###### Media Independent Olmasın Anlamı:
1. **Veri Türünden Bağımsızdır:** HTTP, taşınan verinin formatını veya yapısını anlamaz. İstemci bir istek yapar, sunucu bu isteğe uygun yanıtı hazırlar ve HTTP sadece bu yanıtı taşır. Bu veri bir resim, video, ses dosyası, metin ya da herhangi bir formatta olabilir.
2. **MINE Türleri ile Tanımlama:** HTTP istek ve yanıtlarında medya türleri, **MIME (Multipurpose Internet Mail Extensions)** türleri ile tanımlanır.  Örneğin, bir web tarayıcısı sunucudan bir web sayfası istediğinde, sunucu yanıtında MIME türünü belirtir (örneğin, `text/html`), böylece tarayıcı gelen veriyi nasıl işleyeceğini bilir. Örnek: `text/html` — Bir HTML dosyası, `image/jpeg` — Bir JPEG resmi ve  `video/mp4` — Bir MP4 video dosyası
3. **Her Türlü İçeriği Taşıyabilir:** HTTP, herhangi bir medya türünü veya veriyi taşıyabilir. Bir resim, video, ses dosyası ya da dosya türü fark etmeksizin, HTTP üzerinden iletilebilir. Bu yüzden, metin tabanlı HTML'den yüksek kaliteli video dosyalarına kadar geniş bir yelpazede içerik taşımak için kullanılabilir.
##### 3. Stateless:
+ HTTP'nin **stateless** (durumsuz) olması, her bir isteğin bağımsız olması ve sunucunun, önceki istekler hakkında herhangi bir bilgi saklamaması anlamına gelir.
+ Sunucu, her gelen isteği sanki ilk kez gelmiş gibi değerlendirir, önceki isteklerin bağlamını veya durumunu hatırlamaz.

##### 7.2 POP:
+ POP'un açılımı *Post Office Protocol* 
+ E-posta almak için yaygın olarak kullanılır ve üçüncü sürümü (POP3) en güncel versiyondur. POP3, kullanıcıların e-posta sunucusundaki mesajları bilgisayarlarına indirmelerine ve çevrimdışı erişmelerine olanak tanır.
###### POP3 ve IMAP Farkı:


##### 7.3 SMTP:
+ Açılımı: Simple Mail Transport Protocol
+ e-posta *gönderimi ve iletimi* için kullanılan bir internet protokolüdür.


> [!IMPORTANT]
> + SMTP, genellikle **e-posta gönderme** işlemlerinde kullanılırken, POP3 ve IMAP gibi protokoller **e-posta alma** işlemlerinde kullanılır.
##### 7.4 FTP:
+ FTP, kullanıcıların dosyaları bir makineden diğerine aktarmalarına olanak tanır.
+ 