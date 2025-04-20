#linux_paket
# Dnf veya Yum:
## Dnf Komutları:

### 1. check-update
```sh
$ sudo dnf check-update
```
> **Explanation:**
> + Yum veya DNF tabanlı Linux sistemlerinde paket depolarının indeksini güncellemek, ancak herhangi bir paket yüklemesi yapmamak için kullanılacak komut.
> + apt-get temeli linux dağıtımlarında ise: `sudo apt update`

### 2. makecache
```sh
$ dnf makecache
```
> **Explanation:**
> paket listeleri güncellenir ve sisteminize uygun en güncel paketler hakkında bilgi alınır.

### 3. updateinfo:
+ Bu komut, sisteminizdeki paketlerle ilgili güncelleme bilgilerini görüntülemenizi sağlar.
+ Özellikle güvenlik güncellemeleri, hata düzeltmeleri ve yeni özellikler hakkında detaylı bilgi sunar.
```sh
$ dnf updateinfo 
```
> **Explanation:**

### 4. upgrade:
```sh
$ sudo dnf upgrade
```
> **Explanation:**
> + REHL temeli sistemleri günceller
> + `sudo dnf update` komut birebir aynı işlemi yapar.
> + Bu komut, depolarda bulunan tüm güncellemeleri indirir ve kurar. Hem *güvenlik güncellemelerini* hem de *hata düzeltmeleri* ve *yeni özellikleri içeren* tüm paket güncellemelerini kapsar.

###### 1. `upgrade --assumeno`:
```sh
$ sudo dnf upgrade --assumeno
```
> **Explanation:**
> + Güncellemeleri uygularken hangi paketlerin güncelleneceğini görmek ve onaylamak için interaktif modu kullanabilirsiniz.
> + Bu komut, güncellemeleri listeleyecek ancak onay vermediğiniz sürece hiçbir paket yüklemeyecektir. Güncellemeleri gözden geçirmek için kullanışlıdır.

### 5.history:
#### 1.Temel Kullanım:
```sh
$ sudo dnf history
```
> **Explanation:**

**Çıktı:**
```shell
ID  | Command line                   | Date and time      | Action(s)   | Altered
-----------------------------------------------------------------------------------------
19  | install ntpstat.noarch         | 2024-10-11 19:08   | Install     |    1
18  | install pcre-devel             | 2024-10-11 09:45   | Install     |    4
17  | groupinstall Development Tools | 2024-10-11 04:22   | I, U        |  203
16  | install wget.x86_64            | 2024-10-11 01:05   | Install     |    2
15  | history undo 14                | 2024-10-10 23:09   | Removed     |    4
14  | install python3.12             | 2024-10-10 23:08   | Install     |    4
13  | history undo 12                | 2024-10-10 23:06   | Removed     |    1
12  | install telnet                 | 2024-10-10 23:04   | Install     |    1
11  | remove python39                | 2024-10-10 19:46   | Removed     |    6
10  | install python39               | 2024-10-10 19:44   | Install     |    6
9   | remove python3.11              | 2024-10-10 19:39   | Removed     |    5
8   | install python3.11             | 2024-10-10 19:37   | Install     |    5
7   | remove nginx                   | 2024-10-10 19:29   | Removed     |   20
6   | install vim                    | 2024-10-10 15:49   | Install     |    4
5   | install git                    | 2024-10-10 15:47   | Install     |    7
4   | install zsh                    | 2024-10-10 15:46   | Install     |    1
3   | install nginx                  | 2024-10-10 13:05   | Install     |   61
2   | install tmux                   | 2024-10-10 12:59   | Install     |    2
1   |                                | 2024-10-10 12:19   | Install     |  442
```


#### 2. history info:
```sh
$ sudo dnf history info nginx
```

#### 3. history undo:
```sh
$ sudo dnf history undo 3
```
> **Explanation:**
> + Eğer kurmuş olduğunu bir uygulama var ise örneğin bu uygulama nginx olsun.
> + `dnf history` komutu ile `ID` numarası üzerinden yüklenen paketi kaldırabiliriz.
> + Örneğin nginx'in ID 3 olsun, bu durumda nginx sisteme nasıl yüklendiyse öyle kalkacaktır.
> + `undo` türkçe anlamı `geri al` demektir.

#### 4. history redo:
```sh
$ sudo dnf history redo 3
```
> **Explanation:**

### 6. module:
###### 1. module list:
```sh
$ sudo dnf module list
```
> **Explanation:**

### 7. grouplist:
```sh
$ sudo dnf grouplist
```

### 8. groupinfo:
```sh
$ sudo dnf groupinfo "Development Tools"
```
> **Explanation:**
> 

### 9. groupinstall:
```sh
$ sudo dnf groupinstall "Development Tools"
```
> **Explanation:**

### 10. list:
#### 10.1. list installed:
```sh
$ sudo yum list installed
```
> **Explanation:**
> + Sisteminizde yüklü olan tüm paketlerin bir listesini görüntüler.

