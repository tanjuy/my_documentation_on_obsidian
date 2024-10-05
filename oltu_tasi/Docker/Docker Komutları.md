#### Kernel Namespace:

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
#### Docker Engine


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

#### Docker Engine Kurulumu:

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

#### ps:
```shell
$ docker ps
```
> **Explanation:**
>  Container'ları listeler

```shell
$ docker ps -a
```
> **Explanation:**


#### Kaynak:
[Ayti Tech](https://www.youtube.com/watch?v=ACr92yZF0bg)
