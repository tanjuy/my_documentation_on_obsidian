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

###### 1.3. `-L` parametresi:
```shell
curl -L http://192.168.1.132
```

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

### 19. lsof:
+ `lsof` (_**Li**st **O**pen **F**iles_**), Unix ve Unix benzeri işletim sistemlerinde (Linux, macOS, BSD vb.) **açık dosyaları** listelemek için kullanılan bir komuttur.


> [!NOTE]
> **`lsof` Ne İşe Yarar?**
> + Açık dosyaları, bu dosyaları kullanan süreçleri ve kullanıcıları gösterir.
> + Linux'ta her şey bir dosya olarak kabul edildiği için (`/dev`, soketler, pipe'lar, dizinler, vs.), `lsof` ile şunları listeleyebilirsiniz:
> 	- **Normal dosyalar** (text, binary, config dosyaları)
> 	- **Ağ bağlantıları** (TCP/UDP soketleri)
> 	- **Dinamik kütüphaneler** (.so, .dll)
> 	- **Silinmiş ama hala bir süreç tarafından kullanılan dosyalar**
> 	- **Cihaz dosyaları** (`/dev/sda`, `/dev/tty`, vs.)
> 	- **Paylaşılan bellek segmentleri**

#### Tüm Açık Dosyaları Listeleme:

```shell
sudo lsof
```

**`lsof` Çıktısı:**

```shell
COMMAND     PID   TID TASKCMD     USER   FD    TYPE      DEVICE SIZE/OFF     NODE NAME
systemd       1                   root  cwd     DIR       253,0     4096        2 /
systemd       1                   root  rtd     DIR       253,0     4096        2 /
...
```
> **Explanation:**
> 1. **`COMMAND`**
> 	- Dosyayı açan **sürecin komut adı** (ör: `systemd`, `nginx`, `bash`).
> 	- Burada `systemd` (PID 1), Linux'taki ana init sürecidir.
> 2. **`PID`**
> 	- **Süreç Kimlik Numarası** (Process ID).
> 	- `systemd` genellikle `1` ile başlar (tüm süreçlerin atası).
> 3. **`TID`** (Task ID)
> 	- **Thread (iş parçacığı) kimliği**. Eğer boşsa, ana süreç kastedilir. Bu örnekte thread bilgisi yok.
> 4. **`TASKCMD`**
> 	- Thread'in komut adı (genellikle ana süreçle aynı). Burada gösterilmemiş.
> 5. **`USER`**
> 	- Süreci çalıştıran **kullanıcı**. `systemd`, `root` yetkileriyle çalışır.
> 6. **`FD`** (File Descriptor)
> 	- Dosya tanımlayıcısı. Ne tür bir dosya erişimi olduğunu gösterir:
> 		+ `cwd`: **Current Working Directory** (Sürecin çalışma dizini).
> 		+ `rtd`: **Root Directory** (Sürecin kök dizini).
> 		+ `txt`: Program kodu (binary/shared library).
> 		+ `mem`: Memory-mapped file.
> 		+ `0`, `1`, `2`: Standart akışlar (`0=stdin`, `1=stdout`, `2=stderr`).
> 		+ `4u`: Okuma/yazma için açılmış dosya (numara rastgele, `u`=read-write).
> 7. **`TYPE`**
> 	- Dosya türü:
> 		+ `DIR`: Dizin.
> 		+ `REG`: Normal dosya.
> 		+ `CHR`: Karakter aygıtı (terminal, `/dev/tty` gibi).
> 		+ `IPv4`/`IPv6`: Ağ soketi.
> 		+ `unix`: Unix domain soketi.
> 8. **`DEVICE`**
> 	- Dosyanın bulunduğu **aygıt numarası** (major,minor). `253,0`: Genellikle bir disk bölümünü (ör: `/dev/vda1`) gösterir.
> 9. **`SIZE/OFF`**
> 	- Dosya boyutu (bytes) veya offset (işlemci için bellek konumu). `4096`: Dizinler için tipik blok boyutu.
> 10. **`NODE`**
> 	- Dosyanın **inode numarası**. `2`: Linux'ta `/` dizininin inode'u genellikle `2`'dir.
> 11. **`NAME`**
> 	- Dosyanın **tam yolu** veya bağlantı detayı. `/`: `systemd`'nin çalışma ve kök dizini gösterir.


#### Belirli port'u dinleyen süreçleri listeleme:

```shell
sudo lsof -i :80
```
> **Alternative:**
> + `ps aux | grep nginx` 
> + `ss -tulnp | grep :80`

**Çıktı:**
```shell
COMMAND   PID   USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
nginx   29189   root    6u  IPv4  50882      0t0  TCP *:http (LISTEN)
nginx   29190 nobody    6u  IPv4  50882      0t0  TCP *:http (LISTEN)
nginx   29191 nobody    6u  IPv4  50882      0t0  TCP *:http (LISTEN)
```
> **Explanation:**
> + `nginx` süreci **29189** PID ile **root** kullanıcısı tarafından başlatılmış.
> + `nginx` ayrıca **29190** ve **29191** PID'leriyle **nobody** kullanıcısı altında çalışıyor.
> + Hepsi **TCP 80 (http) portunu dinliyor**.
> + Nginx, master-worker mimarisine sahiptir.
> 	- **PID 29189 (root)** → **Master Process** (Ana süreç, yapılandırmayı yönetir).
> 	- **PID 29190 ve 29191 (nobody)** → **Worker Process** (İstekleri işler).

