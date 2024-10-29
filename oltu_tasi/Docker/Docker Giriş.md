#docker 


> [!CAUTION]
> + Docker da işlemler yapılırken çoğunlukla docker bağlanarak işlemler hale edilmez. Yani Docker işlerimizi yapmamız için gerek komutların çoğunu sağlamıştır.
> + Basit bir örnek vermek gerekirse nginx servisini yeniden başlatmak için 
> + `docker exec -it web_server bash` ile bağlanıp `nginx -s reload` yapmak yerine
> + `docker exec web_server nginx -s reload` yapmanız yeterlidir.

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
### attach:

+ Mevcut bir Docker konteynerine bağlanmak (attach) ve o konteynerin standart çıktısını, hatalarını ve girdisini görüntülemek için kullanılır.
+ `docker attach`, konteynerdeki hem standart çıktı (stdout) hem de standart hata (stderr) ile etkileşime geçmenizi sağlar.
##### Syntax:
+ **Usage:**  `docker attach [OPTIONS] CONTAINER`

##### Örnek 1

```shell
$ docker run --name webserver -d -it -p 80:80 nginx
```
> **Explanation:**
> + `webserver` container'ın `-d` parametresi ile arka planda çalışmasını sağlıyoruz.
> + `-it` parametresi ile de `ctrl+p` ve `ctrl+q` komutların aktif olması sağlıyoruz.

```shell
docker attach webserver
```
> **Explanation:**
> + Arka planda çalışan `webserver` container'ın bu komut ile tekrardan terminal ekrana gelmesini sağlıyoruz.
> + Tekrardan `deattach` moda çalışmasını sağlamak için `ctrl+p` ardından `ctrl+q` basmamız yeterlidir.

> [!IMPORTANT]
> + `docker run`  parametresine `-it` verirsek bize etkileşimli bir `tty` verecektir. Bu parametre sayesinde `ctrl+p` ardından `ctrl+q` verdiğimizde container deattach moda geçecektir.

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
> + Bunun nasıl çalıştığını daha iyi anlamak için; [[Dockerfile]] bölümün bakınız.

---
##### 5. Kaynak Sınırlama:
###### A. run --memory:
```shell
$ docker run --name web_limit_memory -d --memory=256m nginx
```
> **Explanation:**
> + Bu komutta `--memory`  parametresine odaklanacağız. nginx imajından oluşturulacak olan container'ı `256 Megabyte` RAM'e kısıtlıyoruz.
> + `256M` ile `256m` arasında hiç bir fark yoktur.(**incase-sensitive**)
> + `--memory=1G` : 1 gigabyte sınırlaması getirir.
> + `docker inspect web_limit_memory` komutu içerisinde `HostConfig.Memory: 268435456` değerine baktığımız da kaç RAM ile sınırlandığını görebiliriz ve ayrıca `byte` türünden verilmiştir.

---
###### B. run --memory-swap:

> [!CAUTION]
> + `--memory-swap` parametresini kullanabilmek için `--memory` parametresinide kullanmanız gerekmektedir.
> + Eğer `--memory` olmadan kullanırsanız; 
> + `docker: Error response from daemon: You should always set the Memory limit when using Memoryswap limit, see usage.` hata verecaktir.

```shell
$ docker run --name web_limit_memory-swap -d --memory=512M --memory-swap=1G
```
> **Explanation:**
> + bir konteynerin maksimum 512 MB bellek ve **1 GB toplam bellek+swap** kullanmasına izin verir.
> + `docker inspect web_limti_memory-swap` komut ile `HostConfig.MemorySwap:1073741824` veya sadece ilgili alanı vermek için aşağıdaki komut kullanınız.

```shell
$ docker inspect --format='{{.HostConfig.MemorySwap}}' web_limit_memory-swap
```

> [!NOTE]
> + **Varsayılan Değer:** Eğer `--memory-swap` seçeneği belirtilmezse, Docker konteyneri için bellek limitinin iki katına kadar swap alanı otomatik olarak ayrılır.
> + Yani, `--memory` 512 MB ise, toplamda 1 GB (512 MB RAM + 512 MB swap) kullanılabilir.

----
###### C. run --cpus:

