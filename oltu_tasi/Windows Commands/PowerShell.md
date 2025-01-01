#windows

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


### Copy-Item:
###### Örnek 1: Söz dizimi(Syntax)
```powershell
PS C:\Users\tanju> Copy-Item -Path <Kaynak> -Destination <Hedef>
```


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

