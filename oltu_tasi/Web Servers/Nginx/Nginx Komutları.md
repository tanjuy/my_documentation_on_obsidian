#nginx 

#### Nginx Yardım:
```shell
$ sudo nginx -h
```

**Çıktı:**
```shell
nginx version: nginx/1.27.2
Usage: nginx [-?hvVtTq] [-s signal] [-p prefix]
             [-e filename] [-c filename] [-g directives]

Options:
  -?,-h         : this help
  -v            : show version and exit
  -V            : show version and configure options then exit
  -t            : test configuration and exit
  -T            : test configuration, dump it and exit
  -q            : suppress non-error messages during configuration testing
  -s signal     : send signal to a master process: stop, quit, reopen, reload
  -p prefix     : set prefix path (default: /usr/local/nginx/)
  -e filename   : set error log file (default: /var/log/nginx/error.log)
  -c filename   : set configuration file (default: /etc/nginx/nginx.conf)
  -g directives : set global directives out of configuration file
```


#### `nginx.conf` syntax kontrolü:
+ `nginx -t`, Nginx’in yapılandırma dosyalarını test etmek için kullanılan bir komuttur.
+ Bu komut, yapılandırma dosyasında yapılan değişikliklerin doğru olup olmadığını kontrol eder ve herhangi bir hata olup olmadığını bildirir.
+ Özellikle yapılandırmada değişiklik yaptıktan sonra `reload` veya `restart` işlemi yapmadan önce, değişikliklerin doğru ve Nginx tarafından kabul edilebilir olduğundan emin olmak için `nginx -t` komutu kullanılır.

```bash
$ sudo nginx -t 
```
> **Explanation:**
> + Yapılandırmada bir hata varsa, Nginx hata mesajlarını komut satırına yazarak dosyada hangi bölümde hata olduğunu gösterir.
> + Örneğin, bir dosya yolu eksikse veya bir direktif hatalıysa, bunu açıkça belirtir.