```shell
$ docker run --name web_limit_cpu -d --cpus=2 nginx
```
> **Explanation:**
> + `--cpus=2` parametresi ile oluşturulan `web_limit_cpu` container'ın en fazla 2 cpu kullanabileceğin  söylüyoruz.
> + `docker inspect web_limit_cpu` komutu içerisinde `HostConfig.NanoCpus:2000000000` değerinde bakarak kaç cpu ile sınırlandığını görebiliriz. Burada 2 cpu değeri ile sınırlandırılmış.
> + Burada dikkat edilmesi gereken nokta her hangi 2 cpu kullanması yani 10 cpu olan host da rastgele 2 cpu değeri işgal etmesi.
> + `--cpus="1,3"` : Sadece 1. ve 3. çekirdekleri kullanır.

```shell
$ docker inspect --format='{{.HostConfig.NanoCpus}}' web_limit_cpu
```
> **Explanation:**
> + `docker inspect` ile tüm içeriği ekrana vermek yerine `--format` parametresi ile ilgli json parçası alınabilir.

---
###### D. run --cpuset-cpus:

+ Bir Docker konteynerini başlatırken konteynerin hangi CPU çekirdeklerini (CPU cores) kullanabileceğini belirlemenizi sağlayan bir bayraktır.
+ Bu özellik, konteynerin yalnızca belirli CPU çekirdekleri üzerinde çalışmasını sağlayarak kaynak yönetimini ve performans optimizasyonunu artırmanıza yardımcı olur.
+ Özellikle çok çekirdekli sistemlerde, belirli uygulamaların belirli çekirdeklerde çalıştırılması gerektiğinde veya kaynak izolasyonu sağlanmak istendiğinde kullanışlıdır.

```shell
$ docker run --name web_limit_cpuset-cpus -d --cpuset-cpus=1 nginx
```
> **Explanation:**
> + `--cpuset-cpus=1` parametresi işlemci(core) de sadece 1. çekirdeği kullanmaktadır.
> + `--cpuset-cpus="0,1"` : işlemci(core) de sadece 0. ve 1. çekirdeklerin kullanılmasını sağlamaktadır.
> + `--cpuset-cpus="0-3` : konteynerin 0, 1, 2 ve 3 numaralı CPU çekirdeklerini kullanmasını sağlar.
> + **UYARI:** CPU sıralaması 0'dan başlamaktadır.

```shell
$ docker inspect --format='{{.HostConfig.CpusetCpus}}' web_limit_cpus-cpus
```

---
##### E. Ortam Değişkenleri:
+ Ortam değişkenleri(environment variables), konteyner içinde çalışan uygulamalar için yapılandırma bilgileri sağlamak, gizli anahtarları saklamak veya uygulamaların davranışını kontrol etmek gibi çeşitli amaçlarla kullanılabilir.
+ Ortam değişkenleri *bash script* de değişkenler olarak geçmektedir!
###### I. --env KEY=Value:

**Syntax:**
```shell
$ docker run --env <KEY>=<VALUE> <image>
```

**Temel Kullanımı:**
```shell
$ docker run --name env_test --env distro=ubuntu --env=database_server=linux.com \
-e passwd='linux' ubuntu printenv
```
> **Explanation:**
> + Docker konteyneri oluşturulurken ortam değişkenlerini (environment variables) ayarlamak için kullanılır.
> + `--env` ve kısa yazımı `-e` 3 farklı kullanımı mevcuttur ve aynı hedefe hizmet eder.
> + Komut çalıştırdığımızda `printenv` komutu `env_test` container'ın içerisindeki değişkenler bir diğer adı olan ortam değişkenlerini verecektir.
> + `docker exec -it env_test bash` komut ile içerisine girersek ve `echo $distro` komutu verirsek ubuntu çıktısı verecektir.

```shell
$ docker inspect --format '{{.Config.Env}}' env_test
```

###### II. --env-file dosya:

```shell
$ docker run --name env_file_test --env-file=./env.list ubuntu printenv
```

**env.list**
```text
OS=Linux
distro='Arch Linux'
language=Python
packageManager=pacman
```

