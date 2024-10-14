#docker 
## Kernel Namespace:

+ Linux çekirdeğindeki **namespace** özelliği, Docker gibi konteyner teknolojilerinin temelini oluşturur.
+ Namespace'ler, işletim sisteminde *çalışan bir sürecin(running process)*, sistem kaynaklarına erişim şekliyle ilgili izole bir görünüm sağlamasına olanak tanır. Bu izolasyon, konteynerlerin birbirinden bağımsız çalışmasını mümkün kılar.
+ Docker, namespace'leri kullanarak her bir konteynerin kendi ayrı çalışma ortamına sahip olmasını sağlar.
##### Linux Namespace'leri ve Docker İlişkisi:
+ Linux çekirdeğinde namespace'ler, sistem kaynaklarını izole etmek için kullanılır ve şu tür namespace'ler vardır:
###### 1. PID Namespace:
+ Docker, her bir konteynerin kendi işlem kimlikleri (PID veya Process ID) hiyerarşisine sahip olmasını sağlar. Bu sayede konteyner içindeki işlemler(processes) dışarıdaki işlemlerden(processes) izole olur ve her konteyner kendi PID 1 süreci ile başlar.
###### 2. Mount Namespace:
+ Her konteyner kendi dosya sistemini kullanır.
+ Docker, mount namespace kullanarak her konteyner için izole edilmiş bir dosya sistemi sağlar. Bu, konteynerlerin birbirlerinin dosya sistemine erişememesi anlamına gelir.
###### 3. Network Namespace:
+ Docker, her konteyner için ayrı bir ağ yığını oluşturur.
+ Bu, her konteynerin kendi IP adresine, ağ arayüzlerine(network interface) sahip olmasını ve dış dünya ile iletişim kurmasını sağlar.
###### 4. IPC Namespace:
+ IPC (Inter-process Communication) namespace, süreçler(process) arası iletişim kanallarını izole eder. Docker, konteynerlerin kendi IPC kaynaklarını kullanmasını sağlar.
###### 5. UTS Namespace:
+ UTS (Unix Time-sharing System) namespace, her konteynerin kendi hostname ve domain name bilgilerine sahip olmasını sağlar.
+ Bu da hostname’lerin konteynerler arasında çakışmamasını garantiler.
###### 6. User Namespace:
+ Docker, user namespace kullanarak konteyner içindeki kullanıcıların host sistemde farklı haklara sahip olmasını sağlayabilir.
+ Bu, güvenlik açısından önemlidir çünkü konteyner içinde root olan bir kullanıcı, host sistemde root haklarına sahip olmayabilir.
##### Docker ve Namespace Kullanımı:
+ Docker, konteynerleri başlattığında her bir konteyneri yukarıda bahsedilen namespace'ler ile izole eder. Bu sayede, *aynı çekirdeği paylaşan konteynerler arasında tam izolasyon sağlanır.*
+ Ancak, bu konteynerler hala çekirdek seviyesinde paylaşılan kaynakları kullanabilirler, bu da *Docker'ın hafif ve performans açısından verimli olmasını sağlar.*
+ Namespace'lerin Docker'daki bu kullanımı sayesinde, *Docker konteynerleri sanal makinelerden daha hızlı başlar, daha az kaynak kullanır ve daha verimli bir izolasyon sağlar.*
#### Control Groups
+ **Control Group** (kısaca **cgroup**), Linux çekirdeğinde bulunan ve **sistem kaynaklarının** süreçler(processes) arasında **yönetimini sağlayan** bir mekanizmadır.
+ *Cgroup'lar, CPU, bellek, disk I/O, ağ bant genişliği gibi kaynakları izlemek, sınırlandırmak, önceliklendirmek ve izole etmek için kullanılır.*
+ Docker ve diğer konteyner teknolojileri, cgroup'ları kullanarak konteynerlerin sistem kaynaklarını yönetir.
##### Cgroup'un Temel İşlevleri:

###### 1. Kaynak Sınırlandırma(limiting):
+ Cgroup, bir sürecin veya süreç grubunun CPU, bellek veya disk gibi kaynakları ne kadar kullanabileceğini belirleyebilir.
+ Örneğin, bir konteynerin yalnızca belirli bir miktar RAM kullanmasına izin verilebilir.
###### 2. Kaynak İzleme(Accounting):
+ Cgroup, hangi kaynakların ne kadar kullanıldığını izleyebilir. Bu, sistemin hangi süreçlerin ne kadar CPU veya bellek kullandığını takip etmesine olanak tanır.
###### 3. Önceliklendirme (Prioritization):
+ Sistem kaynaklarının adil bir şekilde paylaşılmasını sağlar ve önceliklendirme ile kritik süreçlerin daha fazla kaynak almasına olanak tanır.
+ Örneğin, düşük öncelikli işlemler, CPU payından daha az yararlanabilir.
###### 4. İzolasyon (Isolation):
+ Cgroup, farklı süreçlerin birbirinden izole olmasını sağlayarak, bir grubun kaynak tüketiminin diğerlerini etkilemesini önler.
+ Bu özellikle konteynerler için önemlidir; bir konteynerin fazla bellek veya CPU tüketmesi, diğer konteynerlerin performansını düşürmemelidir.
##### Cgroup ve Docker ilişkisi:
+ Docker, her bir konteynerin **sistem kaynakların**ı etkin bir şekilde yönetmek için **cgroup**'ları kullanır.
+ Docker, her bir konteynere atanmış belirli cgroup'lar aracılığıyla konteynerlerin CPU, bellek ve diğer kaynak kullanımını kontrol eder.
## Docker Engine


> [!NOTE]
> + Kontrol yapısı;
>  + Docker Daemon >>>>>  REST API  >>>>> Docker CLI


+ **Docker Engine**, **konteynerlerin oluşturulması**, **çalıştırılması** ve **yönetilmesinden sorumlu** bir uygulamadır.
+ Docker Engine bir sisteme kurulduğunda docker objeleri(container, volume, network ve image) oluşturabiliriz ve bu ojeleri yönetebiliriz.
##### Docker Engine'in Bileşenleri:
+ Docker Engine, üç ana bileşenden oluşur:
###### 1. Docker Daemon(dockerd):
+ Docker Daemon, Docker Engine'in arka planda çalışan servisidir ve tüm konteyner işlemlerini yönetir.
+ Docker API'sinden gelen talepleri işleyerek konteynerlerin başlatılması, durdurulması, image'ların oluşturulması gibi işlemleri yürütür.
+ Aynı zamanda cgroup, namespace gibi host'un Linux çekirdeği özelliklerini kullanarak konteynerlerin izolasyonunu ve kaynak yönetimini sağlar.
###### 2. Docker CLI:
+ Docker CLI (Command Line Interface), kullanıcıların Docker Daemon ile etkileşime girmesini sağlayan bir komut satırı aracıdır. `docker run`, `docker build`, `docker stop` gibi komutlar aracılığıyla kullanıcılar Docker konteynerlerini yönetebilir.
+  Docker CLI, Docker API'sine çağrılar yapar ve bu çağrılar Docker Daemon tarafından işlenir.
###### 3. Docker API:
+ Docker Engine, RESTful bir API sunar. Bu API, Docker Daemon ile programatik olarak iletişim kurmayı sağlar.
+ Diğer yazılımlar veya araçlar, Docker API'sini kullanarak Docker Engine üzerinde işlem yapabilir. Bu API aynı zamanda Docker CLI'nin daemon ile iletişim kurduğu mekanizmadır.

## Docker Engine Kurulumu:

##### 1. Linux Depodan:

