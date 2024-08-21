>[!INFO] Bilgi:
>Ubuntu da yüklü olan Shell'ler `/etc/shells` dosyasında mevcuttur.
>``` bash
> $ cat /etc/shells
> ```

> [!WARNING] Uyarı 1:
> + `#!/usr/bin/bash` komut önemli dosyamıza çalışma izni verdiğimizde çalışmayı buradan yapıyor. Çalışma yolunu `$ which bash` komut ile bulabilirsiniz.
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

### Değişkenlar:

>[!INFO] Bilgi:
>İki tür değiken(variable) vardır;
>1. *Sistem değişkenleri (System Variables)*: İşletim sistemi ile gelen değikenlerdir.
>2. *Kullanıcı değişkenleri (User Variables)*: Sonradan kullanıcı tarafından oluşturulan değişkenlerdir.
>Değiken türleri string veya integer olabilir.

###### Sistem Değişkenleri:
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
###### Kullanıcı Değişkenleri:
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


> [!CAUTION] Dikkat:
>`$distro` ile `${distro}` kullanımın temel olarak arasında bir fark yok ama `${distro}` daha fazla ek özellikleri vardır.

###### Örnek 2: $variable ile ${variable} kıyaslama:
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

###### Örnek 5: Read ile Birden Fazla Girdi Alma
```bash
#!/usr/bin/env bash

# echo -n "Linux Dağıtımları: "; read distro1 distro2 distro3     # 1
read -p "Linux Dağıtımları: " distro1 distro2 distro3             # 2

echo "Linux Distros: $distro1 - $distro2 - $distro3"
```
> **Explanation:**
> `read` komut ile birden fazla girdi alabiliriz
> 1 deki adımı daha kısaltarak 2'inci adım ile girdi alabiliriz. Aynı görevi görür.

###### Örnek 6: Şifre Yazılışını Gizleme(slience)
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


 