> **Explanation:**
> + `--env` parametresi ile tek tek yazmak yerine key=value değerlerini bir dosyaya yazdığımızda `--env-file` parametresi ile container içerisine aktarabiliriz.
> + `printenv` komut ile bu ortam değişkenlerin ekran yazdırabiliriz.
> + Aşağıdaki komut ile container değişkenlerin görebiliriz.

```shell
$ docker inspect --format '{{.Config.Env}}' env_file_test
```

##### F. Port Açma:
###### -p parametresi:
```shell
$ docker run --name port_publish -d -p 8081:80 nginx
```
> **Explanation:**
> + `-p` parametresi port yayınlamada kullanılır.
> + nginx imajından oluşturulmuş olan `port_publish` container içerisindeki nginx uygulaması 80 port ile docker engine göndermektedir ve docker enginx de 80'den gelen 8081 port'una aktarmaktadır.
> + `$ curl 192.168.1.134:8081` komut ile GET isteği atığımızda container içinde çalışan nginx'e ulaşacaktır. Tabi aynı işlemi tarayıcı ile de yapabilirsiniz.


> [!CAUTION]
> + `-p 8081:80` parametresinde;
> + `8081` : Dış dünyaya açılan port  ---> `80` : container içerisindeki port yayını 
> + `curl 192.168.1.134:8081` 

```shell
$ docker inspect --format='{{.NetworkSettings.Ports}}' port_publish
```

```shell
$ docker inspect --format='{{.HostConfig.PortBindings}}' port_publish
```
> **Explanation:**
> 



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
$ docker logs web-server
```
> **Explanation:**
> + `nginx` imajından oluşturmuş olduğumuz `web-server` container'ın `stdout` ve `stderror` çıktılarını bu komut ekrana yazdıracaktır.
> + Çünkü docker engine,  docker da container'ın içerisinde çalışan process(uygulama)  `stdout` ve `stderror` çıktılarını `docker logs` komuta yönlendirmiştir.
###### 2. -n veya --tail parametresi:
```shell
$ docker logs -t 5 web-server
```
> **Explanation:**
> + nginx imajından oluşturulmuş `web-server` container'ın logs çıktısının sondan 5 satırını ekrana basar.
> + `-n` parametresini uzun yazılışı `--tail` halidir.

###### 3. -f parametresi:
```sh
$ docker logs -f c1a29857d22c
```
> **Explanation:**
> + nginx imajında oluşturulmuş `web-server` container da NAME yerine ID kullanarak container'ın canlı log takibini yapıyoruz.
> + container NAME: `web-server` - container ID: `c1a29857d22c`

---
### top:
+ **Amaç:** Docker konteynerinde çalışan süreçleri (process) görüntülemek için kullanılır. Bu komut, bir konteynerin içinde hangi işlemlerin çalıştığını ve bu işlemlerin ayrıntılarını hızlıca görmenizi sağlar. 
###### Syntax:
+ **Usage:** `docker top CONTAINER [ps OPTIONS]`
+ **Örnek:**  `docker top containerName aux`
+ **Karşılığı:** `[OPTIONS] => aux, `CONTAINER => containerName`
###### 1. Temel Kullanımı:
```shell
$ docker top ps_command 
```
> **Explanation:**
> + ubuntu imajından oluşturulmuş olan `ps_command` container içersinde çalışan tüm süreçleri(processes) ekrana listeler.

###### 2. ps parametreleri:
```shell
$ docker top ps_command -u                # 1
```

```shell
$ docker exec -it ps_command bash         # 2
```

```sh
root@a70184c89e21:/# ps -u                # 3
```
> **Explanation:**
> 1. `docker top` komut ile `ps_command` adındaki container'ın tüm kullanıcılarını `USER`, `PID` gibi işlemleri ekrana yazdırır.
> 2. `docker exec` komut ile `ps_command` adlı container'ın shell açmamıza izin verir.
> 3. `ps_command` adlı container'ın shell de `ps -u` komutu çalıştırsak aynı çıktıyı verecekdir.
> 4. Özetle: `docker top` komutu container'ların içerilerine girmeden `ps` çıktılarını almamızı sağlar ve ayrıca bazı imajlarda veya container'larda  içlerinde `ps`komut bulunmayabilir. Bu rağmen `docker ps` her container da çalışır.


---
### stats:

+ **Amaç:** Docker konteynerlerinizin gerçek zamanlı kaynak kullanımını (CPU, bellek, ağ, disk I/O vb.) izlemenizi sağlayan güçlü bir araçtır. konteynerlerinizin performansını gerçek zamanlı olarak izlemenizi sağlar. Bu, uygulamalarınızın aşırı kaynak tüketip tüketmediğini, bellek sızıntıları olup olmadığını veya beklenmedik CPU kullanımı gibi sorunları hızlıca tespit etmenize yardımcı olur.
###### Syntax:
+ **Usage:** `docker stats [OPTIONS] [CONTAINER...]`
+ **Örnek:**  `docker stats -a containerName`
+ **Karşılığı:** `[OPTIONS] => -a`, `CONTAINER => containerName`

###### 1. Temel Kullanımı:

```shell
$ docker stats
```
> **Explanation:**
> + Her bir konteyner için CPU kullanımı, bellek kullanımı, bellek limiti, ağ I/O ve disk I/O gibi bilgileri canlı olarak gösterir

###### 2. --all Kullanımı:

```shell
$ docker stats --all
```
> **Explanation:**
> + Tüm konteynerleri, hatta durdurulmuş olanları bile görüntüler.

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

### prune:
+ Durdurulmuş (çalışmayan) tüm konteynerleri siler
###### Syntax:
+ **Usage:**  `docker container prune [OPTIONS]`
+ **Örnek:** `docker container prune -f`
+ **Karşılığı:** `[OPTIONS] => -f`

###### 1.Temel Kullanımı:
```shell
$ docker container prune 
```
> **Expalanation:**
> + Durdurulmuş (çalışmayan) tüm konteynerleri kaldırır.

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
### publish:
+ Bir Docker konteynerini çalıştırırken konteynerin içindeki belirli bir portu ana makineye (host) yönlendirmek için kullanılır.
+ Bu komut sayesinde, konteynerin(container) içindeki bir uygulamaya, ana makineden(host) veya dış ağlardan erişim sağlanabilir.
##### Syntax:
+ **Usage:** `docker run -p hostPort:contaierPort`

##### Örnek 1:

```shell
$ docker run --name web_engress -p 5000:80 -dit nginx
```
> **Explanation:**
> + `5000 port` : ana makinenin port'una açılmaktadır.
> + `80 port` : container'ın port'una açılmaktadır. ve içerisinde nginx 80 portundan yayın yapmaktadır.
> + `-it`: parametresi ile interactive tty oluşturduk. Bağlandığımızda(`docker attach web_engress`), `ctrl+p` ardından `ctrl+q` ile deattach moda düşebiliriz.
> + `-p` parametresini uzun yazılışı: `--publish`

```shell
$ curl -i http://192.168.1.134:5000
```
> **Explanation:**
> + Bu komut ile ana makinenin 5000 port'u ile container nginx sunucusuna ulaştığımızı kanıtlar. Bu GET istek atma işlemini tarayıcı ile de yapabiliriz.

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

### Image isimlendirme:
+ Docker’da bir imaj (image) isimlendirme yapısı, imajların daha düzenli bir şekilde tanımlanmasını ve sürüm kontrolünü kolaylaştırmak için kullanılır.
+ İmaj isimlendirme yapısı, Docker Hub gibi bir kaynağa (registry) yüklenecek imajları ve farklı sürümleri belirlemede özellikle önemlidir.
##### Syntax:
```plaintext
<dockerhub_user>/<image_name>:<tag>
```
> + **Explanation:**
> + **dockerhub_user:**  *Bir organizasyon veya kişiyi göstermektedir.*
> + **image_name**: İmajın adı veya tanımlayıcısıdır. Bu isim, imajı diğerlerinden ayıran benzersiz bir tanımlayıcıdır.
> + **tag**: İmajın sürümünü belirtir. Sürüm takibi ve farklı sürümlerin yönetimi için kullanılır. Sıkça kullanılan sürüm isimleri arasında `latest`, `1.0`, `v2.1.3` gibi ifadeler bulunur. `:tag` kısmı belirtilmezse, Docker varsayılan olarak `latest` etiketini kullanır.

