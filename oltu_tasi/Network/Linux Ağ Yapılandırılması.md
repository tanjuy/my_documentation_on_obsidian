# 1. Debian:

Debian sistemlerde ağ yapılandırmasını değiştirmek için kullanılan yöntem, Debian sürümüne ve kullanılan ağ yöneticisine (_NetworkManager_ veya _systemd-networkd_ / klasik _ifupdown_) göre değişiklik gösterebilir.

## 1.1. Debian Terminal Üzerinde IP Adresi Değiştirme Kılavuzu

Debian üzerinde IP adresi yapılandırmak için başlıca 4 yöntem kullanılır:

1. **Geleneksel Yöntem (`/etc/network/interfaces`):** Sunucu (headless) kurulumlarında standart kabul edilir.
2. **Modern / Masaüstü Yöntemi (`nmcli`):** NetworkManager kurulu sistemlerde hızlı yönetim sağlar.
3. **IP Komutu:** Geçici (reboot sonrası silinen) IP ayarları ve hızlı testler için kullanılır.
4. **Systemd-networkd:** sunucu ve bulut ortamlarında sıkça tercih edilir.

### 1.1.1. Geleneksel Yöntem (`/etc/network/interfaces`)

Sunucu sürümlerinde ve ağ yöneticisi olmayan Debian sistemlerinde en yaygın yöntem yapılandırma dosyasını doğrudan düzenlemektir.

#### 1.1.1.1. Ağ Arayüzünün (Interface) Adını Tespit Etme

Öncelikle sistemdeki etkin ağ arayüzlerinin isimlerini listelemelisiniz:

```bash
$ ip link show
```

_(Örnek ağ arayüz ismi: `eth0`, `enp0s3` veya `ens33`)_

#### 1.1.1.2. Yapılandırma Dosyasını Düzenleme

Ağ ayarlarını içeren dosyayı bir metin düzenleyici (`nano` veya `vim`) ile `root` yetkileriyle açın:

```bash
$ sudo vi /etc/network/interfaces
```

#### 1.1.1.3. IP Adresi Yapılandırması

+  **Statik (Sabit) IP Tanımlama:** İlgili ağ arayüzü satırlarını bulun ve aşağıdaki şekilde güncelleyin (_`enp0s3` yerine kendi arayüz adınızı yazın_):

```
# Statik IP Yapılandırması
auto enp0s3
iface enp0s3 inet static
    address 192.168.1.100/24
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 1.1.1.1
```

+  **Dinamik (DHCP) IP Tanımlama:** IP adresinin otomatik alınması isteniyorsa:

```
# DHCP Yapılandırması
auto enp0s3
iface enp0s3 inet dhcp
```

#### 1.1.1.4. Ağ Servisini Yeniden Başlatma

Değişikliklerin geçerli olması için networking servisini yeniden başlatın:

```bash
$ sudo systemctl restart networking
```

### 1.1.2. `nmcli` (NetworkManager CLI) Yöntemi

Masaüstü Debian sürümlerinde veya NetworkManager kurulu sistemlerde komut satırı üzerinden IP değiştirmek için `nmcli` kullanılır.

#### 1.1.2.1. Bağlantı İsimlerini Listeleme

```bash
$ nmcli connection show
```

#### 1.1.2.2. Statik IP Tanımlama

Mevcut bağlantınızın adının `Wired connection 1` olduğunu varsayarsak:

```bash
# IP, Alt Ağ Maskesi ve Ağ Geçidini Ayarlama
sudo nmcli con mod "Wired connection 1" ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1

# DNS Sunucularını Belirleme
sudo nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8 1.1.1.1"

# IP Yapılandırmasını Manuel/Statik Moduna Geçirme
sudo nmcli con mod "Wired connection 1" ipv4.method manual

# Bağlantıyı Yeniden Aktifleştirme
sudo nmcli con up "Wired connection 1"
```

### 1.1.3. Geçici IP Adresi Atama (Anlık Testler İçin)

Sistem yeniden başlatıldığında **kaybolacak** şekilde, anlık olarak IP değiştirmek için `ip` komutu kullanılabilir.

 + **Yeni IP Ekleme:**

```bash
$ sudo ip addr add 192.168.1.100/24 dev enp0s3
```

+ **Eski IP'yi Silme:**

```bash
$ sudo ip addr del 192.168.1.50/24 dev enp0s3
```

#### 1.1.3.1. Kontrol ve Doğrulama Komutları

Yapılan değişikliklerin başarıyla uygulandığını doğrulamak için aşağıdaki komutlar kullanılır:

```bash
# Atanan IP adresini kontrol etme
ip addr show enp0s3

# Ağ geçidi (Routing table) kontrolü
ip route show

# Ağ bağlantısını test etme
ping -c 4 8.8.8.8
```

### 1.1.4. systemd-networkd ile IP Adresi Yapılandırması

`systemd-networkd`, özellikle sunucu ve bulut ortamlarında sıkça tercih edilen, hafif ve performanslı bir ağ yönetim servisidir. modern Debian sürümlerinde varsayılan olarak gelir ancak elle etkinleştirilmesi gerekir.

`systemd-networkd` servisinde tüm ağ yapılandırmaları `/etc/systemd/network/` dizini altında `.network` uzantılı dosyalar ile yönetilir.

#### 1.1.4.1. Servisleri Hazırlama ve Etkinleştirme

`systemd-networkd` kullanmaya başlamadan önce, çakışmayı önlemek için geleneksel `networking` servisini devre dışı bırakıp yeni servisi aktif etmelisiniz.

```bash
# Geleneksel networking servisini durdurun ve devre dışı bırakın
sudo systemctl stop networking
sudo systemctl disable networking

# systemd-networkd ve systemd-resolved servislerini etkinleştirin
sudo systemctl enable systemd-networkd
sudo systemctl start systemd-networkd

# DNS çözünürlüğü için systemd-resolved servisini başlatın
sudo systemctl enable systemd-resolved
sudo systemctl start systemd-resolved
```

#### 1.1.4.2. Ağ Arayüzünün Adını Tespit Etme

İşlem yapılacak ağ arayüzünün adını öğrenin:

```bash
$ networkctl
```

veya

```bash
ip link show
```

(Örnek ağ arayüz ismi: `enp0s3`)

#### 1.1.4.3. Yapılandırma Dosyası Oluşturma

Yapılandırma dosyaları alfabetik sıraya göre işlenir. Bu nedenle isimlerin başında `10-`, `20-` gibi ön ekler kullanılır.

`/etc/systemd/network/` dizininde yeni bir dosya oluşturun:

```bash
$ sudo nano /etc/systemd/network/10-static-enp0s3.network
```

##### 1.1.4.3.1. Statik (Sabit) IP Yapılandırması

Dosya içeriğini aşağıdaki şekilde düzenleyin (_`enp0s3` yerine kendi ağ arayüz adınızı girin_):

```toml
[Match]
Name=enp0s3

[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
DNS=8.8.8.8 1.1.1.1
```

##### 1.1.4.3.1. Dinamik (DHCP) IP Yapılandırması

Eğer IP adresinin otomatik alınmasını istiyorsanız dosya içeriği şu şekilde olmalıdır:

```toml
[Match]
Name=enp0s3

[Network]
DHCP=ipv4
```

#### 1.1.4.4. Yapılandırmayı Uygulama

Değişiklikleri uygulamak için servisi yeniden yükleyin:

```bash
sudo systemctl restart systemd-networkd
```

#### 1.1.4.5. Kontrol ve Doğrulama

Ağ durumunu ve IP adresinin doğru atanıp atanmadığını `networkctl` komutlarıyla kontrol edebilirsiniz:

```bash
# Tüm arayüzlerin özet durumunu görüntüler
networkctl status

# Belirli bir arayüzün ayrıntılı durumunu kontrol eder
networkctl status enp0s3
```

Ayrıca standart IP kontrolü için:

```bash
ip addr show enp0s3
```

[Kaldığım nokta](https://gemini.google.com/app/26391b33b010d8f3)

