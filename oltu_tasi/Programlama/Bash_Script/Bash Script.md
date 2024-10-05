#Bash_Script 

>[!INFO]
> Bash açılımı:  *Bourne Again Shell*
> Ubuntu da yüklü olan Shell'ler `/etc/shells` dosyasında mevcuttur.
>``` bash
> $ cat /etc/shells
> ```

> [!WARNING] Uyarı 1:
> + `#!/usr/bin/bash` komut  dosyamıza çalışma izni verdiğimizde bu dizini kullanarak script'i çalıştırıyor. Çalışma yolunu `$ which bash` komut ile bulabilirsiniz.
> + `#!/usr/bin/env bash` komutunda kullanılabilir. Çalışma dizini `$ which env` komut ile dizin yolunu bulunabilir. Ayrıca env komutun görevi işletim sisteminde bash yolunu kendi bulup çalıştır. İşletim sistemin(linux) bağlı olarak bash dizin yolu çok değişiyorsa env size çok faydası olacaktır. 

> [!WARNING] Uyarı 2:
> Uyarı 1'deki işlemleri yaptıysanız dosyamıza çalışma izni vermemiz gerekmektedir. Bu işlem için `$ chmod +x bash_script_file_name.sh` daha sonrasında `./bash_script_file_name.sh` ile çalıştırabilirsiniz. İzinleri görmek için ise `ls -al` komutunu kullanabilirsiniz.
### Merhaba Dünya:
```bash
#!/usr/bin/bash

echo "Merhaba Dünya"    # 1
```
> **Explanation:**
>  1. `echo` komutu ekrana çıktı verir. Burada ekrana Merhaba Dünya yazdırır.
> 	+ Uyarı 2'deki işlemleri geçekleştiriyoruz.
> 	+ Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=CGJ8XZf8nPc&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=2)

> [!TIP]
> `#!` gibi başlayan komutlar `shebang` nedir. Örneğin; yukarıda olduğu gibi `#!/usr/bin/bash`

### Script Çalıştırma:
```shell
$ bash Merhaba_dünya.sh                              # 1 yol
```
OR
```shell
$ chmod +x Merhaba_dünya.sh                          # 2 yol
$ ./Merhaba_dünya.sh
```
> **Explanation:**
> Script'i iki farklı şekilde çalıştırabiliriz:
> 1. Burada dosya çalışma izini vermeden direk çalıştırabiliriz
> 2. Bu yolda ise `chmod` ile çalışma izni verilmelidir ayrıca script'i çalıştıracak `#!/usr/bin/bash` komut en başa yazılmalıdır.

### Değişkenlar:

>[!INFO]
>İki tür değiken(variable) vardır;
>1. *Sistem değişkenleri (System Variables)*: İşletim sistemi ile gelen değikenlerdir.
>2. *Kullanıcı değişkenleri (User Variables)*: Sonradan kullanıcı tarafından oluşturulan değişkenlerdir.
>Değiken türleri string veya integer olabilir.

##### Sistem Değişkenleri:
```bash
#!/usr/bin/env bash

# Systems Variables
echo $BASH                     # 1
echo "$BASH_VERSION"           # 2
echo $HOME                     # 3
echo $PWD                      # 4
```
> **Explanation:**
> Yukarıda anlatıldığı gibi OS(işletim sistemi) ile gelirler ve
> 	1. bash komutun bulunduğu dizini verir: `/usr/bin/bash`
> 	2.  ==Eğer dikkat ederseniz== # 2 ile gösterilen değişkende çift tırnak kullanılmış. Buda değişkenlerin çift tırnaklar içerisine yazılabileceğini göstermektedir. Bunun ileride göreceğiniz üzeri pek çok avantajı mevcuttur. Bash versiyonu verir: `5.1.16(1)-release`
> 	3. Çalıştırılan ev dizini verir: `/home/ottoman`
> 	4. `$ pwd` komutunda olduğu gibi çalışma dizini verir.
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=WC_Wk_NZ0C4&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=3)

1. `$HOSTNAME`: 
##### Kullanıcı Değişkenleri:
```bash
# User Variables
ad=linux                     # 1
isletim_sistemi=ubuntu       # 2
yorum="linux is awesome"     # 3
tamSayi=5                    # 4

echo $ad                     # 1
echo "$isletim_sistemi"      # 2
echo $yorum                  # 3
echo $tamSayi                # 4
```

> **Explanation:**
> 1. En temel bir değişken oluşturduk ve ekran bastık
> 2. Birden fazla kelimeli bir değişken oluştururken nasıl kullandığımıza dikkat edin ve ayrıca çift tırnaklar içerisinde ekrana bastık.
> 3. Ayrıca değişkenlere string değerlerde verebiliyoruz ve bunu ekran basıyoruz.
> 4. Değişkenlerimize tam sayılarda verebiliyoruz. Dikkat ederseniz bu değişken tanımlarken *camel case* kullandık
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=WC_Wk_NZ0C4&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=3)

>[!CAUTION] Dikkat:
>Değişkenlerimize değer atarken yukarıda da olduğu gibi boşluk bırakmamalıyız!
>Değişkenleri tanımlarken değişken önüne rakam vermeyiniz. Örneğin; `5ad=linux`

##### `$variable` ile`${variable}` kıyaslama:
> [!CAUTION] Dikkat:
> `distro="Ubuntu"` değişken tanımlarsak, 2 farklı şekilde kullanabiliriz:
>`$distro` ile `${distro}` kullanımın temel olarak arasında bir fark yok ama `${distro}` daha fazla ek özellikleri vardır.
###### Örnek 1:  Basit Kullanımı:
```bash
#!/usr/bin/env bash

variable="linux"

echo "$variable_name"                           # 1
echo "${variable}_name"                         # 2
```
> **Explanation:**
> 1. Değişkenimizi karakter dizi(string) ile birleştirildiğinde yeni değişken oluşuyor ama
> 2. Süslü parantezleri kullandığımızda karakter dizisi(string) birleştirebiliyoruz.

###### Örnek 2: Değişken ismini dinamik yapma:
```bash
#!/usr/bin/env bash

prefix="İşletim Sistemi"
suffix="Dağıtım"

OS_distro="${prefix}_${suffix}"
echo OS_distro
```
> **Explanation:**
> Süslü parantezler ile yeni bir değişken oluşturduk.

###### 3. Değişkenin Varsayılan Değeri:
```bash
#!/usr/bin/env bash

distro="Arch Linux"
echo "${distro:-Ubuntu}"
```
> **Explanation:**
> distro değişkenine değer(*Arch Linux*) atanırsa ekrana basar. Aksi taktirde distro değişkenine değer atanmasa *varsayılan değer olarak Ubuntu* ekrana basar. 

###### 3.1 Değişkene değer verme, değer atma:
```bash
#!/usr/bin/bash

# distro=Linux
echo "${distro:=Pardus}"     # Çıktı: Pardus
echo $distro                 # Çıktı: Pardus
```
> **Explanation:**
> + `${distro:=Pardus}` işlemi; eğer *distro* adındaki değişkene değer atanmamışsa *distro* değişkenine *Pardus* değeri atanır.
> + Eğer *distro* değişkenine *Linux* değerini verirsek distro'un tüm değerleri *Linux* olur.
###### 3.2 `${variable:?hata}`:
```bash
#!/usr/bin/bash

echo ${distro:?hata mesajı}
```
> **Explanation:**
> + Eğer distro adlı değişkene değer atanmadıysa soru işaretinden sonra gelen mesaj ekran hata mesajı olarak yazılır ve bash script durur.

###### 3.3 `${variable:+newValue}`: 
```bash
#!/usr/bin/bash

distro=Pardus
echo ${distro:+Debian}      # 1     # Çıktı: Debian
echo $distro                # 2     # Çıktı: Pardus
```
> **Explanation:**
> 1. `distro` değişkeni atanmış değer değil de `Debian` değerini ekran basar 
> 2. ama tekrar değişkeni ekran basarsak kendi değeri yani `Pardus` basar.
> 	+ **UYARI:** Öncesinde değişken tanımlanmışsa ekran çıktı vermez.

###### 4. `${#variable}`:
```bash
#!/usr/bin/bash

distro="Linux"
echo "Karakter Sayısı: ${#distro}"         # Çıktı: Karakter Sayısı: 5
```
> **Explanation:**
> + `distro` değişkenin kaç karakterden oluştuğunu ekrana çık verir.

###### 5. Karakter Dizi Maniplasyonu:
```bash
#!/usr/bin/env bash

string="Linux is Awesome"
echo ${string:6:5}                 # çıktı: is Aw
```
> **Explanation:**
> 1. Değişkenimizi tutmuş olduğu karakter dizini dilimleyebiliyoruz.
> 2. Temel yapısı: **${variable:start:length}**
> 	+ **variable:** Parçalanacak olan dizgeyi barındıran değişkenin adıdır.
> 	+ **start:** Dizgedeki başlangıç noktasıdır. Bu indeks sıfırdan başlar. Yani ilk karakter `0`, ikinci karakter `1` vb. şeklinde numaralandırılır.
> 	+ **length:** strat'dan sonra kaç karakter alınacağını belirtir.
> 3. **6:** start'a karşılık gelir, **5:** length'e karşılık gelir.
> 4. **Özeti:** *string değişkeninin 6. karakterine gel ve 6. karakterden sonra 5 karakter al.*

###### 6. Büyük harf -> Küçük harf
```bash
#!/usr/bin/bash

text="LINUX IS AWESOME!"

lowerCaseText="${text,,}"
echo "$lower_case_text"
```
> **Explanation:**
> + Bash 4.0 ve üstü sürümlerde, bir değişkenin içeriğini küçük harfe çevirmek için `${var,,}` biçimini kullanabilirsiniz.
> + Süslü parantez özeliği ile değişken içeriğini *büyük -> küçük harfe* dönüştürdük.
> + **Alternatif:** `echo "Linux" | tr [:upper:] [:lower:]`

###### 6.1. İlk Harfi Küçültme:
```bash
#!/usr/bin/bash

text="LINUX IS AWESOME!"

lowerCapitalText="${text,}"        # Çıktı: lINUX IS AWESOME!
echo "$lowerCapitalText"
```
> **Explanation:**
> + `text` adlı değişkenin içerisindeki metni ilk harfini küçük harfe çevirir.

###### 6.2. Küçük harf -> Büyük harf
```bash
#!/usr/bin/bash

text="linux is awesome!"
upper_case_text="${text^^}"

echo "$upper_case_text"
```
> **Explanation:**
> Bash 4.0 ve üstü sürümlerde, bir değişkenin içeriğini büyük harfe çevirmek için `${var^^}` biçimini kullanabilirsiniz.
> `"${text^^}"` ifadesi, `text` değişkenindeki tüm harfleri *büyük harfe dönüştürür.*

###### 6.3. İlk Harfi Büyütme:
```bash
os=linux
echo "${os^}"       # Çıktı: Linux
```


>[!INFO]
> + Bash script'in yorum işaret kare'dir; `# bu bir yorumdur.` Yukarıda kullanıldığı gibi.

###### 7. `${variable##/*/}`:

```bash
#!/usr/bin/bash

path=/home/ottoman/bashDersleri/linux.sh

fileName="${path##/*/}"            # 1   # Çıktı: linux.sh
# fileName="${path##*/}"           # 2   # Çıktı: linux.sh
echo "Dosya adı: $fileName"

fileName1="${path#/*/}"            # 3   # Çıktı: ottoman/bashDersleri/linux.sh
echo "Dosya adı 1: $fileName1"
```
> **Explanation:**
> 1. `${path##/*/}` için;
> 	+ `##`: En uzun eşleşmeyi ifade eder.
> 	+ `/*/`: Dize içinde `/` ile başlayan ve `/` ile biten her şeyi ifade eder.
> 2. `path` değişkeninde en uzun `/` ile başlayan ve biten kısmı
> 3. `${path#/*/}` için;
> 	+ `#` Sağdan `/` kadar olan en kısa kesme yapacak.
> 	+ `/*/`: Dize içinde `/` ile başlayan ve `/` ile biten her şeyi ifade eder.

###### 7.1 `${variable%%/*/}`:
```bash
#!/usr/bin/bash

path=/home/ottoman/bashDersleri/linux.sh

fileName="${path%%.sh}"      # 1  # Çıktı:/home/ottoman/bashDersleri/linux 
echo "Dosya Yolu: $fileName"

fileName1="${path%.sh}"      # 2  # Çıktı:/home/ottoman/bashDersleri/linux
echo "Dosya Yolu 2: $fileName1"
```
> **Explanation:**
> 1. Sağdan kesme yaptığı için sadece *sh* uzantısı kesildi. Ayrıca `%%` en uzun kesme işlemi yapar.
> 2. Aynı çıktıyı verir ama `%` en kısa kesme işlemini yapar.

> [!TIP]
> + `${variable##/*/}` : soldan silme işlemini yapar.
> + `${variable%%/*/}` : sağdan sime işlemini yapar. 

###### 8. `${!variable}`:
```bash
#!/usr/bin/bash

OS="Ubuntu"
echo "OS değişken: ${OS}"         # Çıktı: Ubuntu   

linux="OS"
echo "linux değişken: ${linux}"   # Çıktı: linux

echo "!linux değişken: ${!linux}" # Çıktı: Ubuntu   # 1
```
> **Explanation:**
> 1. Normal olarak `linux` değişkenin değeri `OS` yazar ama `!` dolayı `linux` tutuğu değeri olan `Ubuntu` değerini yazar.

###### 9. `${variable/old/new}`
```bash
#!/usr/bin/bash

dir=/usr/local/bin
newDir=${dir/usr/opt}             # 1

echo "Eski dizin: $dir"
echo "Yeni dizin: $newDir"
```
> **Explanation:**
> 1. `dir` adlı değişkendeki `usr` kelimesini `opt` kelimesi ile değiştiriyoruz. 
> 	+ **UYARI:** Sadece ilk kelimeyi değiştirir.

###### 9.1. `${variable//old/new}`
```bash
#!/usr/bin/bash

userLine=$(grep ottoman /etc/passwd)         # 1 
echo "Eski Kullanıcı: $userLine"

newUserLine=${userLine//ottoman/osmanli}         # 2
echo "Yeni Kullanıcı: $newUser"
```
> **Explanation:**
> 1. `/etc/passwd` dosyasında `grep` komut ile `ottoman` geçen satır veya satırları `userLine` adlı değişkene atıyoruz.
> 2. `userLine` değişkenindeki `ottoman` kelimesini `osmanli` kelimesi ile değiştiriyoruz
> 	+ **UYARI:** Tüm kelimeleri değiştirir.