#### 10.2. list installed paketAdı:
```sh
$ sudo yum list installed nginx
```
> **Explanation:**
> + Sistemde nginx paketinin yüklü olup olmadığını ekrana basar.

### 11.repolist:
#### 11.1.repolist enabled:
+ Sisteminizde etkin olan yazılım depolarını listelemek için kullanılır.

```shell
ls /etc/yum.repos.d/
```

**ls Çıktısı**
```shell
total 36
-rw-r--r--. 1 root root  943 May 22  2024 almalinux-ha.repo
-rw-r--r--. 1 root root  905 May 22  2024 almalinux-nfv.repo
-rw-r--r--. 1 root root  885 May 22  2024 almalinux-plus.repo
-rw-r--r--. 1 root root  963 May 22  2024 almalinux-powertools.repo
-rw-r--r--. 1 root root 2666 May 22  2024 almalinux.repo
-rw-r--r--. 1 root root 1041 May 22  2024 almalinux-resilientstorage.repo
-rw-r--r--. 1 root root  871 May 22  2024 almalinux-rt.repo
-rw-r--r--. 1 root root  928 May 22  2024 almalinux-saphana.repo
-rw-r--r--. 1 root root  873 May 22  2024 almalinux-sap.repo
```

> **Explanation:**
> + 

```shell
dnf repolist
```

```shell
repo id                                    repo name
appstream                                  AlmaLinux 8 - AppStream
baseos                                     AlmaLinux 8 - BaseOS
extras                                     AlmaLinux 8 - Extras
```
> **Explanation:**
> 
#### 11.2.repolist disabled:

```shell
dnf repolist disabled
```

```shell
appstream-debuginfo                   AlmaLinux 8 - AppStream debuginfo
appstream-source                      AlmaLinux 8 - AppStream Source
baseos-debuginfo                      AlmaLinux 8 - BaseOS debuginfo
baseos-source                         AlmaLinux 8 - BaseOS Source
extras-debuginfo                      AlmaLinux 8 - Extras debuginfo
extras-source                         AlmaLinux 8 - Extras Source
ha                                    AlmaLinux 8 - HighAvailability
ha-debuginfo                          AlmaLinux 8 - HighAvailability debuginfo
ha-source                             AlmaLinux 8 - HighAvailability Source
nfv                                   AlmaLinux 8 - Real Time for NFV
nfv-debuginfo                         AlmaLinux 8 - Real Time for NFV Debuginfo
nfv-source                            AlmaLinux 8 - Real Time for NFV Sources
plus                                  AlmaLinux 8 - Plus
plus-debuginfo                        AlmaLinux 8 - Plus debuginfo
plus-source                           AlmaLinux 8 - Plus Source
powertools                            AlmaLinux 8 - PowerTools
powertools-debuginfo                  AlmaLinux 8 - PowerTools debuginfo
powertools-source                     AlmaLinux 8 - PowerTools Source
resilientstorage                      AlmaLinux 8 - ResilientStorage
resilientstorage-debuginfo            AlmaLinux 8 - ResilientStorage debuginfo
resilientstorage-source               AlmaLinux 8 - ResilientStorage Source
rt                                    AlmaLinux 8 - Real Time
rt-debuginfo                          AlmaLinux 8 - Real Time Debuginfo
rt-source                             AlmaLinux 8 - Real Time Sources
sap                                   AlmaLinux 8 - SAP
sap-debuginfo                         AlmaLinux 8 - SAP Debuginfo
sap-source                            AlmaLinux 8 - SAP Sources
saphana                               AlmaLinux 8 - SAP HANA
saphana-debuginfo                     AlmaLinux 8 - SAP HANA Debuginfo
saphana-source                        AlmaLinux 8 - SAP HANA Sources
```


#### 11.3.repolist all:

```shell
dnf repolist all
```

```shell
repo id                            repo name                           status
appstream                   AlmaLinux 8 - AppStream                    enabled
appstream-debuginfo         AlmaLinux 8 - AppStream debuginfo          disabled
appstream-source            AlmaLinux 8 - AppStream Source             disabled
baseos                      AlmaLinux 8 - BaseOS                       enabled
baseos-debuginfo            AlmaLinux 8 - BaseOS debuginfo             disabled
baseos-source               AlmaLinux 8 - BaseOS Source                disabled
extras                      AlmaLinux 8 - Extras                       enabled
extras-debuginfo            AlmaLinux 8 - Extras debuginfo             disabled
extras-source               AlmaLinux 8 - Extras Source                disabled
ha                          AlmaLinux 8 - HighAvailability             disabled
ha-debuginfo                AlmaLinux 8 - HighAvailability debuginfo   disabled
ha-source                   AlmaLinux 8 - HighAvailability Source      disabled
nfv                         AlmaLinux 8 - Real Time for NFV            disabled
nfv-debuginfo               AlmaLinux 8 - Real Time for NFV Debuginfo  disabled
nfv-source                  AlmaLinux 8 - Real Time for NFV Sources    disabled
plus                        AlmaLinux 8 - Plus                         disabled
plus-debuginfo              AlmaLinux 8 - Plus debuginfo               disabled
plus-source                 AlmaLinux 8 - Plus Source                  disabled
powertools                  AlmaLinux 8 - PowerTools                   disabled
powertools-debuginfo        AlmaLinux 8 - PowerTools debuginfo         disabled
powertools-source           AlmaLinux 8 - PowerTools Source            disabled
resilientstorage            AlmaLinux 8 - ResilientStorage             disabled
resilientstorage-debuginfo  AlmaLinux 8 - ResilientStorage debuginfo   disabled
resilientstorage-source     AlmaLinux 8 - ResilientStorage Source      disabled
rt                          AlmaLinux 8 - Real Time                    disabled
rt-debuginfo                AlmaLinux 8 - Real Time Debuginfo          disabled
rt-source                   AlmaLinux 8 - Real Time Sources            disabled
sap                         AlmaLinux 8 - SAP                          disabled
sap-debuginfo               AlmaLinux 8 - SAP Debuginfo                disabled
sap-source                  AlmaLinux 8 - SAP Sources                  disabled
saphana                     AlmaLinux 8 - SAP HANA                     disabled
saphana-debuginfo           AlmaLinux 8 - SAP HANA Debuginfo           disabled
saphana-source              AlmaLinux 8 - SAP HANA Sources             disable
```


