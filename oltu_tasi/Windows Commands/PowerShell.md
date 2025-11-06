#windows #powershell


## `Copy-`
### Copy-Item:
###### Örnek 1: Söz dizimi(Syntax)
```powershell
PS C:\Users\tanju> Copy-Item -Path <Kaynak> -Destination <Hedef>
```

## `Get-` 
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


### Remove-Item:
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
