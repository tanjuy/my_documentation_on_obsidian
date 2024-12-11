#linux_commands
### 1. curl
###### 1.1`-I` parametresi:
```bash
$ curl -I http://192.168.1.125/assets/images/clients/c3.png
```
> **Explanation:**

###### 1.2. `-X` parametresi:
```shell
$ curl -X GET www.example.com
```
> **Explanation:**

###### 1.3. ISO indir

```shell
$  curl https://mirror.pseudoform.org/iso/2024.12.01/archlinux-2024.12.01-x86_64.iso -o archlinux-2024.12.01-x86_64.iso
```
> **Explanation:**
> + `https://mirror.pseudoform.org/iso/2024.12.01/archlinux-2024.12.01-x86_64.iso` sitesinden `-o` parametresi ile `archlinux-2024.12.01-x86_64.iso` adında indiriyoruz.
> + `-o` parametresini uzun yazılışı: `--output` 

### 2. update-alternative
```shell
$ sudo update-alternative --config python
```
> **Explanation:**  ==ubuntu==, ==rocky linux==
> python versiyon arasında geçiş yapmamıza izin veriyor.

### 3. openssl
```shell
$ openssl rand -base64 10
```

### 4. shutdown
###### Örnek 1: +dakika
```shell
$ shutdown +10 "10 dakika sonra makine kapanacak"
```
> **Explanation:**
> Makineye uzaktan veya yerel(local) olarak bağlı olan terminal ekranlarına mesaj gönderiyoruz ve +10 anlamı, mesaj da söylendiği gibi 10 dakika sonra kapanacağıdır.

###### Örnek 2: -k parametresi (UYARI)
```shell
$ shutdown -k +5
```
> **Explanation:**
> `-k` parametresi makinenin kapatılmayacağı veya yeniden başlatılmayacağı ama bulunduğu zamandan 5 dakika sonra kapanacağını söylemektedir. Bir UYARI
> Uyarı mesaj tüm terminallere ulaşır.

```shell
$ shutdown -k 22:30:25
```
> **Explanation:**
> Yukarıdaki komut gibi çalışır ama burada belirlen zaman verilmiştir. Uyarı mesajı tüm terminaller 22:30:24 sadece kapanacağı uyarısı verir.

### 5. echo
```shell
$ echo "Linux is Awesome"
```
> **Explanation:**

### 6. find
###### Örnek 1: Temel Kullanımı
```shell
$ find /usr -name words
```
> **Explanation:**


### 7. grep
###### Örnek 1: 
```shell
$ cat /usr/share/dict/words | grep "Ankara"
```
> **Explanation:**

###### Örnek 1.1: Alternatif Kullanım
```shell
$ grep "Ankara" /usr/share/dict/words
```
> **Explanation:**

###### Örnek 2: -i parametresi
```shell
$ grep -i "ankara" /usr/share/dict/words
```
> **Explanation:**
###### Örnek 3: -v parametresi
```shell
$ grep -v "ankara" /usr/share/dict/words
```
> **Explanation:**

###### Örnek 4: -n parametresi
```shell
$ grep -n "Istanbul" /usr/share/dict/words
```

### 8. who
```
$ who
```
> **Explanation:**
> + Sistemde oturum açmış kullanıcılar hakkında bilgi almak için kullanılır.
> + Komut, hangi kullanıcıların sistemde aktif olduğunu, hangi terminal oturumlarında bulunduklarını ve oturum açma zamanlarını gösterir.
> +  Kullanıcı adı  - Terminal - Oturum açma zamanı - Kullanıcının bağlı olduğu IP adresi
### 9. tty
```bash
$ tty
```
> **Explanation:**

### 10. trash-cli
###### Komutun Yüklenmesi
```bash
$ sudo apt install trash-cli
```

###### Dosyayı Çöpe Taşıma:
```bash
$ trash-put [dosya_yolu]
```
> **Explanation:**
> genellikle dosyaları **`~/.local/share/Trash`** klasörüne taşır.


### 11. useradd
###### 1. Temel Kullanımı:
```shell
$ useradd -m -d /home/linus -s /usr/bin/bash -c "Linus Torvalds" linus
```
> **Explanation:**
> + `-m` veya `--create-home`**:** Eğer yok ise kullanıcın `home` dizini oluştur ve ayrıca eğer `-k` parametresinde kullanırsa `skeleton dizini` içerisindeki dosyalar ve klasörler oluşturulmuş olan ev dizinine kopyalanacaktır
> + `-d` veya `--home-dir`**:**  Bu parametre ile istediğiniz dizini kullanıcı için ev dizini yapılır. Burada `/home/linus` dizini home dizin yapılıyor. Eğer bu dizin yok ise oluşturulur.
> + `-s` veya `--shell`**:** Kullanıcın giriş kabuğun adı. Burada `bash` shell'in dizini verilmiş. Ayrıca eğer belirtilmez ise `/etc/default/useradd` dosyasında `SHELL` olarak verilmiş kabuk varsayılan olarak kabul edilecektir.
> + `-c` veya `--comment` **:** Kullanıcının neden oluşturulduğuna dahil kısa bir açıklamayı içerir.
> + `kullanıcı isimi` **:**  Oluşturulacak kullanıcı için bir isim veriyoruz. Buradaki `linus` oluyor.
> + **UYARI:** Ubuntu işletim sisteminde yapılmıştır.