**Başarılı bir test:**
```shell
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

**Hatalı bir test:**
```shell
nginx: [emerg] invalid parameter "on" in /etc/nginx/nginx.conf:5
nginx: configuration file /etc/nginx/nginx.conf test failed
```

**Özetle:**
+ `nginx -t` komutu, yapılandırma değişikliklerini test etmek ve hataları önceden görmek için oldukça yararlıdır.
+ Bu komutu kullanarak, Nginx’in düzgün çalışmamasına neden olacak hataları önceden bulup düzeltebilirsiniz.
#### Reload vs Restart:
+ Nginx’te `reload` ve `restart` komutları, yapılandırmayı güncellemek için kullanılan iki farklı işlemdir, ancak bu işlemler sunucuya farklı şekillerde etki eder.

```bash
$ sudo nginx -s reload
```
> **Explanation:**
> + nginx servisini yeniden başlatıyoruz. `nginx.conf` dosyası düzenlendiğinde gerek duyulan komutur.

```
$ sudo systemctl restart nginx.service
```
> **Explanation:**
> + Yukarıdaki komut ile aynı işi yapar.

##### 1.Reload:
+ `nginx -s reload` veya `sudo systemctl reload nginx.service`
+ `reload` komutu, yapılandırma dosyalarını yeniden yüklemek için kullanılır.
+ Nginx işlemlerini durdurmadan ve mevcut bağlantıları kesmeden yeni yapılandırmayı devreye sokar.
+ Komut çalıştırıldığında, Nginx önce yeni yapılandırma dosyasını doğrular. Eğer geçerliyse, Nginx eski işlemine yeni yapılandırmayla devam eder.
+ *Mevcut bağlantılarda kesinti olmadan yeni gelen istekler yeni yapılandırmaya göre işlenir.*
+ **Özetle**, `reload` yapılandırmayı güncellerken hizmette bir kesintiye neden olmaz.
##### 2.Restart:
+ `nginx -s stop && nginx` veya `sudo nginx restart nginx.service`
+ `restart` komutu, Nginx servisinin tamamen yeniden başlatılması anlamına gelir.
+ Tüm Nginx işlemlerini sonlandırır ve servisi baştan başlatır.
+ Mevcut bağlantılar kesilir ve yeni istekler ancak servis yeniden başladığında işlenmeye devam eder.
+ **Özetle:** `restart` komutu, yeni yapılandırmanın yanı sıra tüm işlemleri de sıfırlar ve tüm bağlantıları yeniler.
##### Hangisi Ne Zaman Kullanılır?
+ **Yapılandırma Güncellemeleri**: Yapılandırmada değişiklik yaptıysanız ve mevcut bağlantıları etkilemeden yeni ayarları devreye almak istiyorsanız `reload` komutunu tercih edin.
+ **Büyük Değişiklikler ve Sorun Giderme**: Nginx’in tamamen durdurulması ve baştan başlatılması gerekiyorsa (örneğin, modül güncellemesi, yeni bir Nginx sürümüne geçiş veya sorun giderme durumlarında) `restart` kullanmak daha uygun olacaktır.

> [!WARNING]
> + `nginx -s reload` komut nginx SSL sertifikaları yeniledikten sonra bu komut düzgün çalışmamaktır.
> + Eğer SSL sertifikası yenilemesi yaptıktan sonra SSL sertifikların tekrardan yüklenmesi için nginx servisini başlatmak için `systemctl restart nginx.service` komutunu kullanınız.


> [!TIP]
> + nginx servisini ayakta kalmasını sağlamak için;
> 1. `nginx -t` komutu ile config dosyasını test ediyoruz.
> 2. `nginx -s reload` komut ile config dosyasını yeniden yüklüyoruz.


#### Nginx logs:
+ Nginx'te log (kayıt) dosyaları, sunucunun faaliyetlerini izlemek ve hataları kaydetmek için kullanılır.
+ Bu loglar, sunucunun nasıl çalıştığını anlamak, hata ayıklamak ve performansı optimize etmek için oldukça faydalıdır.
+ Nginx iki temel türde log dosyası oluşturur: **access log** (erişim kaydı) ve **error log** (hata kaydı).

##### 1.Access Log:
+ **Access log**, sunucuya yapılan her isteği kaydeder. Bu kayıt, sunucuya kimlerin, hangi zamanlarda, hangi sayfalara eriştiğini görmek için kullanılır.
+ **İçerik**: IP adresi, istek tarihi, istek yöntemi (GET, POST), istenen URL, HTTP durumu (200, 404, 500 gibi), yanıt süresi, kullanıcı aracısı (user agent) gibi bilgiler içerir.
+ **Varsayılan Dosya**: Access log genellikle `/var/log/nginx/access.log` dosyasında tutulur.

**nginx.config**
```nginx
http {
    access_log /var/log/nginx/access.log;
    ...
}
```

**access.log izleme**
```shell
$ tail -f /var/log/nginx/access.log
```

##### 2.Error Log:
+ **Error log**, Nginx sunucusunda oluşan hataları kaydeder. Sunucu başlatılamadığında, yapılandırma dosyalarında hata olduğunda veya isteklerin işlenmesinde sorun yaşandığında error log devreye girer.
+ **İçerik**: Hata seviyesi (kritik, uyarı, hata), hata türü, hata mesajı ve hata kaynağı gibi bilgiler içerir.
+ **Varsayılan Dosya**: Error log genellikle `/var/log/nginx/error.log` dosyasında bulunur.

**nginx.conf**
```nginx
http {
    error_log /var/log/nginx/error.log;
    ...
}
```

###### Error Log Seviyeleri:

- **debug**: En ayrıntılı kayıt seviyesidir. Hata ayıklama için gereklidir.
- **info**: Bilgilendirici mesajları içerir.
- **notice**: Önemli fakat müdahale gerektirmeyen olayları içerir.
- **warn**: Uyarı mesajlarını içerir.
- **error**: Hata mesajlarını içerir.
- **crit**: Kritik hataları içerir; müdahale edilmesi gereken hatalardır.

##### Logları Yapılandırma:
+ Logların tutulacağı dosya yolları ve log seviyeleri, Nginx yapılandırma dosyalarında (`nginx.conf`) belirtilir.
+ Her `server` bloğu veya `location` bloğu için ayrı log dosyaları da tanımlanabilir.

```nginx
error_log /var/log/nginx/custom_error.log warn;
access_log /var/log/nginx/custom_access.log;
```


> [!NOTE]
> + `tail -f /var/log/nginx/*` komut ile mevcut dizindeki tüm nginx ile ilgili log'ları ekran basar.
