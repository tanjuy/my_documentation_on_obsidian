#linux_commands 

# Firewall-cmd

### Firewalld nedir?
+ **Firewalld**, Linux tabanlı işletim sistemlerinde kullanılan dinamik bir güvenlik duvarı yönetim aracıdır.
+ Geleneksel statik güvenlik duvarı yapılandırmalarına (örneğin, iptables) kıyasla daha esnek ve kullanıcı dostu bir çözüm sunar.
+ Firewalld, ağ trafiğini yönetmek için "zonalar" ve "servisler" kavramlarını kullanarak, farklı güvenlik seviyelerine sahip ağ arayüzlerini kolayca yapılandırmanıza olanak tanır.

### Firewall-cmd nedir?
+ `firewall-cmd`, Linux sistemlerinde **firewalld** adlı dinamik güvenlik duvarı yöneticisini kontrol etmek ve yapılandırmak için kullanılan bir komut satırı aracıdır.
### A. Durum Komutları:

#### 1. `--state` parametresi:
```sh
$ firewall-cmd --state
```
> **Explanation:**
> + Güvenlik duvarı daemon'unun aktif (yani çalışır durumda) olup olmadığını kontrol eder.

**Çıktı:**

```shell
running
```

#### 2. `--reload` parametresi:

```sh
$ firewall-cmd --reload
```
> **Explanation:**
> + Güvenlik duvarı kurallarını yeniden yükler ve durum bilgilerini saklar.

**Çıktı:**

```shell
success
```
### B. Servis Ekleme:
#### 1. Bir Servis Ekleme:

```sh
sudo firewall-cmd --add-service=http --permanent
```

> **Explanation:**
> + Bu işlemin geçerli olabilmesi için `sudo firewall-cmd --reload` komut çalıştırılmalıdır.
> + `http` servisini (port 80) firewall’a izinli servis olarak ekler.
> + `--permanent` :  Değişiklik kalıcıdır, sistem yeniden başlatıldığında da geçerli olur. Eğer `--permanent` parametresini kullanmadığınızda işletim sistemi yeniden başlatıldığında bu kural sıfırlanır.

#### 1.a. Belirli bir Zone'a bir Servis Ekleme:

```shell
sudo firewall-cmd --zone=home --add-service=https --permanent
```

#### 2. Bir Servis Silme:

```shell
sudo firewall-cmd --remove-service=http --permanent
```

#### 2.a. Belirli bir Zone'dan Servis Silme:

```shell
sudo firewall-cmd --zone=home --remove-service=https --permanent
```

#### 3. Servisleri Listeleme:

```shell
sudo firewall-cmd --list-services
```

#### 3.a. Belirli bir Servisin Zone'u Listeleme:

```shell
sudo firewall-cmd --zone=home --list-services
```


### C. Zone İşlemleri:

#### 1. Tüm Zone'ları Listeleme:

```sh
$ firewall-cmd --list-all-zone
```
> **Explanation:**
> +

**Çıktı:**
```shell
block
  target: %%REJECT%%
  icmp-block-inversion: no
  interfaces:
  sources:
  services:
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

dmz
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: ssh
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

drop
  target: DROP
  icmp-block-inversion: no
  interfaces:
  sources:
  services:
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

external
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: ssh
  ports:
  protocols:
  forward: no
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

home
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: cockpit dhcpv6-client mdns samba-client ssh
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

internal
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: cockpit dhcpv6-client mdns samba-client ssh
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

nm-shared
  target: ACCEPT
  icmp-block-inversion: no
  interfaces:
  sources:
  services: dhcp dns ssh
  ports:
  protocols: icmp ipv6-icmp
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
        rule priority="32767" reject

public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: cockpit dhcpv6-client http ssh
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

trusted
  target: ACCEPT
  icmp-block-inversion: no
  interfaces:
  sources:
  services:
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

work
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: cockpit dhcpv6-client ssh
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

```


#### 2. Aktif Zone'u Listeleme:

```shell
sudo firewall-cmd --list-all
```

**Çıktı:**
```shell
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: cockpit dhcpv6-client http ssh
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

#### 3. Belirli bir Zone'u Listeleme:

```shell
sudo firewall-cmd --zone=home --list-all
```

**Çıkıt:**
```shell
home
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: cockpit dhcpv6-client mdns samba-client ssh
  ports:
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```



```sh
$ firewall-cmd --get-zones
```
> **Explanation:**

```sh
$ firewall-cmd --get-active-zones
```
> **Explanation:**
> + Parametreden de anlaşıldığı üzeri ekran mevcutta aktif olan `zone` getirir.

### Port İşlemleri:

