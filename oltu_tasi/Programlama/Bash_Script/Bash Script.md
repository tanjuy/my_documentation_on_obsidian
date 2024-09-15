#Bash_Script 

>[!INFO] Bilgi:
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

>[!INFO] Bilgi:
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

###### Örnek 3: Değişkenin Varsayılan Değeri:
```bash
#!/usr/bin/env bash

distro="Arch Linux"
echo "${distro:-Ubuntu}"
```
> **Explanation:**
> distro değişkenine değer(*Arch Linux*) atanırsa ekrana basar. Aksi taktirde distro değişkenine değer atanmasa *varsayılan değer olarak Ubuntu* ekrana basar. 

###### Örnek 4: Karakter Dizi Maniplasyonu:
```bash
#!/usr/bin/env bash

string="Linux is Awesome"
echo ${string:6:5}                 # çıktı: is Aw
```
> **Explanation:**
> Değişkenimizi tutmuş olduğu karakter dizini dilimleyebiliyoruz.

###### Örnek 5: Büyük harf -> Küçük harf
```bash
#!/usr/bin/bash

text="LINUX IS AWESOME!"
lower_case_text="${text,,}"

echo "$lower_case_text"
```
> **Explanation:**
> Bash 4.0 ve üstü sürümlerde, bir değişkenin içeriğini küçük harfe çevirmek için `${var,,}` biçimini kullanabilirsiniz.
> Süslü parantez özeliği ile değişken içeriğini *büyük -> küçük harfe* dönüştürdük.

###### Örnek 6: Küçük harf -> Büyük harf
```bash
#!/usr/bin/bash

text="linux is awesome!"
upper_case_text="${text^^}"

echo "$upper_case_text"
```
> **Explanation:**
> Bash 4.0 ve üstü sürümlerde, bir değişkenin içeriğini büyük harfe çevirmek için `${var^^}` biçimini kullanabilirsiniz.
> `"${text^^}"` ifadesi, `text` değişkenindeki tüm harfleri *büyük harfe dönüştürür.*

>[!INFO] Bilgi:
>Bash script'in yorum işaret kare'dir; `# bu bir yorumdur.` Yukarıda kullanıldığı gibi.

### Read Kullanımı:
>[!INFO] Bilgi:
>`read komut` kullanıcıdan girdi almak için kullanılır

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
> Bash Script çalıştırılmadan verilen girdilerdir. Argümanların bir diğer adı **Pozisyonel parametreler** ve İngilizcesi: **Positional parameters** 

###### Örnek 1: $1, $2, $3 ... 
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
> Dosyamızı dikkat ederseniz bash script için özel değişkenleri verdik.
> Dosyayı(Bash Script) çalıştırma aşmasında argüman olarak Linux($1), Mac($2) ve Windows($3) argümanlarını verdik ve her biri sırasıyla değişkenlere atandı.
>  Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)

>[!CAUTION]
>$0 dosyanın isimine karşılık gelir yani $0 eşittir ./bash_arguments.sh

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
> Tüm değişkenlere karşılık gelmektedir. $@ eşittir `$1, $2, $3 ...` 
> Değişkenlerde kullanılan süslü parantez de mevcuttur: `${@}` 
>  Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)

> [!WARNING] Uyarı:
> Eğer alınacak argüman sayısı belirli değilse yan bash script programınıza göre bazen 3 argüman alırken bazen 5 argüman alıyorsa `$@` bash script de özel olan bu değişkeni kullanabilirsiniz.

###### Örnek 3: $@ de sıfırıncı indeks
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

###### Örnek 4: Tüm string argünmalar  $*
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

###### Örnek 5: $@ ile $* Arasındaki Fark

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

