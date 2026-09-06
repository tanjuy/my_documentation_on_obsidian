
# 1. Telif hakkı(Copyright)

Telif Hakkı © 1997 - 2026, PHP Belgeler Grubu (PHP Documentation Group). Bu materyal, yalnızca **Creative Commons Attribution 3.0 Lisansı** veya sonraki sürümlerinde belirtilen hüküm ve koşullara tabi olarak dağıtılabilir. [Creative Commons Attribution 3.0 lisansının](https://www.php.net/manual/en/cc.license.php) bir kopyası bu kılavuzla birlikte dağıtılmaktadır. En güncel sürüme şu anda [» http://creativecommons.org/licenses/by/3.0/](http://creativecommons.org/licenses/by/3.0/) adresinden ulaşılabilir.

# 2. Başlarken(Getting Started)

## 2.1. Giriş - PHP nedir ve neler yapabilir?

### 2.1.1. PHP nedir?

PHP (PHP: Hypertext Preprocessor ifadesinin özyinelemeli bir kısaltmasıdır), özellikle web geliştirme için uygun olan ve HTML içine gömülebilen, yaygın olarak kullanılan açık kaynaklı genel amaçlı bir betik dilidir.

Güzel, ama bu ne anlama geliyor? Bir örnek:

**Örnek #1 Giriş niteliğinde bir örnek**

```php
<!DOCTYPE html>  
<html>  
	<head>  
		<title>Example</title>  
	</head>  
	<body>  
  
	<?php  
		echo "Hi, I'm a PHP script!";  
	?>  
  
	</body>  
</html>
```

PHP, HTML çıktısı üretmek için çok sayıda komut kullanmak yerine (C veya Perl'de görüldüğü gibi), içine gömülü kod barındıran HTML sayfalarından oluşur ve bu kod belirli bir işlev gerçekleştirir (bu örnekte, Hi, I'm a PHP script! çıktısı verir). PHP kodu, PHP moduna girip çıkmayı sağlayan özel `<?php` ve `?>` başlangıç ve bitiş işlem yönergeleri arasına alınır.

PHP’yi istemci taraflı(*client-side*) JavaScript gibi dillerden ayıran şey, kodun sunucuda çalıştırılması ve bunun sonucunda üretilen HTML’in istemciye gönderilmesidir. İstemci, bu betiğin çalıştırılmasıyla elde edilen sonucu görür, ancak altta yatan kodun ne olduğunu bilmez. Hatta bir web sunucusu, tüm HTML dosyalarını PHP ile işleyecek şekilde yapılandırılabilir; bu durumda kullanıcılar PHP kullanıldığını anlayamaz.

PHP kullanmanın en güzel yanı, yeni başlayanlar için son derece basit olması, ancak profesyonel bir programcı için birçok gelişmiş özellik sunmasıdır. PHP'nin özelliklerinin uzun listesini okumaktan çekinmeyin. PHP ile hemen hemen herkes çok kısa sürede basit betikler yazmaya başlayabilir.

Her ne kadar PHP'nin gelişimi sunucu taraflı betik oluşturmaya odaklanmış olsa da, onunla çok daha fazlası yapılabilir. Daha fazlasını öğrenmek için **2.1.2. PHP neler yapabilir?** bölümüne göz atın veya doğrudan web programlamayı öğrenmeye başlamak için **giriş eğitimine(A simple tutorial)** gidin.

### 2.1.2. PHP neler yapabilir?

Her şey. PHP temel olarak sunucu taraflı betik oluşturmaya(*scripting*) odaklanmıştır; bu nedenle form verilerini toplamak, dinamik sayfa içeriği oluşturmak veya çerez (cookie) gönderip almak gibi herhangi bir CGI programının yapabildiği her şeyi yapabilir. Ama PHP bunun çok daha fazlasını yapabilir.

PHP betiklerinin kullanıldığı iki temel alan vardır:

- **Sunucu taraflı betik oluşturma (Server-side scripting):** Bu, PHP'nin en yaygın kullanılan ve ana hedef alanıdır. Bunun çalışması için üç şey gereklidir: PHP yorumlayıcısı (CGI veya sunucu modülü), bir web sunucusu ve bir web tarayıcısı. Tüm bunlar, PHP programlamayı denemek için yerel bir bilgisayarda da çalıştırılabilir. Daha fazla bilgi için [kurulum talimatları](https://www.php.net/manual/en/install.php) bölümüne bakabilirsiniz.
- **Komut satırı betiği oluşturma (Command line scripting):** Bir PHP betiği, herhangi bir sunucu veya tarayıcı olmadan, sadece PHP yorumlayıcısı(*PHP parser*) ile çalıştırılabilir. Bu kullanım şekli, Unix veya macOS’ta `cron`, Windows’ta ise Görev Zamanlayıcı (*Task Scheduler*) ile düzenli olarak çalıştırılan betikler için idealdir. Bu betikler basit metin işleme görevleri için de kullanılabilir. Daha fazla bilgi için [PHP’nin komut satırı kullanım](https://www.php.net/manual/en/features.commandline.php) bölümüne bakabilirsiniz.

PHP; Linux, pek çok Unix türevi (HP-UX, Solaris ve OpenBSD dahil), Microsoft Windows, macOS, RISC OS ve muhtemelen daha fazlası dahil olmak üzere tüm büyük işletim sistemlerinde kullanılabilir. PHP ayrıca günümüzdeki web sunucularının büyük çoğunluğunu desteklemektedir. Buna **Apache**, **IIS** ve daha birçoğu dahildir. **FastCGI PHP** ikili(*FastCGI PHP binary file*) dosyasını kullanabilen **lighttpd** ve **nginx** gibi web sunucuları da bu kapsama girer. PHP, bir modül(*module*) olarak ya da bir CGI işlemcisi(*CGI processor*) olarak çalışabilir.

> [!TIP]
> PHP'nin web sunucularıyla iki farklı şekilde entegre olabilir:
> 1. **Modül(_module_) olarak:** PHP, doğrudan web sunucusunun (örneğin apache) içine bir eklenti gibi yerleştirilir. Sunucu ve PHP tek bir süreç olarak çalışır. 
> 2. **CGI işlemcisi(_CGI processor_) olarak:** PHP, web sunucusundan(örneğin nginx) bağımsız ayrı bir program olarak çalışır. Sunucu her PHP isteği için PHP programını ayrıca başlatır, işlem tamamlanınca sonucu sunucuya iletir. 

Böylece PHP ile geliştiriciler, hem bir işletim sistemi hem de bir web sunucusu seçme özgürlüğüne sahip olurlar. Dahası, **prosedürel programlama (procedural programming)** veya **nesne yönelimli programlama (OOP)** ya da her ikisinin bir karışımını kullanma seçeneğine de sahiptirler.

PHP yalnızca HTML çıktısı vermekle sınırlı değildir. PHP'nin yetenekleri arasında resimler veya PDF dosyaları gibi zengin dosya türleri oluşturmak, verileri şifrelemek ve e-posta göndermek yer almaktadır. Ayrıca JSON veya XML gibi metin tabanlı içerikleri kolaylıkla çıktı olarak verebilir. PHP bu dosyaları otomatik olarak oluşturabilir ve doğrudan ekrana yazdırmak yerine dosya sistemine kaydederek dinamik içerikler için sunucu taraflı bir **önbellek** (*server-side cache*) oluşturabilir.

> [!tip]
> #### Önbellekleme (caching)
> Normalde PHP, bir kullanıcı sayfayı her ziyaret ettiğinde o içeriği **sıfırdan üretir** ve doğrudan tarayıcıya gönderir. Ancak PHP, ürettiği bu dosyayı (resim, PDF, JSON vb.) tarayıcıya göndermek yerine **sunucunun diskine kaydedebilir.**
> Böylece bir sonraki kullanıcı aynı içeriği istediğinde, PHP o içeriği tekrar sıfırdan üretmek zorunda kalmaz; diskten hazır olanı okuyup gönderir. Buna **önbellekleme (caching)** denir.
> **Basit bir örnekle:**
> - Her gün binlerce kişi bir hava durumu sayfasını ziyaret etsin.
> - PHP her seferinde veritabanından veriyi çekip sayfayı yeniden oluşturmak yerine, sayfayı bir kez üretip diske kaydeder.
> - Sonraki ziyaretçilere bu hazır dosya sunulur; bu da sunucunun iş yükünü ciddi ölçüde azaltır ve sayfaların daha hızlı yüklenmesini sağlar.

PHP’nin en güçlü ve en önemli özelliklerinden biri, çok geniş bir [**veritabanı(database)** yelpazesini](https://www.php.net/manual/en/refs.database.php) desteklemesidir. Veritabanı destekli bir web sayfası yazmak, veritabanına özel eklentilerden (örneğin [MySQL](https://www.php.net/manual/en/book.mysqli.php) için) birini kullanarak, ya da [PDO](https://www.php.net/manual/en/book.pdo.php) gibi bir soyutlama katmanı aracılığıyla oldukça kolaydır. Ayrıca, [ODBC](https://www.php.net/manual/en/book.uodbc.php) eklentisi sayesinde Open Database Connectivity standardını destekleyen herhangi bir veritabanına bağlanmak da oldukça kolaydır. CouchDB gibi bazı veritabanları ise [cURL](https://www.php.net/manual/en/book.curl.php) veya [soketler](https://www.php.net/manual/en/book.sockets.php) aracılığıyla kullanılabilir.


> [!TIP]
> #### CouchDB
> PHP, MySQL veya PostgreSQL gibi popüler veritabanları için **doğrudan yerleşik eklentilere** sahiptir. Ancak CouchDB gibi bazı veritabanlarının böyle özel bir eklentisi yoktur.
> Bu durumda PHP, bu veritabanlarıyla iki alternatif yöntemle iletişim kurabilir:
> + **cURL aracılığıyla:** cURL, PHP'nin internet üzerinden HTTP istekleri göndermesini sağlayan bir araçtır. CouchDB gibi veritabanları REST API üzerinden çalıştığından, PHP cURL ile bu veritabanına HTTP istekleri gönderip veri alışverişi yapabilir.
> + **Soketler aracılığıyla:** Soket, iki program arasında doğrudan bir iletişim kanalıdır. PHP, bir veritabanı sunucusuna soket bağlantısı açarak ham veri gönderip alabilir.

PHP ayrıca LDAP, IMAP, SNMP, NNTP, POP3, HTTP, COM (Windows üzerinde) ve sayısız diğer protokolü kullanarak diğer servislerle haberleşme desteğine sahiptir. Ham ağ soketleri açabilir ve diğer herhangi bir protokolü kullanarak etkileşime girebilir. PHP, neredeyse tüm web programlama dilleri arasında karmaşık veri alışverişi sağlayan **WDDX** desteğine sahiptir. Karşılıklı etkileşimden bahsetmişken; Java nesnelerini örnekleme(*instantiation*) ve bunları PHP nesneleri gibi şeffaf biçimde kullanma desteğine sahiptir.

> [!TIP]
> #### WDDX (Web Distributed Data eXchange) 
> **WDDX (Web Distributed Data eXchange)**, farklı programlama dilleri ve platformlar arasında veri alışverişi yapmak için geliştirilmiş XML tabanlı bir veri formatıdır.
> ##### Ne işe yarar?
> Örneğin bir PHP uygulaması, bir Python veya Java uygulamasına veri göndermek istediğinde, her dilin veri yapıları birbirinden farklı olabilir. WDDX bu veriyi her iki tarafın da anlayabileceği ortak bir XML formatına dönüştürür.
> ##### Basit bir örnekle:
> PHP'deki bir dizi (array) şu şekilde WDDX formatına çevrilebilir:
> ```xml
> <wddxPacket>
>  <data>
>    <array length="3">
>      <string>elma</string>
>      <string>armut</string>
>      <string>muz</string>
>    </array>
>  </data>
> </wddxPacket>
> ```
> Bu format daha sonra başka bir dil tarafından okunup kendi veri yapısına dönüştürülebilir.
> 
> **Önemli bir not:** WDDX günümüzde artık çok kullanılan bir teknoloji değildir. Yerini büyük ölçüde **JSON** ve **XML** tabanlı daha modern veri alışveriş formatları almıştır. Nitekim PHP 7.4 sürümünden itibaren WDDX desteği kaldırılmıştır.

PHP, [metin işleme](https://www.php.net/manual/en/refs.basic.text.php) konusunda da güçlü özellikler sunar. Buna Perl uyumlu düzenli ifadeler ([PCRE](https://www.php.net/manual/en/book.pcre.php)) ile birlikte [XML belgelerini ayrıştırmak ve erişmek](https://www.php.net/manual/en/book.pcre.php) için çeşitli eklenti(_extension_) ve araçlar dahildir. PHP, tüm XML eklentilerini [libxml2](https://www.php.net/manual/en/book.libxml.php)'in sağlam temeli üzerine standartlaştırır ve buna ek olarak [SimpleXML](https://www.php.net/manual/en/book.simplexml.php), [XMLReader](https://www.php.net/manual/en/book.xmlreader.php) ve [XMLWriter](https://www.php.net/manual/en/book.xmlwriter.php) desteği sunarak özellik setini genişletir.

Ayrıca hem [**alfabetik**](https://www.php.net/manual/en/extensions.php) hem de [**kategoriye**](https://www.php.net/manual/en/funcref.php) göre sınıflandırılmış daha birçok ilginç eklentileri(_extensions_) mevcuttur. Ayrıca, PHP manüel kendi dokümantasyonunda yer alabilecek ya da yer almayabilecek ek [PECL](https://www.php.net/manual/en/install.pecl.intro.php) eklentileri de mevcuttur; örneğin [Xdebug](https://xdebug.org/).

Bu sayfa, PHP'nin sunabileceği tüm özellikleri ve faydaları listelemek için yeterli değildir. [PHP'nin kurulumu](https://www.php.net/manual/en/install.php) hakkındaki bölümleri okumaya devam edin ve burada bahsedilen eklentilerin(_extensions_) açıklamaları için **[fonksiyon referansı](https://www.php.net/manual/en/funcref.php)** bölümüne göz atın.

> [!tip]
> #### Eklenti (extension) nedir?
> **Eklenti (extension)**, PHP'nin temel yapısına sonradan eklenebilen, belirli bir işlevi yerine getiren ek bir modüldür.
> **Basit bir benzetmeyle:** PHP'yi bir akıllı telefona benzetirsek, eklentiler de bu telefona yüklenen **uygulamalar** gibidir. Telefonun kendisi temel işlevleri yerine getirir; ancak uygulamalar sayesinde çok daha fazlası yapılabilir.
> ##### Neden eklentiler vardır?
> PHP her özelliği varsayılan olarak içine almaz, çünkü:
> - Her proje her özelliğe ihtiyaç duymaz
> - Tüm özellikler dahil edilseydi PHP gereksiz yere şişer ve yavaşlardı
> - Geliştiriciler yalnızca ihtiyaç duydukları eklentileri kurarak PHP'yi hafif ve hızlı tutabilir
> ##### Örnekler:
> + `mysqli` : MySQL veritabanıyla bağlantı kurar
> + `gd` : Resim oluşturur ve düzenler
> + `curl` : İnternet üzerinden veri çeker

## 2.2. Basit Bir Eğitim(A simple tutorial)


> [!NOTE]
> #### İçindekiler(Table of Contents)
> - 2.2.1. PHP destekli ilk sayfanız(*Your first PHP-enabled page*)
> - 2.2.2. İşe Yarar Bir Şey(*Something Useful*)
> - 2.2.3. Formlarla çalışma
> - 2.2.4. Sırada ne var?

Burada PHP'nin temellerini kısa ve basit bir eğitimle göstermek istiyoruz. Bu metin yalnızca PHP ile dinamik web sayfaları oluşturmayı ele almaktadır; oysa PHP sadece web sayfası oluşturmakla sınırlı değildir. Daha fazla bilgi için "**2.1.2. PHP neler yapabilir?**" başlıklı bölüme bakabilirsiniz.

PHP destekli(*PHP-enabled*) web sayfaları, tıpkı normal HTML sayfaları gibi değerlendirilir; bu sayfaları normal HTML sayfalarını oluşturduğunuz ve düzenlediğiniz yöntemlerle aynı şekilde oluşturabilir ve düzenleyebilirsiniz.
### 2.2.1. PHP destekli ilk sayfanız(*Your first PHP-enabled page*)

Bu eğitim, PHP’nin zaten kurulu olduğunu varsayar. Kurulum talimatlarını [» download](https://www.php.net/downloads.php) sayfasında bulabilirsiniz.

Aşağıdaki içeriğe sahip `hello.php` adında bir dosya oluşturun:

**Örnek #1 İlk PHP betiğimiz: `hello.php`**

```php
<?php  
  
echo "Hello World!";  
  
?>
```

Terminalinizi kullanarak bu dosyanın bulunduğu dizine gidin ve aşağıdaki komutla bir geliştirme sunucusu başlatın:

```bash
php -S localhost:8000
```

Tarayıcınızı kullanarak, web sunucunuzun URL'sinin sonuna /hello.php dosya referansını ekleyerek dosyaya erişin. Yukarıda çalıştırılan komuta göre URL şu şekilde olacaktır: [http://localhost:8000/hello.php](http://localhost:8000/hello.php). Her şey doğru yapılandırılmışsa bu dosya PHP tarafından işlenecek ve tarayıcınızda "Hello World!" çıktısını göreceksiniz.


> [!tip]
> ##### Yerel Makine ile Uzak Sunucu Arasında Tünnelleme
> Eğer bir sunucuda çalışıyorsanız ve PHP çıktılarını kendi makinenizin tarayıcısında görmek isterseniz, SSH ile aşağıdaki gibi sunucu ile yerel makineniz arasında güvenli bir tünel açabilirsiniz:
> Bu komutu yerel makinenizde çalıştırarak `192.168.1.133` IP'li makine ile bir güvenli bir tünel açabilirsiniz.
> ```bash
> ssh -L 9090:localhost:8000 ottoman@192.168.1.133 -N
> ```
> ##### Komut Açıklamaları:
> + `ssh` → SSH bağlantısı başlatır.
> + **Yerel port (senin makinan)** 9090 ile **uzaktaki sunucunun kendi localhost portu** 8000 arasında bir tünel açar.
> + `ottoman@192.168.1.133` → SSH ile bağlanılacak kullanıcı ve IP (Ubuntu sunucusu)
> + `-N` → Bağlantıda **komut çalıştırma**, sadece tünel kur (terminal açılmaz).


PHP, normal bir HTML web sayfasının içine gömülebilir. Bu, aşağıdaki örnekte gösterildiği gibi, HTML belgenizin içine PHP ifadeleri(*statements*) yazabileceğiniz anlamına gelir:

```php
<!DOCTYPE html>  
<html>  
	<head>  
		<title>PHP Test</title>  
	</head>  
	<body>  
		<?php echo '<p>Hello World</p>'; ?>  
	</body>  
</html>
```

Bu, aşağıdaki çıktıyı verecektir:

```
<!DOCTYPE html>
<html>
    <head>
        <title>PHP Test</title>
    </head>
    <body>
        <p>Hello World</p>
    </body>
</html>
```

Bu program son derece basittir ve böyle bir sayfa oluşturmak için aslında PHP kullanmanıza gerek yoktur. Yaptığı tek şey, PHP `echo` deyimini(*statement*) kullanarak ekrana _Merhaba Dünya_ yazdırmaktır. Dosyanın herhangi bir şekilde çalıştırılabilir veya özel olması gerekmediğine dikkat edin. Sunucu, bu dosyanın PHP tarafından işlenmesi gerektiğini, `.php` uzantısını kullandığınız için anlar; çünkü sunucu bu uzantıya sahip dosyaları PHP’ye iletecek şekilde yapılandırılmıştır. Bunu, içinde pek çok ilginç işlem yapmanızı sağlayan özel etiketlerin bulunduğu normal bir HTML dosyası gibi düşünebilirsiniz.(Yani, bunu, normal bir HTML dosyası gibi düşünebilirsiniz; ancak içine eklenen özel PHP etiketleri sayesinde dinamik işlemler gerçekleştirebilirsiniz.)

Bu örneğin amacı, özel PHP etiketi(*tag*) formatını göstermektir. Bu örnekte, bir PHP etiketinin başlangıcını belirtmek için `<?php` kullandık. Ardından PHP ifadesini yerleştirdik ve kapatma etiketi olan `?>` işaretini ekleyerek PHP modundan çıktık. Bu şekilde, bir HTML dosyası içinde istediğiniz herhangi bir noktada PHP moduna girip çıkabilirsiniz. Daha fazla ayrıntı için kılavuzun [temel PHP sözdizimi](https://www.php.net/manual/en/language.basic-syntax.php) hakkındaki bölümünü okuyun.


> [!NOTE]
> #### Satır Sonları (Line Feed) Hakkında
> Satır sonlarının(*Line Feed*) HTML’de çok fazla bir anlamı yoktur; ancak yine de HTML kodunuzu daha düzenli ve okunabilir hale getirmek için satır sonları eklemek(*Line Feed*) iyi bir alışkanlıktır. Kapanış etiketi `?>`’nden **hemen sonra** gelen bir satır sonu(*Line Feed*), PHP tarafından kaldırılır. Bu, çıktı üretmemesi gereken birçok PHP bloğu yerleştirdiğinizde veya PHP içeren dosyaları dahil ettiğinizde (*include*) son derece yararlı olabilir. Aynı zamanda biraz kafa karıştırıcı da olabilir. Kapanış `?>` etiketinden sonra bir boşluk koyarak bir boşluk ve bir satır başı(*Line Feed*) çıktı vermesini zorlayabilir veya PHP bloğunuzun içindeki son `echo`/`print` ifadesine açık bir satır beslemesi ekleyebilirsiniz.(Yani, `?>`'den sonra boşluk koyarsanız, çıktıda hem boşluk hem de yeni satır olur. Alternatif olarak, PHP bloğunuzun içindeki son `echo` ya da `print` komutuna manuel olarak bir satır başı(`\n`) ekleyebilirsiniz.)


> [!TIP]
> ```php
> <?php
> echo "Merhaba";
> ?>
> 
> <p>Dünya</p>
> ```
> #### Beklenmeyen boşluk (line feed sorunu)
> 👉 Tarayıcı çıktısı aslında şuna benzer olur:
> ```
> Merhaba
> Dünya
> ```
> Buradaki **satır atlama**, `?>`’den sonra gelen line feed’den kaynaklanır.
> ##### PHP bunu otomatik kaldırır
> Ama PHP’nin özel davranışı şu:
> ```
> Merhaba<p>Dünya</p>
> ```
> 👉 `?>`'den hemen sonra gelen satır sonu **PHP tarafından yok sayılır**


> [!NOTE]
> #### Metin Düzenleyiciler Hakkında
> PHP dosyalarını oluşturmak, düzenlemek ve yönetmek için kullanabileceğiniz birçok metin düzenleyici(*editors*) ve Tümleşik Geliştirme Ortamı (IDE) mevcuttur. Bu araçların kısmi bir listesi [» PHP Düzenleyicileri Listesi](https://www.php.net/manual/en/context.php) adresinde tutulmaktadır. Bir metin düzenleyici(*editors*) önermek isterseniz, lütfen yukarıdaki sayfayı ziyaret edin ve sayfa yöneticisinden düzenleyiciyi listeye eklemesini isteyin. Sözdizimi vurgulama (syntax highlighting) özelliğine sahip bir metin düzenleyiciye(*editors*) sahip olmak oldukça faydalı olabilir.

> [!NOTE]
> #### Kelime İşlemciler Hakkında
> StarOffice Writer, Microsoft Word ve Abiword gibi kelime işlemciler(*word processors*), PHP dosyalarını düzenlemek için uygun değildir. Eğer bu test betiği için bunlardan birini kullanmak isterseniz, dosyayı mutlaka **düz metin (plain text)** olarak kaydettiğinizden emin olmalısınız; aksi takdirde PHP betiği okuyamaz ve çalıştıramaz.

Artık çalışan bir PHP betiğini başarıyla oluşturduğunuza göre, en ünlü PHP betiğini oluşturma zamanı geldi! [`phpinfo()`](https://www.php.net/manual/en/function.phpinfo.php) fonksiyonuna bir çağrı yapın; sisteminiz ve kurulumunuz hakkında kullanılabilir **ön tanımlı değişkenler( [predefined variables](https://www.php.net/manual/en/language.variables.predefined.php))**, yüklenmiş PHP modülleri ve **[yapılandırma](https://www.php.net/manual/en/configuration.php) ayarları** gibi pek çok faydalı bilgiyi göreceksiniz. Bu önemli bilgileri incelemek için biraz zaman ayırın.

**Örnek #2 PHP'den sistem bilgilerini alma**

```php
<?php  
  
phpinfo();  
  
?>
```

### 2.2.2. İşe Yarar Bir Şey(*Something Useful*)

Şimdi biraz daha yararlı bir şeyler yapalım. Ziyaretçinin ne tür bir tarayıcı kullandığını kontrol edeceğiz. Bunun için, tarayıcının HTTP isteğinin bir parçası olarak gönderdiği "**user agent**" (kullanıcı aracısı) dizgisini(*string*) inceleyeceğiz.
Bu bilgi bir [değişkende](https://www.php.net/manual/en/language.variables.php) saklanır. PHP'de değişkenler her zaman dolar işareti (`$`) ile başlar. Şu an ilgilendiğimiz değişken ise `$_SERVER['HTTP_USER_AGENT']` değişkenidir.

> [!NOTE]
> [`$_SERVER`](https://www.php.net/manual/en/reserved.variables.server.php), tüm web sunucusu bilgilerini içeren özel ve önceden tanımlanmış bir PHP değişkenidir. Bu tür değişkenler [_superglobal_](https://www.php.net/manual/en/language.variables.superglobals.php) olarak adlandırılır. Daha fazla bilgi için süper küreseller hakkındaki ilgili kılavuz sayfasına bakın.

Bu değişkeni ekrana yazdırmak için basitçe şunu yapabilirsiniz:

**Örnek #1 Bir değişkeni yazdırma (dizi elemanı - *Array element*)**

```PHP
<?php  
  
echo $_SERVER['HTTP_USER_AGENT'];  
  
?>
```

Bu betiğin örnek bir çıktısı şu şekilde olabilir:

```
Mozilla/5.0 (Linux) Firefox/112.0
```

PHP'de pek çok değişken [türü](https://www.php.net/manual/en/language.types.php) mevcuttur. Yukarıdaki örnekte, bir dizi(_array_) değişkeninin bir elemanını ekrana yazdırdık. Diziler(_array_) oldukça kullanışlı olabilir. [`$_SERVER`](https://www.php.net/manual/en/reserved.variables.server.php), PHP'nin size otomatik olarak sunduğu değişkenlerden yalnızca biridir. Bu değişkenlerin bir listesini kılavuzun(*manual*) [Reserved Variables](https://www.php.net/manual/en/reserved.variables.php)(rezerve değişkenler)" bölümünde listelenmiştir ya da önceki bölümdeki örnekte kullandığımız [`phpinfo()`](https://www.php.net/manual/tr/function.phpinfo.php) fonksiyonunun çıktısına bakarak tam listeye ulaşabilirsiniz.

Bir PHP etiketi içerisine birden fazla PHP ifadesi koyabilir ve tek bir `echo` işleminden daha fazlasını yapan küçük kod blokları oluşturabilirsiniz. Örneğin, kullanıcının Firefox tarayıcısı kullanıp kullanmadığını kontrol etmek isterseniz şunu yapabilirsiniz:

**Örnek #2 [Kontrol yapısı](https://www.php.net/manual/en/language.control-structures.php) ve [fonksiyon](https://www.php.net/manual/en/language.functions.php) kullanımına örnek**

```PHP
<?php  
  
if (str_contains($_SERVER['HTTP_USER_AGENT'], 'Firefox')) {  
	echo 'You are using Firefox.';  
}  
  
?>
```

Bu betiğin örnek bir çıktısı şu şekilde olabilir:

```
You are using Firefox.
```

Burada birkaç yeni kavram tanıtıyoruz. Bir `if` deyimi kullandık. Bir `if` ifadesi kullandık. Eğer C dilinde kullanılan temel sözdizimine aşinaysanız, bu yapı size oldukça mantıklı gelecektir. Aksi halde, bir başlangıç düzeyi PHP kitabı edinip ilk birkaç bölümü okumanız veya kılavuzun(*manual*) [Dil Referansı](https://www.php.net/manual/en/langref.php) bölümüne göz atmanız faydalı olabilir.

Tanıttığımız ikinci kavram ise [`str_contains()`](https://www.php.net/manual/tr/function.str-contains.php) fonksiyon çağrısıydı. [`str_contains()`](https://www.php.net/manual/tr/function.str-contains.php), bir string'in başka bir string'i içerip içermediğini belirleyen, PHP'nin yerleşik(*built-in*) bir fonksiyonudur. Bu durumda [`$_SERVER['HTTP_USER_AGENT']`](https://www.php.net/manual/tr/reserved.variables.server.php) (*haystack*) değerinin içinde `'Firefox'` (*needle*) arıyoruz. Eğer *needle*,  *haystack*'ın içinde bulunursa, fonksiyon **[true](https://www.php.net/manual/en/reserved.constants.php#constant.true)**  değerini döndürür. Aksi takdirde **[false](https://www.php.net/manual/en/reserved.constants.php#constant.false)** değerini döndürür. Eğer **true** dönerse, [`if`](https://www.php.net/manual/en/control-structures.if.php) ifadesi(*expression*) olumlu sonuçlanır ve süslü parantezler `{ }` içindeki kod çalıştırılır. Aksi takdirde kod çalıştırılmaz. `if`, [`else`](https://www.php.net/manual/en/control-structures.else.php) ve [`strtoupper()`](https://www.php.net/manual/en/function.strtoupper.php)(büyük harfe çevir) veya [`strlen()`](https://www.php.net/manual/en/function.strlen.php)(metin uzunluğu) gibi diğer fonksiyonlarla benzer örnekler oluşturmaktan çekinmeyin. İlgili her kılavuz sayfası da örnekler içermektedir. Fonksiyonların nasıl kullanılacağından emin değilseniz, hem [bir fonksiyon tanımının nasıl okunacağı](https://www.php.net/manual/en/about.prototypes.php) hakkındaki kılavuz(*manual*) sayfasını hem de [PHP fonksiyonları hakkındaki](https://www.php.net/manual/en/language.functions.php) bölümü incelemeniz faydalı olacaktır.

> [!tip]
> #### `str_contains` fonksyion nedir?
> `str_contains`, PHP’de bir metin (*string*) içinde başka bir metnin(*string*) geçip geçmediğini kontrol eden bir fonksiyondur. Dönüş değeri `true` veya `false`'dur.
> ##### Fonksiyon İmzası:
> ```PHP
> str_contains(string $haystack, string $needle): bool
> ```
> + *haystack* - içinde arama yapılan metin(*string*), türkçe karşılığı: samanlık
> + *needle* - aranan değer(*string*), türkçe karşılığı: iğne
> ##### Basit Örnek:
> ```PHP
> <?php
> $text = "Merhaba Dünya";
> 
> if (str_contains($text, "Dünya")) {
>     echo "Bulundu!";
> }
> ```

Bunu bir adım daha ileri götürebilir ve bir PHP bloğunun tam ortasında bile PHP moduna nasıl girip çıkabileceğinizi gösterebiliriz:

**Örnek #3 HTML ve PHP modlarının birlikte kullanımı**

```PHP
<?php  
if (str_contains($_SERVER['HTTP_USER_AGENT'], 'Firefox')) {  
?>  
	<h3>str_contains() returned true</h3>  
	<p>You are using Firefox</p>  
<?php  
} else {  
?>  
	<h3>str_contains() returned false</h3>  
	<p>You are not using Firefox</p>  
<?php  
}  
?>
```

Bu betiğin örnek bir çıktısı şu şekilde olabilir:

```
<h3>str_contains() returned true</h3>
<p>You are using Firefox</p>
```

Bir şeyler çıktı vermek için bir PHP `echo` ifadesi kullanmak yerine, PHP modundan çıktık ve doğrudan HTML gönderdik. Burada dikkat edilmesi gereken önemli ve güçlü nokta, betiğin **mantıksal akışının** bozulmadan kalmasıdır. `str_contains()` fonksiyonundan gelen sonuca bağlı olarak, HTML bloklarından yalnızca biri ziyaretçiye gönderilecektir. Başka bir deyişle, bu durum `'Firefox'` dizgisin(*string*) bulunup bulunmadığına bağlıdır.
### 2.2.3. Formlarla çalışma

PHP’nin en güçlü özelliklerinden biri, HTML formlarını ele alma biçimidir. Anlaşılması gereken temel kavram, herhangi bir form öğesinin(*form element*) PHP betiklerinizde otomatik olarak kullanılabilir hale geleceğidir. PHP ile form kullanımı hakkında daha fazla bilgi ve örnek için kılavuzun **Harici kaynaklı değişkenler** ([Variables from external sources](https://www.php.net/manual/en/language.variables.external.php)) bölümünü okuyun.

Aşağıda basit bir HTML formu örneği verilmiştir:

**Örnek #1 Basit bir HTML formu**

**Dosya adı:** `index.php` veya `index.html`

```HTML
<form action="action.php" method="post">
    <label for="name">Your name:</label>
    <input name="name" id="name" type="text">

    <label for="age">Your age:</label>
    <input name="age" id="age" type="number">

    <button type="submit">Submit</button>
</form>
```

Bu formda özel bir durum yoktur; herhangi bir özel etiket içermeyen, düz bir HTML formudur. Kullanıcı bu formu doldurup gönder butonuna bastığında `action.php` sayfası çağrılır. Bu dosyanın içine şuna benzer bir kod yazarsınız:

**Örnek #2 Formdan gelen veriyi yazdırma**

**Dosya adı:** `action.php`

```PHP
<php?
Hi <?php echo htmlspecialchars($_POST['name']); ?>.  
You are <?php echo (int) $_POST['age']; ?> years old.
```

Bu betiğin örnek bir çıktısı şu şekilde olabilir:

```
Hi Joe. You are 22 years old.
```

[`htmlspecialchars()`](https://www.php.net/manual/en/function.htmlspecialchars.php) ve `(int)` kısımları dışında, bu kodun ne yaptığı oldukça açık olmalıdır. `htmlspecialchars()` fonksiyonu, HTML için özel anlam taşıyan karakterlerin uygun şekilde kodlanmasını sağlar; böylece kullanıcıların sayfanıza HTML etiketleri veya JavaScript enjekte etmesi engellenmiş olur. `age` alanı için ise bunun bir sayı olduğunu bildiğimizden, onu doğrudan bir `int` (tam sayı) türüne [dönüştürebiliriz](https://www.php.net/manual/en/function.htmlspecialchars.php). Bu işlem(türü dönüşümü), gereksiz tüm karakterlerden otomatik olarak kurtulmamızı sağlar. İsterseniz PHP'nin bunu [filter](https://www.php.net/manual/en/function.filter-input.php) eklentisini(*extension*) kullanarak sizin yerinize otomatik olarak yapmasını da sağlayabilirsiniz. [`$_POST['name']`](https://www.php.net/manual/en/reserved.variables.post.php) ve [`$_POST['age']`](https://www.php.net/manual/en/reserved.variables.post.php) değişkenleri PHP tarafından sizin için otomatik olarak ayarlanır.

> [!tip]
> #### filter eklentisi ile
> Veriyi temizleme ve doğrulama işlemlerini kendin yazmak yerine, PHP’nin hazır filter sistemini kullanabilirsin.
> 
> **Dosya adı:** `action.php`
> ```PHP
> <?php
>
> $name = filter_input(INPUT_POST, 'name', FILTER_SANITIZE_SPECIAL_CHARS);
> $age = filter_input(INPUT_POST, 'age', FILTER_VALIDATE_INT);
> 
> echo "Hi ${name} \n";
> echo '<br>';
> echo "You are ${age} years old.";
> ``` 
> 

Daha önce [`$_SERVER`](https://www.php.net/manual/en/reserved.variables.server.php) süper global değişkenini kullanmıştık; yukarıda ise tüm POST verilerini içeren [`$_POST`](https://www.php.net/manual/en/reserved.variables.post.php) süper global değişkenini tanıttık. Formumuzun `method` değerinin POST olduğuna dikkat edin(`<form action="action.php" method="post">`). Eğer GET metodunu(`method="get"`) kullansaydık, form verileri [`$_GET`](https://www.php.net/manual/en/reserved.variables.get.php) süper global değişkeni içinde yer alacaktı.  Ayrıca, istek verilerinizin(*request data*) kaynağının nereden geldiği sizin için önemli değilse [`$_REQUEST`](https://www.php.net/manual/en/reserved.variables.request.php) süper global değişkenini de kullanabilirsiniz. Bu değişken, GET, POST ve COOKIE verilerinin birleşimini içerir.
### 2.2.4. Sırada ne var?

Edindiğiniz bu yeni bilgilerle, artık PHP kılavuzunun(*manual*) büyük bir kısmını ve örnek arşivlerinde bulunan çeşitli betikleri anlayabilecek düzeye gelmiş olmalısınız.

PHP'nin neler yapabileceğini gösteren çeşitli slayt sunumlarını görüntülemek için **PHP Konferans Materyalleri Sitesi'ne** bakın: [» http://talks.php.net/](http://talks.php.net/)

# 3. Kurulum ve Yapılandırma


> [!NOTE]
> #### İçindekiler(Table of Contents)
> +  3.1. Genel Kurulum Hususları
> +  3.2. Unix Sistemlerde Kurulum

## 3.1. Genel Kurulum Hususları

Kuruluma başlamadan önce, PHP’yi ne amaçla kullanmak istediğinizi belirlemeniz gerekir. [2.1.2. PHP neler yapabilir?](https://www.php.net/manual/en/introduction.php#intro-whatcando) bölümünde açıklandığı gibi, PHP’yi kullanabileceğiniz iki temel alan vardır:

+ Web siteleri ve web uygulamaları (sunucu taraflı betik yazımı)
+ Komut satırı betik yazımı

İlk ve en yaygın kullanım şekli için üç şeye ihtiyacınız vardır:  **PHP’nin kendisi**, **bir web sunucusu** ve **bir web tarayıcısı**. Muhtemelen zaten bir web tarayıcısına sahipsiniz; işletim sistemi kurulumunuza bağlı olarak bir web sunucusuna da sahip olabilirsiniz (örneğin; Linux ve macOS'ta Apache; Windows'ta IIS). Ayrıca bir şirketten web alanı (*hosting* - *webspace*) kiralayabilirsiniz. Bu şekilde kendi başınıza herhangi bir şey kurmanıza gerek kalmaz; yalnızca PHP betiklerinizi yazar, kiraladığınız sunucuya yükler ve sonuçları tarayıcınızda görürsünüz.

Sunucuyu ve PHP'yi kendiniz kurmanız durumunda, PHP'yi sunucuya bağlama yöntemi için iki seçeneğiniz vardır. Birçok sunucu için PHP’nin doğrudan bir modül arayüzü (SAPI olarak da adlandırılır) bulunmaktadır. Bu sunucular arasında Apache, Microsoft Internet Information Server(IIS), Netscape ve iPlanet sunucuları yer almaktadır. Eğer web sunucunuzun PHP modül desteği yoksa(örneğin; nginx), PHP'yi her zaman bir **CGI** veya **FastCGI** işlemcisi olarak kullanabilirsiniz. Bu, sunucunuzu PHP'nin CGI çalıştırılabilir dosyasını kullanarak sunucudaki tüm PHP dosyası isteklerini işleyecek şekilde yapılandırdığınız anlamına gelir.

Ayrıca, PHP’yi komut satırı betikleri yazmak için kullanmakla ilgileniyorsanız(örneğin, çevrimdışı olarak görselleri otomatik üreten ya da verilen argümanlara göre metin dosyalarını işleyen betikler yazma), her zaman komut satırı çalıştırılabilir dosyasına(*command line executable*) ihtiyacınız olacaktır. Daha fazla bilgi için [komut satırı PHP uygulamaları yazma](https://www.php.net/manual/en/features.commandline.php) hakkındaki bölümü okuyun. Bu durumda bir sunucuya veya tarayıcıya ihtiyaç yoktur.

Bu noktadan itibaren bu bölüm, Unix ve Windows üzerinde web sunucuları için sunucu modül arayüzleri(*module interfaces*) ve CGI çalıştırılabilir(*CGI executables*) dosyaları ile PHP kurulumunu ele almaktadır. Komut satırı çalıştırılabilir dosyasına(*command line executable*) ilişkin bilgileri de aşağıdaki bölümlerde bulacaksınız.

PHP kaynak kodu ve Windows için derlenmiş (binary) sürümler şu adreste ulaşılabilir:  [https://www.php.net/downloads.php](https://www.php.net/downloads.php)

## 3.2. Unix Sistemlerde Kurulum

> [!NOTE]
> #### İçindekiler(Table of Contents)
> + 3.2.1. Debian GNU/Linux ve Türevlerinde Paketlerden Kurulum
> + 3.2.2. DNF Kullanan GNU/Linux Dağıtımlarında Paketlerden Kurulum
> + 3.2.3. OpenBSD'de Paketlerden veya Port'lardan Kurulum
> + 3.2.4. Unix ve macOS Sistemlerde Kaynak Koddan Kurulum
> + 3.2.5. CGI ve Komut Satırı Kurulumları
> + 3.2.6. Unix Sistemlerde Apache 2.x


Çoğu Unix (ve Linux) işletim sistemi ve dağıtımı, kendi paket yönetim sistemleri üzerinden PHP’nin ve eklentilerinin paketlenmiş bir sürümünü sunar. Bu sistemleri kullanarak PHP kurulumuna dair temel bilgiler içeren bölümler mevcuttur.

PHP ayrıca bazı üçüncü taraf **uygulama sunucularının(third-party application)** bir bileşeni olarak da kurulabilir.

> [!tip]
> #### Uygulama sunucuları
> Bazı hazır yazılım paketleri, içlerinde PHP'yi **zaten kurulu ve yapılandırılmış** olarak sunarlar. Yani PHP'yi ayrıca kendiniz kurup yapılandırmak zorunda kalmazsınız; bu paketleri kurduğunuzda PHP de otomatik olarak gelir.
>
>  **En yaygın örnekler:**
> 
> |Paket|İçindekiler|
> |---|---|
> |**XAMPP**|Apache + PHP + MySQL + Perl|
> |**WAMP**|Windows + Apache + MySQL + PHP|
> |**MAMP**|macOS + Apache + MySQL + PHP|
> |**LAMP**|Linux + Apache + MySQL + PHP|
> 
>  ##### Bu paketler ne işe yarar?
>  Özellikle yeni başlayanlar için oldukça kullanışlıdır. Örneğin XAMPP'ı kurduğunuzda:
>  - Apache web sunucusu
>  - PHP
>  - MySQL veritabanı
>
>hepsi tek seferde kurulur ve birbirleriyle uyumlu şekilde çalışmaya hazır hale gelir.

Son olarak PHP, her zaman kaynak kod dağıtımlarından (*source distributions*) kurulabilir; bu yöntem, hangi özelliklerin, uzantıların ve sunucu API'lerinin (SAPI) etkinleştirileceğini seçme konusunda en büyük esnekliği sağlar. PHP'yi farklı sunucu API'leriyle kullanmak üzere derleme(*compiling*) ve yapılandırmaya(*configuring*) ilişkin bilgiler içeren bölümler de mevcuttur.
### 3.2.1.  Debian GNU/Linux ve Türevlerinde Paketlerden Kurulum

PHP kaynak kodundan kurulabildiği gibi, Debian GNU/Linux üzerinden paketler(`apt`) aracılığıyla da kurulabilir. Bu durum Ubuntu, Kali Linux ve Linux Mint gibi Debian tabanlı diğer dağıtımlar için de geçerlidir.


> [!warning]
> Üçüncü taraflarca derlenen sürümler resmi olmayan olarak kabul edilir ve PHP projesi tarafından doğrudan desteklenmez. Bu resmi olmayan derlemelerde karşılaşılan hatalar, [» resmi indirme alanındaki](https://www.php.net/downloads.php) derlemeler kullanılarak **tekrarlanamıyorsa(reproduce a bug)**, söz konusu resmi olmayan derlemelerin sağlayıcısına bildirilmelidir.
> 
> (Yazılım dünyasında "**reproduce a bug**" ifadesi, **bir hatayı tekrar tekrar oluşturabilmek, hatanın tekrarlanabilir olması** anlamına gelir.)

Paketler `apt` veya `aptitude` komutlarından biri kullanılarak kurulabilir. Bu kılavuz(*manual*) sayfası bu iki komutu **dönüşümlü olarak** kullanmaktadır.
#### 3.2.1.1. APT Kullanımı

Öncelikle, Apache 2 ile entegrasyon için `libapache-mod-php` veya PEAR için `php-pear` gibi ilgili başka paketlerin de istenilebileceğini unutmayın.

İkinci olarak, bir paket kurmadan önce paket listesinin güncel olduğundan emin olmak akıllıca olacaktır. Bu işlem genellikle `apt update` komutu çalıştırılarak yapılır.

**Örnek #1 Apache 2 Kullanarak Debian’da PHP Kurulumu**

```
# apt install php-common libapache2-mod-php php-cli
```

APT, Apache 2 için PHP modülünü ve tüm bağımlılıklarını otomatik olarak kuracak, ardından etkinleştirecektir.  Değişikliklerin etkili olması için Apache'nin yeniden başlatılması gerekir. Örneğin:

**Örnek #2 PHP kurulduktan sonra Apache'yi durdurma ve başlatma**

```
# /etc/init.d/apache2 stop
# /etc/init.d/apache2 start
```
#### 3.2.1.2. Yapılandırma Üzerinde Daha İyi Kontrol

Önceki bölümde PHP yalnızca çekirdek modülleriyle kurulmuştu. Büyük olasılıkla **MySQL**, **cURL**, **GD** gibi ek modüllere ihtiyaç duyacaksınız. Bu modüller de `apt` komutu kullanılarak kurulabilir.

**Örnek #3 Ek PHP paketlerini listeleme yöntemleri**

```
# apt-cache search php
# apt search php | grep -i mysql
# aptitude search php
```

Paket listesi; `php-cgi`, `php-cli` ve `php-dev` gibi temel PHP bileşenlerinin yanı sıra çok sayıda PHP eklentisini de içerir. Bir eklenti kurulduğunda, gerekli bağımlılıkları karşılamak için ek paketler otomatik olarak kurulacaktır.

**Örnek #4 PHP'yi MySQL ve cURL ile kurma**

```
# apt install php-mysql php-curl
```

APT, `/etc/php/7.4/php.ini`, `/etc/php/7.4/conf.d/*.ini` gibi ilgili `php.ini` dosyalarına gerekli ayarları otomatik olarak ekler. Ayrıca, eklentiye bağlı olarak `extension=foo.so` benzeri satırlar da eklenir. Ancak bu değişikliklerin etkili olabilmesi için web sunucusunun (örneğin; Apache) yeniden başlatılması gerekir.
#### 3.2.1.3. Yaygın Problemler

PHP betikleri web sunucusu tarafından işlenmiyorsa, PHP'nin büyük olasılıkla web sunucusunun yapılandırma dosyasına eklenmediği anlamına gelir; Debian'da bu dosya `/etc/apache2/apache2.conf` veya benzeri bir dosya olabilir. Daha fazla ayrıntı için Debian kılavuzuna(*manual*) bakın.

Eğer bir eklenti kurulmuş gibi görünmesine rağmen fonksiyonları(yani, o eklentinin fonksiyonları) "*undefined*" hatası veriyorsa, uygun `.ini` dosyasının yüklendiğinden ve/veya kurulumdan sonra web sunucusunun yeniden başlatıldığından emin olun.(Web sunucunu yeniden başlatma: `sudo systemctl apache2`)

### 3.2.2. DNF Kullanan GNU/Linux Dağıtımlarında Paketlerden Kurulum

PHP kaynak kodundan kurulabildiği gibi, Red Hat Enterprise Linux, OpenSUSE, Fedora, CentOS, Rocky Linux ve Oracle Enterprise Linux gibi **DNF** kullanan sistemlerde paketler aracılığıyla da kurulabilir.


> [!warning]
> Üçüncü taraflarca derlenen sürümler resmi olmayan olarak kabul edilir ve PHP projesi tarafından doğrudan desteklenmez. Bu resmi olmayan derlemelerde karşılaşılan hatalar, [» resmi indirme alanındaki](https://www.php.net/downloads.php) derlemeler kullanılarak **tekrarlanamıyorsa(reproduce a bug)**, söz konusu resmi olmayan derlemelerin sağlayıcısına bildirilmelidir.
> 
> (Yazılım dünyasında "**reproduce a bug**" ifadesi, **bir hatayı tekrar tekrar oluşturabilmek, hatanın tekrarlanabilir olması** anlamına gelir.)

Paketler dnf komutu kullanılarak kurulabilir.  
#### 3.2.2.1. Paketlerin Kurulumu

Birinci olarak, [» PEAR](https://pear.php.net/) için `php-pear` veya [» MySQL eklentisi](https://www.php.net/manual/en/book.mysqlnd.php) için `php-mysqlnd` gibi ilgili diğer paketlere de ihtiyaç duyulabileceğini unutmayın.

> [!tip]
> #### PEAR nedir?
> **PEAR (PHP Extension and Application Repository)**, PHP için geliştirilmiş hazır kod kütüphanelerinin bulunduğu bir **merkezi depodur.**
> Yani başkalarının yazdığı, tekrar tekrar kullanılabilir PHP kodlarının toplandığı bir **kütüphane arşividir.**
> **Basit bir benzetmeyle:**
> PEAR'ı bir **alet çantası** gibi düşünebilirsiniz. Her işi sıfırdan kendiniz yapmak yerine, çantadan ihtiyacınız olan aleti çıkarıp kullanırsınız.
> **Örneğin PEAR ile:**
> - E-posta göndermek
> - PDF oluşturmak
> - Veritabanı işlemleri yapmak
> - XML işlemek
> 
> gibi yaygın görevler için hazır kütüphaneler bulabilir ve bunları projenize kolayca ekleyebilirsiniz.
> **Önemli bir not:** PEAR günümüzde artık çok aktif kullanılan bir araç değildir. Yerini büyük ölçüde **Composer** adlı daha modern bir paket yöneticisi almıştır. Composer, günümüz PHP projelerinde PEAR'ın yaptığı işi çok daha gelişmiş bir şekilde yapmaktadır.

İkinci olarak, bir paket kurmadan önce paket listesinin güncel olduğundan emin olmak akıllıca olacaktır. Bu işlem genellikle `dnf update` komutu çalıştırılarak yapılır.

**Örnek #1 DNF Kurulum Örneği**

```
# dnf install php php-common
```

DNF, web sunucusu için PHP yapılandırmasını otomatik olarak kuracaktır; ancak değişikliklerin etkili olması için sunucunun yeniden başlatılması gerekebilir. Örneğin:

**Örnek #2 PHP kurulduktan sonra Apache'yi yeniden başlatma**

```
# sudo systemctl restart httpd
```
#### 3.2.2.1. Yapılandırma Üzerinde Daha İyi Kontrol

Önceki bölümde PHP yalnızca çekirdek modülleriyle kurulmuştu. Büyük olasılıkla **MySQL**, **cURL**, **GD** gibi ek modüllere ihtiyaç duyacaksınız. Bunlar da `dnf` komutu kullanılarak kurulabilir.

**Örnek #3 Ek PHP paketlerini listeleme yöntemleri**

```
# dnf search php
```

Paket listesi; `php-cli`, `php-fpm` ve `php-devel` gibi temel PHP bileşenlerinin yanı sıra birçok PHP eklentisini de içerecektir. Eklentiler kurulduğunda, bu paketlerin bağımlılıklarını karşılamak için gerekli ek paketler otomatik olarak kurulacaktır.

**Örnek #4 PHP'yi MySQL ve GD ile kurma**

```
# dnf install php-mysqlnd php-gd
```

DNF, `/etc/php/8.3/php.ini`, `/etc/php/8.3/conf.d/*.ini` gibi farklı `php.ini` ilgili dosyalara otomatik olarak uygun satırları ekleyecek ve eklentiye bağlı olarak `extension=foo.so` benzeri girişler ekleyecektir. Ancak bu değişikliklerin geçerli olması için web sunucusunun (Apache gibi) yeniden başlatılması gerekmektedir.

> [!tip]
> Bir PHP eklentisi kurduğunuzda, DNF sadece dosyaları bilgisayara kopyalamakla kalmaz; aynı zamanda PHP'nin bu eklentiyi **tanıyıp kullanabilmesi** için gerekli ayar dosyalarını da **otomatik olarak düzenler.**
> #### İki temel kavram:
> ##### 1. php.ini ve .ini dosyaları nedir?
> Bunlar PHP'nin **ayar dosyalarıdır.** PHP nasıl davranacağını, hangi eklentileri kullanacağını bu dosyalara bakarak öğrenir. Örneğin:
> ```ini
> /etc/php/8.3/php.ini          → Ana ayar dosyası
> /etc/php/8.3/conf.d/*.ini     → Eklentilere ait ayrı ayar dosyaları
> ```
> ##### 2. `extension=foo.so` ne demektir?
> Bu, PHP'ye **"bu eklentiyi yükle ve kullan"** diyen bir satırdır. Örneğin GD eklentisi için:
> ```
> extension=gd.so
> ```
> Bu satır olmadan PHP, GD eklentisinin kurulu olduğunu bilemez.
> **Kısacası:** Siz sadece `dnf install php-gd` komutunu çalıştırırsınız; DNF hem eklentiyi kurar hem de `extension=gd.so` gibi gerekli satırı ayar dosyasına **otomatik olarak yazar.** Bunu elle yapmanıza gerek kalmaz.

### 3.2.3. OpenBSD'de Paketlerden veya Port'lardan Kurulum

#### 3.2.3.1. İkili(Binary) Paketlerin Kullanımı

PHP'yi OpenBSD'ye kurmak için ikili(*binary*) paketleri kullanmak önerilen ve en basit yöntemdir. Çekirdek paket, ek modüllerden ayrılmıştır; her biri diğerinden bağımsız olarak kurulabilir ve kaldırılabilir. İhtiyacınız olan dosyaları OpenBSD CD'nizde veya FTP sitesinde bulabilirsiniz.

Kurmanız gereken ana paket `php` paketidir. Bu paket temel motoru (ayrıca **fpm**, **gettext** ve **iconv** eklentilerini) içerir ve aralarından seçim yapabileceğiniz birkaç farklı sürüm halinde sunulabilir.

> [!tip]
> PHP'yi kurmak için öncelikle `php` adlı **ana paketi** kurmanız gerekir. Bu paket:
> - PHP'nin **temel çalışma motorunu** içerir
> - Motorun yanında **fpm, gettext ve iconv** adlı üç temel bileşeni de beraberinde getirir
> - **Birden fazla sürümü** mevcut olabilir (örneğin php8.1, php8.2, php8.3 gibi), hangisini kuracağınızı siz seçersiniz
> 
> **Her bileşen ne işe yarar?**
> 
> |Bileşen|Ne işe yarar?|
> |---|---|
> |**fpm**|PHP'yi nginx gibi sunucularla çalıştırmak için kullanılır|
> |**gettext**|Çok dilli uygulama geliştirmek için çeviri desteği sağlar|
> |**iconv**|Farklı karakter kodlamaları arasında dönüşüm yapar (örneğin UTF-8'e çevirme)|

Ardından, `php-mysqli` veya `php-imap` gibi modül paketlerine göz atın. Bu modülleri `php.ini` dosyanızda etkinleştirmek veya devre dışı bırakmak için `phpxs` komutunu kullanmanız gerekir.

**Örnek #1 OpenBSD Paket Kurulum Örneği**

```
# pkg_add php
# pkg_add php-apache
# pkg_add php-mysqli
  (install the PEAR libraries)
# pkg_add pear

Follow the instructions shown with each package!

  (to remove packages)
# pkg_delete php
# pkg_delete php-apache
# pkg_delete php-mysqli
# pkg_delete pear
```

OpenBSD üzerindeki ikili (binary) paketler hakkında daha fazla bilgi için » [packages(7)](https://man.openbsd.org/packages.7) kılavuz sayfasını okuyun.

#### 3.2.3.2. Portlar ile Kurulum

PHP'yi [ports tree](https://www.google.com/search?q=https://www.openbsd.org/ports.html) (port ağacı) kullanarak kaynak koddan da derleyebilirsiniz. Ancak bu yöntem sadece OpenBSD sistemine aşina olan kullanıcılar için önerilir. PHP portu, çekirdek ve eklentiler olarak ayrılmıştır. Eklentiler, desteklenen tüm PHP modülleri için alt paketler(*sub-packages*) oluşturur. Bu modüllerin bazılarını oluşturmak istemiyorsanız no_* FLAVOR seçeneğini kullanın. Örneğin imap modülünü derlemeyi atlamak için FLAVOR'ı `no_imap` olarak ayarlayın.
#### 3.2.3.3. Yaygın Sorunlar

+ Apache ve Nginx artık OpenBSD'de varsayılan sunucu değildir; ancak her ikisi de port'larda ve paketlerde kolaylıkla bulunabilir. Yeni varsayılan sunucu 'httpd' olarak adlandırılmaktadır.
+ httpd'nin varsayılan kurulumu [» chroot(2) jail](https://man.openbsd.org/chroot) içinde çalışır; bu durum PHP betiklerinin yalnızca `/var/www` altındaki dosyalara erişimini kısıtlayacaktır. Bu nedenle PHP oturum dosyalarının saklanması için bir `/var/www/tmp` dizini oluşturmanız ya da alternatif bir oturum arka ucu(*backend*) kullanmanız gerekecektir.

> [!tip]
> #### Backend Nedir?
> **"Arka uç (backend)"** burada oturum verilerinin **nerede ve nasıl saklanacağını** belirleyen sistemi ifade etmektedir.
> PHP'de oturum (session) verileri varsayılan olarak **dosya sistemine** kaydedilir. Ancak bu her zaman mümkün veya uygun olmayabilir. Bu durumda alternatif arka uçlar kullanılabilir:
> 
> |Arka Uç|Ne işe yarar?|
> |---|---|
> |**Dosya sistemi**|Oturum verileri `/tmp` gibi bir dizine dosya olarak kaydedilir (varsayılan)|
> |**Veritabanı**|Oturum verileri MySQL gibi bir veritabanına kaydedilir|
> |**Redis**|Oturum verileri Redis adlı hızlı bellek içi veri deposuna kaydedilir|
> |**Memcached**|Oturum verileri Memcached adlı önbellek sistemine kaydedilir|

Buna ek olarak, veritabanı soketlerinin jail içine yerleştirilmesi veya localhost arayüzünü dinlemesi gerekmektedir. Ağ işlevlerini kullanıyorsanız `/etc/resolv.conf` ve `/etc/services` gibi `/etc` dizinindeki bazı dosyaların `/var/www/etc` dizinine taşınması gerekecektir. OpenBSD PEAR paketi doğru chroot dizinlerine otomatik olarak kurulur. 

[GD Graphics Library](http://www.libgd.org/) eklentisi için OpenBSD paketi, X.Org’un kurulu olmasını gerektirir. Eğer temel kurulum sırasında `xbase.tgz` dosya seti eklenmediyse, bu bileşen sonradan da kurulabilir (bkz. [» OpenBSD FAQ#4](https://www.openbsd.org/faq/faq4.html#FilesNeeded)).
### 3.2.4. Unix ve macOS Sistemlerde Kaynak Koddan Kurulum

Derleme (compiling) işlemi için gereken önkoşul yazılımlar şunlardır:

- [GNU **make**](https://www.gnu.org/software/make/make.html)
- Bir C derleyicisi (PHP 8.0.0 itibarıyla C99 uyumluluğu gereklidir; PHP 8.4.0 itibarıyla ise C11 uyumluluğu gereklidir)
- Bir web sunucusu
- Modüle özel bileşenler (örneğin GD, PDF kütüphaneleri vb.)

Git kaynak kodundan doğrudan derleme(*building*) yaparken veya özel değişiklikler sonrasında derleme gerçekleştirirken, aşağıdaki ek araçlara da ihtiyaç duyulabilir:

- **autoconf:** (PHP yapılandırma dosyalarını oluşturmak için kullanılır)
    - **PHP 7.3 ve sonrası:** 2.68+
    - **PHP 7.2:** 2.64+
    - **PHP 7.1 ve öncesi:** 2.59+
- **re2c:** (PHP'nin sözcük analizcisini -lexer- oluşturmak için kullanılır)
    - **PHP 8.3 ve sonrası:** 1.0.3+
    - **PHP 8.2 ve öncesi:** 0.13.4+
- **bison:** (PHP'nin ayrıştırıcısını -parser- oluşturmak için kullanılır)
    - **PHP 7.4 ve sonrası:** 3.0.0+
    - **PHP 7.3 ve öncesi:** 2.4+ (Bison 3.x dahil)

Kaynak koddan PHP derlemek için daha ayrıntılı adımlar, kaynak paketinin içindeki [`README.md`](https://github.com/php/php-src/blob/master/README.md) dosyasında bulabilirsiniz.

PHP’nin ilk kurulum ve yapılandırma süreci, `configure` betiğinin komut satırı seçenekleri kullanılarak kontrol edilir. Mevcut seçeneklerin kısa açıklamalarıyla birlikte listesi `./configure --help` komutu çalıştırılarak görüntülenebilir. Bu kılavuz(*manual*), farklı seçenekleri ayrı ayrı belgelemektedir. [Temel seçenekler ekte(*appendix*) bulunabilirken](https://www.php.net/manual/en/configure.about.php), farklı eklentilere özgü seçenekler referans sayfalarında açıklanmaktadır.

Yapılandırma betiği çalıştırıldıktan sonra PHP, `make` komutu kullanılarak derlenebilir. Derleme(*build*) sırasında karşılaşılan sorunların nasıl çözüleceğine dair daha fazla bilgi için [Sıkça Sorulan Sorular'ın (FAQ) Kurulum bölümüne](https://www.php.net/manual/en/faq.installation.php) bakabilirsiniz.


> [!NOTE]
> Bazı Unix sistemleri (OpenBSD ve SELinux gibi), güvenlik nedeniyle sayfaların hem yazılabilir hem de çalıştırılabilir olarak eşlenmesine izin vermeyebilir; buna [» PaX MPROTECT](https://en.wikibooks.org/wiki/Grsecurity/Appendix/Grsecurity_and_PaX_Configuration_Options#Restrict_mprotect()) veya [» W^X ihlal koruması](https://en.wikipedia.org/wiki/W%5EX) adı verilmektedir. Bu tür bellek eşlemesi PCRE'nin JIT desteği için gereklidir; bu nedenle ya PHP, [PCRE'nin JIT desteği](https://www.php.net/manual/en/pcre.installation.php) olmadan derlenmelidir ya da ikili dosya sistem tarafından sağlanan herhangi bir yöntemle beyaz listeye eklenmelidir.


> [!TIP]
> #### "sayfa" ne demek?
> Burada "sayfa" bilgisayarın **RAM belleğinin** küçük bloklarını ifade eder. İşletim sistemi belleği bu sayfalar halinde yönetir.
> 
> ---
> **"Yazılabilir" ve "çalıştırılabilir" ne demek?**
> + Her bellek sayfasının izinleri vardır, tıpkı dosya izinleri gibi:
> + **Çalıştırılabilir (executable):** O bellek bölgesindeki kod çalıştırılabilir
> ---
> **Peki neden ikisi aynı anda tehlikeli?**
> Bir bellek bölgesi hem yazılabilir hem de çalıştırılabilirse, kötü niyetli bir saldırgan oraya **zararlı kod yazıp hemen çalıştırabilir.** Bu çok ciddi bir güvenlik açığıdır.
> ---
> **PaX MPROTECT ve W^X ne yapar?**
> Bu güvenlik mekanizmaları şunu söyler:
> > "Bir bellek bölgesi ya yazılabilir **ya da** çalıştırılabilir olabilir, **ikisi birden olamaz!**"
> 
> W^X ifadesindeki **^** işareti matematikteki **"ya da"** anlamına gelir.
> 
> ---
> **PHP ile ilgisi nedir?**
> PCRE'nin JIT özelliği, hız kazanmak için kodu bellekte hem yazıp hem de hemen çalıştırması gerektiğinden, bu güvenlik mekanizmalarıyla **çakışır** ve çalışamaz.

> [!NOTE]
> Android araç zinciri(*toolchain*) ile ARM için çapraz derleme (cross-compiling) şu anda desteklenmemektedir.
### 3.2.5. CGI ve Komut Satırı Kurulumları

Varsayılan olarak PHP, hem CLI(komut satırı) hem de CGI programı olarak derlenir ve CGI işleme(*CGI processing*) için kullanılabilir. PHP'nin modül desteğine sahip olduğu bir web sunucusu çalıştırıyorsanız, performans nedeniyle genellikle o çözümü tercih etmelisiniz. Ancak CGI sürümü, kullanıcıların farklı PHP destekli sayfaları farklı kullanıcı kimlikleri altında çalıştırmasına olanak tanır.

> [!tip]
> **CGI (Common Gateway Interface)**, web sunucularının (Apache, Nginx, vb.) harici programlarla (PHP, Python, Perl, vb.) iletişim kurmasını sağlayan standart bir protokoldür.
> Kısacası; web sunucusunun tek başına yapamadığı "dinamik içerik üretme" işini, başka bir programa havale etme yöntemidir.
> #### CGI Nasıl Çalışır?
> Süreç genellikle şu adımları izler:
> 1. **İstek:** Bir kullanıcı tarayıcısına `index.php` yazdığında, web sunucusu bu dosyanın statik bir HTML olmadığını anlar.
> 2. **Yönlendirme:** Sunucu, bu dosyayı işlemek üzere CGI arayüzü üzerinden PHP yorumlayıcısını çağırır.
> 3. **İşleme:** PHP kodu çalıştırılır, veritabanına bağlanır ve sonuç olarak bir HTML çıktısı üretir.
> 4. **Yanıt:** Web sunucusu bu HTML çıktısını alır ve kullanıcıya geri gönderir.
> #### CGI ve Modern Alternatifleri
> + **Klasik CGI:** Her istek geldiğinde yeni bir program süreci başlatır. 1000 kişi aynı anda girerse 1000 tane PHP süreci açılır. Bu, sunucuyu çok yorar ve yavaştır.
> + **FastCGI:** Süreçleri açık tutar. Bir istek bittiğinde program kapanmaz, sıradaki isteği bekler. Çok daha performanslıdır.
> + **PHP-FPM:** Modern sistemlerde (özellikle Nginx ile) en çok kullanılan yöntemdir. PHP için özelleşmiş bir FastCGI yöneticisidir.


> [!WARNING]
> CGI modunda yayınlanan(*deployed*) bir sunucu, çeşitli olası güvenlik açıklarına karşı savunmasızdır. Bu tür saldırılardan kendinizi nasıl koruyacağınızı öğrenmek için lütfen [CGI güvenliği](https://www.php.net/manual/en/security.cgi-bin.php) bölümünü okuyun.
#### 3.2.5.1. Test Etme

PHP'yi kaynak koddan bir CGI programı olarak derlediyseniz, derlemenizi(*build*) `make test` komutunu çalıştırarak test edebilirsiniz. Derlemenizi test etmek her zaman iyi bir fikirdir. Bu sayede, kullandığınız platformda PHP ile ilgili olası sorunları erken aşamada tespit edebilir ve ileride daha büyük problemlerle uğraşmak zorunda kalmazsınız.
#### 3.2.5.1. Değişkenleri Kullanma

[Sunucu tarafından sağlanan bazı ortam değişkenleri](https://www.php.net/manual/en/reserved.variables.server.php), mevcut [CGI/1.1 standardında](https://datatracker.ietf.org/doc/html/rfc3875) tanımlı değildir. Bu standartta yalnızca şu değişkenler tanımlanmıştır:

AUTH_TYPE, CONTENT_LENGTH, CONTENT_TYPE, GATEWAY_INTERFACE, PATH_INFO, PATH_TRANSLATED, QUERY_STRING, REMOTE_ADDR, REMOTE_HOST, REMOTE_IDENT, REMOTE_USER, REQUEST_METHOD, SCRIPT_NAME, SERVER_NAME, SERVER_PORT, SERVER_PROTOCOL ve SERVER_SOFTWARE.

Bunların dışındaki tüm değişkenler (örneğin bazı Apache veya Nginx'e özel değişkenler) **"vendor extensions"** (üretici eklentileri) olarak kabul edilmelidir.

> [!TIP]
> #### `CGI/1.1,` nedir?
> CGI/1.1, web sunucuları ile CGI programları arasındaki iletişimi düzenleyen bir **standarttır.** Bu standartta hangi ortam değişkenlerinin bulunması **zorunlu** olduğu belirlenmiştir.
> #### Ortam değişkeni ne demek?
> Ortam değişkenleri, web sunucusunun PHP'ye otomatik olarak ilettiği bilgilerdir. Örneğin:
> 
> |Değişken|Ne bilgi taşır?|
> |---|---|
> |`REMOTE_ADDR`|Ziyaretçinin IP adresi|
> |`REQUEST_METHOD`|İsteğin GET mi POST mu olduğu|
> |`QUERY_STRING`|URL'deki `?` sonrası parametreler|
> |`SERVER_NAME`|Sunucunun adı|
> 
> CGI/1.1 standardı yalnızca **belirli değişkenleri** zorunlu olarak tanımlamıştır. Bunların dışında kalan değişkenler ise her sunucunun kendi isteğine göre eklediği **ekstra değişkenlerdir** ve standartta resmi olarak yer almaz.
> **Kısacası:** Standartta tanımlı değişkenler her sunucuda **kesinlikle bulunur**, ancak bunların dışındakiler sunucudan sunucuya **farklılık gösterebilir** ve her sunucuda bulunacağı garanti değildir.
### 3.2.6. Unix Sistemlerde Apache 2.x



https://www.php.net/manual/en/install.unix.apache2.php