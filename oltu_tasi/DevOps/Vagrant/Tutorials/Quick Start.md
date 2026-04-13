+ Vagrant, sanal makine yaşam döngüsünü (oluşturma, başlatma, durdurma, silme vb.) yönetir ve bağımlılıkları standardize edilmiş ve geçici (disposable) bir geliştirme ortamı içerisinde izole eder.

# Vagrant ile geliştirme ortamları nedir?

> **Çevrilen Site:** Developer / Vagrant / Tutorials / Quick Start / [What are development environment](https://developer.hashicorp.com/vagrant/tutorials/get-started/development-environment)

+ Geliştirme ortamları; kod yazmak, test etmek ve hata ayıklamak için tutarlı kurulumlar(*setups*) sağlar.
+ Yapılandırma sapması (configuration drift) ve bağımlılık sorunları gibi zorlukları çözerken, güvenilirlik ve taşınabilirlik sağlayarak ekiplerin daha etkili bir şekilde iş birliği yapmasına yardımcı olurlar.


> [!IMPORTANT]
> + Vagrant, geliştirici ortamlarını oluşturmayı ve yönetmeyi basitleştiren bir **HashiCorp** aracıdır.

+ Ana makine (*host machine – yerel bilgisayarınız*) ile misafir makine (*guest machine – sanal ortam*) arasında köprü kurarak sorunsuz entegrasyon sağlar.
+ **Vagrantfile** adı verilen yapılandırma dosyalarını kullanarak kurulum ve yapılandırma sürecini otomatikleştirir; böylece ekipler ortam yönetimi yerine geliştirme sürecine odaklanabilir.

> [!NOTE]
> Vagrant, sanal ortamınızı manuel olarak yapılandırmaya kıyasla birçok avantaj sunar:
> + Vagrant, tutarlı ve yeniden üretilebilir ortamlar sağlar. Bu sayede “benim makinemde çalışıyor” sorununu azaltır ve daha sorunsuz bir ekip çalışması mümkün kılar.
> + Vagrant ortamları taşınabilir ve paylaşılabilirdir; ekiplerin projeler ve altyapılar arasında kurulumları verimli şekilde çoğaltmasına olanak tanır.(**Taşınabilirlik**)
> + Vagrant, alttaki sanallaştırma araçlarıyla etkileşimi kolaylaştırır; sürümleri tespit eder ve doğru parametreleri (flags) uygular. Böylece ekip üyeleri aynı sağlayıcının(virtualbox, VMware, Docker, vb.) farklı sürümlerini kullansa bile tutarlı davranış elde edilir. Senkronize klasörler (synced folders), otomatik ağ yapılandırması ve HTTP tünelleme gibi özelliklerle geliştirme iş akışlarını iyileştirir.

+ Vagrant; VirtualBox, VMware, Docker ve diğer sağlayıcılarla çalışır. Böylece altyapı ve uygulama gereksinimlerinize uygun ortamları esnek biçimde oluşturmanıza imkân tanır.

## Geliştirme İş Akışınızı Akıcı Hale Getirin

+ Vagrant, geliştirme ortamlarını tanımlamak ve yönetmek için tutarlı bir iş akışı sunar.
+ Bu iş akışının merkezinde yer alan **Vagrantfile**, işletim sistemi, yazılımlar ve yapılandırmalar da dahil olmak üzere ortamınızı tanımlayan bir plan (blueprint) görevi görür.


> [!TIP]
> ##### Teknik Terim:
> Blueprint = Kurulum ve yapılandırma sürecini tarif eden standartlaştırılmış teknik plan.



> [!NOTE]
> Standart Vagrant iş akışı şu adımlardan oluşur:
> + **Scope (Kapsam Belirleme)** – Geliştirme ortamınız için gereksinimleri belirleyin; örneğin işletim sistemi, araçlar ve bağımlılıklar.
> + **Author (Yazma/Oluşturma)** – Ortamınızı tanımlamak için Vagrantfile dosyasını yazın.
> + **Manage (Yönetme)** – Ortamları başlatmak, durdurmak ve silmek için Vagrant komutlarını kullanın.
> + **Share (Paylaşma)** – Tutarlı kurulumlar sağlamak amacıyla Vagrantfile dosyasını veya paketlenmiş bir box’ı ekibinizle paylaşın.


> [!TIP]
> ##### Teknik Terim:
> Box = İçinde hazır bir işletim sistemi bulunan ve Vagrant’in kullanarak yeni ortam oluşturduğu temel VM imajı.

## Sonraki Adımlar

+ Geliştirme ortamlarının avantajlarını ve Vagrant'ın bu ortamların yönetimini nasıl basitleştirdiğini artık anladığınıza göre, ilk ortamınızı tanımlamaya hazırsınız.
+ Bu eğitim serisinde, bir web uygulaması için temel bir ortam oluşturarak başlayacak; Vagrant ile bir geliştirme ortamı inşa edip yöneteceksiniz.
+ Vagrant'ı yerel makinenize kurmak için bir sonraki eğitimle devam edin.

# Vagrant Kurulumu

> **Çevrilen Site:** [Developer](https://developer.hashicorp.com/) / [Vagrant](https://developer.hashicorp.com/vagrant) / [Tutorials](https://developer.hashicorp.com/vagrant/tutorials) / [Quick Start](https://developer.hashicorp.com/vagrant/tutorials/get-started) / [Install Vagrant](https://developer.hashicorp.com/vagrant/tutorials/get-started/install)

+ Vagrant’i kullanmak için sisteminize kurmanız gerekir. HashiCorp, Vagrant’i [binary dağıtım paketi](https://developer.hashicorp.com/vagrant/install) olarak sunar. Bunun yanında, Vagrant popüler paket yöneticileri aracılığıyla da kurulabilir.

## İkilik Dosyayı(Binary) Kurulumu

+ Önceden derlenmiş (pre-compiled) bir binary indirerek **vagrant** binary dosyasını temin edin. Vagrant’i kurmak için sisteminize uygun paketi bulun ve zip arşivi olarak indirin.
+ Vagrant’i indirdikten sonra paketi açın (unzip). Vagrant, **vagrant** adlı tek bir binary dosya olarak çalışır. Paket içindeki diğer dosyaları güvenle silebilirsiniz; Vagrant çalışmaya devam edecektir.
+ Son olarak, `vagrant` binary dosyasının **PATH** (sistem yolu) üzerinde tanımlı olduğundan emin olun. Bu işlem, kullandığınız işletim sistemine göre farklılık gösterecektir.

### A. Mac veya Linux

+ PATH değişkeninizde bulunan konumların iki nokta (:) ile ayrılmış listesini görüntüleyin.

```shell
$ echo $PATH
```

+ Vagrant binary dosyasını listelenen konumlardan birine taşıyın.
+ Bu komut(aşağıdaki komut), dosyanın şu anda indirilenler (Downloads) klasörünüzde olduğunu ve PATH listenizin `/usr/local/bin` dizinini içerdiğini varsayar; ancak kendi konumlarınız farklıysa komutu özelleştirebilirsiniz.

```bash
mv -v ~/Downloads/vagrant /usr/local/bin/
```

+ İkilik dosyaları (binaries) sistem yolunuza (PATH) ekleme hakkında daha fazla ayrıntı için bu [Stack Overflow makalesine](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix) göz atın.

### B. Windows

+ Bu [Stack Overflow makalesi](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows), Windows’ta PATH ortam değişkeninin kullanıcı arayüzü üzerinden nasıl ayarlanacağına dair talimatlar içermektedir.

## Kurulum Doğrulama

+ Yeni bir terminal oturumu açarak ve Vagrant’in kullanılabilir alt komutlarını listeleyerek kurulumun başarılı olup olmadığını doğrulayın.

```
$ vagrant --help
Usage: vagrant [options] <command> [<args>]

    -h, --help                       Print this help.

Common commands:
     autocomplete    manages autocomplete installation on host
     box             manages boxes: installation, removal, etc.
     cloud           manages everything related to Vagrant Cloud
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login           
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     serve           start Vagrant server
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     upload          upload to machine via communicator
     validate        validates the Vagrantfile
     version         prints current and latest Vagrant version
     winrm           executes commands on a machine via WinRM
     winrm-config    outputs WinRM configuration to connect to the machine

For help on any individual command run `vagrant COMMAND -h`

Additional subcommands are available, but are either more advanced
or not commonly used. To see all subcommands, run the command
`vagrant list-commands`.
        --[no-]color                 Enable or disable color output
        --machine-readable           Enable machine readable output
    -v, --version                    Display Vagrant version
        --debug                      Enable debug output
        --timestamp                  Enable timestamps on log output
        --debug-timestamp            Enable debug output with timestamps
        --no-tty                     Enable non-interactive output
```

+ Bir alt komutun ne işe yaradığını ve hangi seçenekleri sunduğunu görmek için `vagrant --help` komutunu ilgili alt komutla birlikte kullanın.

```
$ vagrant up --help
Usage: vagrant up [options] [name|id]
Options:
        --[no-]provision             Enable or disable provisioning
        --provision-with x,y,z       Enable only certain provisioners, by type or by name.
        --[no-]destroy-on-error      Destroy machine if any fatal error happens (default to true)
        --[no-]parallel              Enable or disable parallelism if provider supports it
        --provider PROVIDER          Back the machine with a specific provider
        --[no-]install-provider      If possible, install the provider if it isn't installed
        --[no-]color                 Enable or disable color output
        --machine-readable           Enable machine readable output
    -v, --version                    Display Vagrant version
        --debug                      Enable debug output
        --timestamp                  Enable timestamps on log output
        --debug-timestamp            Enable debug output with timestamps
        --no-tty                     Enable non-interactive output
    -h, --help                       Print this help
```

+ Eğer binary dosyasının bulunamadığına dair bir hata alırsanız, büyük olasılıkla PATH ortam değişkeninizi doğru şekilde yapılandırmamışsınızdır. PATH değişkeninizin, Vagrant’i kurduğunuz dizini içerdiğinden emin olun.

## Sonraki Adımlar

+ Artık Vagrant’i yerel sisteminize kurduğunuza göre, ilk `Vagrantfile` dosyanızı yazmak ve Vagrant ile geliştirme ortamınızı oluşturmak için bir sonraki eğitime geçin.

# Geliştirme Ortamının Kurulumu

>  [Developer](https://developer.hashicorp.com/) / [Vagrant](https://developer.hashicorp.com/vagrant) / [Tutorials](https://developer.hashicorp.com/vagrant/tutorials) / [Quick Start](https://developer.hashicorp.com/vagrant/tutorials/get-started) / [Set up environment](https://developer.hashicorp.com/vagrant/tutorials/get-started/setup-project)

+ Vagrant kurulduğuna göre artık ilk geliştirme ortamınızı oluşturmaya hazırsınız.
+ Bu eğitimde, bir `Vagrantfile` oluşturacak, ilk Vagrant ortamınızı kuracak ve Vagrant yaşam döngüsünü keşfedeceksiniz.

## Ön Gereksinimler

+ Bu eğitimi takip edebilmek için şunlara ihtiyacınız vardır:
	- Bilgisayarınızda yerel olarak kurulu [Vagrant CLI](https://developer.hashicorp.com/vagrant/tutorials/get-started/install-cli) (Komut Satırı Arayüzü).
	- Sanallaştırma sağlayıcısı (virtualization provider) olarak kurulu [VirtualBox 7.1.4](https://www.virtualbox.org/wiki/Downloads)

> [!WARNING]
> Eğer **Apple Silicon** (M1/M2/M3 çipli) bir macOS kullanıyorsanız, aşağıdaki VirtualBox global ayarını devre dışı bırakmanız (unset) gerekebilir. Bu ayar, Apple Silicon üzerinde sanal makine başlatırken sorunlara yol açabilir.
> ```shell
>  $ VBoxManage setextradata global "VBoxInternal/Devices/pcbios/0/Config/DebugLevel"
> ```


> [!TIP]
> Bu eğitimlere ait yapılandırmanın (konfigürasyonun) tamamını **[Learn Vagrant Get Started](https://github.com/hashicorp-education/learn-vagrant-get-started)** GitHub deposunda bulabilirsiniz. Bu eğitime özel nihai yapılandırma, **01.Vagrantfile** dosyasında yer almaktadır.

+ Vagrant projeniz için bir dizin oluşturun.

```shell
mkdir learn-vagrant-get-started
```

+ Dizine geçiş yapın.

```shell
cd learn-vagrant-get-started
```

## Yeni Bir Vagrant Ortamı Başlatma

+ Vagrant, bir projeyi başlatmak için `vagrant init` adında yerleşik bir komuta sahiptir; bu komut argüman olarak bir "box" (kutu/kalıp) adı ve URL alabilir. Dizini başlatın ve `hashicorp-education/ubuntu-24-04` box'ını belirtin.

```shell
$ vagrant init hashicorp-education/ubuntu-24-04 --box-version 0.1.0
Bu dizine bir `Vagrantfile` yerleştirildi. Artık ilk sanal ortamınızı 
`vagrant up` komutuyla ayağa kaldırmaya hazırsınız! Vagrant kullanımı 
hakkında daha fazla bilgi için lütfen Vagrantfile içindeki yorumları 
ve `vagrantup.com` adresindeki dokümantasyonu okuyun.
```

> [!TIP]
> ##### Box adı:
> ```shell
> hashicorp-education/ubuntu-24-04
> ```
> Anlamı:
> + `hashicorp-education` → box’ı yayımlayan organizasyon
> + `ubuntu-24-04` → box’ın adı
> 
> Yani bu ifade, **HCP Vagrant Registry** üzerinde kayıtlı bir box kimliğidir.
> ---
> ##### Sürüm(Version)
> Bu kısım box’ın **sürüm numarasını** belirtir.
> ```shell
> --box-version 0.1.0
> ```
> + Burada `0.1.0` box’ın versiyonudur.
> + Bu parametreyi vermezseniz, Vagrant genellikle en güncel sürümü indirir.

+ Bu komut, belirtilen box'ı [HCP Vagrant Registry](https://portal.cloud.hashicorp.com/vagrant/discover)'den alır ve dizininizde bir `Vagrantfile` oluşturur.
+ `Vagrantfile;` projenizi çalıştırmak için ihtiyaç duyduğunuz makine türünü ve kaynakları, yüklenecek yazılımları ve bunlara nasıl erişmek istediğinizi tanımlar.
+ Ayrıca projenizin **kök dizinini** işaretler. Vagrant'taki yapılandırma seçeneklerinin çoğu bu kök dizine göre belirlenir.

> [!info]
> #### Yapılandırmanın Bu Dizine Göre Belirlenmesi
> Vagrant'ın en güçlü özelliklerinden biri olan **Paylaşılan Klasörler (Synced Folders)** bu mantıkla çalışır.
> + **Otomatik Eşleme:** Vagrant, bilgisayarınızdaki bu kök dizini (Vagrantfile'ın olduğu yer), sanal makinenin içindeki `/vagrant` diziniyle otomatik olarak eşleştirir. Yani bilgisayarınızda o klasöre bir dosya attığınızda, anında sanal makinenin içinde de görünür.
> + **Göreceli Yollar (Relative Paths):** Vagrantfile içinde bir dosya yolu belirttiğinizde (örneğin bir kurulum betiği: `config.vm.provision "shell", path: "setup.sh"`), Vagrant bu `setup.sh` dosyasını bilgisayarınızın her yerinde aramaz; sadece bu **kök dizin** içinde arar.
> 
> **Özetle:** Vagrantfile'ın olduğu klasör, projenin "çapa" noktasıdır. Tüm yollar, paylaşılan dosyalar ve komutlar bu noktayı referans alır.

+ Vagrantfile'ınızı versiyon kontrol sistemine (Git vb.) dahil etmelisiniz; bu, projedeki her kişinin herhangi bir ön yapılandırma işiyle uğraşmadan Vagrant'tan yararlanmasını sağlar.
+ Oluşturulan Vagrantfile aşağıdaki yapılandırmayı içerir:

**Vagrantfile**

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp-education/ubuntu-24-04"
  config.vm.box_version = "0.1.0"
end
```


> [!TIP]
> + **Box:** Sanal makinenin ham kalıbıdır (örneğin Ubuntu 24.04).
> + **Vagrantfile:** Bu makinenin özelliklerini (RAM, CPU, ağ ayarları) belirten reçetedir. Ruby diliyle yazılır.
> + **Root Directory (Kök Dizin):** Vagrantfile'ın bulunduğu klasördür. Sanal makine içindeki dosyalar genellikle varsayılan olarak bu dizinle senkronize edilir (`/vagrant` klasörü altına).

## Vagrant Box’ları

+ Sıfırdan bir sanal makine oluşturmak yavaş ve zahmetli bir süreç olacağından, Vagrant bunun yerine bir sanal makineyi hızla klonlamak için bir temel imaj (base image) kullanır. 
+ Bu temel imajlar, Vagrant'ta "box" olarak bilinir ve Vagrant ortamınız için kullanılacak box'ı belirtmek, yeni bir `Vagrantfile` oluşturduktan sonra her zaman atılan ilk adımdır.
+ Bu eğitim serisinde; hazırlık (provisioning) betiklerini, ağ yapılandırmalarını, paylaşılan klasör ayarlarını ve çoklu makine yapılandırmalarını içerecek şekilde Vagrantfile'ı özelleştireceksiniz.
+ Bir Vagrant projesini başlattığınızda (initialize), ilgili box belirli bir isim altında sisteme kurulur; böylece birden fazla Vagrant ortamı aynı box’ı yeniden kullanabilir. Vagrant, mevcut kullanıcının box’larını global (sistem genelinde) olarak saklar.

---
### Örnek  Senaryo

+ Sistemde iki farklı proje var: `web-app` ve `api-service`
+ Her ikisi de şu box’ı kullanıyor: `hashicorp-education/ubuntu-24-04`

#### 1️⃣ İlk proje

```shell
mkdir web-app
cd web-app
vagrant init hashicorp-education/ubuntu-24-04
vagrant up
```

Ne olur?
+ Box sistemde yoksa indirilir (1 kez)
+ Global box dizinine kaydedilir
+ Bu box’tan bir VM klonlanır
+ `web-app` için ayrı bir sanal makine oluşur
#### 2️⃣ İkinci proje

```shell
mkdir api-service
cd api-service
vagrant init hashicorp-education/ubuntu-24-04
vagrant up
```

Bu sefer ne olur?
+ Box tekrar indirilmez
+ Global depodan kullanılır
+ Yeni ve ayrı bir VM klonlanır

#### 3️⃣ İzolasyon örneği

+ `web-app` VM içinde: `touch test.txt`
+ Bu dosya yalnızca `web-app` VM’de vardır.
+ `api-service` VM içinde bu dosya yoktur.
+ Çünkü;
	- Her proje box’tan ayrı klon üretir
	- Temel imaj değişmez
	- VM’ler birbirinden izoledir

---
+ Her proje, box’ı başlangıç imajı olarak kullanır ve onu klonlar; temel imajın kendisini asla değiştirmez. Bu da şu anlama gelir: Eğer iki projeniz de `hashicorp-education/ubuntu-24-04` box’ını kullanıyorsa, bir misafir makinede (guest machine) dosya eklemeniz diğer makineyi etkilemez.


> [!TIP]
> + **Host (ana makine)** → Senin fiziksel bilgisayarın (Windows / Linux / macOS)
> + **Guest (misafir makine)** → VirtualBox içinde çalışan sanal Ubuntu makinesi


> [!INFO]
> + Vagrant, indirdiğiniz bu box dosyalarını (kalıpları) her proje için ayrı ayrı indirmek yerine, ana makinenizde **merkezi bir dizinde** saklar. Bu sayede aynı işletim sistemini kullanan 10 farklı projeniz olsa bile, o box dosyası diskinizde sadece bir kez yer kaplar.
> + İşletim sisteminize göre bu dosyaların tutulduğu varsayılan konumlar şunlardır:
> + 📂 İşletim Sistemine Göre Konumlar
> 	- **Windows:**  `C:\Users\<Kullanıcı_Adınız>\.vagrant.d\boxes`
> 	- **macOS:**  `~/.vagrant.d/boxes` (Açık hali: `/Users/<Kullanıcı_Adınız>/.vagrant.d/boxes`)
> 	- **Linux:**  `~/.vagrant.d/boxes` (Açık hali: `/home/<Kullanıcı_Adınız>/.vagrant.d/boxes`)


> [!WARNING]
> + Vagrant box isimleri, genellikle **kullanıcı adı / box adı** biçimindedir. 
> + Ancak box isimleri resmi (canonical) olduklarını garanti etmez; registry üzerinde herkes box yayımlayabilir. 
> + Üçüncü taraflar tarafından yayımlanan box’lar için HashiCorp destek ekibi yardımcı olmaz.

+ Bu eğitimlerin geri kalanında, yalnızca az önce eklediğiniz `hashicorp-education/ubuntu-24-04` box'ını kullanacaksınız. Kendi geliştirme iş akışınızda Vagrant'ı kullanmaya hazır olduğunuzda, diğer box'ları nasıl keşfedeceğinizi bilmeniz gerekecektir.
+ Daha fazla box bulmak için en iyi yer **[HCP Vagrant Registry](https://portal.cloud.hashicorp.com/vagrant/discover)**’dir. HCP Vagrant Registry, çeşitli platformlar ve teknolojiler üzerinde çalışan, herkese açık ve ücretsiz box’ların bulunduğu bir dizin sunar. İlgilendiğiniz box’ı bulmak için HCP Vagrant Registry’de arama yapabilirsiniz.

## Ortamı başlatın(Start the environment)

+ Sanal makinenizi `vagrant up` komutuyla başlatın:

```shell
$ vagrant up
==> default: Box 'hashicorp-education/ubuntu-24-04' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: 0.1.0
==> default: Loading metadata for box 'hashicorp-education/ubuntu-24-04'
    default: URL: https://vagrantcloud.com/api/v2/vagrant/hashicorp-education/ubuntu-24-04
==> default: Adding box 'hashicorp-education/ubuntu-24-04' (v0.1.0) for provider: virtualbox (arm64)
    default: Downloading: https://vagrantcloud.com/hashicorp-education/boxes/ubuntu-24-04/versions/0.1.0/providers/virtualbox/arm64/vagrant.box
## ...
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box hashicorp-education/ubuntu-24-04'...
==> default: Machine booted and ready!
```

+ Bu işlem sırasında Vagrant aşağıdaki işlemleri gerçekleştirir:
	1. Eğer box yerel sistemde mevcut değilse, [HCP Vagrant Registry](https://portal.cloud.hashicorp.com/vagrant/discover)’den indirir.
	2. `Vagrantfile` dosyasına göre sanal makine sağlayıcısını (örneğin VirtualBox, VMware vb.) yapılandırır.
	3. Sanal makineyi kurmak için Vagrantfile içinde tanımlanmış ayarları uygular.
+ `hashicorp-education/ubuntu-24-04` box'ı VirtualBox sağlayıcısını kullanır. Eğer Vagrant varsayılan olarak farklı bir sağlayıcıya yönelirse, VirtualBox sağlayıcısını açıkça belirtin:

```shell
vagrant up --provider=virtualbox
```


> [!TIP]
> ##### Neden "Bilgisayar" yerine "Ortam" deniyor?
> Çünkü "bilgisayar" dendiğinde akla sadece fiziksel makine gelir. Ancak "ortam" dendiğinde, o makinenin içindeki **izole edilmiş, her şeyiyle hazır ve kopyalanabilir** bir çalışma alanı kastedilir.
> Vagrant'ın asıl amacı, bu "ortamı" bir dosya (**Vagrantfile**) içine sığdırmaktır. Böylece:
> - Siz projeyi başka bir arkadaşınıza verdiğinizde, o da aynı "ortama" sahip olur.
> - "Benim bilgisayarımda çalışıyordu, sende neden çalışmıyor?" sorusu ortadan kalkar çünkü ikiniz de aynı dijital ortamda çalışırsınız.
> **Özetle:** Ortam = İşletim Sistemi + Yazılımlar + Ayarlar + Kodun çalışma alanı.

## Sanal makineye erişim

+ Ortam(*environment*) çalışır durumdayken, SSH kullanarak sanal makineye bağlanın:

```shell
$ vagrant ssh
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 6.8.0-51-generic aarch64)
```

+ `vagrant ssh` komutu, ana makineniz (host) ile sanal makine arasında güvenli bir bağlantı kurar. Kurulum sırasında Vagrant’ın otomatik olarak oluşturduğu SSH anahtarını kullanır; böylece SSH kullanıcı adı ve parola gibi bilgileri manuel olarak yapılandırmanız gerekmez.
+ Misafir (guest) makine içinde, ortamın doğru şekilde kurulduğunu doğrulamak için işletim sistemi ve sürümünü kontrol edin:

```shell
$ lsb_release -a
Distributor ID: Ubuntu
Description:    Ubuntu 24.04.1 LTS
Release:        24.04
Codename:       focal
```

+ Sanal makine içerisinde yazılım yükleyebilir, uygulamaları test edebilir ve projenizi geliştirebilirsiniz. İşiniz bittiğinde misafir makineden çıkın:

```shell
logout
```

## Ortam yaşam döngüsünü yönetme

+ Kaynakları optimize etmek ve iş akışlarını düzenlemek için sanal makinenizin yaşam döngüsünü yönetebilirsiniz. Aşağıdaki komutları ana makinenizde (host) kullanın.
+ Çalışmanıza geçici olarak ara vermek için makineyi **askıya alın (suspend)**. Bu işlem mevcut bellek durumunu kaydeder ve makineyi tamamen kapatmadan durdurur.

```
$ vagrant suspend
==> default: Saving VM state and suspending execution...
```

+ Devam etmeye hazır olduğunuzda, ortamı önceki durumuna döndürmek için `vagrant resume` komutunu kullanın.

```shell
$ vagrant resume
==> default: Resuming suspended VM...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2200
    default: SSH username: vagrant
    default: SSH auth method: password
==> default: Machine booted and ready!
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
```

+ **Durdurma (Halt)** komutuyla makineyi güvenli bir şekilde kapatın. Bir sonraki `vagrant up` komutunda Vagrant, makineyi tamamen kapalı (powered-off) ve temiz bir durumdan başlatacaktır.
+ Bu, ortamı(*environment*) aktif olarak kullanmadığınız zamanlarda kaynakları korumak için kullanışlıdır.

```shell
$ vagrant halt
==> default: Attempting graceful shutdown of VM...
```

+ Sanal makineyi ve içindeki tüm verileri tamamen silmek için `destroy` komutunu kullanın. Artık ortama ihtiyaç duymadığınız durumlarda dikkatli şekilde kullanmanız önerilir. İstendiğinde `y` yazarak işlemi onaylayın.

```shell
$ vagrant destroy
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Destroying VM and associated drives...
```


> [!NOTE]
> + Makineyi yok etmek (`destroy`), indirilmiş olan "box" dosyasını silmez.
> + Bunun sebebi, birden fazla projenin aynı box dosyasını referans alabilmesidir. Box dosyasını, box ismini belirterek `remove` alt komutuyla silebilirsiniz:
> ```shell
> $ vagrant box remove hashicorp-education/ubuntu-24-04
> Removing box 'hashicorp-education/ubuntu-24-04' (v0.1.0) with provider 'virtualbox'...
> ```

## Sonraki adımlar

+ İlk Vagrant ortamınızı oluşturdunuz, Vagrantfile dosyasını incelediniz ve sanal makine yaşam döngüsünü yönetmeyi öğrendiniz.
+ Yazılımları otomatik olarak kurmak ve makinenizi yapılandırmak için ortamınızı nasıl hazırlayacağınızı (provisioning) öğrenmek üzere bir sonraki eğitimle devam edin.


> [!INFO]
> Bu eğitimde ele alınan konular hakkında daha fazla bilgi için aşağıdaki belgelere göz atabilirsiniz:
> + **[Vagrantfile](https://developer.hashicorp.com/vagrant/docs/vagrantfile)** (Vagrant Yapılandırma Dosyası)
> + **Vagrant [box](https://developer.hashicorp.com/vagrant/docs/boxes)** (Vagrant Kalıpları)
> + **Vagrant [provider](https://developer.hashicorp.com/vagrant/docs/providers)** (Vagrant Sağlayıcıları)

# Geliştirme Ortamını Hazırlamak (Provisioning)

> [Developer](https://developer.hashicorp.com/) / [Vagrant](https://developer.hashicorp.com/vagrant) / [Tutorials](https://developer.hashicorp.com/vagrant/tutorials) / [Quick Start](https://developer.hashicorp.com/vagrant/tutorials/get-started) / [Provision environment](https://developer.hashicorp.com/vagrant/tutorials/get-started/provision)

> [!TIP]
> BT ve DevOps dünyasında **"Provisioning"**, bir altyapıyı (sanal makine, sunucu vb.) sadece oluşturmakla kalmayıp, onu **çalışmaya hazır hale getirme** sürecidir.

+ Bir önceki eğitimde ilk Vagrant ortamınızı kurdunuz.
+ Bu eğitimde ise **Vagrantfile** dosyanıza hazırlama (*provisioning*) betikleri ekleyerek ortamınızı genişleteceksiniz.
+ Bu betikler; yazılım kurulumu, ayarların yapılandırılması ve gerçek dünya geliştirme iş akışlarını taklit eden, container tabanlı bir uygulama olan Terramino demo uygulamasının hazırlanması dâhil olmak üzere ortam kurulumunu otomatikleştirecektir.(Bu betikler, gerekli programları otomatik olarak kurar, ayarları yapar ve Terramino adlı örnek uygulamayı çalışmaya hazır hale getirir.)

> [!TIP]
> ##### Terramino nedir?
> + **Terramino**, HashiCorp tarafından Vagrant, Docker ve Terraform gibi araçların nasıl çalıştığını öğretmek amacıyla geliştirilmiş **örnek (demo) bir uygulamadır.**
> + Teknik olarak bakıldığında, basit bir "Tetris" benzeri oyunun web tabanlı ve konteynerize edilmiş (Docker ile paketlenmiş) halidir. Bu tür eğitimlerde kullanılmasının temel nedenleri şunlardır:
> ##### 1. Uygulama Yapısını Öğretmek
> Terramino, sadece bir kod dosyası değil; içinde bir web sunucusu, uygulama mantığı ve belirli bağımlılıklar barındıran tam bir pakettir. Vagrant eğitiminde, bu uygulamanın sanal makine içinde nasıl otomatik olarak ayağa kaldırılacağı gösterilir.
> ##### 2. Konteyner İş Akışlarını Simüle Etmek
> Metinde de belirtildiği gibi, "gerçek dünya geliştirme iş akışlarını taklit eder." Yani modern bir yazılımcının projesini Docker ile nasıl paketlediğini ve bu paketin bir sanal sunucu içinde nasıl çalıştırıldığını (Vagrant aracılığıyla) deneyimlemenizi sağlar.
> ##### 3. "Provisioning" (Hazırlama) Testi
> Vagrantfile içine yazdığınız kodların (örneğin Docker'ı kuran ve Terramino'yu başlatan komutların) gerçekten çalışıp çalışmadığını görmeniz için görsel bir çıktıdır. Kurulum bittiğinde tarayıcınızdan sanal makinenin IP adresine giderek bu oyunu görebilirsiniz.
> ##### Özet
> Terramino sizin için **"deney tahtası"**dır. Vagrant ile bir sunucu hazırladığınızda, o sunucunun gerçekten işe yarayıp yaramadığını içinde bu uygulamayı çalıştırarak test edersiniz.

## Vagrantfile dosyanızı güncelleme


> [!TIP]
> Bu eğitimlere ait yapılandırmanın (konfigürasyonun) tamamını **[Learn Vagrant Get Started](https://github.com/hashicorp-education/learn-vagrant-get-started)** GitHub deposunda bulabilirsiniz. Bu eğitime özel nihai yapılandırma, `02.Vagrantfile` dosyasında yer almaktadır.

+ Öncelikle, Docker’ı ve Terramino demo uygulaması için gerekli bağımlılıkları kurmak amacıyla `install-dependencies.sh` adında bir betik (script) oluşturun.

```shell
# Install dependencies for Terramino demo app

# Update package list
apt-get update

# Install required packages
apt-get install -y ca-certificates curl gnupg git

# Add Docker's official GPG key
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
chmod a+r /etc/apt/keyrings/docker.gpg

# Add Docker repository
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker packages
apt-get update
apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Add vagrant user to docker group
usermod -aG docker vagrant

# Clone Terramino repository if it doesn't exist
if [ ! -d "/home/vagrant/terramino-go/.git" ]; then
  cd /home/vagrant
  rm -rf terramino-go
  git clone https://github.com/hashicorp-education/terramino-go.git
  cd terramino-go
  git checkout containerized
fi

# Create reload script
cat > /usr/local/bin/reload-terramino << 'EOF'
#!/bin/bash
cd /home/vagrant/terramino-go
docker compose down
docker compose build --no-cache
docker compose up -d
EOF

chmod +x /usr/local/bin/reload-terramino

# Add aliases
echo 'alias play="docker compose -f /home/vagrant/terramino-go/docker-compose.yml exec -it backend ./terramino-cli"' >> /home/vagrant/.bashrc
echo 'alias reload="sudo /usr/local/bin/reload-terramino"' >> /home/vagrant/.bashrc
# Source the updated bashrc
echo "source /home/vagrant/.bashrc" >> /home/vagrant/.bash_profile
```

+ Ardından, betiği çalıştırılabilir hale getirin.

```shell
chmod +x install-dependencies.sh
```