##### Resmi olan:
```shell
nginx:latest
```

##### Özel Repository ve Etiket:
```shell
chuanwen/cowsay:latest
```


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
+ Docker'da **volume** (hacim), konteynerlerin verilerini kalıcı olarak saklamak ve paylaşmak için kullanılan bir depolama mekanizmasıdır.
+ Konteynerler genellikle geçici yapılar olduğundan, konteynerler silindiğinde içinde bulunan veriler de kaybolur
+ **Docker volume**, bu sorunu çözerek verileri konteyner yaşam döngüsünden bağımsız hale getirir.


### 1. Temel Kullanımı:

```shell
$ docker volume create ottoman_volume
```
> **Explanation:**
> + `first_volume` adında volume oluşturduk.

```shell
$ docker volume ls
```
> **Explanation:**
> + Oluşturulmuş volume'leri listeler.

```shell
$ docker volume inspect ottoman_volume
```
> **Explanation:**
> + `first_volume` volume hakkında detaylı bilgiyi ekrana basar.

```json
[
    {
        "CreatedAt": "2024-10-19T15:40:03+03:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/ottoman_volume/_data",
        "Name": "first_volume",
        "Options": null,
        "Scope": "local"
    }
]
```

```shell
$ docker run --name ottoman_container -it -v ottoman_volume:/app alpine sh
```
> **Explanation:**
> + Yukarıda `docker volume` oluşturduğumuz `ottoman_volume`, alpine container'ın içerisinde `/app` dizinine bağlıyoruz.
> + `/app` dizinini yoksa oluşturulur eğer var ise direk bağlanır. 

**Container:**
```shell
/app # touch file.txt
```

**Host:**
```shell
/var/lib/docker/volumes/first_volume/_data# ls  # output: file.txt
```
> **Explanation:**
> + ottoman_container içerisnde `touch` komut ile *file.txt* dosyası oluşturduğumuzda gördüğünüz gibi belirtilen dizinde `ls` komut ile kontrol edildiğinde aynı dosyayı görebiliriz.


> [!NOTE]
> + `ottoman_container` container'ın içerisindeki `/app` klasöründe yapılan tüm işlemler  `/var/lib/docker/volumes/ottoman_volume/_data` dizininde etkili olacaktır.
> + Eğer `ottoman_container` silinse bile veriler `/var/lib/docker/volumes/ottoman_volume/_data` olduğu için veri kaybına neden olmayacaktır. Hata bu volume tekrardan başka container'a da bağlanabilir.

```shell
$ docker run --name ottoman_container2 -it -v ottoman_volume:/app2 alpine sh
```
> **Explanation:**
> + Daha önce oluşturmuş olduğumuz `ottoman_volume` volume'e yeni oluşturmuş olduğumuz `ottoman_container2` adında container bağlıyoruz.
> + Sonuç olarak `ottoman_volume` iki container bağlanmış oluyor. Hata bu iki container'ı da silip tekrardan yeni container oluşturduğumuzda `ottoman_volume`'deki verileri alırız.

### volume create:

###### Syntax:
+ **Usage:** `docker volume create [OPTIONS] [VOLUME]`
+ **Örnek:**  `docker volume create containerName`
+ **Karşılığı:** `[OPTIONS] => -v`, `CONTAINER => containerName`

```shell
$ docker 
```
### volume rm:
###### Syntax:
+ **Usage:** `docker volume rm [OPTIONS] VOLUME [VOLUME...]`
+ **Örnek:** `docker volume rm -f volumeName`
+ **Karşılığı:** `[OPTIONS] => -f`, `VOLUME => volumeName`

```shell
$ docker volume rm ottoman_volume
```
> **Explanation:**
> + `ottoman_volume` adındaki volume'ü siliyoruz.

### Bind Mount:

```shell
$ docker run --name ottoman -it -v ~/apps:/apps alpine sh
```
> **Explanation:**
> + HOST:  Yerel makinede `/apps` adında bir dizin oluşturuyoruz.
> + CONTAINER: container içerisinde  `/app` adında dizin oluşturmazsınız *Docker Engine* kendi oluşturacak.
> + Sonuç olarak yerel makinede(HOST) oluşturulan  ve container içerisinde oluşturulan dizineler arasında veri alış verişi gerçekleştirebiliyoruz.