> [!CAUTION]
> + `useradd` komutu linux distro'lar göre farklı davranabilir.  

### 12. ps
+ Linux/Unix sistemlerinde çalışan süreçleri (process) listelemek için kullanılır.

```bash
$ ps -ef 
```
> **Explanation:**
> 
### 13.ctop

### 14. scp
+ **Amaç:** `scp` (Secure Copy Protocol), Linux ve diğer Unix tabanlı sistemlerde dosyaları güvenli bir şekilde bir bilgisayardan diğerine kopyalamak için kullanılan bir komuttur.
+ SSH protokolünü kullanarak veri aktarımı yapar, bu da verilerin şifrelenmiş bir şekilde iletilmesini sağlar.
+ Bu sayede dosyaların başka bir cihaza güvenli bir şekilde aktarılması mümkün olur.

##### Syntax:
```shell
$ scp [options] source ... target
```

#### host `->` server:

```shell
$ scp file_name username@target_IP:/target/folder/
```
###### Örnek 1:
```shell
$ scp nginx-course-files.zip  ottoman@192.168.1.132:/home/ottoman
```
> **Explanation:**
> + Ana makinemizde(host) mevcut olan nginx-course-files.zip dosyasını uzak sunucuda olan `192.168.1.132` IP'li ve ottoman kullanıcısın ev dizine gönderiyoruz.

#### server `->` host:
```shell
$ scp username@source_IP:/source/folder/file_name /target/folder/
```

> [!NOTE]
> + Eğer scp komutunu linux veya unix(mac) gibi işletim sistemleri üzerinde kullanıyorsanız ve host makine ile server makine aynı kullanıcıyı kullanıyorsa sadece IP adresini yazmamız yeterli olacaktır.
> + Örneğin; linux'un kullanıcısı `ottoman` ve sunucun kullanıcısı `ottoman` olursa komut; 
> + `scp file_name ottoman@192.168.1.134` yerine `scp file_name 192.168.1.134` yazabiliriz. 

#### scp parametreleri:
###### `-r` parametresi:

###### `-C` parametresi:

###### `-P` parametresi:


### 15. tree

###### 1. Temel Kullanımı:
```
$ tree
```
> **Explanation:**
> + Dosya sistemindeki dizin ve alt dizinlerin hiyerarşik bir yapıda görsel olarak gösterilmesini sağlar.
> + `tree` komutu çalıştırdığınız dizinde hiyerarşik bir şekilde dosya ve dizinleri ekran yazdırır.

###### 2. `-d` parametresi:
```sh
$ tree -d
```
> **Explanation:**
> + Yanlızca dizinleri yani klasörleri listeler.

###### 3. -L parametresi:
```sh
$ tree -L 2
```
> **Explanation:**
> + 

### 16. rsync:

```sh
$ rsync -av --delete ~/Dropbox/oltu_tasi ~/Documents/my_documantion_on_obsidian
```

###### --dry-run parametresi:
```sh
$ rsync -av --delete --dry-run ~/Dropbox/oltu_tasi \
 ~/Documents/my_documantion_on_obsidian
```

### 17. id:
```shell
$ id
```

### 18. Journalctl:

#### `-u` parametresi:
+ `-u` paramtresi ile belirtilen bir hizmetin (unit) **systemd günlüklerini** görmek için kullanılır.
+ Bu günlükler(logs), hizmetin çalışmaya başladığı andan itibaren kaydedilen önemli olaylar, hatalar ve uyarılar gibi bilgileri içerir.

```shell
$ sudo journalctl -u <unit_name>
```
> **Explanation:**
> + `<unit_name>`: Birimin adını belirtir. Örneğin, `nginx`, `sshd`, `apache2` gibi.


> [!TIP]
> + `-u` parametresi servis birimleri(`service unit`) ile anlatılmıştır ama diğer `systemd` birimleri ile kullanılabilir.

##### Ne İşe Yarar?
1. **Unit Log'larını görmek:** Bir unit'ün neden çalışmadığını veya hata verildiğini anlamanıza yardımcı olur.
2. **Hata Analizi:** Hizmet başlatıldığında oluşan hataların detaylarını gösterir.


