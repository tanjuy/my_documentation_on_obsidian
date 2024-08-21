#linux_paket
# Dnf veya Yum:
## Dnf Komutları:

###### check-update
```
$ sudo dnf check-update
```
> **Explanation:**
> + Yum veya DNF tabanlı Linux sistemlerinde paket depolarının indeksini güncellemek, ancak herhangi bir paket yüklemesi yapmamak için kullanılacak komut.
> + apt-get temeli linux dağıtımlarında ise: `sudo apt update`

###### makecache
```
$ dnf makecache
```
> **Explanation:**
> paket listeleri güncellenir ve sisteminize uygun en güncel paketler hakkında bilgi alınır.

## Yum Komutları:
###### check-update
```
$ sudo yum check-update
```
> **Explanation:**
> dnf komutları başlığında açıklanmıştır: [[Linux Paket Komutları#check-update|check-update]]

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

