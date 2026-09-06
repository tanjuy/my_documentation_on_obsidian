#windows #powershell


## `Copy-`
### Copy-Item:
###### Örnek 1: Söz dizimi(Syntax)
```powershell
PS C:\Users\tanju> Copy-Item -Path <Kaynak> -Destination <Hedef>
```

## `Get-` 

### Get-Content:

**Amaç:** Bir dosyanın içeriğini satır satır okuyup çıktı olarak verir (nesne akışı olarak).

#### 1. Temel Sözdizimi:

```powershell
Get-Content
    [-Path] <String[]>
    [-ReadCount <Int64>]
    [-TotalCount <Int64>]
    [-Tail <Int32>]
    [-Filter <String>]
    [-Include <String[]>]
    [-Exclude <String[]>]
    [-Force]
    [-Credential <PSCredential>]
    [-Delimiter <String>]
    [-Wait]
    [-Raw]
    [-Encoding <Encoding>]
    [-AsByteStream]
    [-Stream <String>]
    [<CommonParameters>]
```

https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-content?view=powershell-7.6

### Get-Command:

+  PowerShell'de **`Get-Command`**, sistemde mevcut olan komutları, cmdlet'leri, fonksiyonları(Function) ve uygulamaları(Application) bulmak için kullanılır.
+ **Linux'taki `which` veya CMD'deki `where` komutuna benzer**, ancak daha güçlüdür.


> [!NOTE]
> + **Cmdlet** → PowerShell'in dahili komutları
> + **Function** → PowerShell fonksiyonları
> + **Application** → Harici yürütülebilir dosyalar (.exe)
> + **Alias** → Cmdlet’lere kısayol olan isimler

#### Bir Uygulamanın Yerini Bulma:

```powershell
Get-Command notepad.exe
```

```powershell
CommandType     Name               Version      Source
-----------     ----               -------      ------
Application     notepad.exe        10.0.26...   C:\Windows\system32\notepad.exe
```

#### Belirli sütünleri Erişim:

```powershell
(Get-Command notepad.exe).Source
```
> **Explanation:**
> + `Get-Command notepad.exe` çıktısındaki her bir kolona bu şekil de ulaşabiliriz.

**Çıktı:**
```powershell
C:\Windows\system32\notepad.exe
```

#### Tüm `cmdlet` komutlarını listeleme:

```powershell
Get-Command -CommandType cmdlet
```
> **Explanation:**
> + **Cmdlet** → PowerShell'in dahili komutları

**Çıktı:**
```powershell
CommandType     Name                                            Version    Source
-----------     ----                                            -------    ------
Cmdlet          Add-AppProvisionedSharedPackageContainer        3.0        Dism
Cmdlet          Add-AppSharedPackageContainer                   2.0.1.0    Appx
Cmdlet          Add-AppxPackage                                 2.0.1.0    Appx
Cmdlet          Add-AppxProvisionedPackage                      3.0        Dism
Cmdlet          Add-AppxVolume                                  2.0.1.0    Appx
Cmdlet          Add-BitsFile                                    2.0.0.0    BitsTransfer
Cmdlet          Add-CertificateEnrollmentPolicyServer           1.0.0.0    PKI
Cmdlet          Add-Computer                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-Content                                     3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-History                                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-JobTrigger                                  1.1.0.0    PSScheduledJob
Cmdlet          Add-KdsRootKey                                  1.0.0.0    Kds
...
```

#### Tüm harici uygulamaları (.exe) listeleme:

```powershell
Get-Command -CommandType Application
```

**Çıktı:**
```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Add-AppProvisionedSharedPackageContainer           3.0        Dism
Cmdlet          Add-AppSharedPackageContainer                      2.0.1.0    Appx
Cmdlet          Add-AppxPackage                                    2.0.1.0    Appx
Cmdlet          Add-AppxProvisionedPackage                         3.0        Dism
Cmdlet          Add-AppxVolume                                     2.0.1.0    Appx
Cmdlet          Add-BitsFile                                       2.0.0.0    BitsTransfer
Cmdlet          Add-CertificateEnrollmentPolicyServer              1.0.0.0    PKI
Cmdlet          Add-Computer                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-Content                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-History                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-JobTrigger                                     1.1.0.0    PSScheduledJob
Cmdlet          Add-KdsRootKey                                     1.0.0.0    Kds
Cmdlet          Add-LocalGroupMember                               1.0.0.0    Microsoft.PowerShell.LocalAccounts
...
```

### Get-Location:
###### Örnek 1: Yarım Sayfası
```powershell
PS C:\Users\tanju> Get-Location -?
```
> **Explanation:**
> `Get-Location` hakkında yardım sayfasını açar. 
###### Örnek 1: Dizin Konumu
```powershell
PS C:\Users\tanju> Get-Location 
```
> **Explanation:**
> Bulunduğumuz dizini ekrana basar, *linux* de  `pwd` komutudur . 

### Get-NetTCPConnection:


### Get-CimInstance:

+ **`Get-CimInstance`**, PowerShell’de **CIM (Common Information Model)** sınıflarını sorgulamak için kullanılan **modern ve önerilen** bir komuttur.

+ `Get-CimInstance`
	- Windows’un sistem bilgilerini
	- Donanım, işletim sistemi, servisler, süreçler vb.
	- **CIM / WMI altyapısı üzerinden** 

#### Örnek 1: Win32_WinSAT

+ `Get-CimInstance Win32_WinSAT`, **Windows işletim sisteminde Windows System Assessment Tool (WinSAT)** tarafından yapılan donanım performans değerlendirme sonuçlarını **PowerShell üzerinden sorgulamak** için kullanılan bir komuttur.

```powershell
Get-CimInstance Win32_WinSAT
```

**Komut Çıkıtısı:**

```powershell
CPUScore              : 9,2
D3DScore              : 9,9
DiskScore             : 8,65
GraphicsScore         : 7,9
MemoryScore           : 9,2
TimeTaken             : MostRecentAssessment
WinSATAssessmentState : 1
WinSPRLevel           : 7,9
PSComputerName        :
```


> [!NOTE]
> #### Win32_WinSAT nedir?
> **Win32_WinSAT**, Windows Management Instrumentation (WMI) / CIM sınıfıdır ve:
> + CPU
> + RAM
> + Grafik
> + Disk
> 
> bileşenlerinin **WinSAT tarafından ölçülen performans skorlarını** içerir.
> + Bu skorlar, eski adıyla **Windows Experience Index (WEI)** verileridir.


### Get-FileHash:

`Get-FileHash`, PowerShell'de bir dosyanın **kriptografik özetini (hash değerini)** hesaplayan cmdlet'tir. Bu hash değeri, dosyanın içeriğini temsil eden sabit uzunlukta bir karakter dizisidir.

Bu komut genellikle şu amaçlarla kullanılır:

- Dosyanın değiştirilip değiştirilmediğini doğrulamak.
- İndirilen dosyanın bütünlüğünü (integrity) kontrol etmek.
- Bir dosyanın orijinal olup olmadığını doğrulamak.
- Güvenlik analizleri ve adli bilişim (digital forensics) çalışmalarında dosya kimliği oluşturmak.

#### Örnek 1:

```powershell
Get-FileHash ".\Rocky-10.2-x86_64-minimal.iso" -Algorithm SHA256
```

Hash değerleri aynıysa:
- Dosya bozulmamıştır.
- İndirme sırasında veri kaybı yaşanmamıştır.
- Dosya büyük olasılıkla yayınlanan dosyanın aynısıdır.


> [!TIP]
> #### Büyük Dosyalarda Performans
> `Get-FileHash` dosyanın tamamını okuyarak hash hesaplar. Bu nedenle:
> - 1 GB dosya → tamamı okunur.
> - 100 GB dosya → tamamı okunur.
> 
> Ancak dosyanın tamamı belleğe yüklenmez; akış (stream) halinde okunur. Bu sayede çok büyük dosyalar için de bellek kullanımı düşük kalır, ancak okuma süresi dosya boyutuna bağlı olarak artar.

| Özellik                  | Açıklama                                                           |
| ------------------------ | ------------------------------------------------------------------ |
| Amaç                     | Dosyanın hash değerini hesaplamak                                  |
| Varsayılan algoritma     | SHA256                                                             |
| Desteklenen algoritmalar | SHA1, SHA256, SHA384, SHA512, MD5                                  |
| Kullanım alanı           | Dosya bütünlüğü doğrulama, güvenlik, adli bilişim, yedek doğrulama |
| Büyük dosyalar           | Dosya akış halinde okunur; tamamı RAM'e yüklenmez                  |

## Remove-Item:
+ Dosya silme ve Dosya silme işlemi yapar.

```powershell
PS C:\Users\tanju> Remove-Item fileName
```
> **Explanation:**
> + Mevcut dizin içerisinde `fileName` adlı dosyayı kaldıracaktır.

```powershell
PS C:\Users\tanju> Remove-Item fileName1, fileName2, fileName3
```
> **Explanation:**
> + Mevcut dizin içerisinde ardışık dosya silme işlemi
> + Örneğin; burada 3 dosyayı aynı anda silecektir.


> [!NOTE]
> + `Remove-Item`'ın alias'ı `rm` olmaktdir.

## `Test-`
### Test-NetConnection:
+ `Test-NetConnection`, Windows PowerShell'de kullanılan ve ağ bağlantılarını test etmek için geliştirilmiş bir cmdlet'tir.
+ Bu cmdlet, belirli bir IP adresine, etki alanına, bilgisayara veya porta olan bağlantıyı test etmek için kullanılır.

####  `Test-NetConnection` Cmdlet'inin Özellikleri:
1. **Ping Testi:** Hedef bilgisayara(IP adresi veya Domain alanı) ICMP paketleri gönderme:
2. **Port Kontrolü:** 

#### 1.Ping Testi:
+ Bir bilgisayara veya Web sitesine ping göndermek için kullanılır.

```powershell
PS C:\Users\tanju> Test-NetConnection www.google.com
```

**Çıktı:**
```powershell
ComputerName           : www.google.com
RemoteAddress          : 216.58.212.36
InterfaceAlias         : Wi-Fi
SourceAddress          : 192.168.1.106
PingSucceeded          : True
PingReplyDetails (RTT) : 18 ms
```

#### 2.Port Kontrolü:

## Rename-

### Rename-Item:

+ Tek bir dosyayı yeniden adlandırma

```powershell
Rename-Item -Path "eski_dosya.txt" -NewName "yeni_dosya.txt"
```


> [!NOTE] Title
> **Kısa kullanım:**
> ```powershell
> Rename-Item "C:\temp\eski.txt" "yeni.txt"
> ```
