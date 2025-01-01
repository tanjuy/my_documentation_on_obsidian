#docker #k8s 
### Kubernetes Nedir?
+ Kubernetes, konteynerleştirilmiş uygulamaların dağıtımını, ölçeklenmesini ve yönetimini otomatikleştirmek için kullanılan açık kaynaklı bir konteyner orkestrasyon motorudur.
+ Açık kaynaklı proje, Cloud Native Computing Foundation (CNCF) tarafından barındırılıyor.
+ Eğer CNCF'nin ne olduğunu açıklamak gerekirse, konteyner teknolojileri ve bulut yerel uygulamalarının geliştirilmesi ve yaygınlaştırılmasını destekleyen bir vakıftır.

### 1.Node:
+ **Node** (düğüm), Kubernetes kümesindeki bir fiziksel sunucu veya sanal makinedir.
+ Kubernetes kümesi (cluster) içinde her bir düğüm, üzerinde konteynerleri çalıştırarak iş yüklerini barındırır.
+ İki tür düğüm vardır:
	1. **Master Node**: Kubernetes kontrol düzlemini (control plane) çalıştırır. Kaynakları yönetir ve iş yüklerinin uygun düğümlerde dağıtılmasını sağlar.
	2. **Worker Node**: İş yüklerini taşıyan düğümdür ve kullanıcı uygulamalarını çalıştırır.

### 2.Master Node:
+ Master Node'un bir diğer adı Control plane olarak adlandırılır.
+ **Control Plane**, Kubernetes kümesinin "beyni"dir. Tüm node’ları, iş yüklerini ve kaynakları yönetir.
+ Kullanıcıdan gelen komutları ve talepleri işleyerek hangi konteynerlerin hangi node’larda çalışacağını belirler.
###### Control Plane Bileşenleri:
+ **API Server**: Kubernetes’in dış dünya ile iletişim kurduğu ana bileşendir. `kubectl` komutları ve diğer araçlar API Server üzerinden küme ile etkileşime geçer.
+ **etcd**: Tüm küme verilerinin saklandığı bir veritabanıdır. Kümenin durumuna ait bilgileri depolar.
+ **Controller Manager**: İş yükleri ve bileşenlerin durumunu izler ve gerektiğinde düzeltici işlemler yapar (örneğin, bir pod’un kapanması durumunda yeni bir pod başlatmak gibi).
+ **Scheduler**: Yeni oluşturulan pod’ları uygun node'lara yerleştirir.

#### 2.1.Controller Manager:
+ Controller Manager, Kubernetes'teki kontrol döngülerinin (controllers) toplandığı bir bileşendir.
+ Kontrol döngüleri, Kubernetes'in **"istenen durum" (desired state)** ile **"mevcut durum" (current state)** arasındaki farkı algılayıp bu farkı kapatmaya çalışmasını sağlar.
##### Controller:
+ Kubernetes'te bir **controller**, sürekli olarak kümenin mevcut durumunu izler ve bunu, kullanıcının belirttiği istenen duruma uydurmak için çalışır.
+ Controller Manager, birden fazla kontrol döngüsünü tek bir süreçte çalıştırarak, bu kontrol döngülerini etkin bir şekilde koordine eder.
##### Controller Manager'ın Görevleri:
1. **Replication Controller:** 
	+ Pod'ların istenen kopya sayısının çalışıp çalışmadığını kontrol eder.
	+ Eksik Pod'ları oluşturur ve fazla olan Pod'ları siller.
2. **Node Controller:**
	+ Düğümlerin(nodes) sağlık durumunu izler.
	+ Bir düğümün erişilemez olduğunu algılarsai bu düğümdeki Pod'ları başka düğümlerde yeniden planlar.
3. adsa

