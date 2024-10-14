#linux_commands 

# Firewall-cmd

### Firewalld nedir?
+ **Firewalld**, Linux tabanlı işletim sistemlerinde kullanılan dinamik bir güvenlik duvarı yönetim aracıdır.
+ Geleneksel statik güvenlik duvarı yapılandırmalarına (örneğin, iptables) kıyasla daha esnek ve kullanıcı dostu bir çözüm sunar.
+ Firewalld, ağ trafiğini yönetmek için "zonalar" ve "servisler" kavramlarını kullanarak, farklı güvenlik seviyelerine sahip ağ arayüzlerini kolayca yapılandırmanıza olanak tanır.

### Firewall-cmd nedir?
+ `firewall-cmd`, Linux sistemlerinde **firewalld** adlı dinamik güvenlik duvarı yöneticisini kontrol etmek ve yapılandırmak için kullanılan bir komut satırı aracıdır.
### A. Durum Komutları:

###### 1. `--state` parametresi:
```sh
$ firewall-cmd --state
```
> **Explanation:**
> + Güvenlik duvarı daemon'unun aktif (yani çalışır durumda) olup olmadığını kontrol eder.

###### 2. `--reload` parametresi:
```sh
$ firewall-cmd --reload
```
> **Explanation:**
> + Güvenlik duvarı kurallarını yeniden yükler ve durum bilgilerini saklar.

### B. Servis Ekleme:
###### 1. Temel Kullanımı:
```sh
$ firewall-cmd --add-service=http 
```
> **Explanation:**
> 

### Zone Değiştirme:

###### 1. Zone'ları Listeleme:

```sh
$ firewall-cmd --list-all-zone
```
> **Explanation:**
> +

```sh
$ firewall-cmd --get-zones
```
> **Explanation:**

```sh
$ firewall-cmd --get-active-zones
```
> **Explanation:**
> + Parametreden de anlaşıldığı üzeri ekran mevcutta aktif olan `zone` getirir.