##### 2. Docker Resmi Sitesiden:
[Resmi Sitesi](https://docs.docker.com/engine/install/ubuntu/)


> [!WARNING]
> + Eğer güvenlik ayarlarını yönetmek için `ufw` veya `firewalld` kullanıyorsanız, docker kullanarak oluşturmuş olduğunuz portları güvenlik duvarı tarafından bypass olacaktır.
> + Docker yalnızca iptables-nft ve iptables-legacy ile uyumludur. `nft` ile oluşturulan güvenlik duvarı kuralları Docker yüklü bir sistemde desteklenmez.
> + Kullandığınız tüm güvenlik duvarı kurallarının iptables veya ip6tables ile oluşturulduğundan ve bunları DOCKER-USER zincirine eklediğinizden emin olun

###### Eski Sürümleri Kaldırma:
+ Docker Engine'i kurabilmeniz için öncelikle çakışan paketleri kaldırmanız gerekmektedir.
```shell
$ for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

###### apt depolarını kullanarak yükleme:
```shell
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

#### Docker Engine Hakkında
+ Docker engine 2 kısımdan oluşmaktadır; Docker Client ve Docker Server
+ Docker Client(CLI) --> REST API --> Docker Server(Dockerd)
##### Docker Client:
+ **Görev:** Docker Client, kullanıcıların Docker komutlarını girdiği arayüzdür. Kullanıcılar `docker run`, `docker build`, `docker pull` gibi komutları Docker Client aracılığıyla gönderir.
+ **Çalışma Şekli:** Docker Client, kullanıcının yazdığı komutları alır ve bunları Docker Server’a (Daemon'a) API istekleri olarak gönderir. 
+ Kendisinin doğrudan container yönetimi veya işleme yeteneği yoktur, yalnızca komutları ileten bir araçtır.
+ **İletişim:** Docker Client, Docker Daemon ile Docker REST API aracılığıyla iletişim kurar. Bu iletişim yerel olarak (aynı makine üzerinde) veya uzak makineler üzerinden olabilir.
+ Uzak bir Docker Daemon'a bağlanmak için, Docker Client'ı bir sunucudaki Docker Engine ile konuşacak şekilde yapılandırabilirsiniz.

##### Docker Server(Dockerd):
+ **Görev:** Docker Server, tüm Docker işlemlerini yürüten ve konteynerlerin oluşturulmasını, çalıştırılmasını ve yönetilmesini sağlayan arka plandaki bir servistir. Bu servis, Docker Client’tan gelen istekleri alır ve Docker Engine’in tüm işlevlerini yürütür.
	+ Konteynerleri oluşturur, çalıştırır ve durdurur.
	+ images oluşturur ve depolar.
	+ Docker ağlarını ve volumes yönetir.

## Container
### version:
```shell
$ docker version
```
> **Explanation:**
> + Docker engine hakkında bilgi verir; Docker engine 2 kısımdan oluşur;  Docker Server ve  Docker Client olmak üzeri.

---
### info:
```shell
$ docker info
```
> **Explanation:**
> + **Docker Server**: Toplam container sayısını, çalışan container sayısını, durdurulan container sayısını ve toplam image sayısını verir.
> + **Docker Swarm:** Docker da swarm aktif olup olmadığını buradan kontrol edebiliriz.

---
### inspect:

###### Syntax:
+ **Usage:** `docker inspect [OPTIONS] NAME|ID [NAME|ID...]`
+ **Örnek:** `docker inspect  -f 'json' web-server`
+ **Karşılığı:** `[OPTION] => -f` 'json', `NAME => web-server`

```sh
$ docker inspect web-server
```
> **Explanation:**
> + 


---
### run:
###### Syntax:
+ **Usage:** `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`
+ **Örnek:** `docker run  --rm  ubuntu ls -al`
+ **Karşılığı:** `[OPTION] => --rm`, `IMAGE => ubuntu`, `[COMMADN] => ls`, `[ARG...] => -al`
###### 1. run yardım sayfası:
```docker
$ docker run --help
```
> **Explanation:**
> + `run` komutunda kullanılabilecek tüm opsiyonları veya seçenekleri ekrana basar.

###### 1. Temel Kullanımı:
```docker
$ docker run hello-world
```
> **Explanation:**
> + `run` komut `hello-world` adlı imajı önce kendi depolarında var mı diye bakar ve ayağı kaldırmaya çalışacaktır. 
> + Eğer kendi yerel makinesinde mevcut değil ise [dockerhub](https://hub.docker.com/)'dan çekecek ve daha sonrasında ayağı kaldıracaktır.

###### 2. `run --name` parametresi:

```shell
$ docker run --name merhaba hello-world
```
> **Explanation:**
> + Temel kullanım ile aynıdır ama oluşan container'a rastgele docker tarafından isim verilmek yerine `--name` parametresi ile kendimiz  container'a `merhaba` ismini vermiş bulunuyoruz.
> + `docker ps -a` komutu ile vermiş olduğunuz isimi(`merhaba`) NAME tabında görebilirsiniz.

###### 3. `run -d` parametresi:
+ Çalıştırılacak olan container'ı arka planda çalışmasını sağlar

```shell
$ docker run -d --name web-server nginx
```
> **Explanation:**
> + nginx imajından oluşturduğumuz container'ı `-d` parametresi ile arkaplanda çalışmasını sağlıyoruz.
> + `--name` parametresi yukarıda açıklanmıştır. Kısacası, container'ı `--name` parametresi ile *web-server* olarak adlandırıyoruz.

> [!TIP]
> + nginx gibi bazı uygulamalar process'leri deamon yapıda çalıştığı için docker durudurulana kadar çalışacaktır. 

###### 4. `[COMMAND] [ARG...]` kullanımı:
```shell
$ docker run --name tarih ubuntu date
```
> **Explanation:**
> + `ubuntu` imajından oluşturulan `tarih` adındaki container `date` komutunu çalıştıracaktır.
> + Bunun nasıl çalıştığını daha iyi anlamak için; [[Dockerfile]] bölümün bakınız..

---
### exec:
###### Syntax:
+ **Usage:** `docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`
+ **Örnek:** `docker exec  -d  web-server nginx -s reload`
+ **Karşılığı:** `[OPTION] => -d`, `CONTAINER => web-server`, `COMMADN => nginx`, `[ARG...] => -s reload`


> [!WARNING]
> + `docker exec` komutunu kullanabilmeniz için container host(yerel makine) üzerinde çalışır olması gerekmektedir.


```
$ docker 
```

---
### stop:
+ 

---
### start:

---
### log:
+ `docker logs` komutu, Docker konteynerlerinin çıktısını (loglarını) görüntülemek için kullanılan önemli bir araçtır.
+ Bu komut sayesinde, bir konteynerin çalışması sırasında üretilen **standart çıktı (stdout)** ve **standart hata (stderr)** mesajlarına erişebilirsiniz.
+ Uygulamanızın çalışmasını izlemek, hata ayıklamak ve performansını değerlendirmek için `docker logs` komutu oldukça faydalıdır.
###### Syntax:
+ **Usage:** `docker logs [OPTIONS] CONTAINER`
+ **Örnek:**  `docker logs -f containerName`
+ **Karşılığı:** `[OPTIONS] => -f`, `CONTAINER => containerName`
###### 1. Temel Kullanımı:
```shell
$ docker logs merhaba
```


---
### rm:
+ **Amaç:** Docker da container silme işlemini yapar. Diğer bir tanımla Durdurulmuş (stopped) konteynerleri Docker ortamından kaldırmak.
###### Syntax:
+ **Usage:** `docker rm [OPTIONS] CONTAINER [CONTAINER...]`
+ **Örnek:**  `docker rm -v containerName`
+ **Karşılığı:** `[OPTIONS] => -v`, `CONTAINER => containerName`

###### 1. Temel Kullanımı:
```shell
$ docker rm merhaba
```
> **Explanation:**
> + `merhaba` adındaki container'ı siliyoruz.
> + `docker container rm merhaba` komut ile aynıdır ve aynı işlevi yapar.


> [!CAUTION]
> + `docker rm` kullanabilmek için container'ın durdurulmuş olması gerekmektedir. 
> + Docker da container kaldırma işlemi ya container'ın adı ile yada container'ın ID ile yapılır. 
> 	+ **container adı ile:** `docker rm containerName` 
> 	+ **container ID ile:** `docker rm containerID` 
> + Container'ın ID veya adını almak için `docker ps -a` komutunu kullanınız.

###### 2. Çalışan Container Kaldırma:
```
$ docker rm -f web-server
```
> **Explanation:**
> + `nginx` imajından oluşturulmuş `web-server` adında bir container mevcuttur.
> + Normal şartlarda `rm` komutu ile çalışan container kaldırılmaz ama `-f` parametresi ile çalışan bir container kaldırılabilir
> + `-f` veya `--force` parametresi, *zorla(force)* kaldırma anlamında kullanılır.

---
### ps:
+ **Amaç:** Docker da container silme işlemini yapar. Diğer bir tanımla Durdurulmuş (stopped) konteynerleri Docker ortamından kaldırmak.
###### Syntax:
+ **Usage:** `docker ps [OPTIONS]`
+ **Örnek:**  `docker ps -a`
+ **Karşılığı:** `[OPTIONS] => -a`

###### 1. Çalışan Container
```shell
$ docker ps
```
> **Explanation:**
>  Container'ları listeler

###### 2. Tüm Container
```shell
$ docker ps -a
```
> **Explanation:**

###### 3. `ps --no-trunc`:
```shell
$ docker ps -a --no-trunc
```
> **Explanation:**
> + `--no-trunc` komutu çıktı verirken her hangi bir kısaltma yapmaz.
> + Bu komut, standart `docker ps -a` çıktısının tüm bilgilerini kesintisiz olarak gösterir.

---
## Image

### Union File System Nedir?
+ **Docker Union File System (Birleştirme Dosya Sistemi)**, Docker’ın imaj ve container’ları verimli bir şekilde yönetmek için kullandığı katmanlı bir dosya sistemidir.
+ Bu dosya sistemi, birden fazla katmanı üst üste birleştirerek tek bir dosya sistemi olarak sunar.
+ Docker imajlarının yapı taşlarını oluşturan bu katmanlar, birbirinden bağımsızdır ve birleştirme dosya sistemi sayesinde birbirlerinin üzerine eklenir.
+ Union File System, birçok farklı dosya sistemini birleştirip, bu dosya sistemlerinden oluşan katmanları tek bir birim olarak gösteren bir dosya sistemi türüdür.
+ Linux'ta yaygın kullanılan UnionFS türlerinden bazıları şunlardır: *OverlayFS*, *AUFS (Advanced Multi-layered Unification Filesystem)*, *Btrfs* ve *ZFS*
+ UnionFS, Docker imajlarının katmanlar halinde inşa edilmesini ve bu katmanların birleştirilerek tek bir dosya sistemi gibi kullanılmasını sağlar.
#### Docker Union File System'in Çalışma Şekli:
###### 1. İmajların Katmanları:
+ Docker imajları, her biri salt okunur olan bir dizi katmandan oluşur.
+ İmajlar, birbirinin üstüne eklenen bu katmanlardan oluştuğu için bir değişiklik yapıldığında, yalnızca değişen katman yeniden oluşturulur ve böylece veri tekrarından kaçınılır.
+ Katmanlar sıkıştırılmış formatta saklanır ve gerektiğinde açılır.
###### 2. Container'ın Yazılabilir Katmanı:
+ Docker container’ı çalıştığında, imajın üzerine bir yazılabilir katman eklenir.
+ Container’da yapılan değişiklikler (örneğin, yeni dosyaların eklenmesi, dosyaların düzenlenmesi veya silinmesi) sadece bu yazılabilir katmanda saklanır.
+ 

### ls(images):
```shell
$ docker image ls
```
> **Explanation:**
> + Yerel makinenize indirilmiş olan imajları listeler:
> + **Alternatif:** `docker images` komut aynı çıktıyı verir.

---
### inspect:


---
### rm:
```shell
$ docker image rm 
```

---
## Volume

#### Kaynak:
[Ayti Tech](https://www.youtube.com/watch?v=ACr92yZF0bg)