#### 2.2.Etcd:
+ Kubernetes (k8s) içinde **etcd**, Kubernetes'in **veri depolama** çözümüdür ve Kubernetes kümesinin tüm yapılandırma bilgilerini, kümedeki bileşenlerin durumunu, iş yüklerini ve daha fazlasını depolar.
+ **Dağıtık bir anahtar-değer veritabanı** olan etcd, Kubernetes'in kritik bir bileşenidir ve kümenin sağlıklı çalışması için önemlidir.
+ Etcd'in temel özellikleri şunlardır:
	1. **Dağıtık Depolama:** Etcd, yüksek erişilebilirlik ve veri bütünlüğünü sağlamak için birden fazla node üzerinde çalışır.
	2. **Konsensüs Sağlama:** Etcd, Raft protokolünü kullanarak küme içinde konsensüs sağlar. Bu sayede verilerin tutarlılığı garanti altına alınır.
	3. **Yüksek Performanslı Veri Erişimi:** Etcd hızlı okuma ve yazma işlemleri için optimize edilmiştir, bu da Kubernetes API'sinin hızlı yanıt vermesine olanak tanır.
	4. **Geri Yükleme ve Yedekleme:** Etcd, önemli bir veri kaynağı olduğu için düzenli olarak yedeklenmesi önerilir. Bir kümede sorun çıkarsa, etcd yedeklerinden geri yükleme yapılabilir



> [!IMPORTANT]
> + **Etcd cluster** birden fazla master veya control plane toplamından oluşur.
> + Lider(Leader) ve Takipçiler(Followers) etcd cluster arasında gerçeklerşir.

#### 2.3.API Server:
+ Kubernetes'te **API Server**, Kubernetes'in **merkezi kontrol bileşeni** ve iletişim merkezidir.
+ Tüm bileşenlerin ve kullanıcıların Kubernetes ile etkileşime geçmek için kullandığı API'yi sağlar.
+ Temel olarak, Kubernetes kümesiyle ilgili tüm CRUD (Create, Read, Update, Delete) işlemleri API Server üzerinden gerçekleştirilir.

##### API Server'un Görevi:
1. **API Sunma:**
	+ Kullanıcılar, geliştiriciler, `kubectl` komutları veya diğer Kubernetes bileşenleri (örn. Controller Manager, Scheduler) API Server'a HTTP REST çağrıları yaparak Kubernetes kümesine erişir.
2. **Doğrulama ve Yetkilendirme:**
	+ Gelen tüm istekleri doğrular ve bu isteğin yetkilendirilmiş olup olmadığını kontrol eder.
	+ Örneğin, bir kullanıcı bir Pod oluşturmak istediğinde, bu işlemin yetkilendirilip yetkilendirilmediğini kontrol eder.
3. **Etcd ile İletişim:**
	+ Kubernetes kümesindeki durum bilgisi **etcd** adlı dağıtılmış anahtar-değer deposunda saklanır.
	+ API Server, etcd ile iletişim kurarak kümenin durumunu okur ve günceller.
4. **Diğer Bileşenlerle Haberleşme:**
	+ Controller Manager, Scheduler gibi Kubernetes bileşenleri, kümenin durumunu anlamak ve güncellemeler yapmak için API Server ile iletişim kurar.
5. **Durum Yönetimi:**
	+ Kubernetes'teki istekler genellikle istenen durumun belirtilmesiyle ilgilidir (örn. "3 adet Pod çalıştır").
	+ API Server bu istekleri alır ve kümenin gerçek durumunu bu istenen durumla uyumlu hale getirmek için diğer bileşenlere yönlendirir.

##### API Server Çalışma Prensibi:
+ Kubernetes API Server'ın **çalışma prensibinde**, bir istemciden (örneğin `kubectl`, REST API veya başka bir araç) gelen bir istek, **Authentication**, **Authorization** ve **Admission Control** adımlarından geçerek işlenir.
+ Bu aşamalar, güvenliği ve küme yönetiminin düzenini sağlar. 
###### 1.Authentication (Kimlik Doğrulama):
**Nedir?**
+ Kullanıcının veya istemcinin **kim olduğunu doğrulama** işlemidir. İstemcinin API Server'a gönderdiği isteğin kimden geldiğini belirlemek için yapılır.
---
**Nasıl Çalışır?**
+ Kullanıcı veya istemci, bir kimlik doğrulama mekanizması aracılığıyla kendini tanıtır. Bu genellikle bir **token**, **sertifika** veya **kullanıcı adı ve parola** kullanılarak yapılır.
+ API Server, kimlik doğrulama bilgilerini belirli bir mekanizmaya yönlendirerek doğrular.
---
**Desteklenen Mekanizmalar:**
+ **x509 Sertifikaları:** Kullanıcı kimliğini TLS sertifikaları ile doğrular.
+ **Service Account Token:** Kubernetes içindeki Pod'lar, bu yöntemle kimlik doğrulaması yapar.
+ **Bearer Token:** API isteklerinde taşıyıcı jeton (bearer token) kullanılır.
+ **OIDC (OpenID Connect):** Harici kimlik sağlayıcılarla entegrasyon yapılır.
---
 **Sonuç:**