###### 9.2 `${variable/deleteWord}`:
```bash
#!/usr/bin/bash

floatNum=123.456

integer1=${floatNum/.}                          # 1
echo "Nokta işaretini sil: $integer1"

integer2=${floatNum/.*}                         # 2
echo "Nokta işaretinden sonra sil: $integer2"
```
> **Explanation:**
> 1. `floatNum` adındaki değişkeninde nokta`(.)` işaretini siler.
> 2. `floatNum` adındaki değişkeninde yıldız`(*)` meta karakteri ile noktadan`(.)` sonra gelen tüm ifadeleri sil. 
###### 9.3 `${variable/#new/old}`:
```bash
#!/usr/bin/bash

fileName1=shScript.sh
echo "Değişken adı: $fileName1"        # Çıktı: shScript.sh    

fileName2="${fileName1/#sh/bash}"      # Çıktı: bashScript.sh  # 1
echo "Yeni değişken adı: $fileName2"
```
> **Explanation:**
> 1. değişken içerisinde  `sh` geçen harfleri `bash` harfleri ile değiştirmektedir. Ama  `#` işareti sadece sol taraftan eşleşen bir kere değişiklik yapılmasını sağlar. Eğer dikkat etiyseniz  sondaki `sh` da bir değişiklik olamadığıdır. 

###### 9.3 `${variable/%new/old}`:
```bash
#!/usr/bin/bash

fileName1=shScript.sh
echo "Değişken adı: $fileName1"        # Çıktı: shScript.sh    

fileName2="${fileName1/%sh/bash}"      # Çıktı: shScript.bash  # 1
echo "Yeni değişken adı: $fileName2"

```
> **Explanation:**
> 1. Yukarıdakinin aynısı ama değişiklik yapmaya sağdan başlar ve bir kez yapar.
### Read Kullanımı:
>[!INFO]
> + `read komut` kullanıcıdan girdi almak için kullanılır

###### Örnek 1: Read ile Girdi Alma
```bash
#!/usr/bin/env bash

echo -n "Lütfen işlem sistemini giriniz: "             # 1
read distro                                            # 2
echo "İşletim sisteminiz: $distro"                     # 3
echo "İşletim sisteminiz: ${distro}"                   # 4
```
> **Explanation:**
> 1. `echo` komut ile ekrana basıyoruz ama -n parametresi ile *yeni bir satıra(trailing newline)* geçmesini durduruyoruz.
> 2. `read` komut ile girilen değeri distro değişkene veriyoruz.
> 3. Çift tırnak kullanarak hem karakter dizisi (string) değer yazıyoruz hem de değişkeni yazdırıyoruz. 
> 4. 3. basamak ile aynı ama böyle değişken yazdırman ek özelikleri vardır aşağıda açılanmıştır.

###### Örnek 2: Read ile Birden Fazla Girdi Alma
```bash
#!/usr/bin/env bash

# echo -n "Linux Dağıtımları: "; read distro1 distro2 distro3     # 1
read -p "Linux Dağıtımları: " distro1 distro2 distro3             # 2

echo "Linux Distros: $distro1 - $distro2 - $distro3"
```
> **Explanation:**
> `read` komut ile birden fazla girdi alabiliriz
> 1 deki adımı daha kısaltarak 2'inci adım ile girdi alabiliriz. Aynı görevi görür.

###### Örnek 3: Şifre Yazılışını Gizleme(slience)
```bash
#!/usr/bin/env bash

read -p "Kullanıcı ad: " username
read -sp "Şifreniz: " password                     # 1
echo
echo "Kullanıcı adınız: $username ve Şifreniz: $password"
```
> **Explanation:**
> `-s parametresi` ile girilen değeri ekran yazılmasını kapatıyoruz.
> `-p parametresi` ile girdi öncesi kullanıcıyı bilgilendirebiliyoruz.

###### Örnek 4: REPLY Değişkeni
```bash
echo -n "Linux distro'nuzu giriniz: "; read
echo "Linux distro: $REPLY"
```
> **Explanation:**
> Sistem değişkeni olan REPLY read'den gelen değeri alır. 
> Video

###### Örnek 5: read ile array parametresi
```bash
echo -n "Enter 3 Linux Distros: "
read -a distros
echo "Distro sırası: ${distros[0]}, ${distros[1]}, ${distros[2]}"
```
> **Explanation:**
> `read -a distros` komutu okunan veya alınan değerleri array dizi değişkenin(distros) sıralı indeksine atıyoruz. Script çalıştırıldığında girdi şu şekilde oluyor: 
> `Enter 3 Linux Distros: Arch Ubuntu Debian` girdi vermeliyiz veya her değer girdiğimizde *Enter* tuşuna basmalıyız.


### Bash Script Argümanlar

+ Bash Script çalıştırılmadan verilen girdilerdir. Argümanların bir diğer adı **Pozisyonel parametreler** ve İngilizcesi: **Positional parameters** 
###### Örnek 1: `$1, $2, $3 ...` 
**Bash Script Dosyası: bash_argument**
```bash
#!/usr/bin/env bash

echo "Dosyanı ismi: $0"
echo "İlk Argüman: $1"
echo "İkinci Argüman: $2"
echo "Üçüncü Argüman: $3" 
```

**Bash Script Çalıştırma İşlemi:**
```shel
$ ./bash_argumants Linux Mac Windows              
```
> **Explanation:**
>  + Dosyamızı dikkat ederseniz bash script için özel değişkenleri verdik.
>  + Dosyayı(Bash Script) çalıştırma aşmasında argüman olarak Linux($1), Mac($2) ve Windows($3) argümanlarını verdik ve her biri sırasıyla değişkenlere atandı.
>  + Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)

>[!CAUTION]
> + $0 dosyanın isimine karşılık gelir yani $0 eşittir ./bash_arguments.sh

###### Örnek 2: Tüm Argümanlar `$@`
```bash
echo $@
echo ${@}
```

```shell
$ ./bash_arguments Linux Mac Windows 
```
OR
```shell
$ ./bash_arguments Linux Mac
```

> **Explanation:**
> + Tüm değişkenlere karşılık gelmektedir. $@ eşittir `$1, $2, $3 ...` 
> + Değişkenlerde kullanılan süslü parantez de mevcuttur: `${@}` 
> + Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)

> [!WARNING] Uyarı:
> Eğer alınacak argüman sayısı belirli değilse yan bash script programınıza göre bazen 3 argüman alırken bazen 5 argüman alıyorsa `$@` bash script de özel olan bu değişkeni kullanabilirsiniz.

###### Örnek 3: `$@` de sıfırıncı indeks
**Bash Script Dosyası: bash_arguments.sh**
```bash
#!/usr/bin/env bash

echo "Girilen Argüman Sayısı: $#"           # Linux Mac Windows
dizi=($@)
# dizi=("$@")
echo "0.index: ${dizi[0]}"                  # Linux
```

**Terminal**
```shell
$ ./bash_arguments Linux Mac Windows
```
> **Explanation:**
> Dosyamızı çalıştırırsak girilen argüman da 0.index'i Linux olacaktır.
> >  Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)

> [!WARNING] Uyarı:
> `$0, $1, $2, $3, ...` girilen argümanlarda 0. indeks *dosyanın adı*
> `$@` da girilen argümanlarda 0. indeks *ilk argüman* oluyor.

###### Örnek 4: Tüm string argünmalar  `$*`
**Bash Script Dosyası: bash_arguments.sh**
```bash
echo $*              # Çıktı: Linux Mac Windows Solaris
```

**Terminal**
```shell
$ ./bash_arguments.sh Linux Mac Windows Solaris 
```
> **Explanation:**
> Tüm konumsal parametreleri tek bir kelime olarak birleştirir ve bu kelimeleri bir dize (string) olarak döndürür.
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)

###### Örnek 5: `$@` ile `$*` Arasındaki Fark

**Bash Script Dosyası: bash_arguments.sh**
```bash
echo "Argüman Sayısı: $#"
diziAt=("$@")
diziStar=("$*")

echo "${diziAt[0]}"                    # Çıktı: Linux
echo "${diziStar[0]}"                  # Çıktı: Linux Mac Windows Solaris
```

**Terminal**
```shell
$ ./bash_arguments.sh Linux Mac Windows Solaris 
```

> **Explanation:**
> diziAt değişkeni ekrana indeksi 0 olanı verir yani *Linux* yazar
> diziStar değişkeni ekrana tüm argümanları yazar çünkü diziStar değişkeni tek bir değerde *string* olarak alır.
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)

###### Örnek 6:  Argüman Sayısı `$#` 
**Bash Script Dosyası: bash_argument_1**
```bash
echo $@                          # çıktı: Linux Mac Windows Solaris
echo $#                          # çıktı: 4                   
```

**Bash Script Çalıştırma İşlemi:**
```shell
$ ./bash_arguments Linux Mac Windows Solaris   
```
> **Explanation:**
>  `$#` veya `${#}` bash script özel değişkenleri, her ikiside aynı çıktıyı verir ve girilen(Linux Mac Windows Solaris) argüman saysını(4) verir.
>  Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)


> [!TIP]
> + `echo $$` komutu;
> + Bash veya diğer POSIX uyumlu kabuklarda **mevcut shell (kabuk) oturumunun işlem kimliğini (PID)** ekrana yazdırmak için kullanılır.(PID: Process ID)
> + Yani, bu komut çalıştırıldığında, o anki shell'in işlem kimliği olan bir sayı döndürülür.

### Shift Komutu:
**Tanım:** Bash script'te `shift` komutu, pozisyonel parametreleri (komut satırı argümanlarını) sola kaydırarak yönetir. Pozisyonel parametreler, bir bash script'e geçirilen argümanları ifade eder ve `$1`, `$2`, `$3`, ... gibi sembollerle erişilir. `shift` komutu her kullanıldığında, pozisyonel parametreler bir kez sola kaydırılır ve ilk argüman (`$1`) devre dışı kalır.


> [!WARNING]
> `shift` komutu `$0` argümanında kaydırma yapmaz.  `shift` komut kaydırma işlemini `$1` argümanı ile yapmaya başlar. 

###### Örnek 1: Basit Kullanımı
```bash
#!/usr/bin/env bash

echo "1.Argüman: $1"                    # windows          
echo "2.Argüman: $2"                    # linux
shift                                   # Pozisyonel parametreleri sola kaydır.
echo "shift'ten sonra 1.Argüman: $1"    # linux
echo "shift'ten sonra 2.Argüman: $2"    # unix
```

**Terminal:**
```shell
$ ./apps.sh windows linux unix
```

> **Explanation:**
> 1. Eğer bu bash script'in adı `apps.sh` olursa ve linux terminal de  
> 	+ 1.Argüman: windows, 2.Argüman: linux  olacaktır.
> 2. *Shift komutndan sonra*:
> 	+ 1.Argüman: linux, 2. Argüman: unix olacaktır.

###### Örnek 2: shift parametresi ile
```bash
#!/usr/bin/env bash

echo "1.Argüman: $1"                 # windows        
echo "2.Argüman: $2"                 # unix
echo "3.Argüman: $3"                 # linux
shift 2                              # Pozisyonel parametreleri 2 adım kaydır.
echo "Shift'ten sonra 1.Argüman: $1" # linux
```

**Terminal:**
```shell
$ ./apps.sh windows unix linux
```
> **Explanation:**
>  + Eğer bash script dosyanın adı `apps.sh` olursa ve girilen argümanlarda 2 adım kaydırdığımızda(*shift komutu*) sadece *linux* çıktısını verecektir

### Mantık Komutları:
#### test komutu:
```bash
test <expression>
```
Veya
```bash
[ <expression> ]
```
> **Explanation:**
> + Yukarıda test komutun genel kullanımı verilmiştir.
> + `test` komutu, dosya ve dizinlerin durumunu kontrol etmek, karşılaştırmalar yapmak ve mantıksal ifadeleri değerlendirmek için kullanılır.
> + `test` komutu, bir ifadenin veya koşulun doğru olup olmadığını kontrol eder ve sonucuna göre `0` (başarı) veya `1` (başarısızlık) döndürür.
> + `test` komut koşullu ifadelerde sıklıkla kullanılır.

##### 1. Dosya ve Dizin Kontrolleri:
1. ` -e <file>` :  Dosya veya Dizin var mı?
2. ` -f <file>` :  Dosya var mı ve düzenli bir dosya(*a regular file*) mı?
3. ` -d <directory` :  Dizin var mı ve gerçekten bir dizin mi?
4. ` -r <file>` : Dosya okunabilir mi?
5. ` -w <file>` : Dosya yazılabilir mi?
6. ` -x <file>` : Dosya çalıştırılabilir mi?
7. ` -s <file>` : Dosya var mı ve boyutu 0'dan büyük mü?

###### Örnek 1: Dosya veya Dizin var mı?
```bash
$ test -e /etc/passwd                  # 1
```
Veya
```shell
$ [ -e /etc/passwd ]                   # 2
```

```bash
$ echo $?
```

> **Explanation:**
> 1. etc dizininde passwd dosyası var mı diye bakıyoruz. Eğer komutu çalıştırsanız, çıktı vermeyecektir hemen arkasından `echo $?` komut çalıştırılırsa çıktısı 0 verirse true yani dosya mevcut aksi taktirde 1 verirse false dosya mevcut değildir.
> 2.  1 de yazılanla aynıdır.