|Özellik|Docker Volume|Bind Mount|
|---|---|---|
|**Yönetim**|Docker tarafından yönetilir|Host dosya sistemi tarafından yönetilir|
|**Depolama Konumu**|Docker'ın belirlediği bir konumda (örneğin `/var/lib/docker/volumes/`)|Host'taki belirli bir dizin veya dosya|
|**Kapsam**|Docker ortamına özel, konteyner yaşam döngüsünden bağımsız|Host dosya sistemiyle doğrudan bağlantılı|
|**Performans**|Docker tarafından optimize edilmiş|Platforma göre değişebilir, daha az optimize olabilir|
|**Paylaşılabilirlik**|Kolayca paylaşılabilir|Aynı dizin paylaştırılabilir, ancak dikkatli olunmalıdır|
|**Taşınabilirlik**|Taşınması kolay, Docker volume yedeklenebilir|Host dizinlerine bağlı olduğu için taşıması zor olabilir|
|**Güvenlik**|Daha güvenli, çünkü Docker Engine tarafından kontrol edilir|Host dosya sistemiyle doğrudan bağlı olduğundan daha riskli olabilir|
##### Hangi Durumda Hangi Yöntem Tercih Edilmeli?
- **Volume** kullanımı, konteynerlerinizi farklı platformlarda çalıştırmayı veya taşımayı planlıyorsanız daha iyi bir seçenektir. Ayrıca, veri güvenliği, kalıcılığı ve performans gereksinimleri için de uygundur.
- **Bind Mount** ise belirli bir host dosya sistemi ile sıkı entegrasyon gerektiğinde (örneğin, belirli bir dizindeki dosyalarla çalışmak) kullanışlıdır. Ancak güvenlik ve taşınabilirlik açısından dikkat edilmelidir.

## Network:
+ Docker'da **network** (ağ), konteynerlerin birbirleriyle ve dış dünya ile nasıl iletişim kuracağını belirleyen bir yapıdır.
+ Docker, her konteyneri izole bir ortamda çalıştırırken, konteynerler arası iletişimi sağlamak için ağ mekanizmaları kullanır.
+ Docker ağları, konteynerler arasında veri alışverişini yönetir ve dış dünyadan gelen trafiği düzenler.
+ Docker, farklı senaryolar için önceden yapılandırılmış birkaç ağ sürücüsü (network driver) sunar. Her sürücü, konteynerlerin nasıl bağlanacağını ve iletişim kuracağını belirler.
### Docker Network Türleri:

#### 1.Bridge Network:
+ *Varsayılan ağ türüdür. Eğer bir container oluşturulduğu zaman varsayılan olarak Bridge Network bağlanacaktır.*

> [!CAUTION]
> + Eğer varsayılan `bridge` oluşturduğunda container'lar birbirlerini çözümleyemiyorlar fakat
> + Eğer kullanıcı tarafından oluşturulmuş `bridge` container'ların birbirlerini çözülemesine izin veriyor. 

##### Varsayılan Ağ:
```shell
$ docker run --name default_network -it alpine sh
```
> **Explanation:**
> + Eğer `--network` parametresi yazılmazsa docker engine varsayılan olarak gelen `bridge` ağına bağlanacaktır.
> + `docker network ls` komut ile tüm docker ağını listeleyebilirsiniz.
> + Eğer container içerisinde `ip addr` veya `ifconfig` komutunu çalıştırsak container'ın IP'sini görebiliriz. 

```shell
$ docker network inspect -f '{{json .Containers}}' bridge | jq
```
> **Explanation:**
> + `-f` parametresi ile sadece *Containers* json verisini alıp `jq` komutuna yönlendiriyoruz.
> + Çıktıdan gördüğümüz üzere `default_network` adındaki container'ın IP'sini görebiliriz.
> + `js` paket kurulumu: `sudo apt install jq`