### 12.config-manager:
#### 12.1.`--set-enabled`:

```shell
sudo dnf config-manager --set-enabled powertools 
```

**almalinux-powertools.repo dosyası:**
```repo
# almalinux-powertools.repo

[powertools]
name=AlmaLinux $releasever - PowerTools
mirrorlist=https://mirrors.almalinux.org/mirrorlist/$releasever/powertools
# baseurl=https://repo.almalinux.org/almalinux/$releasever/PowerTools/$basearch/os/
enabled=0
gpgcheck=1
countme=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-AlmaLinux
```
> **Explanation:**
> + `--set-enabled` parametresi `/etc/yum.repos.d` dizinindeki `almalinux-powertools.repo` dosyası içerisindeki `[powertools]` bölümündeki `enabled=0` ifadesini `enabled=1`'e dönüştürmektedir.
> + Bu komutu kullanmadan bir düzenleyici(editor; vim) ile de bu işlemi manuel olarak yapabilirsiniz.
> + `sudo dnf repolist` komut ile aktif etmiş olduğumuz `powertools` deposunu görebiliriz.

#### 12.2.`--set-disabled`:

```shell
sudo dnf config-manager --set-disabled powertools
```

**almalinux-powertools.repo dosyası:**
```repo
# almalinux-powertools.repo

[powertools]
name=AlmaLinux $releasever - PowerTools
mirrorlist=https://mirrors.almalinux.org/mirrorlist/$releasever/powertools
# baseurl=https://repo.almalinux.org/almalinux/$releasever/PowerTools/$basearch/os/
enabled=1
gpgcheck=1
countme=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-AlmaLinux
```
> **Explanation:**
> + Az önce aktif etmiş olduğumuz `powertools` deposunu `--set-disabled` parametresi ile pasif duruma alıyoruz
> + Yani `enabled=1` ifadesini `enabled=0` durumuna çekiyoruz.
> + Bu işlem `sudo vim /etc/yum.repos.d/almalinux-powertools.repo` komutu ile dosyayı açtığımızda `enabled=1` ifadesini `enabled=0` çevirmek yeterli olacaktır.

#### 12.3.`--add-repo`:
+ Bir URI veya bir dosyadan depo ekleme.

**Syntax:**
```shell
sudo dnf config-manager --add-repo URI
```

**Brave Tarayıcı deposu:**
```shell
sudo dnf config-manager --add-repo https://brave-browser-rpm-release.s3.brave.com/brave-browser.repo
```

> **Explanaation:**
> + `--add-repo` parametresi ile  brave deposu eklediğimiz de `/etc/yum.repos.d/` dizininde `brave-browser.repo` dosyası oluşturacaktır.
> + Aşağıda içeriği görünmektedir;

**brave-browser.repo dosyası:**
```repo
[brave-browser]
name=Brave Browser
enabled=1
gpgcheck=1
gpgkey=https://brave-browser-rpm-release.s3.brave.com/brave-core.asc
baseurl=https://brave-browser-rpm-release.s3.brave.com/$basearch
```


---
## Yum Komutları:
#### 1.check-update:
```
$ sudo yum check-update
```
> **Explanation:**
> dnf komutları başlığında açıklanmıştır: [[Linux Paket Komutları#check-update|check-update]]


---
# Apt:
## Apt Komutları:
###### update:
```
$ sudo apt-get update
```
> **Explanation:**

###### dist-upgrade:
```
$ sudo apt-get dist-upgrade
```
> **Explanation:**
> Bu komut, sistemde yüklü olan tüm paketlerin en son sürümlerine güncellenmesini sağlar ve ayrıca sistemin kararlılığını korumak için bazı paketlerin yüklenmesi veya kaldırılması gerekiyorsa bu işlemleri de yapar.