###### Örnek 6:  Argüman Sayısı $# 
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
> Eğer bash script dosyanın adı `apps.sh` olursa ve girilen argümanlarda 2 adım kaydırdığımızda(*shift komutu*) sadece *linux* çıktısını verecektir

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
> Yukarıda test komutun genel kullanımı verilmiştir.
> `test` komutu, dosya ve dizinlerin durumunu kontrol etmek, karşılaştırmalar yapmak ve mantıksal ifadeleri değerlendirmek için kullanılır.
> `test` komutu, bir ifadenin veya koşulun doğru olup olmadığını kontrol eder ve sonucuna göre `0` (başarı) veya `1` (başarısızlık) döndürür.
> `test` komut koşullu ifadelerde sıklıkla kullanılır.

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
> home dizini altında ottoman dizini var mı diye bakıyoruz. `ècho $?` komut başarılı ise 0 verir aksi taktirde 1 verir.
> yorum(#) satırı ile alternatifi verilmiştir.

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
> operand'lar tam sayı(5) olduğu için `-eq` kullanıldı ve *5 sayısı 5 sayısına eşit mi* sorar.
> Ayrıca yorum(#) satırında alternatifi verilmiştir. Yine `echo $?` komut ile durum kontrolü yapılabilir.
  
###### Örnek 2: -lt (küçüktür)
```shell
$ [ 3 -lt 5 ]                      # test 3 -lt 5
```
> **Explanation:**
> operand'lar tamsayı olduğu için `-lt` kullanıldı ve  *3 sayısı 5'den küçük mü* sorar.
> Ayrıca yorum(#) satırında alternatifi verilmiştir. Yine `echo $?` komut ile durum kontrolü yapılabilir.

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
> Operand'ların string olduğu için sembol(=) kullanabiliyoruz. Ayrıca yorum satır(#) ile de alternatifi yazılmıştır.  `echo $?` kontrol edebiliriz. 0 => başarılı  1 => başarısız.

###### Örnek 2:  test -z

```shell
kardiz=""
$ [ -z $kardiz ]                          # test -z $kardiz
```
> **Explanation:**
> kardiz adlı değişkenin boş olup olmadığını kontrol ediyoruz. Eğer `echo $?` komutu sıfır verirse kardiz boş karakterli ama bir verirse kardiz değişkeninde karakter dizini atanmıştır.

###### Örnek 3: test -n
```shell
kardiz="not empty"
$ [ -n $kardiz ]                          # test -n $kardiz
```
> **Explanation:**
> `test -z` komutun tam tersi çalışır. `echo $?` ile baktığımızda kardiz değişkenin içerisi boş değilse çıktı 0 boş ise 1 verir.

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
-eq / eşit ise                / if [ "$a" -eq "$b" ] / (equal)
-ne / eşit değil ise          / if [ "$a" -ne "$b" ] / (not equal)
-gt / büyük ise               / if [ "$a" -gt "$b" ] / (greater than)
-ge / büyük veya eşit ise     / if [ "$a" -ge "$b" ] / (greater than or equal)
-lt / küçük ise               / if [ "$a" -lt "$b" ] / (less than)
-le / küçük veya eşit ise     / if [ "$a" -le "$b" ] / (less than or equal)

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

> [!INFO] Bilgi
> `[[ ... ]]`  ifadesi `test` komutunda göre daha güçlü ve daha esnektir. 

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
> Tam sayı karşılaştırılamsı yapıldığı için `-eq` kullanıldı.
> 1 ile 2 arasında bir fark yok aynı sonuç verir. Eğer koşul doğru ise yani değişken değeri 10'a eşit ise ekran çıktıyı yazdırır.
> 

###### Örnek 2: if çift parantez ile
```bash
#!/usr/bin/bash

sayi=10
if (( $sayi > 9 )); then
	echo "Koşul Doğru"
fi
```
> **Explanation:**
> Örnek 1 ile aynı ama burada çift parantezler sayesinde simge(>) kullanabiliyoruz.

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
> sayi adlı değişkenimiz 9'a eşit olduğundan if ve elif bloklarına giriş yapmayacak ve en son seçenek olarak else kodu çalışacaktır.

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
> Harfler arasında da sıralama olup ve bu bağlı olarak karşılaştırma yapabiliriz tam sayılarda olduğu gibi. `[[ ... ]]` yerine *test* komutunda kullanabiliriz.

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
> Daha fazlası için [[Bash Script#1. Dosya ve Dizin Kontrolleri|Dosya ve Dizin Kontrolleri]] bakınız.
> Eğer dosya veya istenen dizin mevcut(-f) ise `if` bloğu çalışır aksi taktirde `else` bloğu çalışır. 

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
> Yukarıdaki Örnek 3 ile aynı ama burada dosyanın yazılabilir mi kontrol ediyoruz. `ls -l` teyit edebiliriz, eğer *w* varsa  dosya yazılabilir demektir. `chmod -x dosya_adı` ile yazma haklarını alıp tekrar deneyerek script'inizi kontrol edebilirsiniz. 

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


### AND ve OR operatörleri

> [!INFO] Bilgi:
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
#### Tam Sayılar(Integer) ile
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
> Değişkenlere atanan değerler ile matematik işlemleri yapılıyor.

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
> Örnek 2 yaptığımızın aynı işlemleri yaptık ama `expr` komutunu kullandık.
> **Burada dikkat edilmesi gereken nokta** aritmetik operatörler arasına kesinlikle boşluk bırakmalıyız ve ayrıca çarpma işlemi de kullanılan yıldız işaret özel karakteri olmasını engellemek için ters slash(/) yıldız işaretin önüne koyuyoruz.



> [!TIP] 
> `((i++))` veya `i=$((i+1))` döngülerde `i` değişkenini her döngüde artırır.
> `((i--))` veya `i=$((i-1))` döngülerde `i` değişkenini her döngüde azaltır.

#### Ondalıklı(Float) Sayılar ile

> [!INFO] Bilgi:
> Ondalıklı sayılarla işlem yapabilmemiz için `bc` komutunu kullanıyoruz:
> `bc` ifadelerin etkileşimli yürütülmesi ile [arbitrary precision numbers](https://en.wikipedia.org/wiki/Arbitrary-precision_arithmetic#:~:text=In%20computer%20science%2C%20arbitrary%2Dprecision,memory%20of%20the%20host%20system.) destekleyen bir dildir. (man bc)

###### Örnek 1: Basit Gösterim
```bash
echo "20.5+5" | bc                   # Çıktı: 25.5
```
> **Explanation:**
> `echo` komutun çıktısını `bc` komutuna yönlendiriyoruz ve `bc` komutun aldığı veriyi değerlendiriyor.

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
> sayi1 ve sayi2 adlı değişken oluşturarak echo komut ile hem bc parametresi olan scale hem de değişken değerlerini bc komutunda yönlendirdik.
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=w69wvsDzCJo&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=9)

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
> Diziler(arrays) tüm programlama dillerinde olduğu gibi indeksi *0(sıfır)'dan* başlar.
> Linux: 0, Windows: 1, Unix: 2 indeks de olacaktır.
> Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=7GoukBA6tZc&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=13)

###### Örnek 2: Diziye eleman ekleme
```bash
#!/usr/bin/env bash

OS=( "Linux" "Windows" "Unix" )

echo "Tüm dizi: ${OS[@]}"
OS[3]='Mac'
echo "Tüm dizi tekrar: ${OS[@]}"
```
> **Explanation:**
> OS dizin en son indeksi 2 bu yüzden biz 'Mac' elmanı 3. indekse ekliyoruz. Aksi taktirde mevcut dizini değiştirecektir.

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
>  `unset` komut ile 1. dizin de olan windows dizinden silinecektir.
>  `echo -e` de -e parametresi echo komutun backslach kaçış karakterlerin yorumlanmasına izin verecektir *(man echo)*. Böylelikle daha düzgün görünüm elde edeceğiz.
>  ==UYARI:== Window'u sildik ve indeksi 1'di ve Eğer `$!OS[@]` komut ile bakarsak index 1 olmadığını görebiliriz.

### Döngüler(Loops)
#### While Döngüsü:
###### While Şablonu:
```bash
while condition
do
	<expression>
done	
```

###### Örnek 1: Basit Kullanım:
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
> C temeli programlama diline benzer bir for döngüsü

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
> Python programlama diline benzer bir for döngüsü

###### Örnek 2: for ile linux komutları
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

###### Örnek 1: Basit Kullanımı
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

###### Örnek 2: Select ile Dizi Kullanımı
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

#### Koşullu ifadelerde RegEx
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
