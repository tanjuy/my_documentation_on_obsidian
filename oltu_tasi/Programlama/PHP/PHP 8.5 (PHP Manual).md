
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