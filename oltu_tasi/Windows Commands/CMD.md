#windows 
### Change Directory:
###### Örnek 1:  
```cmd
C:\Users\tanju> cd
```
> **Explanation:**
> Sadece `cd` yazarsak bulunduğunuz dizin yolunu verecektir. linux dağıtımlarında buna eş değer `pwd` komutudur.

### Kopyalama:
###### Söz dizimi(Syntax):
```cmd
C:\Users\tanju> copy [kaynak_dosya] [hedef_dizin]
```

###### Örnek 1: 

## netsh Komutu:

+ **`netsh` (Network Shell)** komutu, ağ yapılandırmalarını görüntülemek ve değiştirmek için kullanılan güçlü bir komut satırı aracıdır.
+ Netsh, Windows'un ağ bileşenlerini yapılandırmak için kullanılır.

### interface
#### Örnek 1: IP ve Ağ Ayarlarını Görüntüleme

```cmd
netsh interface ipv4 show config
```
> **Explanation:**
> + Tüm ağ bağdaştırıcılarının mevcut IP, DNS ve Gateway yapılandırmasını gösterir.

### wlan

#### Örnek 1: Bağlanılmış tüm Wi-Fi ağlarını listeleme:

```cmd
netsh wlan show profiles
```

### shutdown Komutu:

#### Yeniden Başlatma:

```cmd
shutdown /r /t 0
```

> + **`/r`** → Yeniden başlatma işlemi yapar.
> + **`/t 0`** → Bekleme süresi olmadan hemen yeniden başlatır (saniye cinsinden, örn. `/t 5` 5 saniye bekler).

```cmd
shutdown /r /fw /t 0
```