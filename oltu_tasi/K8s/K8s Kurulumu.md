 #k8s #docker 
# Senaryo 1:


> [!CAUTION]
> + Eğer Yerel(local) ağda kurulum yapıyorsanız, ana makineleriniz(Host) dinamik IP'den yani dhcp'den statik IP çevirmeniz gerekmektedir.

## Master Host:

```dns
127.0.0.1 localhost
127.0.1.1 nginx-tutorial3

192.168.1.100 master.academy.local master       # <---
192.168.1.101 node1.academy.local node1         # <----
192.168.1.102 node2.academy.local node2         # <-----

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
> **Explanation:**
> + `/etc/hosts` dosyasında;
> + Her bir IP'iye karşılık gelen `fdqn` isimlerini ve `hostname` isimlerini veriyoruz. 
> + Eğer bu IP'ler içerisinden `ping` atarsak `fdqn` veya `hostname` adları ile ICMP paketlerini alındığını görmemiz gerekir.
> + Örneğin; `ping master.academy.local` veya `ping master` şeklinde bu IP'lerden ICMP paketleri atabiliyor olmamız gerekmektedir. 

```shell
ping node1.academy.local
```
> **Explanation:**
> + `ping` komutu ile test ediyoruz `host` dosyasında yazmış olduğumuz domainlerin IP adreslerini çözümlenip çözümlenmediğini kontrol ediyoruz.
## Node Host 1:

```dns
127.0.0.1 localhost
127.0.1.1 nginx-tutorial3

192.168.1.100 master.academy.local master       # <---
192.168.1.101 node1.academy.local node1         # <----
192.168.1.102 node2.academy.local node2         # <-----

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
> **Explanation:**
> + Master düğümünde yapılan işlemler birebir aynıdır.

```shell
ping master.academy.local
```
## Node Host 2:

```dns
127.0.0.1 localhost
127.0.1.1 nginx-tutorial3

192.168.1.100 master.academy.local master       # <---
192.168.1.101 node1.academy.local node1         # <----
192.168.1.102 node2.academy.local node2         # <-----

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
> **Explanation:**
> + Master düğümünde yapılan işlemler birebir aynıdır.

```shell
ping master.academy.local
```

## Kaynak:
1. [Academy CB](https://www.youtube.com/watch?v=ZuwroGhhPc4&list=PL_WRo6uz2NWWfuLNIw24YxnPO2e6dD6sP&index=2)

# Senaryo 2:

==Burası yapılacak==

## Kaynak:
1. [Deploy a Dual Stack Kubernetes Cluster (v1.30) on Ubuntu 24.04 LTS!](https://www.youtube.com/watch?v=96mqy5iCjoA)