#### 2.Host Network:
+ Konteynerin(container) Docker ana bilgisayarıyla(Host) **aynı ağ yapısını** kullanmasını sağlar.
+ Bu durumda, konteyner ana bilgisayarın ağ arayüzünü kullanır ve kendi özel IP adresine sahip olmaz.
+ Performans açısından avantajlı olabilir, çünkü ağ katmanını atlayarak doğrudan ana bilgisayarın ağı kullanılır.
+ **Kapsamlı izolasyona gerek olmayan** durumlarda tercih edilir.

##### Örnek 1:
```shell
$ docker run --name host_network --network host nginx
```
> **Explanation:**
> + `--network host` parametresi ile ana makinenin(host) ara yüzünü(interface) kullanılması istenmektedir. Yani *docker engine* linux kernel'dan network namespace kullanımına izin vermeyecektir.
> + Docker’da `host` ağı, konteynerlerin doğrudan ana makinenin (host) ağına bağlanmasını sağlar. Bu sayede konteyner, ana makineyle aynı IP adresine sahip olur ve ağa doğrudan erişebilir.
> + `curl -X GET 192.168.1.134` veya tarayıcıda 192.168.1.134 ile GET isteği atığımızda direk nginx varsayılan ekranı gelecektir. Sanki docker container'ın içinde değil de ana makinede çalışıyor. 


```shell
$ docker network inspect host --format '{{json .Containers}}' | jq
```
> **Explanation:**
> + Bu komut ile host alanındaki contianer'ları teyit edebiliriz. `host_network` container'ı da orada göreceğiz. 
> + IP adresi yok çünkü ana makinenin ara yüzünü kullanıyor.



#### 3.Overlay Network:
+ **Küme (Swarm) modunda** birden fazla Docker daemon ana bilgisayarı (host) arasında iletişim sağlamak için kullanılır.
+ Docker Swarm veya Kubernetes gibi dağıtılmış sistemlerde, konteynerlerin farklı fiziksel sunucularda (node'larda) çalışsa bile aynı sanal ağdaymış gibi iletişim kurmasına olanak tanır.

#### 4.None Network:
+ Konteynerin(container) **herhangi bir ağa bağlanmamasını** sağlar.
+ Bu ağ türü, konteynerin izole bir şekilde çalışmasını ve diğer konteynerlerle veya dış dünya ile iletişim kurmamasını sağlar.

```shell
$ docker run -it --name none_network --network none alpine sh
```
> **Explanation:**
> + `none_network` adındaki container'ı `--network` parametresi ile `none` driver'ına bağlıyoruz.
> + Artık none_network container'ı ağ üzerinden dışarı ulaşamaz.
> + Açılan shell de `ip a` veya `ifconfig` komut ile baktığımızda sadece `lo` ara yüzü görünecektir.

```shell
$ docker network inspect none -f '{{json .Containers}}' | jq
```
> **Explanation:**
> + Bu komut ile hangi container'ların `none` sürücüsüne(driver) bağlı olduğunu görebiliriz.

#### 5.Macvlan Network:

### Docker network komutları:
#### 1.Network ls:
+ **Usage:** `docker network ls [OPTIONS]`
```shell
$ docker network ls
```
> **Explanation:**
> + Docker üzerinde mevcut olan ağları listelemek için kullanılır.
> + Bu komutu çalıştırdığınızda Docker'ın varsayılan ağları ve sizin oluşturduğunuz özel ağlar gösterilir.
> + Çıktıda her ağ için `NETWORK ID`, `NAME`, `DRIVER` ve `SCOPE` gibi bilgiler yer alır.
#### 2.Network inspect:

#### 3.Network create:
+ Docker’da özel bir ağ oluşturmak için kullanılan komuttur.
+ Bu komut sayesinde konteynerler arasında izole bir ağ ortamı yaratabilir, konteynerlerin güvenli bir şekilde birbiriyle iletişim kurmasını sağlayabilirsiniz.
##### Syntax:
+ **Usage:**  `docker network create [OPTIONS] NETWORK`

##### Örnek 1:
```bash
$ docker network create first_network
```
> **Explanation:**
> + `first_network` adında bir `bridge` ağ oluşturduk.
> + Eğer dikkat ederseniz `--driver` parametresini kullanmazsak *docker engine*  varsayılan olarak `bridge driver` kullanır.
> + `docker network ls` ile `first_network` ağın oluşturulup oluşturulmadığına bakabilirsiniz.

```shell
$ docker run --name web --hostname web --network first_network -it alpine sh
```

```shell
$ docker run --name database --hostname database --network first_network \
-it busybox sh
```
> **Explanation:**
> + 2 tane container oluşturduk ve her ikisi de aynı oluşturmuş olduğumuz ağı paylaşmaktadır.
> + Eğer dikkat ederseniz `--hostname` parametresi ile container'lar hostname'lerini belirli bir isim verdik.
> + Eğer web container'ın kabuğundan(shell) `ping database` ve database container'ın kabuğundan(shell) `ping web`  ile komutlarını çalıştırdığımızda ping atacaktır. Böylelikle iki container aynı ağda konuştuğunu görebiliriz.


```shell
$ docker network inspect first_network | jq
```
> **Explanation:**
> + Oluşturmuş olduğumuz `first_network` ağını yukarıdaki komut ile detaylarını inceleyebiliriz.
> + `jq` komut ile daha güzel çıktı veriyor.


> [!CAUTION]
> - `first_network` kendimiz oluşturduğumuz ve 2 container bağladığımız için bu iki contianer birbirlerini hostname'leri çözümleyebilecektir.
> - Docker engine ile varsayılan olarak gelen  brigde `hostname` çözümleme yoktur.

#### 4. Network connect:
##### Syntax:
+ **Usage:**  `docker network connect [OPTIONS] NETWORK CONTAINER`

##### Örnek 1:
```shell
$ docker run --name webserver --hostname webserver -itd alpine sh
```
> **Explnation:**
> + `--network` parametresini tanımlamadığımız için varsayılan olarak *docker engine* bridge adındaki ağı(network) verecektir

```shell
$ docker network create web_net
```
> **Explnation:**
> + `web_net` adında bir ağ(network) oluşturuyoruz. Tabi `--driver` parametresi kullanılmadığı için `web_net` sürücüsü(driver) `bride` olacaktır.

```shell
$ docker network connect web_net webserver
```
> **Explnation:**
> + Oluşturmuş olduğumuz `web_net` ağını(network) `webserver` adındaki container'a bağlıyoruz.

```shell
$ docker inspect webserver -f '{{json .NetworkSettings.Network}}'
```
> **Explnation:**
> + container'ın `inspect` komut ve `-f` parametresi ile süzersek 2 tane ara yüzün(interface) `webserver` container'ına bağlı olduğunu görebilirsiniz.

```shell
$ docker exec webserver ip addr
```
> **Explnation:**
> + Yine `exec` komut ile 2 tane ara yüzün(interface) bağlı olduğunu görebiliriz.

#### 5.Network disconnect:
##### Syntax:
+ **Usage:**  `docker network disconnect [OPTIONS] NETWORK CONTAINER`

##### Örnek 1:
+ Aşağıdaki işlemler **4.Network connect** devamı niteliğindedir.
```shell
$ docker network disconnect bridge webserver
```
> **Explnation:**
> + Yukarıda da gördüğün üzeri 2 tane ara yüzün(interface) webserver container'a bağlı olduğunu görebilirsiniz.
> + Bu komut ile `bridge` adındaki ağı(network) kaldırıyoruz.

```shell
$ docker inspect webserver -f '{{json .NetworkSettings.Network}}'
```
> **Explnation:**
> + Bu komut ile `bridge` adındaki ağın kaldırıldığını ve web_net kaldığını teyit edebiliriz.

```shell
$ docker exec webserver ip addr
```
> **Explnation:**
> + Yine bu komut ile de 1 tane ara yüzün(interface) kaldığını görebiliriz.

## Plugins

```shell
$ docker info --format "{{json Plugins}}"
```
> **Explanation:**
> + docker engine ile birlikte gelen eklentileri(plugins) listeler.


## Kaynak:
[Ayti Tech](https://www.youtube.com/watch?v=ACr92yZF0bg)
[Hızlandırılmış Docker Eğitimi - Part 2/2](https://www.youtube.com/watch?v=ty3s47TDjo4)