+ Eğer kimlik doğrulama başarısız olursa, istek **reddedilir** ve süreç burada sona erer.
+ Başarılı olursa, istemcinin kimliği (örn. kullanıcı adı) sonraki adıma geçirilir.
###### 2.Authorization (Yetkilendirme):
**Nedir?**
+ Kimliği doğrulanan kullanıcının **belirli bir eylemi gerçekleştirme yetkisi olup olmadığını kontrol etme** işlemidir.
---
**Nasıl Çalışır?**
+ Yetkilendirme, istemcinin API Server'da yapmak istediği işlemi (örneğin, bir Pod oluşturma) kontrol eder.
+ API Server, bu isteği yetkilendirme mekanizmalarına iletir ve izin alır ya da reddeder.
---
**Yetkilendirme Mekanizmaları:**
+ **RBAC (Role-Based Access Control):** Kubernetes'te en yaygın kullanılan mekanizma. Kullanıcılar, roller (roles) ve rollerin bağlamları (bindings) ile yönetilir.
+ **ABAC (Attribute-Based Access Control):** İzinler bir JSON dosyasına dayalı olarak atanır.
+ **Webhook:** Harici bir yetkilendirme sistemine API çağrısı yapılarak izin kontrol edilir.
---
**Sonuç:**
+ Yetkilendirme başarısız olursa, istek **reddedilir** ve süreç sona erer.
+ Başarılı olursa, istek Admission Control'e iletilir.
###### 3.Admission Control (Giriş Kontrolü):
**Nedir?**
+ İsteğin küme politikalarına uygun olup olmadığını kontrol eder ve gerektiğinde isteği değiştirir veya reddeder.
---
**Nasıl Çalışır?**
+ Admission Control, **admission plugins** adı verilen bir dizi modül aracılığıyla çalışır. Bu eklentiler, isteğin kabul edilip edilmeyeceğine karar verir.
+ Bazı eklentiler isteği **değiştirebilir** (örneğin, bir varsayılan değer eklemek), bazıları ise isteği sadece **doğrular**.
**Örnek Admission Plugins:**
+ **NamespaceLifecycle:** Kapatılmış bir namespace'e istek yapılmasını engeller.
+ **LimitRanger:** Namespace'teki kaynak kullanım sınırlarını kontrol eder.
+ **PodSecurityPolicy:** Pod'ların güvenlik politikalarına uygun olup olmadığını kontrol eder.
+ **MutatingAdmissionWebhook ve ValidatingAdmissionWebhook:** Harici webhook'larla entegrasyon sağlar.
---
**Sonuç:**
+ Eğer Admission Control isteği reddederse, istek işlenmez.
+ Kabul edilirse, istek etcd'ye kaydedilir ve işlem tamamlanır.


#### 2.4.Kube-schedular:
+ Scheduler, yeni oluşturulan ve bir düğüme atanmayı bekleyen Pod'lar için uygun bir düğüm (node) seçer.
+ Bu seçim, çeşitli kriterlere (kaynak durumu, etiketler, kısıtlamalar vb.) ve politika kurallarına göre yapılır.
+ Örneğin, bir Deployment ile bir uygulamanın 3 kopyasının çalıştırılmasını istediğinizde, Controller Manager bu kopyaları çalıştırır ve çalışmadığı durumlarda tekrar başlatır.

### 3.Worker Node:
#### 3.1.Kubelet:

#### 3.2.Kube proxy:

#### 3.3.CRI:

#### 3.4.Pod:


### 3.Cluster:
+ Kubernetes'te **cluster** (küme), dağıtılmış bir uygulama ortamını oluşturmak için bir araya gelen bir dizi node'dan (düğüm) oluşur.
+ Cluster, **Control Plane** (kontrol düzlemi) ve **Worker Nodes** (işçi düğümleri) olarak iki ana bileşenden oluşur.

##### Worker Nodes:
+ Worker node'lar, uygulama konteynerlerini çalıştıran fiziksel veya sanal sunuculardır.
+ Her bir worker node, iş yüklerini taşır ve kümedeki diğer node'larla birlikte çalışarak uygulamanın ölçeklenebilirliğini ve dayanıklılığını sağlar.
###### Worker Node Bileşenleri:
+ **Kubelet**: Node’da çalışan bir Kubernetes agent’ıdır. Pod’ların durumunu API Server’a bildirir ve node üzerindeki pod’ları yönetir.
+ **Kube-proxy**: Küme içindeki ağ iletişimini ve servislerin yönlendirmesini sağlar.
+ **Container Runtime**: Konteynerleri çalıştırmak için kullanılan yazılımdır. Docker, containerd veya CRI-O gibi çeşitli runtime’lar olabilir.

