

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

##### $variable ile ${variable} kıyaslama:
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
> Bash Script çalıştırılmadan verilen girdilerdir.

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

>[!CAUTION] Uyarı:
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
> Tüm değişkenlere karşılık gelmektedir. $@ eşittir $1, $2, $3 ... 
> Değişkenlerde kullanılan süslü parantez de mevcuttur: ${@} 
>  Video: [Süleyman ŞEKER](https://www.youtube.com/watch?v=Nm8v__0iui0&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=5)

> [!WARNING] Uyarı:
> Eğer alınacak argüman sayısı belirli değilse yan bash script programınıza göre bazen 3 argüman alırken bazen 5 argüman alıyorsa `$@` bash script de özel olan bu değişkeni kullanabilirsiniz.

###### Örnek 3: $@ de sıfırıncı indeks
**Bash Script Dosyası: bash_arguments.sh**
```bash
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
echo $#
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

###### Örnek 1:  Basit Kullanımı:
```bash
#!/usr/bin/bash

OS=( "Linux", "Windows", "Unix" )

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

OS=( "Linux", "Windows", "Unix" )

echo "Tüm dizi: ${OS[@]}"
OS[3]='Mac'
echo "Tüm dizi tekrar: ${OS[@]}"
```
> **Explanation:**
> OS dizin en son indeksi 2 bu yüzden biz 'Mac' elmanı 3. indekse ekliyoruz. Aksi taktirde mevcut dizini değiştirecektir.

###### Örnek 3: Diziden eleman silme
```bash
#!/usr/bin/bash

OS=( "Linux", "Windows", "Unix" )

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

