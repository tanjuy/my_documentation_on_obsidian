#linux_paket
# Dnf veya Yum:
## Dnf Komutları:

#### 1. check-update
```sh
$ sudo dnf check-update
```
> **Explanation:**
> + Yum veya DNF tabanlı Linux sistemlerinde paket depolarının indeksini güncellemek, ancak herhangi bir paket yüklemesi yapmamak için kullanılacak komut.
> + apt-get temeli linux dağıtımlarında ise: `sudo apt update`

#### 2. makecache
```sh
$ dnf makecache
```
> **Explanation:**
> paket listeleri güncellenir ve sisteminize uygun en güncel paketler hakkında bilgi alınır.

#### 3. updateinfo:
+ Bu komut, sisteminizdeki paketlerle ilgili güncelleme bilgilerini görüntülemenizi sağlar.
+ Özellikle güvenlik güncellemeleri, hata düzeltmeleri ve yeni özellikler hakkında detaylı bilgi sunar.
```sh
$ dnf updateinfo 
```
> **Explanation:**

#### 4. upgrade:
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

#### 5.history:
###### 1.Temel Kullanımı:
```sh
$ sudo dnf history
```
> **Explanation:**

###### 2. history info:
```sh
$ sudo dnf history info nginx
```

###### 3. history undo:
```sh
$ sudo dnf history undo 3
```
> **Explanation:**
> + Eğer kurmuş olduğunu bir uygulama var ise örneğin bu uygulama nginx olsun.
> + `dnf history` komutu ile `ID` numarası üzerinden yüklenen paketi kaldırabiliriz.
> + Örneğin nginx'in ID 3 olsun, bu durumda nginx sisteme nasıl yüklendiyse öyle kalkacaktır.
> + `undo` türkçe anlamı `geri al` demektir.

###### 4. history redo:
```sh
$ sudo dnf history redo 3
```
> **Explanation:**

#### 6. module:
###### 1. module list:
```sh
$ sudo dnf module list
```
> **Explanation:**

#### 7. grouplist:
```sh
$ sudo dnf grouplist
```

#### 8. groupinfo:
```sh
$ sudo dnf groupinfo "Development Tools"
```
> **Explanation:**
> 

#### 9. groupinstall:
```sh
$ sudo dnf groupinstall "Development Tools"
```
> **Explanation:**

#### 10. list:
##### A. list installed:
```sh
$ sudo yum list installed
```
> **Explanation:**
> + Sisteminizde yüklü olan tüm paketlerin bir listesini görüntüler.

###### A.1. list installed paketAdı:
```sh
$ sudo yum list installed nginx
```
> **Explanation:**
> + Sistemde nginx paketinin yüklü olup olmadığını ekrana basar.



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