###### Kubernetes Cluster'ın Amacı ve Avantajları:
+ **Yüksek Erişilebilirlik(High Availability) ve Dayanıklılık**: Cluster, iş yüklerini birden fazla node’a dağıttığı için uygulama kesintilerini önler. Bir node kapanırsa, diğer node'lar iş yükünü devralır.
+ **Otomatik Ölçeklendirme**: İhtiyaç durumunda yeni pod'lar başlatılarak iş yükleri otomatik olarak ölçeklendirilir.
+ **Kaynak Yönetimi ve İzleme**: Control plane bileşenleri sayesinde kaynakların yönetimi yapılır ve sistemin her zaman güncel bir durumu saklanır.
### K8s Bileşenleri:

#### 3.Namespace:
+ **Namespace** (ad alanı), Kubernetes'te kaynakları izole etmek ve gruplandırmak için kullanılır.
+ Özellikle, aynı kümede farklı ekiplerin veya projelerin bağımsız olarak çalışmasına olanak tanır.
+ Kubernetes, küme düzeyinde bazı varsayılan ad alanlarına sahiptir (`default`, `kube-system`, `kube-public`), ancak kullanıcılar özel ad alanları da oluşturabilir.

#### 4.ReplicaSet:
+ **ReplicaSet**, bir pod’un belirli sayıda kopyasını (replikasını) çalıştıran bir birimdir. Pod’ları belirli bir sayıda tutarak yüksek erişilebilirlik(**High Availability**) sağlar.
+ Eğer bir pod kapanırsa, ReplicaSet eksik pod sayısını tamamlamak için otomatik olarak yeni pod’lar başlatır.

#### 5.Deployment:
+ **Deployment**, iş yüklerinin düzenli ve sürdürülebilir bir şekilde dağıtılmasını sağlar.
+ Bir uygulamanın güncellenmesini, ölçeklendirilmesini ve gerektiğinde eski sürümlere dönülmesini kolaylaştırır.
+ Deployment, arka planda bir ReplicaSet yönetir, bu da pod’ların sayısını kontrol altında tutar ve dağıtımları yönetir.

#### 6.Service:
+ **Service**, pod’lar arasındaki iletişimi ve dış erişimi yönetmek için kullanılan bir yapı birimidir. Pod’ların IP adresleri değişebilir, bu yüzden Service, pod’ların IP adreslerinden bağımsız bir erişim sunar.
+ Farklı tipte servisler vardır:
	1. **ClusterIP**: İç erişim sağlar (dışa kapalıdır).
	2. **NodePort**: Belirli bir port üzerinden dışarıdan erişim sağlar.
	3. **LoadBalancer**: Bulut ortamında yük dengeleyici sağlar.
	4. **ExternalName**: Harici DNS adlarını çözümlemek için kullanılır.
#### 7.ConfigMap ve Secret:
+ **ConfigMap** ve **Secret**, pod’lar için yapılandırma bilgilerini saklar. Uygulamaların çalışma zamanı yapılandırmalarını çevresel değişkenler veya dosyalar olarak sağlar.
+ ConfigMap, yapılandırma bilgilerini düz metin olarak saklarken, Secret, hassas bilgileri şifreli bir şekilde tutar.

#### 8.Volume:
+ **Volume**, konteynerlerin dosya sistemini paylaşmasını veya veri depolamasını sağlamak için kullanılan birimdir. Bir pod’da çalışan konteynerler bir volume’a erişebilir.
+ Farklı türde volume’lar vardır; örneğin, `emptyDir`, `hostPath`, `persistentVolumeClaim`, `nfs`.

#### 9.PersistentVolume (PV) ve PersistentVolumeClaim (PVC):
+ **PersistentVolume (PV)**: Kalıcı depolama sağlayan bir kaynak birimidir. Depolama genellikle harici bir kaynaktan (bulut depolama, ağ dosya sistemi gibi) gelir.

#### Raft Algoritması:

+ Kubernetes'te **etcd**, kümenin yapılandırma verilerini ve durum bilgilerini saklayan bir dağıtık veri deposudur.
+ **Raft algoritması**, etcd'nin veri tutarlılığını ve hata toleransını sağlamak için kullandığı konsensüs mekanizmasıdır.
##### etcd'de Raft Algoritması Nasıl Çalışır?
+ **Raft algoritması**, etcd'deki düğümlerin (nodes) birbiriyle uyumlu çalışmasını ve aynı veriyi paylaşmasını sağlar.
+ Bu, özellikle dağıtık bir ortamda, düğümler arasında veri tutarlılığını garanti eder. İşleyiş şu şekilde özetlenebilir:
###### 1.Lider ve Takipçiler:
+ *Lider(Leader):*
	+ Raft, her zaman bir lider düğüm seçer.
	+ Tüm yazma (write) işlemleri lider düğüm üzerinden gerçekleştirilir.
	+ Lider, diğer düğümlerle sürekli iletişim kurarak liderliğini sürdürür.
+ *Takipçiler (Followers):*
	+ Liderin gönderdiği talimatları (log girişlerini) alır ve uygular.
	+ Eğer lider başarısız olursa, takipçilerden biri yeni lider olmak için aday olur.
###### 2.Log Replicasyonu:
+ Lider düğüm, bir yazma isteği aldığında bunu kendi log'una ekler ve diğer düğümlere çoğaltır.
+ Diğer düğümler (takipçiler), log girişini onayladıktan sonra işlem kesinleşir (committed state).
+ Çoğunluk sağlandığında işlem tamamlanmış kabul edilir.
###### 3.Lider(Leader) Seçimi:
+ Eğer mevcut lider başarısız olursa (örneğin ağ bağlantısı kesildiğinde veya çöktüğünde):
	1. Takipçiler belirli bir süre liderden mesaj almazsa (heartbeat), liderin başarısız olduğunu varsayar.
	2. Bir takipçi, lider olmak için aday olur ve diğer düğümlerden oy ister.
	3. Oyların çoğunluğunu alan düğüm yeni lider olur.
###### 4.Tutarlılık Garantisi:
+ Raft, **katı tutarlılık** (strong consistency) sağlar.
+ Lider, yalnızca çoğunluğun onayladığı log girişlerini kesinleştirir. Bu, düğümlerden biri başarısız olduğunda bile verinin tutarlı kalmasını sağlar.
##### Raft ve etcd'nin Avantajları Kubernetes'te Neler Sağlar?
1. **Veri Tutarlılığı:** Raft, verilerin tüm etcd düğümlerinde aynı olmasını sağlar.
2. **Hata Toleransı:** Etcd kümesinde düğümlerden biri veya birkaçı başarısız olsa bile, çoğunluk çalıştığı sürece küme işlevselliğini korur.
3. **Yüksek Erişilebilirlik:** Etcd, Raft sayesinde birden fazla düğümde dağıtılarak sürekli kullanılabilir bir yapı sunar.
4. **Küme Yönetimi:** Kubernetes'in tüm yapılandırma ve durum bilgileri etcd'de saklandığı için, Raft'ın sağladığı bu güvenilirlik ve tutarlılık Kubernetes'in sorunsuz çalışması için kritiktir.

##### Kubernetes'te etcd ve Raft'ın Önemi
+ Kubernetes API sunucusu (kube-apiserver), etcd'ye doğrudan bağlıdır.
+ Tüm cluster bilgileri, pod'ların durumu, node bilgileri ve yapılandırmalar etcd'de saklanır.
+ Tüm küme, tek bir lider düğüm üzerinden senkronize çalışır, bu da yönetimi kolaylaştırır.

### Yönetim Araçları:
#### Kubectl:

#### Openshift:

#### Kdash:
+ Resmi [Sitesi](https://github.com/kdash-rs/kdash) 
### Docker, Podman, Containerd ve LXC/LXD Farkları:

| Özellik                | Docker                             | Podman                             | containerd            | LXC/LXD                                 |
| ---------------------- | ---------------------------------- | ---------------------------------- | --------------------- | --------------------------------------- |
| **Daemon**             | Var (Docker Daemon)                | Yok                                | Yok                   | Yok                                     |
| **Root'suz Kullanım**  | Rootless Docker (sonradan eklendi) | Daha iyi rootless desteği          | N/A                   | Kısmen                                  |
| **Kapsam**             | Geniş kapsam (Docker CLI, API)     | Docker alternatifi, CLI benzerliği | Yalnızca runtime      | Tam sistem bazlı konteynerler           |
| **Kullanım Alanı**     | Geliştirme ve dağıtım              | Güvenli konteyner çalıştırma       | Kubernetes ile uyumlu | Tam teşekküllü Linux OS'leri çalıştırma |
| **Performans**         | Yüksek                             | Yüksek                             | Çok yüksek            | Yüksek (daha fazla kaynak kullanabilir) |
| **Kullanım Kolaylığı** | Kolay                              | Kolay                              | Orta                  | Zor                                     |

###### 1.Docker:
+ **Docker**, en popüler konteyner platformlarından biridir. Uygulamaları ve bağımlılıklarını bir arada paketleyip çalıştırmak için bir platform sunar.
+ Docker ile, konteynerleri oluşturmak, dağıtmak ve yönetmek kolaydır. Docker, varsayılan olarak Docker Engine üzerine kurulu olup, `containerd` adlı bir arka plandan yararlanır.
+ **Avantajları**: Kapsamlı dokümantasyonu, geniş ekosistemi ve Docker Hub üzerinden kolay erişilebilir konteyner imajları.
+ **Mimari**: Docker Engine, containerd (konteyner runtime) ve runc (standart Linux container runtime) bileşenlerinden oluşur.

###### 2.Podman:
+ **Podman** ise Docker'a benzer bir yapıdadır, ancak en büyük farkı, arka planda çalışan bir arka plan sürecine (`daemon`) ihtiyaç duymamasıdır.
+ Podman, özellikle root'suz (rootless) konteyner çalıştırma yeteneği ile Docker’dan ayrılır.
+ **Avantajları**: Daha güvenli yapı sunar, Docker komutlarıyla büyük ölçüde uyumludur ve root'suz çalıştırmaya daha uygun bir mimariye sahiptir.
+ **Mimari**: `Daemon` gerektirmeyen doğrudan bir çalıştırma yapısına sahiptir. Varsayılan olarak `containerd` kullanmaz.
+ **Kullanım Alanları**: Özellikle güvenlik açısından daha esnek ve yönetimsel anlamda Docker'dan bağımsız bir seçenek arayanlar tarafından tercih edilir.

###### 3. Containerd:
+ **Containerd**, Docker'ın temel bileşenlerinden biri olarak başlamış bir konteyner runtime katmanıdır. 
+ Başlıca görevi, konteynerlerin yaşam döngüsünü (oluşturma, çalıştırma, durdurma) yönetmektir.
+ Docker Engine içinde yer alır, ancak Docker dışındaki projelerde de bağımsız olarak kullanılabilir.
+ **Avantajları**: Hafif ve hızlıdır, Kubernetes gibi orchestrator'lar ile uyumlu çalışır.
+ **Mimari**: Daha düşük seviyede çalışan bir `runtime` sağlayarak konteynerleri `runc` gibi daha düşük seviye runtime’larla entegre eder.
+ **Kullanım Alanları**: Genellikle Kubernetes gibi orchestrator'larla birlikte, performansı ve stabilitesi nedeniyle tercih edilir.
###### 4.LXC/LXD:
+ **LXC** (Linux Containers), konteynerizasyonun temelini atan teknolojilerden biridir.
+ LXC, kullanıcı alanında çalışan izole edilmiş Linux sistemleri yaratır ve geleneksel sanallaştırmaya oldukça benzerdir.
+ **LXD**, LXC'nin genişletilmiş bir versiyonudur ve bir yönetim katmanı ekleyerek LXC konteynerlerinin daha rahat yönetilmesini sağlar.
+ **Avantajları**: Daha sistem tabanlı konteynerler (sanal makinelere benzer), tam teşekküllü Linux işletim sistemleri oluşturmak için uygundur.
+ **Mimari**: LXC/LXD, konteynerleri daha çok VM gibi çalıştırır ve belirli sistem kaynaklarına izole erişim sağlar
+ **Kullanım Alanları**: Daha çok tam işletim sistemi simülasyonları için; özellikle sistem seviyesinde izole bir ortam gerektiğinde.


### 2.Geliştrme Ortamında:
**Kaynak:** [Resmi Sitesi](https://kubernetes.io/docs/tasks/tools/)

### Kaynaklar:
1.Kubernetes Resmi [Sitesi](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)