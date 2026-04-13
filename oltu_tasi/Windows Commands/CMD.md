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
## shutdown Komutu:

#### Yeniden Başlatma:

```cmd
shutdown /r /t 0
```

> + **`/r`** → Yeniden başlatma işlemi yapar.
> + **`/t 0`** → Bekleme süresi olmadan hemen yeniden başlatır (saniye cinsinden, örn. `/t 5` 5 saniye bekler).

```cmd
shutdown /r /fw /t 0
```


## powercfg Komutu:

+ **Şunlar için geçerlidir:** Windows 7, Windows Server 2008 R2, Windows Server 2012, Windows 8


> [!NOTE]
> `powercfg`, bilgisayarın;
> + Güç planlarını yönetir
> + Uyku (*sleep*) ve hazırda bekletme (*hibernate*) ayarlarını değiştirir.
> + Pil tüketimini analiz eder
> + Donanımın güç kullanımını raporlar


### 1. Pil raporu (laptop için)

```CMD
powercfg /batteryreport
```

> - Pil sağlığı ve geçmiş kullanım
> - Komut Çıktııs: `Battery life report saved to file path C:\Windows\System32\battery-report.html.`


### 2. Enerji raporu oluşturma

```CMD
powercfg /energy
```

> - 60 saniye sistem analiz edilir.
> - Sonunda bir **HTML rapor** oluşturur
> - Genelde: `C:\Windows\System32\energy-report.html`


## slmgr Komutu:

#### A. Yarım Sayfası

```CMD
slmgr /?
```
#### B. Lisans türü

+ Komut İstemi’ni (Yönetici olarak) aç ve şu komutu çalıştır:

```cmd
slmgr /dli
```

Açılan pencerede:
- `Retail` yazıyorsa → Başka bir bilgisayara **Aktarılabilir**
- `OEM` yazıyorsa → Başka bir bilgisayara **Aktarılamaz**

> [!NOTE]
> #### 1️⃣ Retail (Perakende) Lisans
> Eğer Windows 11’i ayrı olarak satın aldıysan (Microsoft Store, fiziksel kutu vs.) bu genelde **Retail lisans** olur.
> + 🔹 **Aktarılabilir mi?** → ✅ Evet
> + 🔹 Şart: Eski bilgisayardan lisansın kaldırılması gerekir.
> + 🔹 Aynı anda iki bilgisayarda kullanılamaz.
> 
> Microsoft’un resmi lisans politikalarına göre Retail lisanslar başka bir cihaza taşınabilir.
> #### 3️⃣ Volume (Kurumsal) Lisans
> Eğer Windows 11 bilgisayarı satın aldığında hazır yüklü geldiyse (örneğin Dell, HP, Lenovo vb.), bu genelde OEM lisanstır
> + 🔹 **Aktarılabilir mi?** → ❌ Hayır
> + 🔹 Anakart ile eşleştirilmiştir.
> + 🔹 Başka bilgisayara yasal olarak taşınamaz.
> 
> OEM lisans donanıma (özellikle anakarta) gömülüdür.