|Sütun|Açıklama|
|---|---|
|`COMMAND`|Portu dinleyen sürecin adı. Burada **nginx** gözüküyor.|
|`PID`|Sürecin (Process ID) kimliği.|
|`USER`|Süreci çalıştıran kullanıcı. İlk satırda **root**, diğerlerinde **nobody** olarak görülüyor.|
|`FD`|Dosya tanıtıcısı (File Descriptor). Burada **6u**, açık dosyanın okuma/yazma (`u` = "update") modunda olduğunu gösteriyor.|
|`TYPE`|Bağlantının tipi. Burada **IPv4**, IPv4 protokolünün kullanıldığını belirtiyor.|
|`DEVICE`|Cihaz numarası. Çekirdek tarafından atanır.|
|`SIZE/OFF`|Dosyanın boyutu veya offset değeri. TCP bağlantılarında genellikle **0t0** olur.|
|`NODE`|Ağ bağlantısı için düğüm numarası.|
|`NAME`|Açık dosyanın adı veya ağ bağlantısı. Burada *_TCP _:http (LISTEN)__ yani **80 numaralı portun dinlendiğini** gösteriyor.|
#### Bir kullanıcının açık dosyaları:

```shell
sudo lsof -u ottoman
```
> **Explanation:**
> + `ottoman` kullanıcısın açtığı tüm dosyaları ve ağ bağlantılarını listelemek için kullanılır.

```shell
COMMAND     PID    USER   FD      TYPE     DEVICE SIZE/OFF       NODE NAME
systemd    1042 ottoman  cwd       DIR      253,0     4096          2 /
systemd    1042 ottoman  rtd       DIR      253,0     4096          2 /
systemd    1042 ottoman  txt       REG      253,0  1849992     403473 /usr/lib/systemd/systemd (deleted)
...
```

#### Belirli bir program tarafından:

```shell
sudo lsof -c nginx
```
> **Explanation:**
> + **nginx** adlı süreç (veya süreçler) tarafından açılmış tüm dosyaları ve ağ bağlantılarını listelemek için kullanılır.
> + **Alternative:** `netstat -tulnp | grep nginx` veya  `ss tulnp | grep nginx`

**Çıktı:**
```shell
COMMAND   PID     USER   FD    TYPE     DEVICE SIZE/OFF    NODE NAME
nginx   29189     root  cwd     DIR      253,0     4096       2 /
nginx   29189     root  rtd     DIR      253,0     4096       2 /
nginx   29189     root  txt     REG      253,0  4588336  438401 /usr/bin/nginx
nginx   29189     root  mem     REG      253,0  2220400  415390 /usr/lib/x86_64-linux-gnu/libc.so.6
nginx   29189     root  mem     REG      253,0   108936  404576 /usr/lib/x86_64-linux-gnu/libz.so.1.2.11
nginx   29189     root  mem     REG      253,0  4455728  418251 /usr/lib/x86_64-linux-gnu/libcrypto.so.3
nginx   29189     root  mem     REG      253,0   667864  418253 /usr/lib/x86_64-linux-gnu/libssl.so.3
nginx   29189     root  mem     REG      253,0   477296  404485 /usr/lib/x86_64-linux-gnu/libpcre.so.3.13.3
nginx   29189     root  mem     REG      253,0   198664  404325 /usr/lib/x86_64-linux-gnu/libcrypt.so.1.1.0
nginx   29189     root  mem     REG      253,0   240936  415384 /usr/lib/x86_64-linux-gnu/ld-linux-x86-64.so.2
nginx   29189     root  DEL     REG      0,1             1081 /dev/zero
nginx   29189     root    0u    CHR      1,3      0t0       5 /dev/null
nginx   29189     root    1u    CHR      1,3      0t0       5 /dev/null
nginx   29189     root    2w    REG      253,0    88818 1049333 /var/log/nginx/error.log
```
> **Explanation:**

| Sütun      | Açıklama                                                                                    |
| ---------- | ------------------------------------------------------------------------------------------- |
| `COMMAND`  | Sürecin adı (**nginx**)                                                                     |
| `PID`      | Sürecin Process ID’si (örn: `29189`, `29190`, `29191`)                                      |
| `USER`     | Süreci çalıştıran kullanıcı (örn: `root`, `nobody`)                                         |
| `FD`       | Açık dosya tanıtıcısı (örn: `6u` → okuma/yazma)                                             |
| `TYPE`     | Dosya veya bağlantı türü (örn: `DIR` → dizin, `REG` → normal dosya, `IPv4` → ağ bağlantısı) |
| `DEVICE`   | Aygıt kimliği (örn: `8,1`)                                                                  |
| `SIZE/OFF` | Dosya boyutu veya offset değeri                                                             |
| `NODE`     | Dosya veya bağlantının düğüm numarası                                                       |
| `NAME`     | Açık dosyanın veya ağ bağlantısının adı                                                     |