###### Örnek 2: Dosya var mı?
```shell
$ [ -f /etc/passwd ]                # test -f /etc/passwd
```
> **Explanation:**
> etc dizininde passwd dosyası var mı diye bakılıyor. `echo $?` komutunu çalıştırsak 0 verirse başarılı 1 verirse başarısız yani dosya yok orada.
> yorum(#) satırı ile alternatifi verilmiştir.

###### Örnek 3: Dizin var mı?
```shell
$ [ -d /home/ottoman ]               # test -d /home/ottoman 
```
> **Explanation:**
> + home dizini altında ottoman dizini var mı diye bakıyoruz. `ècho $?` komut başarılı ise 0 verir aksi taktirde 1 verir.
> + yorum(#) satırı ile alternatifi verilmiştir.

##### 2. Sayı Karşılaştırılması:
1. `-eq` :  equal                -> eşittir.
2. `-ne` :  not equal         -> eşit değil
3. `-gt` :  greater than    -> büyüktür
4. `-ge` :  great or equal -> büyük veya eşittir
5. `-lt` :  less than          -> küçüktür
6. `-le` : less or equal     -> küçüktür veya eşittir

###### Örnek 1: -eq (eşittir)
```shell
$ test 5 -eq 5                     # [ 5 -eq 5 ]
```
> **Explanation:**
> + operand'lar tam sayı(5) olduğu için `-eq` kullanıldı ve *5 sayısı 5 sayısına eşit mi* sorar.
> + Ayrıca yorum(#) satırında alternatifi verilmiştir. Yine `echo $?` komut ile durum kontrolü yapılabilir.
  
###### Örnek 2: -lt (küçüktür)
```shell
$ [ 3 -lt 5 ]                      # test 3 -lt 5
```
> **Explanation:**
> + operand'lar tamsayı olduğu için `-lt` kullanıldı ve  *3 sayısı 5'den küçük mü* sorar.
> + Ayrıca yorum(#) satırında alternatifi verilmiştir. Yine `echo $?` komut ile durum kontrolü yapılabilir.

##### 3.String Karşılaştırılması:
1. `=` veya `==`  :  Karakterleri(Strings) eşittir.
2. `!=` :  Stringler eşit değildir
3.  `-z <string>` :  String uzunluğu sıfır mı? (Boş mu?)
4.  `-n <string>` :  String uzunluğu sıfırdan büyük mü? (Boş değil mi?)

###### Örnek 1: = veya ==
```shell
$ test "linux" = "linux"            # [ "linux" = "linux" ] 
```
Veya
```shell
$ test "linux" == "linux"           # [ "linux" == "linux" ] 
```

> **Explanation:**
> + Operand'ların string olduğu için sembol(=) kullanabiliyoruz. Ayrıca yorum satır(#) ile de alternatifi yazılmıştır.  
> + `echo $?` kontrol edebiliriz. 0 => başarılı  1 => başarısız.

###### Örnek 2:  test -z

```shell
kardiz=""
$ [ -z $kardiz ]                          # test -z $kardiz
```
> **Explanation:**
> + kardiz adlı değişkenin boş olup olmadığını kontrol ediyoruz. 
> + Eğer `echo $?` komutu sıfır verirse kardiz boş karakterli ama bir verirse kardiz değişkeninde karakter dizini atanmıştır.

###### Örnek 3: test -n
```shell
kardiz="not empty"
$ [ -n $kardiz ]                          # test -n $kardiz
```
> **Explanation:**
> + `test -z` komutun tam tersi çalışır. 
> + `echo $?` ile baktığımızda kardiz değişkenin içerisi boş değilse çıktı 0 boş ise 1 verir.

### Koşul İfadeleri: IF, ELIF and ELSE 

> [!TIP] Ipucu
> *test komut* `if elif else` koşullarında çok kullanılır. 


```bash
#!/usr/bin/bash

if [ condition ]; then
    situation
elif [ condition ]; then
    situation
else
	situation
fi
```

##### 1.Tam Sayı(INTEGER) Karşılaştırması:
```bash
# Test Komutu
-eq / eşit ise                / if [ "$a" -eq "$b" ] / (equal)
-ne / eşit değil ise          / if [ "$a" -ne "$b" ] / (not equal)
-gt / büyük ise               / if [ "$a" -gt "$b" ] / (greater than)
-ge / büyük veya eşit ise     / if [ "$a" -ge "$b" ] / (greater than or equal)
-lt / küçük ise               / if [ "$a" -lt "$b" ] / (less than)
-le / küçük veya eşit ise     / if [ "$a" -le "$b" ] / (less than or equal)

# [[ ... ]] komutu

-eq / eşit ise                / if [[ "$a" -eq "$b" ]] / (equal)
-ne / eşit değil ise          / if [[ "$a" -ne "$b" ]] / (not equal)
-gt / büyük ise               / if [[ "$a" -gt "$b" ]] / (greater than)
-ge / büyük veya eşit ise     / if [[ "$a" -ge "$b" ]] / (greater than or equal)
-lt / küçük ise               / if [[ "$a" -lt "$b" ]] / (less than)
-le / küçük veya eşit ise     / if [[ "$a" -le "$b" ]] / (less than or equal)

 <  / küçük                   / if (("$a" < "$b"))
 <= / küçük eşit              / if (("$a" <= "$b"))
 >  / büyük                   / if (("$a" > "$b"))
 >= / büyük eşit              / if (("$a" >= "$b"))   
```

##### 2. Karakter(String) Karşılaştırması:
```bash
 =   / eşit ise              / if [ "$a" = "$b" ]
 ==  / eşit ise              / if [ "$a" == "$b" ]
 !=  / eşit değil ise        / if [ "$a" != "$b" ]
 <   / küçük                 / if [[ "$a" < "$b" ]]    / Alfabetik dizilime göre
 >   / büyük                 / if [[ "$a" > "$b" ]]    / Alfabetik dizilime göre
 ==  / eşit is               / if [[ "$a" == "$b" ]]
```

> [!INFO]
> +  `[[ ... ]]`  ifadesi `test` komutunda göre daha güçlü ve daha esnektir. 

###### Örnek  1: if koşulu
```bash
#!/usr/bin/bash

sayi=10
if [ $sayi -eq 10 ]; then               # 1
# if test $sayi -eq 10; then            # 2
	echo "Koşul Doğru"
fi
```
> **Explanation:**
> + Tam sayı karşılaştırılamsı yapıldığı için `-eq` kullanıldı.
> + 1 ile 2 arasında bir fark yok aynı sonuç verir. Eğer koşul doğru ise yani değişken değeri 10'a eşit ise ekran çıktıyı yazdırır.
###### Örnek 2: if `((...))` ile
```bash
#!/usr/bin/bash

sayi=10
if (( $sayi > 9 )); then
	echo "Koşul Doğru"
fi
```
> **Explanation:**
> + Örnek 1 ile aynı ama burada çift parantezler `((...))` sayesinde simge(>) kullanabiliyoruz.

###### Örnek 3: if elif else
```bash
#!/usr/bin/bash

sayi=9
if (( $sayi < 9 )); then
	echo "$sayi, 9'dan küçüktür."
elif (( $sayi > 9 )); then
	echo "$sayi, 9'dan büyüktür."
else
	echo "$sayi, 9'a eşittir."
fi
```
> **Explanation:**
> + sayi adlı değişkenimiz 9'a eşit olduğundan if ve elif bloklarına giriş yapmayacak ve en son seçenek olarak else kodu çalışacaktır.

###### Örnek 4:  Harf karşılaştırma
```bash
#!/usr/bin/bash

harf="c"
if [[ "a" > $harf  ]]; then
        echo "c harfi a'dan önde"
elif [[ "b" > $harf ]]; then
        echo "c harfi b'den önde"
elif [[ "d" > $harf ]]; then
        echo "c harfi d'den önde"
else
        echo "c harfi sonucu"
fi	
```
> **Explanation:**
> + Harfler arasında da sıralama olup ve bu bağlı olarak karşılaştırma yapabiliriz tam sayılarda olduğu gibi. 
> + `[[ ... ]]` yerine *test* komutunda kullanabiliriz.

##### 3. Dosya Doğrulama Operatörleri:

###### Örnek 1:  Dosya veya Dizin var mı?
```bash
#!/usr/bin/bash

echo -e "Dosyanın Adını Giriniz:\c"               # 1
read fileName                                     # 2

if [ -e $fileName ]; then                         # 3
	echo "$fileName dosyası bulundu."
else
	echo "$fileName dosyası bulunamadı."
fi
```
> **Explanation:**
>  1. `echo` 'un `-e` parametresi backslash kaçışın(backslash escapes) dizilerin yorumlanmasını  aktif olmasını sağlar ve `\c` dizisi,  daha fazla üretmesin durdurur. (man echo)
>  2. [[Bash Script#Read Kullanımı|read komut]] bakınız.
>  3. [[Bash Script#test komutu|test komutuna]] bakınız. 


###### Örnek 2: Dosya var mı ve düzenli bir dosya mı?
```bash
#!/usr/bin/bash

if [ -f /etc/passwd ]; then
# if test -f /etc/passwd; then
	echo "passwd dosyası var".
else
	echo "passwd dosyası yok."
fi
```
> **Explanation:**
> +  Daha fazlası için [[Bash Script#1. Dosya ve Dizin Kontrolleri|Dosya ve Dizin Kontrolleri]] bakınız.
> + Eğer dosya veya istenen dizin mevcut(-f) ise `if` bloğu çalışır aksi taktirde `else` bloğu çalışır. 

###### Örnek 3: Dosya var mı ve boyutu 0'dan büyük mü?
```bash
#!/usr/bin/bash

read -p "Dosya Adını Giriniz: " fileName               # 1

if [ -s $fileName ]; then                              # 2
	echo "$fileName dosyanın içeriği doludur."
else
	echo "$fileName dosyanın içeriği boştur."
fi
```
> **Explanation:**
> 1. [[Bash Script#Read Kullanımı|read komut]] bakınız.
> 2. [[Bash Script#test komutu|test komutuna]] bakınız.
> Eğer bash script'in çalıştırılan dizin içerisinde girilen dosya ismi boş ise `if` bloğu aksi taktirde `else` bloğu çalışır.

###### Örnek 4: Dosya yazılabilir mi?
```bash
#!/usr/bin/env bash

read -p "Dosya Adını Giriniz: " fileName

if [ -w $fileName ]; then
	echo "$fileName dosyası yazılabilir."
else
	echo "$fileName dosyası yazılabilir değil."
fi
```
> **Explanation:**
> + Yukarıdaki Örnek 3 ile aynı ama burada dosyanın yazılabilir mi kontrol ediyoruz. `ls -l` teyit edebiliriz, eğer *w* varsa  dosya yazılabilir demektir. 
> + `chmod -x dosya_adı` ile yazma haklarını alıp tekrar deneyerek script'inizi kontrol edebilirsiniz. 

###### Örnek 5: İç içe if else ve dosyalar ile
```bash
#!/usr/bin/bash

echo -e "Dosyanın ismini giriniz: \c"; read fileName

if [ -f $fileName ]; then                                    # 1
	if [ -w $fileName ]; then                                # 2
		echo "Dosya yazılabilir. Çıkış işlemi için Ctrl+D"
		cat >> $fileName                                     # 3
	else
		echo "$fileName dosyası yazılabilir değil!"
	fi
else
	echo "Dosya mevcut değil!"
fi
```
> **Explanation:**
> 1. [[Bash Script#test komutu|test -f komutu]] bakınız.
> 2. [[Bash Script#test komutu|test -w komutu]] bakınız.
> 3. `cat` komutun standart girdisini(klavye) standart çıktıya(değişken) yönlendiriyoruz.
> Birinci if de düzenli dosya var mı diye bakıyoruz. if'in içindeki if'de dosya yazılabilir mi diye bakıyoruz.
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=a5Vumkx-PCM&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=12)

##### 4. Not(`!`) operatörü
```bash
if ! command; then
  <expression>
fi
```

###### Örnek 1: Dosya kontrolünde Not operatörü
```bash
#!/usr/bin/bash

if ! [ -f "/usr/share/dict/word" ]; then
	echo "word dosyası yok!"
else
	echo "word dosyası mevcuttur."
fi
```
> **Explanation:**
> + **`-f "dosya.txt"`** dosyanın var olup olmadığını kontrol eder.
> + `!` operatörü ile eğer dosya yoksa (`false` dönerse), bu durum tersine çevrilir ve `if` bloğu çalışır.

###### Örnek 2: id komutunda Not operatörü
```bash
#!/usr/bin/bash

userName="ottoman"
if ! id $userName &> /dev/null; then
	echo "$userName adında kullanıcı mevcut değil."
else
	echo "$userName adında kullanıcı mevcut."
fi
```
> **Explanation:**
> + Eğer `ottoman` adında kullanıcı yok ise; `if` bloğu `false` olacaktır. Not(`!`) operatörü `false` değerini  `true` yapacak ve `if` bloğu çalışacaktır.
> + Eğer `ottoman` adında kullanıcı var ise; `if` bloğu `true` olacaktır. Not(!) operatörü `true` değerini `false` yapacak sonuç olarak `else`  bloğu çalışacaktır.


### AND ve OR operatörleri

> [!NOTE]
> Bash script de
> AND operatörün simgesi : `&&` veya `-a` 
> OR operatörün simgesi : `||` veya `-o`

###### Örnek 1 : AND Operatörü:
```bash
#!/usr/bin/env bash

dersNotu=30
if [ $dersNotu -gt 50 ] && [ $dersNotu -lt 100 ]; then      # 1
# if [ $dersNotu -gt 50 -a $dersNotu -lt 100 ]; then        # 2
# if [[ $dersNotu -gt 50 && $dersNotu -lt 100 ]]; then      # 3
	echo "Dersten geçtiniz."
else
	echo "Dersten kaldınız!"
fi
```
> **Explanation:**
> 1. iki test komutunu and(&&) operatörü ile karşılaştırdık
> 2. Yorum satırındaki ise yalnızca test komut kullandık ve içerisinde and(-a) operatörü ile  karşılaştırdık
> 3. Yorum satırındaki ise `[[ ... ]]` komutu `&&` operatörünü desteklemektedir. Ayrıca dikkat ederseniz test komutları olan `-gt` ve `-lt` desteklemektedir. 
> and operatörü her iki koşul doğru olduğunda çalışır 

###### Örnek 2: OR Operatörü:
```bash
#!/usr/bin/bash

vize=66
final=50
if [ $vize -gt 50 ] || [ $final -gt 60 ]; then              # 1
# if [ $vize -gt 50 -o $final -gt 60 ]; then                # 2
# if [[ $vize -gt || $final -gt 60 ]]; then                 # 3
	echo "Dersten geçtiniz."
else
	echo "Dersten kaldınız!"
fi
```
> **Explanation:**
> 1. İki test komutunu or(||) operatörü ile karşılaştırdık.
> 2. Tek test komut içerisinde or(-o) operatörü ile karşılaştırma yapıyoruz.
> 3. Yukarıdaki örnek 1 de olduğu gibi `[[ ... ]]` komut `||` operatörünü desteklemektedir.  Ayrıca dikkat ederseniz test komutları olan `-gt` ve `-lt` desteklemektedir.

### Aritmatik İşlemler
####  1. Tam Sayılar(Integer) ile
###### Söz dizimi - Syntax:
```bash
((expression))
```
###### Örnek 1: En basit gösterimi
```bash
#!/usr/bin/bash

echo $((1+1))                            # Çıktı: 2
```
> **Explanation:**
> Burada dikkat etmemiz gereken nokta çift paranteze alma olmalıdır. Ayrıca terminal de direk de deneyebilirsiniz: `$ echo $((1+1))` 

> [!TIP]
> - Bash script'te **`(( ... ))`** yapısı;
> - **Aritmetik İşlemler**: Toplama, çıkarma, çarpma, bölme gibi matematiksel işlemleri yapmak.
>- **Karşılaştırmalar**: Sayısal değerlerin karşılaştırılması (eşitlik, büyüklük, küçüklük gibi).
>- **Değişken Değerlerini Güncelleme**: Değişkenlerin değerini güncellemek ve arttırma/azaltma işlemleri yapmak. `((i++))`,  `((x=x+1)), ((x+=1))` gibi.

> [!NOTE]
> 1. `$(( ... ))` Yapısı
> 	- **Sonucu döndürür**: `echo` komutuyla veya bir değişkenle kullanılabilir.
> 	- **Daha çok çıktı üretmek için kullanılır**.
> 1. `(( ... ))` Yapısı
> 	- **Sonuç döndürmez**, ancak değişkenlerin değerini günceller.
> 	- Çıktı üretmez, sadece değişkenler üzerinde işlem yapar.
> 	- Bir koşul ifadesi içinde (örneğin `if`, `while`) kullanılabilir.

|    Yapı    |                      Amacı                       |                    Kullanım Alanı                     |                    Sonuç                    |
| :--------: | :----------------------------------------------: | :---------------------------------------------------: | :-----------------------------------------: |
| `$((...))` |          Değer üretir ve çıktı döndürür          |        Değişken atamak, `echo` ile çıktı almak        | Sonucu bir değişkene atar veya ekrana basar |
| `((...))`  | Aritmetik işlemi çalıştırır ve exit status döner | Değişkenin değerini güncellemek, koşullarda kullanmak | Çıktı üretmez, sadece exit status döndürür  |

###### Örnek a: `(( ... ))` yapısı
```bash
#!/usr/bin/bash

a=5
b=3
((a += b))
echo "a: $a"
```
> **Explanation:**
> + `((a+=b))` aritmetik işlemi yapar ve değeri `a` değişkeni üzerinde ekler.
###### Örnek b: `$(( ... ))` Yapısı
```bash
#!/usr/bin/bash

a=7
b=6
sonuc=$((a+b))
echo "Sonuc: $sonuc"
```
> **Explanation:**
> +  `a` ve `b` toplama işlemini yapar ve `sonuc` adındaki değişkene atar.

###### Örnek 2: Değişkenler ile Toplama:
```bash
#!/usr/bin/bash

sayi1=25
sayi2=5

echo "Toplama: $(( $sayi1+$sayi2 ))"               # Çıktı: 30
echo "Çıkarma: $(( $sayi1-$sayi2 ))"               # Çıktı: 20
echo "Çarpma : $(( $sayi1*$sayi2 ))"               # Çıktı: 125
echo "Bölme  : $(( $sayi1/$sayi2 ))"               # Çıktı: 5
echo "Kalan  : $(( $sayi1%$sayi2 ))"               # Çıktı: 0
```
> **Explanation:**
> + Değişkenlere atanan değerler ile matematik işlemleri yapılıyor.

###### Örnek 3: expr komutu
```bash
#!/usr/bin/bash

sayi1=25
sayi2=5

echo "Toplama: $(expr $sayi1 + $sayi2)"
echo "Çıkarma: $(expr $sayi1 - $sayi2)"
echo "Çarpma : $(expr $sayi1 \* $sayi2)"
echo "Bölme  : $(expr $sayi1 / $sayi2)"
echo "Kalan  : $(expr $sayi1 % $sayi2)"
```
> **Explanation:**
> + Örnek 2 yaptığımızın aynı işlemleri yaptık ama `expr` komutunu kullandık.
> + **Burada dikkat edilmesi gereken nokta** aritmetik operatörler arasına kesinlikle boşluk bırakmalıyız ve ayrıca çarpma işlemi de kullanılan yıldız işaret özel karakteri olmasını engellemek için ters slash(/) yıldız işaretin önüne koyuyoruz.


> [!TIP] 
> + `((i++))` veya `i=$((i+1))` döngülerde `i` değişkenini her döngüde artırır.
> + `((i--))` veya `i=$((i-1))` döngülerde `i` değişkenini her döngüde azaltır.

#### 2. Ondalıklı(Float) Sayılar ile

> [!INFO]
> +  Ondalıklı sayılarla işlem yapabilmemiz için `bc` komutunu kullanıyoruz:
> + `bc` ifadelerin etkileşimli yürütülmesi ile [arbitrary precision numbers](https://en.wikipedia.org/wiki/Arbitrary-precision_arithmetic#:~:text=In%20computer%20science%2C%20arbitrary%2Dprecision,memory%20of%20the%20host%20system.) destekleyen bir dildir. (man bc)

###### Örnek 1: Basit Gösterim
```bash
echo "20.5+5" | bc                   # Çıktı: 25.5
```
> **Explanation:**
> + `echo` komutun çıktısını `bc` komutuna yönlendiriyoruz ve `bc` komutun aldığı veriyi değerlendiriyor.

###### Örnek 2: bc komutu ile tüm işlemler
```bash
#!/usr/bin/bash

echo "20.5+5" | bc                  # Çıktı: 25.5       # 1
echo "20.5-5" | bc                  # Çıktı: 15.5       # 2
echo "20.5*5" | bc                  # Çıktı: 102.5      # 3
echo "scale=2;20.5/5" | bc          # Çıktı: 4.10       # 4
echo "scale=2;20.5%5" | bc          # Çıktı: 0          # 5
```
> **Explanation:**
> 1. Örnek 1 de açıklanmıştır.
> 2. Örnek 1 ile aynı ama çıkarma işlemi yapılıyor.
> 3. Örnek 1 ile aynı ama çarpma işlemi yapılıyor.
> 4. Burada bölme işlemi gerçekleştiriyoruz ama `bc` 'deki scale komut ile hassasiyetini 2 rakam(digit) çıkarıyoruz  aksi taktirde eksik göstermektedir. scale parametresini kaldırarak tekrar bir deneyiniz.
> 5.  4. basamakta anlatılan ile aynı ama burada kalan operatörü ile yapılıyor. scale parametresi, `bc`'in parametresidir.
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=w69wvsDzCJo&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=9)

###### Örnek 3: bc komutu ve değişken
```bash
#!/usr/bin/bash

sayi1=20.5
sayi2=5
echo "scale=2;$sayi1/$sayi2" | bc
```
> **Explanation:**
> + sayi1 ve sayi2 adlı değişken oluşturarak echo komut ile hem bc parametresi olan scale hem de değişken değerlerini bc komutunda yönlendirdik.
> + Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=w69wvsDzCJo&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=9)

###### Örnek 4: bc matematik kütüphanesi kullanma
```bash
sayi1=25
sayi2=3
echo "scale=4; sqrt($sayi1)" | bc -l       # Çıktı: 5.0000        # 1
echo "scale=4; $sayi2^3" | bc -l           # Çıktı: 27            # 2
```
> **Explanation:**
> 1. `bc -l` komutundaki `-l` parametresi matematik kütüphanesini kullanmamıza izin vermektedir. Böylelikle sqrt fonksiyonundan faydalanabiliyoruz. 
> 2. Yine burada da `bc -l` komutundaki `-l` parametresi sayesinde sayi2 içerisindeki 3'ün küpünü alabildik.

#### 3. Let Komutu:
**Syntax -Söz Dizimi:**
```shell
$ let <arithmetic expression>
```
###### Tanım:
+ Bash script'te **`let`** komutu, aritmetik işlemler yapmak için kullanılan eski ve basit bir yapıdır.
+ **`let`** komutu, değişkenlerin değerlerini güncellemek veya aritmetik hesaplamalar yapmak için kullanılır.
+ Aslında, **`(( ... ))`** yapısının alternatiflerinden biridir.
+ `let` komutu, **değişken isimlerinin başında `$` işareti kullanmanıza gerek kalmadan** aritmetik işlemleri yürütür ve sonuçları değişkenlere atar.
+ Ancak, modern Bash de genellikle **`(( ... ))`** kullanımı daha yaygındır, çünkü daha esnektir ve daha okunabilir kod yazmanıza olanak tanır.
###### Örnek 1:  Temel Kullanımı
```bash
#!/usr/bin/bash

let "toplam = 5 + 4"            # Alternatif: let toplam=5+4
echo "Sonuc: $toplam"
```
> **Explanation:**
> + İki değeri toplar ve toplam değişkenine atar.

```bash

#!/usr/bin/bash

sayi1=25
sayi2=5

let "toplam = $sayi1 + $sayi2"; echo "Toplama: $toplam"
let "cikarma = $sayi1 - $sayi2"; echo "Çıkarma: $cikarma"
let "carpma = $sayi1 * $sayi2"; echo "Çarpma: $carpma"
let "bolme = $sayi1 / $sayi2"; echo "Bölme: $bolme"
let "kalan = $sayi1 % $sayi2"; echo "Kalan: $kalan"
```
###### Örnek 2: Değişkenin Değerini Artırma veya Azaltma
```bash
#!/usr/bin/bash

let "x = 10"
echo "x'in ilk değeri: $x"             # Çıktı: x'in ilk değeri: 10

let "x++"
echo "x'in değeri: $x"                 # Çıktı: x'in değeri: 11

let "x--"
echo "x'in yeni değeri: $x"            # Çıktı: x'in yeni değeri: 10
```
> **Explanation:**
> + `x++` x'in değerini bir artırır ve `x--` x'in değerini bir azaltır.
> + C programlamadan gelen bir özellik.

###### Örnek 3: Birden Fazla Aritmetik İşlem
```bash
#!/usr/bin/bash

let "a = 5"
let "b = 8"
let "c = a * b + 2"
echo "c'in değeri: $c"          # Çıktı: c'in değeri: 42
```

###### Örnek 4: if ile birlikte kullanma
```bash
#!/usr/bin/bash

let "a = 5"                             # 1
let "b = 3"

if let "a >= b"; then                   # 2
	echo "a, b'den büyüktür."
else
	echo "a, b'den küçük veya eşittir."
fi
```
> **Explanation:**
> 1. `let` komut ile *değişken* tanımlayabiliyoruz.
> 2. `if` bloklarında koşul kontrolleri içinde kullanabiliyoruz.

###### Örnek 5: let ve Positional arg.
```bash
#!/usr/bin/bash

let "a = $1 + 20"; echo "$1'in 20 fazlası: $a"
```
> **Explanation:**
> + `$1` ile bash script'e bir argüman alıyoruz ve `let` anahtarı ile 20 ile toplayıp ekrana veriyoruz.

##### `let` ve `(( ... ))` Karşılaştırması
- Bash'te modern kullanımda, **`(( ... ))`** yapısı, **`let`** komutuna göre daha yaygın ve esnek bir yöntemdir.
- `(( ... ))` kullanımı, özellikle büyük ve karmaşık ifadelerde daha okunabilir kod yazmanızı sağlar.
###### Örnek 1: let ile
```bash
#!/usr/bin/bash

let "a = 5 + 6"
echo "a'ın değeri: $a"            # Çıktı: a'ın değeri: 11
```

```bash
#!/usr/bin/bash

(( a = 5 + 6))
echo "a'ın değeri: $a"            # Çıktı: a'ın değeri: 11
```
> **Explanation:**
> + İki kodu karşılaştırınız.

### Case Kullanımı
```bash
case variable in
	variable_name )
		situation;;
	variable_name )
		situation;;
esac
```

###### Örnek 1:  Basit Kullanımı
```bash
#!/usr/bin/env bash

arac=$1                                                  # 1
case $arac in                                            # 2
	"araba" )                                            # 3
		echo "$arac 200TL'ye günlük kiralanır.";;
	"Motorsiklet" )                                      # 3
		echo "$arac 100TL'ye günlük kiralanır.";;   
	"Bisiklet" )                                         # 3
		echo "$arac 50TL'ye günlük kiralanır.";;         
	* )                                                  # 4
		echo "$arac kiralık değil!";;
esac
```
> **Explanation:**
>1. arac adında değişken oluşturuyoruz ve bu değeri [[Bash Script#Bash Script Argümanlar|bash script argümanı]] ile alıyoruz.
>2. Buradaki `$arac` değişkeni hangisi ile eşleşirse o blok çalışacaktır örneğin *araba* ile eşleşirse onun bulunduğu blok çalışacaktır. Eğer hiçbiri ile eşleşmezse `yıldız(*)` bloğu çalışacaktır. 
> 	+ `$ ./using_case.sh araba`  Terminal de çalıştırılırsa *araba* bloğu çalışacaktır.
> 
> Uyarı : case ile açıldığında esac ile kapatmamız gerekir.

###### Örnek 2: Karakterler ile case
```bash
#!/usr/bin/bash

read -p "Bir karakter giriniz: " character
case $character in 
	[a-z] )                                                            # 1
		echo "Kullanıcı $character harf girişi yaptı, a-z arasında";;
	[0-9] )                                                            # 2
		echo "Kullanıcı $character rakam girişi yaptı, 0-9 arasında";;
	? )                                                                # 3
		echo "Kullanıcı $character özel karakter girişi yaptınız";;
	* )                                                                # 4
		echo "Bilinmeyen karakter";;
esac
```
> **Explanation:**
> 1. a ile z arasında bir harf girildiğinde bu blok çalışacaktır.
> 2. 0 ila 9 arasında bir sayı girildiğinde bu blok çalışacaktır.
> 3. Özel bir karakter örneğin `},[, % veya +`  girildiğinde bu blok çalışacaktır.
> 4. `*` da ise hiç bir blok çalışmadığında çalışacak olan bloktur.
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=HDxzd__1rTs&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=14)

###### Örnek 3: `|` kullanımı
```bash
#!/usr/bin/bash

ay=$(date +%m)                                 # 1

case $ay in
	2 )
		echo "Bu ay 28 gündür. 4 yılda 29 gündür.";;
	04|06|09|11 )                              # 2
		echo "Bu ay 30 gündür.";;
	* )
		echo "Bu ay 31 gündür.";;
esac
```
> **Explanation:**
> 1. `date` komutun `+%m` format yapısını kullanarak o zaman dilimin tarihini `ay` adlı değişkene atıyoruz.
> 2. `04|06|09|11` yapısında; Pipe(`|`) simgesin `case` için özel anlamı var. Bu simgenin anlamı *veya* denilebilir. `ay` değişkenin değeri, 04 veya 06 veya 09 veya 11 olursa `case`'in bu bloğu çalışacaktır.  

### Diziler(Arrays)

**Tanım:** dizi,  birden fazla veriyi tek bir değişken altında saklamaya olanak tanıyan bir veri yapısıdır.

> [!WARNING]
> Dizilerde dizi elemanlarını ayıran *boşluk* dur.
> `dizi=("Linux" "Unix" "Mac" "Windows")     #  Yazımı Doğru` 
> `dizi=("Linux", "Unix", "Mac", "Windows")   #  Yazımı Yanlış Virgül olmayacak`

###### Örnek 1:  Basit Kullanımı:
```bash
#!/usr/bin/bash

OS=( "Linux" "Windows" "Unix" )

echo "Tüm dizin: ${OS[@]}"                  # Tüm dizi elemanlarını gösterir.
echo "index 2: ${OS[2]}"                    # Çıktı: Unix
echo "Tüm dizinin index sırası: ${!OS[@]}"  # Çıktı: 0 1 2
echo "Tüm dizinin index sayısı: ${#OS[@]}"  # Çıktı: 3

```
> **Explanation:**
> + Diziler(arrays) tüm programlama dillerinde olduğu gibi indeksi *0(sıfır)'dan* başlar.
> + Linux: 0, Windows: 1, Unix: 2 indeks de olacaktır.
> + Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=7GoukBA6tZc&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=13)

###### Örnek 2: Diziye eleman ekleme
```bash
#!/usr/bin/env bash

OS=( "Linux" "Windows" "Unix" )

echo "Tüm dizi: ${OS[@]}"
OS[3]='Mac'
echo "Tüm dizi tekrar: ${OS[@]}"
```
> **Explanation:**
> + OS dizin en son indeksi 2 bu yüzden biz 'Mac' elmanı 3. indekse ekliyoruz. Aksi taktirde mevcut dizini değiştirecektir.

###### Örnek 3: Diziden eleman silme
```bash
#!/usr/bin/bash

OS=( "Linux" "Windows" "Unix" )

echo -e "Tüm dizi\t\t: ${OS[@]}"           # Çıktı: Linux, Windows, Unix
unset OS[1] 
echo -e "Tüm dizi tekrar\t: ${OS[@]}"      # Çıktı: Linux, Unix
echo -e "Tüm indeksleri\t\t: ${!OS[@]}"     # Çıkıt: 0 2
```
> **Explanation:**
>  + `unset` komut ile 1. dizin de olan windows dizinden silinecektir.
>  + `echo -e` de -e parametresi echo komutun backslach kaçış karakterlerin yorumlanmasına izin verecektir *(man echo)*. Böylelikle daha düzgün görünüm elde edeceğiz.
>  + ==UYARI:== Window'u sildik ve indeksi 1'di ve Eğer `$!OS[@]` komut ile bakarsak index 1 olmadığını görebiliriz.

##### Dizilerde Dilimleme(Array Slice):
+ Array dilimleme, `${array[@]:başlangıç:uzunluk}` söz dizimi kullanılarak yapılır.
+ **başlangıç**: Dilimleme işleminin başlayacağı dizinin indeksi.
+ **uzunluk**: Dilimleme sonucunda kaç eleman alınacağını belirten sayı.

###### 1. Temel Kullanım 
```bash
#!/usr/bin/bash

progLang=("Javascript" "Python" "Java" "Bash" "Mojo" "Ruby" )   # 1

slice=("${progLang[@]:1:3}")                                    # 2
echo "Dilimlenmiş Dizi: ${slice[@]}"                            # 3
```
**Çıktı:**
```shell
$ Dilimlenmiş Dizi: Python Java Bash
```

> **Explanation:**
> 1. `progLang` adında bir dizi(array) taımladık.
> 2. Dilimleme(slice) işlemi yapıyoruz. İndeksi 1 olan yani `python` ile başlayıp indeksi 3 olan yani `bash` değerine kadar diziyi alıp bir değişkene atıyoruz.
> 3. `slice` değişkenin tutuğu array'i `echo` ile ekran basıyoruz.
> 	+ **UYARI:** 1 indeksi ve 3 indeksi dahil olmuştur.

###### 2. Sadece Başlangıç:
```bash
#!/usr/bin/bash

progLang=("Javascript" "Python" "Java" "Bash" "Mojo" "Ruby" )  

slice=("${progLang[@]:3}")                                     # 1    
echo "Dilimlenmiş Dizi: ${slice[@]}"
```
**Çıktı:**
```shell
$ Dilimlenmiş Dizi: Bash Mojo Ruby
```
> **Explanation:**
> 1. Dizinin 3. indeksinden başlayarak geri kalan tüm elemanları alır.

###### 3. Negatif İndislerle Dilimleme:
```bash
#!/usr/bin/bash

progLang=("Javascript" "Python" "Java" "Bash" "Mojo" "Ruby" )  

slice=("${progLang[@]: -3:3}")                                 # 1
echo "Dilimlenmiş Dizi: ${slice[@]}"
```
**Çıktı:**
```shell
$ Dilimlenmiş Dizi: Bash Mojo Ruby
```
> **Explanation:**
> 1. Dizilerde sondan indeksleme yapıldığında;
> 	+ **-1**: Dizinin son elemanını ifade eder.
> 	+ **-2**: Son elemandan bir önceki elemanı ifade eder.
> 	+ Başlangıç: -3 ve uzunluk: 3 yani sondan -3 elemanına gel ve -3'den sonra 3 elaman al.


### Döngüler(Loops)
#### While Döngüsü:
###### While Şablonu:
```bash
while condition
do
	<expression>
done	
```

###### 1. Basit Kullanım:
```bash
#!/usr/bin/bash

i=1
while [ $i -le 10 ]                                         # 1
do                                                          # 2
	echo "Değer: $i"                  
	i=$((i+1))       # ((i++)) veya ((++i))                 # 3
done                                                        # 4
```
> **Explanation:**
> 1. `while` da kullanılan koşul [[Bash Script#test komutu|test komutu]]
> 2. kodları `do` ile başlıyoruz.
> 3. Döngü süreci boyunca değişkeni(`$i`) bir artıyoruz ve [[Bash Script#Aritmatik İşlemler|Aritmatik işlemlerden]] kullanılıyor.
> 	+ `$((i+1))` yerine `$((i++))` veya `$((++i))` kullanabiliriz.
> 1. Kodu `done` ile bitirmemiz gerekir.

###### 1.1 `[[ ... ]]` ile kullanımı:
```bash
#!/usr/bin/bash

counter=1
while [[ counter -lt 10 ]]; do
	sleep 3
	echo "Değer: $counter"
	((counter++))
done
```
> **Explanation:**
> + Yukarıdaki kodun aynısı fakat  `test` komutun alternatifi olan  `[[ ... ]]` komutu `while` döngüsü ile kullanıyoruz.
###### Örnek 2:  while ile sleep komutu
```bash
#!/usr/bin/env bash

i=10
while [ $i -gt 0 ]; do          # 1
	echo "Sayı: $i"
	((i--))                     # 2
	sleep 1                     # 3
done
```
> **Explanation:**
> 1.  `while` da kullanılan koşul [[Bash Script#test komutu|test komutu]]
> 2.  loop döngüleri ait olan bir aritmetik kısaltması kullanıyoruz.
> 3. `sleep 1` komut her döngüde 1 saniye bekletiyor. Komutun çalışması adı üzerinde 1 saniye uyu.

#### For Döngüsü:
##### For Şablonu 1:
```bash
for (( i=0; i<=5; i++ ))
do
	<expression>
done
```

###### Örnek 1:  Basit Kullanımı
```bash
#!/usr/bin/bash

for (( i=0; i<=5; i++ ))
do
	echo "Sayı $i"
done
```
> **Explanation:**
>+  C temeli programlama diline benzer bir for döngüsü

##### For Şablonu 2:
```bash
for i in 1 2 3 4 5
do
	 <expression>
done
```

###### Örnek 1: Basit Kullanımı
```bash
#!/usr/bin/bash

for i in 1 2 3 4 5; do
	echo "Sayı: $i"
done
```
> **Explanation:** 
> + *Python programlama* diline benzer bir for döngüsü

###### Örnek 2: `for` ile linux komutları
```bash
#!/usr/bin/bash

for i in ls pwd; do                      # 1
	echo -e "\nÇalışan Komut: $i"        # 2
	$i
done                                     # 3
```
> **Explanation:** 
> 1. `for loop` ile linux komutların sırayla değişkene gönderdik ve loop içinde çalıştırdık.
> 2.  echo komutunda `\n` yorumlanması için `-e` parametresi kullanıldı.
> 3. `for loop` bittiğini söylemek için `done` sona ekliyoruz.

###### Örnek 2.1: `for` ile `ls` komutu:
```bash
#!/usr/bin/env bash

for l in $( ls ); do                     # 1
	echo $l                              # 2
done
```
> **Explanation:** 
> 1. `ls` komut bulunduğu dizindeki dosya veya dizinlerini `for loop` gönderir.
> 2. `for loop` ise bu dosya veya dizinleri ekrana çıktı verir. Bu temelde daha gelişmiş kodlarda yazılabilir.
###### Örnek 3: brace expansion ile
```bash
#!/usr/bin/bash

for i in {1..5}; do                   # Çıktı: 1 2 3 4 5
# for i in {1..10..2}; do             # Çıktı: 2 4 6 8 10
	echo "Sayı: $i"
done
```
> **Explanation:** 
> - `{1..5}` kullanabilmek için bash versiyonun 3 üzerinde olması gerekir. `echo $BASH_VERSION` komut ile veya `bash --version` komutu ile bash versiyonu öğrenebiliriz.
> - Yukarıdaki Örnek 1 gibi `1 2 3 4 5` ifadesi `{1..5}` eş değerdir.
> - `{1..10..2}`  ifadesi sayılar arasında 2'şer olarak gider. Syntax: `{start..stop..step}` 

#### Select Döngüsü:
```bash
select variable in list
do
	<expression>
done
```

###### 1. Basit Kullanımı
```bash
#!/usr/bin/bash

select il in Ankara İzmir İstanbul
do
	echo "$il seçildi."
done
```
> **Explanation:** 
> + Kullanıcının bir menüden seçim yapmasını sağlayan bir döngü yapısıdır.
> + Verilen seçenekleri(`Ankara İzmir İstanbul`) numaralandırılmış bir menü olarak ekranda gösterir.

###### 2. Select ile Dizi Kullanımı
```bash
#!/usr/bin/bash

iller=("Ankara" "İstanbul" "İzmir")               # 1
select il in ${iller[@]}                          # 2
do
	echo "$il seçildi."
done
```
> **Explanation:** 
> 1. [[Bash Script#Diziler(Arrays)|Dizler]] bakınız.
> 2. Bu adımda diziyi(`${iller[@]}`) entegrasyonu yapıyoruz.

###### 2.1 Select ve Prompt(`PS3`)
```bash
#!/usr/bin/bash

langs='Bash Python C Java Quit'             # 1
PS3='Seçim yapınız: '                       # 2

select lang in $langs; do
	if [[ $lang == 'Quit' ]]; then
		break
	fi
	echo "$lang dersine hoş geldiniz."
done
```
> **Explanation:** 
> 1. `select loop` seçenekleri `string` olarak verdik ve boşluk karakterine göre dilimleme işlemini yaptı.
> 2. `select` komutu bir dizi seçeneği ekrana yazdırır ve kullanıcıdan bir seçim yapmasını ister. Varsayılan olarak, kullanıcının seçim yapacağı sırada bir `#?` karakteri görünür. İşte burada **`PS3`** devreye girer ve bu istem mesajını özelleştirmenize olanak tanır.


> [!TIP]
> + Bash scriptlerinde **`PS3`**, kullanıcıya bir **seçenek menüsü** sunduğunuzda gösterilen özel bir değişkendir.
> + Özellikle **`select`** komutuyla birlikte kullanılır. `select` komutu, kullanıcıdan bir seçim yapmasını sağlayan bir menü oluşturur ve **`PS3`** değişkeni, bu menüyü sunarken kullanıcının karşısına çıkacak istem (prompt) mesajını belirler.

###### Örnek 3: Select ile if Kullanımı:
```bash
#!/usr/bin/env bash

echo "Bir meyve seçin: "
select fruit in Elma Armut Portakal Çilek
do
	if [ -n "$fruit" ]; then                      # 1
		echo "Seçiminiz $fruit"
		break                                     # 2
	else
		echo "Geçersiz seçim. Lütfen tekrar deneyiniz."
	fi
done
```
> **Explanation:** 
> 1. [[Bash Script#test komutu#3.String Karşılaştırılması|Strings Karşılaştırma]] bakınız.
> 2. `break` döngüleri kırar.

###### Örnek 4: Select ile case Kullanımı:
```bash
#!/usr/bin/env bash

distros=("Ubuntu" "Debian" "Arch_Linux")                  # 1
echo "Bir il seçiniz: "
select distro in ${distros[@]}                            # 1
do
	case $distro in                                       # 2
	Ubuntu )
		echo "Ubuntu  seçildi.";;                         
	Debian )
		echo "Debian seçildi."                            # 3
		echo "Debian bitti.";;
	Arch_Linux )
		echo "Arch Linux seçildi.";;
	* )
		echo "1-3 arasında değer giriniz!";;
	esac
done
```
> **Explanation:** 
> 1. [[Bash Script#Diziler(Arrays)|Dizilere]] bakınız.
> 2. [[Bash Script#Case Kullanımı|Case Kullanımına]] bakınız.
> 3. `;;`: Bu bloğun sonunu belirtir. Bu sayede, eşleşen duruma ait komutlar çalıştıktan sonra diğer durumlara bakılmaz.

#### Until Döngüsü:
```bash
until condition
do
	<expression>
done
```

###### Örnek 1: Basit Kullanımı
```bash
#!/usr/bin/bash

i=0
until [ $i -ge 10 ]; do                   # 1
# until (($i >= 10)); do                  # yukardakine alternatif
	echo "Sayı: $i"
	((i++))               #  i=$((i+1))   # 2
done
```
> **Explanation:** 
> 1. [[Bash Script#test komutu|test komutuna]]  bakınız. `-ge` : büyük veya eşittir. 
> 2.  Her döngüde değeri artıracaktır. 
#### Break - Continue Anahtarları

###### Örnek 1: Break
```bash
#!/usr/bin/env bash

for ((i=0; i<=10; i++)); do                       # 1
	if [ $i -gt 5 ]; then                         # 2
		echo "Çıkılıyor..."
		break                                     # 3
	fi
	echo $i
done 
```
> **Explanation:** 
> 1. [[Bash Script#For Döngüsü|For Döngüsüne]] bakınız.
> 2. [[Bash Script#Koşul İfadeleri IF, ELIF and ELSE|Koşul ifadeleri]] bakınınız.
> 3. Bir döngüden (loop) çıkmak için kullanılır. `for`, `while`,`select` veya `until` gibi döngü yapılarında döngünün çalışmasını sonlandırıp, döngüden çıkışı sağlar.
> 	- if koşulu sağlandığında yani değişken 5'den büyük olduğunda `break` komut çalışacaktır.

###### Örnek 2: Continue
```bash
#!/usr/bin/env bash

for ((i=0; i<=10; i++ )); do                      # 1
	if [ $i -eq 2 -o $i -eq 6 ]; then             # 2
		echo "Değer yok"
		continue                                  # 3
	fi
	echo "$i"
done
```
> **Explanation:** 
> 1. [[Bash Script#For Döngüsü|For Döngüsüne]] bakınız.
> 2. [[Bash Script#Koşul İfadeleri IF, ELIF and ELSE|Koşul ifadeleri]] bakınınız.
> 3. Bir döngünün (loop) mevcut iterasyonunu atlayıp, bir sonraki iterasyona geçmek için kullanılır.
> 	+ if koşulu sağlandığında yani değişken 2 veya 6'ya eşit olunduğunda `continue` döngüyü baş alır.

### Fonksiyonlar
```bash
function function_name() {                # Fonksiyonu Tanımlama
	<expression>
}

function_name                             # Fonksiyonu Çağırma
```

```bash
function_name() {                         # Fonksiyonu Tanımlama
	<expression>                          # Dikkat: function anahtarı yok!
}

function_name                             # Fonksiyonu Çağırma
```

```bash
function function_name() {                
	echo "Your name: $1 $2..."           # Fonksiyonun argüman alması $1
}

function_name "Ahmet Hasan..."           # Fonksiyon parametesi alması Ahmet
```

###### Örnek 1: Basit Kullanımı
```bash
#!/usr/bin/env bash

function Merhaba() {                     # 1
	echo "Merhaba Dünya"
}

cikis () {                               # 2 
	exit                                 # 3
}

Merhaba                                  # 4
cikis                                    # 4
```
> **Explanation:** 
> 1. `function` anahtarını kullanarak fonksiyon tanımlanmıştır.
> 2. `function` anahtarı kullanılmadan fonksiyon tanımlanmıştır. Her ikisi de aynı sonucu vermektedir.
> 3. `exit` komut ile de bash script çalışmasını durduruyor.
> 4. Fonksiyonların çalışabilmesi için onları çağrılması gerekir. Burada da fonksiyon çağrılıyor.

###### Örnek 2:  Bir sayın karesini alma
```bash
#!/usr/bin/env bash

echo -e "Bir sayı giriniz :\c"; read sayi          # 1

function karesiYap() {                             # 2
	echo "Sayının karesi: $((sayi*sayi))"
}

karesiYap                                          # 3
```
> **Explanation:** 
> 1. [[Linux komutları#echo|echo]] komutuna bakınız.
> 2. Burada karsiYap adında fonksiyon tanımlıyoruz.
> 3. Fonksiyonun çalışması için çağırıyoruz.

###### Örnek 3: Fonksiyon argüman ve parametre alması
```bash
#!/usr/bin/env bash

function distros() {                             # 1
	echo "Linux Dağıtımları: $1 $2 $3"           # 2
}

distros "Ubuntu" "Arch Linux" "Debian"           # 3
```
> **Explanation:** 
> 1. `distros` adında bir fonksiyon tanımlıyoruz.
> 2. 3 tane argüman(`$1 $2 $3`) girişi tanımlıyoruz istenirse daha fazlası tanımlanabilir.
> 3. Ve yukarıda tanımlanan 3 argümana karşılık olarak 3 tane parametre(`"Ubuntu" "Arch Linux" "Debian"`) veriyoruz.

##### Global & Local Değişken
**Global Değişken:** Her yerden ulaşılabilen değişkenlere denir.
**Local Değişken:** Sadece tanımlandığı fonksiyon içinde geçerli olan değişkendir. Bir fonksiyon içinde `local` anahtar kelimesi ile tanımlanan bir değişken, sadece o fonksiyonun içinde kullanılabilir.
###### Örnek 1:
```bash
#!/usr/bin/env bash

function distroName() {
	local distro=$1                            # 1
	echo "Disto Name: $distro"
}

distroName Debian
echo "Distro: $distro"                         # 2
```
> **Explanation:** 
> 1. Burada `local` adında kullandığımız anahtar kelimesine dikkat edin. Bu değişkenin yerel olmasını sağlıyor yani fonksiyon bittiğinde değişkenin ömrü de bitiyor. 
> 2. Eğer yukarıda `local` anahtarı kullanmazsak global değişken olacak ve burada da ekrana `Debian` çıktısı verecektir.
> 	+ `local` anahtarı kaldırarak test ediniz.


##### Return Alternatif:

> [!WARNING]
> + Programlama dillerinde `return` anahtar kelimesi değer döndürmek, kodu sonlandırmak ve durum kodu döndürmek için kullanılır.
> + Ancak, Bash'te `return` anahtar kelimesi yalnızca **durum kodu** (exit status) döndürmek için kullanılır ve bu kod 0-255 arasında bir değer olabilir.

###### `return` ve `exit` Arasındaki Farklar:

| Özellik                     | `return`                                    | `exit`                                          |
| --------------------------- | ------------------------------------------- | ----------------------------------------------- |
| **Kullanım yeri**           | Sadece fonksiyon içinde kullanılır          | Tüm script içinde herhangi bir yerde kullanılır |
| **Amaç**                    | Fonksiyondan çıkmak ve durum kodu döndürmek | Script'i sonlandırmak ve durum kodu döndürmek   |
| **Kapsam**                  | Sadece fonksiyonlar için geçerli            | Tüm script'i durdurur                           |
| **Durum kodu**              | 0-255 arası bir durum kodu                  | 0-255 arası bir durum kodu                      |
| **Sonraki kodun çalışması** | Fonksiyon dışındaki kodlar çalışır          | `exit` sonrası script'in geri kalanı çalışmaz   |

###### 1. Return Kullanımı:
```bash
#!/usr/bin/bash

myFunction() {                            # 1
	echo "Fonksiyon çalışıyor"
	return 0    # başarılı                 # 2
}

myFunction
echo "Durum kodu: $?"                     # 4
```
> **Explanation:** 
> 1. `myFunction` adında bir fonksiyon tanımladık. 
> 	+  **UYARI:** Eğer fark etiyseniz `function` anahtarını kullanmadan fonksiyon tanımladık.
> 	+ Kodun okunaklığını artırmak için `function` anahtarını kullanabilirsinz.
> 1. `return` anahtar ile **durum kodunu** geri dönüyoruz. `0` kodu başarılıdır.
> 2. `$?` sistem değişkeni ile durum kodunu kontrol ediyoruz.


> [!CAUTION]
> + **`return`**: Sadece durum kodları döndürmek için kullanılır (0-255 arası değerler).

###### 2. Değer Döndürmek İçin `echo` Kullanma:
```bash
#!/usr/bin/bash

function myFunction() {                     # 1
	local result="Hello, World"             # 2
	echo $result                            # 3
}
output=$(myFunciton)                        # 4
echo "Fonksiyondan dönen değer: $output"    # 5
```
> **Explanation:** 
> 1. `myFunction` adında bir fonksiyon tanımladık.
> 2. `local` anahtarı ile `result` adında değişken tanımlayıp, değerini veriyoruz.
> 3. Fonksiyon çağrıldığında `echo` komut ile `result` değişkenini ekrana basıyoruz.
> 4. Fonksiyonu ekran basmak yerine `output` adlı değişkene yönlendiriyoruz.
> 5. `$output` değişkenini ekrana basıyoruz.

###### 3. `return` ve `echo` kullanımı:
```bash
#!/usr/bin/bash

myFunction() {
	local num=$1
	if (( num > 10 )); then
		echo "$num 10'dan büyük"
		return 0       # başarılı
	else
		echo "$num 10'dan küçük veya eşit."
		return 1       # başarısız
	fi
}

output=$(myFunction 5)
echo "Fonksiyondan Dönen: $output"
echo "Durum Kodu: $?"

if [ $? -eq 0 ]; then
	echo "Sistem başarılı bir şekilde çalıştı."
else
	echo "Sistem de sorun var"
fi
```
> **Explanation:** 

##### Fonksiyonlarda Array:

###### Array(dizi) geri döndürme:
```bash
#!/usr/bin/bash

function myFunction() {                           # 1
	local myArray=( "ubuntu" "pardus" "debian" )  # 2
	echo "${myArray[@]}"                          # 3
}

output=($(myFunction))                            # 4

echo "Array Değerleri: ${output[@]}"              # 5
```
> **Explanation:** 
> 1. `myFunction` adında bir fonksiyon tanımlıyoruz.
> 2. `local` anahtarını kullanarak yerel `myArray` adında bir array(dizi) tanımladık.
> 3. array tüm içeriğini `echo` ile standart çıktıya gönderiyoruz.
> 4. Burada `echo`ile gelen standart çıktıyı alıyoruz.
> 5. Final olarak tüm Array ekrana basıyoruz.
###### Fonksiyon ile Array Dilimleme:
```bash
#!/usr/bin/bash

sliceArray() {
	local array=("${@}")                  # 1
	echo "${array[@]:1:3}"                # 2
}

result=$(sliceArray "Mojo" "Python" "Javascript" "Java" "Ruby")     # 3
echo "Dilimlenmiş Dizi: $result"
```

**Çıktı:**
```shell
$ Dilimlenmiş Dizi: Python Javascript Java
```
> **Explanation:**
>  1. `${@}` ile array argümanlarını alıp `array` adlı değişkene atıyoruz. Ayrıca `local` anahtar ile değişkeni yerel yapıyoruz.
>  2. `array` adlı diziyi 1 indeksinden başlayarak 3 indeksine kadar dilimliyoruz.
>  3. `sliceArray` fonksiyona parametreleri giriyoruz.

### Meta Karakterler:
##### Tanım:
+ Özel bir anlama sahip olan karakterlerdir.
+ Normalde yazı karakteri olarak kullanılmazlar; komutların işlenme şeklini değiştirirler, anlamlarını genişletirler ya da bazı işlemleri kontrol ederler.
##### `;` Noktalı virgül:
```shell
$ ls; date
```
> **Explanation:** 
> Aynı satırda birden fazla komut çalıştırmak için kullanılır. Burada `ls` komut çalışır ardından `date` komut çalışıtır.

##### `*` Yıldız:
```shell
$ ls -l s*
```
> **Explanation:** 
> `ls` komutu listelerken s ile başlayan dizin veya dosyaları listeler yani *yıldız* herhangi bir karakter dizini temsil eder.

##### `?` Soru işareti:
```shell
$ ls /bin/??
```
> **Explanation:** 
> `ls` komut bin dizin altında 2 karakterli dizin veya dosya listeleyecektir yani *soru işareti* bir karakteri temsil eder.

##### `[]` Köşeli parantez:
###### Örnek 1: `[123]` kullanımı
```shell
$ ls dosya[12].txt
```
> **Explanation:** 
> + Eğer bulunduğunuz dizinde `dosya1.txt` veya `dosy2.txt` var ise listeleyecektir.
> + `dosya[12].txt` anlamı `dosya1.txt` veya `dosya2.txt` veya her ikisi demektir.

###### Örnek 2: `[1-3]` kullanımı
```shell
$ ls dosya[1-3].txt
```
> **Explanation:** 
> + `[1-3]` arasındaki sayıları yazar.
> + `dosya[1-3].txt` anlamı `dosya1.txt` veya `dosya2.txt` veya `dosya3.txt` veya hepsi demektir.

##### `{}` Süslü parantez:
###### Örnek 1: {1..5} kullanımı
```shell
$ echo {1..5}                    # çıktı: 1 2 3 4 5
```
> **Explanation:** 
> + 1'den 5'e kadar olan sayıları ekran basar.


> [!TIP]
> + `{sayı..sayı..adım}` veya `{alfabe..alfabe}` gibi yapılara *brace expansion* veya *türkçesi süslü parantez genişlemesi* denir.
> + `for loop` veya türkçesi ile `for döngüleri` ile sık sık kullanılır. [[Bash Script#For Döngüsü#For Şablonu 2|For loop]] bakınız.

###### Örnek 2: {1,2,3} kullanımı
```shell
$ touch dosya{1,2,3}.txt
```
> **Explanation:** 
> + Burada süslü parantez genişlemesi(brace expansion) ile tek komut ile birden fazla dosya oluşturuyoruz.
> + **Çıktı**: dosya1.txt, dosya2.txt, dosya3.txt olacaktır.

```shell
$ mkdir -p proje/{src,bin,doc}
```
> **Explanation:** 
> + Bu komut da yukarıdakinin aynısı ama burada dizinler oluşturuyoruz.
> + **Çıktı:**  proje/src, proje/bin, proje/doc olacaktır.

###### Örnek 3: String ile 
```shell
$ echo Merhaba{" Ali", "Mehmet"}
```
> **Explanation:** 
> + Karakter dizileri ile kombinasyon yapılabilir.
> + **Çıktı:** Merhaba Ali Merhaba Mehmet

```shell
$ touch file.txt{,.bak}
```
> **Explanation:** 
> + Dosyayı alıp verilen 2. isime göre yeniden adlandırıyor.
> + **Çıktı:** file.txt.bak olacaktır.

###### Örnek 4: Sayı ile alfabe kombinasyonu
```shell
$ touch file_{a,b,c}{1..5}.txt
```
> **Explanation:** 
> + `{a,b,c}` ile `{1..5}` kombinasyonu ile dosya oluşturuyoruz.
> + **Çıktı:** file_a1.txt  file_a3.txt  file_a5.txt  file_b2.txt  file_b4.txt  file_c1.txt  file_c3.txt  file_c5.txt file_a2.txt  file_a4.txt  file_b1.txt  file_b3.txt  file_b5.txt  file_c2.txt  file_c4.txt
> + **Uyarı:** file_ isimden sonra gelen yapıya dikkat ediniz.

### Tırnak İşareti Kullanımı(Quotes)


> [!TIP]
> 1. **Ters Tırnak(Backtick)**   \`Command\`
> 2. **Düz Tek Tırnak**             'String'
> 3. **Düz Çift Tırnak**            "String + Variables + Escape Characters"

#### Düz Çift Tırnak:
**Tanım:** Tıpkı tek tırnak da olduğu gibi karakter dizinlerini ekrana basar ama eğer karakter dizinlerin içerisinde *değişken* veya *kaçış karakterleri* varsa bunlar yorumlanır.

```shell
$ echo "Kullanıcı: $USER"                  # Çıktı Kullanıcı: ottoman              
```
> **Explanation:**
> + USER sistem değişkeni yorumlanır ve değişkenin içerisindeki yazdırılır.
> + **Uyarı:** Lütfen aynı komut *tek tırnak* ile uygulayıp karşılaştırın.
#### Ters Tırnak(Backtick):
###### Örnek 1: Temel Kullanımı
```shell
$ echo `date`
```
> **Explanation:**
> Ters tırnak içerisinde komut çalışır ve `echo` komut çalışan çıktıyı ekrana basar.

###### Örnek 2: Alternatifi
```shell
$ echo $(date)
```
> **Explanation:**
> Ters tırnak(backtick) yaptığı işin aynısını yapar yani backtick'e bir alternatif.

###### Örnel 3: Çift Tırnak İçerisinde Kullanımı
```shell
$ echo "Sistemin adı `hostname`"
```
> **Explanation:**
> + Backtick içerisinde yazılan hostname bir komut olduğu için önce hostname komut çalışır ardından echo komut çalışır.
> + Çift tırnak *değişkenleri, escape characters(kaçış dizinlerini)* ve *backtick* içerisindeki komutları yorumlar.
#### Düz Tek Tırnak:
**Tanım:** Tek tırnaklar, içindeki her şeyi **kelime anlamında** alır ve hiçbir değişken, özel karakter veya kaçış dizisi (`\`) değerlendirilmez. Yani, ne yazarsanız o çıktı olarak alınır.

```shell
$ echo 'Kullanıcı: $USER'                  # Çıktı: Kullanıcı: $USER
```
> **Explanation:**
> + USER bir sistem değişkendir ama tek tırnaktan dolayı değişkeni(`$USER`) yorumlamadı.
> + **Uyarı:** Lütfen aynı komut *çift tırnak* ile uygulayıp karşılaştırın.


### Yönlendirme(Redirection)
#### Tanım:
 + **Yönlendirme (redirection)**, komutların çıktısını bir dosyaya kaydetme, hataları başka bir yere yönlendirme veya bir dosyadaki verileri komutlara giriş olarak kullanma gibi işlemleri ifade eder.
 

> [!INFO]
> 3 iletişim kanalı var;
> 1. INPUT **------------->** Klavye `<`  (0)
> 2. OUTPUT **----------->** Ekran (Standart Output - Çıktı) `1>` (1)
> 3. OUTPUT **----------->** Ekran (Standart Error - Hata) `2>` (2)

###### Örnek 1: Command `>` file
```shell
$ history > gecmis.txt
```
> **Explanation:**
> + `history` komut çıktısını ekran basmak yerine `gecmis.txt` dosyaya yönlendirecektir.
> + **UYARI:** `gecmis.txt` dosya içeriği doluysa üzerinde yazacaktır(override).

###### Örnek 1.1: Command > file ile  noclobber
```shell
$ set -o noclobber
```
> **Explanation:**
> + Bash'in üzerine yazma korumasını açar.
> + Eğer bir dosyaya `>` operatörü ile yazmaya çalıştığınızda dosya zaten varsa, Bash bir hata verecek ve dosya *üzerine yazılmasını(no override)* engelleyecektir.

```shell
$ echo "Linux is awesome" > gecmis.txt        # Çıktı: file exists: gecmis.txt
```
> **Explanation:**
> + **Noclobber** seçeneği aktif olduğu için `gecmis.txt` dosyasını üzerine yazılamıyacaktır.
> + Ve hata verecektir; *file exists: gecmis.txt*


> [!TIP]
> `Command 1> file` ile `Command > file` aynı anlama gelmektedir ve aynı çıktıyı vermektedir.

```shell
$ echo "Linux is awesome" >| gecmis.txt
```
> **Explanation:**
> + Eğer `noclobber` aktifse ve yine de bir dosyanın üzerine yazmak istiyorsanız, `>|` operatörünü kullanabilirsiniz.

**Veya**

```shell
$ set +o noclobber
```
> **Explanation:**
> + Eğer üzerine yazma korumasını devre dışı bırakmak isterseniz
> + `noclobber` seçeneğini devre dışı bırakır.

###### Örnek 2: Command `2>` file
```shell
$ find /etc -name network 2> hata.txt
```
> **Explanation:**
> + `find` komut ile `/etc` dizini içerisinde `network` kelimesini arıyoruz. 
> + Eğer hata yok ise ekrana basar aksi taktirde hataları `2>` ile `hata.txt` dosyasına yazar.

###### Örnek 3: Command `>>` file
```shell
$ echo "Bu metini dosyanın sonuna ekle" >> gecmis.txt
```
> **Explanation:**
> + `echo` komutu çıktısını ekrana basmak yerine `gecmis.txt` dosyanın sonuna ekler.
> + **UYARI:** `gecmis.txt` dosyanın içeriğini silmeden dosyanın sonuna ekleyecektir.

###### Örnek 4: Command  `>` file `2>&1`
```shell
$ find /etc -name network > hatalıHatasız.txt 2>&1
```
> **Explanation:**
> + `find` komut ile `/etc` dizini içerisinde `network` kelimesini arıyoruz.
> + Tüm çıktıları yani hatasız çıktıyı ve hatalı çıktıyı `hatalıHatasız.txt` dosyasına yazar.
> + Alternatif Komut: `$ find /etc -name network &> hatalıHatasız.txt`

###### Örnek 4.1: Command `&>>` file
```shell
$ find /etc -name network &>> hatalHatasız.txt
```
> **Explanation:**
> + `find` komut ile `/etc` dizini içerisinde `network` kelimesini arıyoruz.
> + Tüm çıktıları yani hatasız çıktıyı ve hatalı çıktıyı `hatalıHatasız.txt` dosyasına yazar.
> + **UYARI:** `hatalHatasız.txt` dosyanın içeriğini silmeden dosyanın sonuna ekleyecektir.
###### Örnek 4.2: Command `>` file `2>` error
```shell
$ find /etc -name network > hatasız.txt 2> hatalı.txt
```
> **Explanation:**
> + `find` komut ile `/etc` dizini içerisinde `network` kelimesini arıyoruz.
> + Hata çıktısını `hatalı.txt` dosyasına ve hata vermeyen çıktıları da `hatalı.txt` dosyasına yönlendiriyoruz.

###### Örnek 5: Command < file
```shell
$ cat < gecmis.txt
```
> **Explanation:**
> + Hatırlarsanız `histroy > gecmis.txt` komutunu kullanmıştık ve dosyanın içerisine `histroy` komutun çıktısın aktarmıştık.
> + `gecmis.txt` dosyanın içeriğini `cat` komutuna yönlendiriyoruz ve `cat` komutu da çıktıyı ekran aktarıyor.

### Kurallı İfadeler(Regular Expressions-RegEx)
###### Tanım: 
+ Bash scriptlerde **Regular Expressions (RegEx)**, bir metin içerisinde belirli bir desen (pattern) tanımlamak ve bu deseni aramak için kullanılan güçlü bir yapıdır.
+ RegEx, özellikle metin işleme ve manipülasyon işlemlerinde yaygın olarak kullanılır.
+ Bash, RegEx'i `grep`, `sed`, `awk`, `[[ ... ]]` gibi komutlarla kullanmanıza olanak tanır.
###### Bash'te RegEx Kullanım Alanları:
1. **Desen Arama(Pattern) ve Eşleşme:** Bir metinde belirli bir deseni (kelime, sayı vb.) bulmak için kullanılır.
2. **Metin İşleme**: `sed` ve `awk` gibi araçlarla metin üzerinde işlem yapmak (örneğin, bir deseni değiştirmek).
3. **Koşul Kontrolleri**: `[[ ... ]]` yapısıyla RegEx ile koşul kontrolü yapılabilir.
###### RegEx Sembolleri ve Anlamları:
| Sembol | Anlamı                                                                       |
| ------ | ---------------------------------------------------------------------------- |
| `.`    | Herhangi bir karakter                                                        |
| `^`    | Satırın başını ifade eder (başlangıç)                                        |
| `$`    | Satırın sonunu ifade eder (bitiş)                                            |
| `*`    | Sıfır veya daha fazla tekrar                                                 |
| `+`    | Bir veya daha fazla tekrar                                                   |
| `?`    | Sıfır veya bir kez                                                           |
| `[]`   | Köşeli parantez içindeki karakterlerden herhangi biri                        |
| `[^]`  | Köşeli parantez içindeki karakterler dışındaki herhangi bir karakter         |
| `\`    | Kaçış karakteri, özel karakterleri normal bir karakter olarak kullanmak için |
| `()`   | Grup oluşturmak                                                              |

> [!WARNING]
> Bash script'deki [[Bash Script#Meta Karakterler|meta karakterleri]] ile RegEx'deki benzer ve farklı yönleri var ama her ikisi de farklı amaçlara hizmet eder.

###### Örnek 1: Şapka(`^`)
```shell
$ cat /usr/share/dict/words | grep "^kar"
```
> **Explanation:**
> + Pipe (`|`)  ile `cat` komut çıktısını `grep` komutuna yönlendiriyoruz.
> + `grep` komutu `kar` ile başlayan kelimeleri ekrana basar. Çünkü `kar` önünde  şapka(`^`) karakteri var.

###### Örnek 2: Dolar(`$`)
```shell
$ cat /usr/share/dict/words | grep "kar$"
```
> **Explanation:**
> + Pipe (`|`)  ile `cat` komut çıktısını `grep` komutuna yönlendiriyoruz.
> + `grep` komutu `kar` ile bitten kelimeleri erkana basar. Çünkü `kar` sonunda dolar(`$`) karakteri var.

###### Örnek 3: Nokta(`.`)
```shell
$ cat /usr/share/dict/words | grep ".kar."
```
> **Explanation:**
> + Nokta(`.`) herhangi bir karakter ile eşleşmeyi ifade etmektedir. Örneğin; Ana**kara**, D**akar'**\s gibi.

###### Örnek 4: Yıldız(`*`)
```shell
$ cat /usr/share/dict/words | grep "^kar*"
```
> **Explanation:**
> + `kar` kelimesi veya `ka` ile başlayan kelimeleri ekrana basar. Örneğin; **ka**yak, **kar**te, gibi.
> + Yıldız(`*`) kendine önce olan veya olmayan harfleri arar.
> + **UYARI:** Yıldız(`*`) ifadesi meta karakter için farkı anlamı var ama *regex* için farklı bir anlamı var.

##### Koşullu ifadelerde RegEx
###### Tanım:
+ Bash, RegEx kontrolleri için `[[ ... ]]` yapısını ve `=~` operatörünü destekler.
+ `[[ ... ]]` yapısı `test` komutundan daha gelişmiş yapıya sahiptir. 
+ `test` komutu *regex* desteklemektedir.


> [!TIP]
> Regex bir çok programlama yapılarında kullanılmaktadır ve hemen hemen benzerdir. Regex yapısını anlamanın en kolay yolu pratik yapmaktır.

###### Genel Şablonu:
```bash
if [[ $varible =~ regex_pattern ]]; then
	# Koşul doğru ise çalıştırılacak kodlar
else
	# Koşul yanlış ise çalıştırılacak kodlar
fi
```

###### Örnek 1: `[[ ... ]]` ile RegEx Kullanımı
```bash
#!/usr/bin/bash

text="linuxIsAwesome123"
if [[ $text =~ ^l[a-zA-Z]*[0-9]+$ ]];then
	echo "Desen(pattern) eşleşti."
else
	echo "Eşleşme Yok!"
fi
```
> **Explanation:**
> + if yapısı için [[Bash Script#Koşul İfadeleri IF, ELIF and ELSE|Koşul ifadeleri]] bakınız.
> + `^l` : l harfi ile başlayan kelimelere bakar.
> + `[a-zA-Z]` : a'dan z'e veya A'dan Z'e  kadar olan harflerden herhangi bir olabilir.
> + `*` işareti önündeki harflerden sıfır veya daha fazlası ile eşleşme yapar.
> + `[0-9]`: 0'dan 9'a kadar her hangi bir sayı olabilir.
> + `+` işareti `*` işaretine benzer ama en az bir sayı olmak zorundadır.

##### POSIX Karakterleri

- `[:blank:]`: boşluk karakterlerini ifade etmek için kullanılır.
- **`[:space:]`**: Tüm boşluk karakterlerini (tab, newline, space vs.) içerir.
- **`[:alnum:]`**: Alfabetik harfler ve sayılar (a-z, A-Z, 0-9).
- **`[:digit:]`**: Sadece rakamlar (0-9).
- **`[:alpha:]`**: Sadece alfabetik harfler (a-z, A-Z).

###### Örnek 1: `[:blank:]` kullanımı
```bash
$ echo "Merhaba     Dünya" | grep -P "[[:blank:]]"
```
> **Explanation:**
> + **`[:blank:]`** karakter sınıfı kullanılarak metindeki **boşluk veya tab karakterleri** aranır.
> + Eğer satırda boşluk karakteri varsa `grep` bunu bulacaktır.

### Hata Ayıklama (Debugging)
+ Bash script'te **hata ayıklama (debugging)**, bir script’in çalışma sürecini adım adım izleyerek, hataların veya beklenmeyen davranışların nedenini bulmaya yönelik bir yöntemdir.
+ Bash script'lerde hata ayıklama, script'in nasıl çalıştığını daha iyi anlamaya ve yanlış sonuçlara neden olan hataları düzeltmeye yardımcı olur.
##### bash -x ile
###### Örnek 1: Temel Kullanımı
```bash
#!/usr/bin/bash                       # 1  alternatif: #!/usr/bin/bash -x

sayi=0

while ((sayi <= 10); do                # 2
	sleep 3
	echo "Sayı: $sayi"
	((sayi++))
done
```

**Terminal:**
```shell
$ bash -x ./scriptFile.sh
```

**Çıktı:**
```shell
+ sayi=0
./let_komutu.sh: line 40: syntax error near unexpected token `do'
./let_komutu.sh: line 40: `while ((sayi <= 10); do'
```

> **Explanation:**
> 1.  Eğer `#!/usr/bin/bash` yerine `#!/usr/bin/bash -x`  komutu yazarsanız, direk olarak bash script'i `./scriptFile.sh` ile çalıştırabilirsiniz.
> 2. `while` komutu yazılırken `)` eksik yazılarak hata oluşturulmuştur. Bundan dolayı `Çıktı` da `sayi=0` ekrana basmış daha sonrasında yani `while` komutunda hata vermiştir.

##### set -x ve set +x ile
###### Örnek 1.1: Temel Kullanımı
```bash
#!/usr/bin/bash

sayi=0
set -x                        # Komut izlemeyi açar.
while ((sayi <= 10); do       
	sleep 3
set +x                        # Komut izlemeyi kapatır.
	echo "Sayı: $sayi"
	((++sayi))
done
```

**Terminal:**
```shell
$ ./scriptFile.sh
```

**Çıktı:**
```shell
+ (( sayi <= 10 ))
+ sleep 3
+ set +x
Sayı: 0
```
> **Explanation:**
> + `set -x` ile `set +x` arasında aldığımız yerleri hata ayıklama(debugging) yapacak ama diğer dışarda kalan kodları hata ayıklamaya girmeyecektir.

### Hata Kodları

| Hata Kodu | Anlamı                                                                                                         |
| :-------: | -------------------------------------------------------------------------------------------------------------- |
|   **0**   | Başarı durumu. Komut başarılı bir şekilde çalıştı ve sorunsuz tamamlandı.                                      |
|   **1**   | Genel hata. Genellikle bir komut beklenmedik bir şekilde çalışmadığında döndürülür.                            |
|   **2**   | Misuse of shell builtins. Shell built-in komutlarının yanlış kullanılması sonucunda döner.                     |
|  **126**  | Komut çalıştırılabilir değil. Dosya mevcut, ancak çalıştırma yetkisi yok ya da çalıştırılamaz.                 |
|  **127**  | Komut bulunamadı. Genellikle PATH değişkeninde olmayan veya yanlış yazılmış bir komut için döner.              |
|  **128**  | Geçersiz çıkış durumu. Çıkış durumu olarak geçersiz bir sayı veya sinyal kullanıldığında oluşur.               |
|  **130**  | Ctrl+C (SIGINT) sinyali ile iptal edildi. Komut kullanıcı tarafından durduruldu.                               |
|  **137**  | SIGKILL sinyaliyle (kill -9) sonlandırıldı. Komut zorla kapatıldı.                                             |
|  **139**  | Segmentasyon hatası (Segmentation fault). Program bellek adreslerine yanlış bir şekilde eriştiğinde döner.     |
|  **143**  | SIGTERM sinyali ile sonlandırıldı. Komut `kill` komutuyla normal şekilde sonlandırıldı.                        |
|  **255**  | Geçersiz çıkış durumu veya komut çalıştırılamadı. Komut başlatılamadı veya beklenmeyen bir hata meydana geldi. |


### Sinyaler

+ Linux'te **sinyaller (signals)**, işlemler (processes) arasındaki iletişimi sağlayan, işlemlerin belirli olaylar karşısında nasıl davranacağını yönlendiren yazılım kesmeleridir.
+ Bir işlem, belirli bir sinyali aldığında, bu sinyal işlemin yürütülmesini keser ve işlemin o sinyale karşılık belirlenen davranışı sergilemesine neden olur.
+ Sinyaller genellikle işlemleri durdurmak, devam ettirmek veya sonlandırmak için kullanılır, ancak daha birçok işlevi olabilir. Her sinyalin bir numarası ve bir ismi vardır.

| Sinyal        | Numara | Tanım                                                 | Varsayılan Davranış                                                                         |
| ------------- | ------ | ----------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **SIGHUP**    | 1      | Oturum sonlandırma (hangup)                           | Terminal oturumu kapandığında bir işlemi sonlandırmak veya yapılandırmayı yeniden yüklemek. |
| **SIGINT**    | 2      | Kesme (interrupt)                                     | Kullanıcı tarafından **Ctrl+C** ile gönderilir. İşlemi keser (sonlandırır).                 |
| **SIGQUIT**   | 3      | Çıkış (quit)                                          | `Ctrl+\` ile gönderilir. İşlemi sonlandırır ve çekirdek dökümü oluşturur.                   |
| **SIGILL**    | 4      | Geçersiz komut (illegal instruction)                  | Çekirdek dökümü ve sonlandırma                                                              |
| **SIGTRAP**   | 5      | İz tuzağı (trace trap)                                | Çekirdek dökümü ve sonlandırma                                                              |
| **SIGABRT**   | 6      | İşlem abort (abnormal termination)                    | Çekirdek dökümü ve sonlandırma                                                              |
| **SIGBUS**    | 7      | Bellek hatası (bus error)                             | Çekirdek dökümü ve sonlandırma                                                              |
| **SIGFPE**    | 8      | Sayısal işlem hatası (floating point error)           | Çekirdek dökümü ve sonlandırma                                                              |
| **SIGKILL**   | 9      | Zorla sonlandırma (kill)                              | İşlemi zorla sonlandırır. İşlem bu sinyali yakalayamaz veya engelleyemez.                   |
| **SIGUSR1**   | 10     | Kullanıcı tanımlı sinyal 1                            | Kullanıcılar tarafından özelleştirilebilir.                                                 |
| **SIGSEGV**   | 11     | Segmentasyon hatası (segmentation fault)              | Belleğe hatalı erişim nedeniyle oluşur. İşlem sonlandırılır.                                |
| **SIGUSR2**   | 12     | Kullanıcı tanımlı sinyal 2                            | Kullanıcılar tarafından özelleştirilebilir.                                                 |
| **SIGPIPE**   | 13     | Kırık boru (broken pipe)                              | Bir işlem, yazma işlemi için kapalı bir boruya (pipe) veri göndermeye çalıştığında oluşur.  |
| **SIGALRM**   | 14     | Zamanlayıcı alarmı (alarm)                            | `alarm()` fonksiyonu tarafından belirlenen süre dolduğunda gönderilir.                      |
| **SIGTERM**   | 15     | Sonlandırma (terminate)                               | İşlemi düzgün şekilde sonlandırır. İşlemlere kapatma zamanı verir.                          |
| **SIGSTKFLT** | 16     | Yığın hatası (stack fault)                            | Sonlandırır                                                                                 |
| **SIGCHLD**   | 17     | Çocuk süreç sonlandırıldı (child terminated)          | Bir alt işlem (child process) sona erdiğinde ebeveyn işleme (parent) gönderilir.            |
| **SIGCONT**   | 18     | Devam etme (continue)                                 | Duraklatılmış bir işlemi devam ettirir. `fg` komut ile gönderilir.                          |
| **SIGSTOP**   | 19     | Duraklatma (stop)                                     | İşlemi durdurur. İşlem bu sinyali yakalayamaz. Duraklatır (engellenemez)                    |
| **SIGTSTP**   | 20     | Terminal duraklatma (terminal stop)                   | Bir işlemi terminal üzerinden geçici olarak duraklatır. `Ctrl+z` ile gönderilir.            |
| **SIGTTIN**   | 21     | Arka plan işleminin giriş yapma isteği                | Duraklatır                                                                                  |
| **SIGTTOU**   | 22     | Arka plan işleminin çıkış yapma isteği                | Duraklatır                                                                                  |
| **SIGURG**    | 23     | Acil soket durumu (urgent condition on socket)        | Yoksayar                                                                                    |
| **SIGXCPU**   | 24     | CPU zamanı sınırı aşıldı (cpu time limit exceeded)    | Çekirdek dökümü ve sonlandırma                                                              |
| **SIGXFSZ**   | 25     | Dosya boyutu sınırı aşıldı (file size limit exceeded) | Çekirdek dökümü ve sonlandırma                                                              |
| **SIGVTALRM** | 26     | Sanal zaman alarmı (virtual alarm)                    | Sonlandırır                                                                                 |
| **SIGPROF**   | 27     | Profil zamanlayıcı alarmı (profiling timer expired)   | Sonlandırır                                                                                 |
| **SIGWINCH**  | 28     | Pencere boyutu değişti (window resize)                | Yoksayar                                                                                    |
| **SIGIO**     | 29     | G/Ç kullanılabilir (I/O now possible)                 | Yoksayar                                                                                    |
| **SIGPWR**    | 30     | Güç arızası (power failure)                           | Sonlandırır                                                                                 |
| **SIGSYS**    | 31     | Geçersiz sistem çağrısı (bad system call)             | Çekirdek dökümü ve sonlandırma                                                              |

> [!TIP]
>  + `kill -l $? komutu`;
>  + 

###### Örnek 1: SIGTSTP ve SIGCONT
```bash
#!/usr/bin/bash

echo "PID: $$"                 # 1

sayi=0
while (( sayi < 10 )); do
	sleep 10
	((sayi++))
	echo "Sayı: $sayi"
done
exit 0
```

**Sinyal Komutu:**
```bash
$ kill -TSTP PID_value           # 2
```

```bash
$ kill -CONT PID_value           # 3
```

```shell
$ kill -INT PID_value            # 4
```

```shell
$ kill -KILL PID_value           # 5
```
> **Explanation:**
>1.  Yukarıdaki bash script'i çalıştırıyoruz. Ekrana PID'sini basıyor ve 10 saniye aralıklarla sayı değerini ekrana veriyor.
>2. **SIGTSTP** sinyali, **Terminal Stop Signal** anlamına gelir ve Linux/Unix sistemlerinde bir işlemi **geçici olarak duraklatmak** için kullanılır.
>	+ Kullanıcılar bu sinyali terminalden genellikle **Ctrl + Z** tuş kombinasyonuna basarak gönderirler.
>	+ Bu sinyal, bir işlemi arka plana almak ve işlem durdurulduğunda yeniden devam ettirebilmek için kullanılır.
>	+ **Duraklatma**: İşlem durdurulur, ancak tamamen sonlandırılmaz. İşlem, sistemin belleğinde kalır ve işlem yeniden başlatılana kadar CPU kullanmaz.
>	+ **Devam ettirme**: Bir işlem duraklatıldığında, **`fg`** (foreground) komutu kullanılarak yeniden çalışmaya devam edebilir ya da **`bg`** komutu ile arka planda çalıştırılabilir.
>3. **SIGCONT** sinyali, Linux/Unix sistemlerinde bir işlemi **devam ettirmek** için kullanılan bir sinyaldir.
>	+ **SIGCONT**, duraklatılmış bir işlemi (örneğin, **SIGSTOP** veya **SIGTSTP** ile durdurulmuş olan bir işlemi) yeniden çalışmaya başlatır.
>4. **SIGINT** (Signal Interrupt), Linux/Unix sistemlerinde bir işlemi **klavye üzerinden kesmek** (genellikle sonlandırmak) için kullanılan bir sinyaldir.
>	+ **Düzgün sonlandırma**: **SIGINT** sinyali, işlemin kendi temizlik işlemlerini yapmasına izin verir. Örneğin, bir dosya işleme uygulaması, sonlandırılmadan önce açık dosyalarını kapatabilir.
>5. **SIGKILL** sinyali, bir işlemi **hemen ve zorla sonlandırmak** için kullanılan bir sinyaldir. Linux/Unix sistemlerinde **sinyal numarası 9** olan bu sinyal, işlem tarafından engellenemez veya yakalanamaz.
>	+ **Engellenemez ve yakalanamaz**: İşlem, **SIGKILL** sinyalini işleyemez veya durduramaz. İşlem, sinyal gönderildiği anda sonlanır.

##### Trap:
+ Linux'ta **`trap`** komutu, **bash** betiklerinde belirli sinyalleri yakalamak ve bu sinyaller alındığında özel bir işlem yapmak için kullanılır.


> [!CAUTION]
> + `KILL` sinyalini `trap` komut ile yakalayamazsınız.
> + `trap 'echo "KILL ile çıkamazsınız!"' KILL`  ile bash script içerisinde kullandığınızda `trap` komutu `KILL` sinyalini tutamayacaktır. 

###### Örnek 1:
```bash
#!/usr/bin/bash

trap 'echo "Ctrl+C ile çıkamazsınız"' INT
trap 'echo "Ctrl+Z ile çıkamazsınız"' TSTP

echo "Çıkmak için yeter yazın!"

while((1)); do
	echo -n "Devam ediyorum..."
	read str
	if [ "${str,,}" = "yeter" ]; then
		break
	fi
done
echo "Çıkış sağlandı"
```

**Sinyal Komutu:**
```bash
$ kill -TSTP script_PID                    # 1
```

```shell
$ kill -INT script_PID                     # 2
```

> **Explanation:**
> 1. Eğer `TSTP` sinyalini komut veya bunun eşdeğeri olan `Ctrl+z` gönderdiğimiz zaman ekran `$ Ctrl+C ile çıkamazsınız`  mesajını ekrana verir.
> 2. Eğer `INT`  sinyalini komut veya bunun eşdeğeri olan `Ctrl+c` gönderdiğimiz zaman ekran `$ Ctrl+Z ile çıkamazsınız`  mesajını ekrana verir.

###### Örnek 2:
```bash
#!/bin/bash
trap 'rm -f /tmp/gecici_dosya.txt; echo "Temizlik yapıldı!"' EXIT
touch /tmp/gecici_dosya.txt
echo "Betiği çalıştırıyorsunuz..."
sleep 5
```
> **Explanation:**
> 