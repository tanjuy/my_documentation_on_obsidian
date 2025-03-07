#Bash_Script


> [!INFO]
> Bash Script Dosyasını çalıştırılabilir hale nasıl getiririz: Örneğin; dosya adı: `apps.sh`
> 1. `$ chmod +x apps.sh`    komut ile çalıştırma izni veriyoruz.
> 2. `ls -ltr` komut ile çalıştırma iznini görebilir.
> 3. `$ ./apps`  komut ile bash script  uygulamayı çalıştırıyoruz.

##### Uygulama 1: shift - Positional Arg
```bash
#!/usr/bin/bash

echo "$0 programını çalıştırdınız"
echo "1.Argüman: $1"                          # windos
echo "2.Argüman: $2"                          # linux
echo "3.Argüman: $3"                          # unix
echo "Tüm Argümanlar: $*"                     # windows linux unix mac
echo "Argüman Sayısı: $#"                     # 4
shift                                         # 1 adım kaydırır.
echo "shift sonrası 1.Argüman: $1"            # linux
echo "shift sonrası 1.Argüman: $2"            # unix
echo "shift sonrası 1.Argüman: $3"            # mac
echo "shift sonrası Tüm Argümanlar: $*"       # linux unix mac
echo "shift sonrası Argüman Sayısı: $#"       # 3
```

**Terminal:**
```shell
$ ./apps.sh windows unix linux mac 
```
> **Explanation:**
> `shift` komut Pozisyonel parametreleri bir adım kaydıracaktır yani `shift` komutundan sonraki `$1` argümanın değeri bir sonraki olan `$2` argümanın değerini alacaktır. `$2` ise kendisinden bir sonra olan argümanın değerini alacaktır.

##### Uygulama 2: while - Positional Arg - shift
```bash
#!/usr/bin/bash

while [ "$1" != "" ]; do
	echo "Argüman: $1"
	shift
done
```

```shell
$ ./apps.sh linux windows mac ...
```

> **Explanation:**
> + `while` döngüsü ile  tek seferde  birden fazla argümanı `$1` ile alıp sırayla işleyebiliriz.
> + `shift` komut her döngüde `$1` argüman değerini kaydırıp bir sonraki argümanı `$1` vermektedir.
> + Bu işlemleri `$@` ile de yapabiliriz.

##### Uygulama 3: if - test - positional arg
```bash
#!/usr/bin/bash

dosya=$1

if [ $# -lt 1 ]; then                             # 1
	echo "Lütfen dosya ismi giriniz !!!"
	echo "Kullanım şekli=$0 dosya_isimi"
elif [ -d $dosya ]; then                          # 2
	echo "$dosya bir klasördür."
elif [ -f $dosya ]; then                          # 3
	echo "$dosya normal bir dosyadır."
elif [ -e $dosya ]; then                          # 4
	echo "$dosya özel bir dosyadır."
else
	echo "$dosya şeklinde bir dosya/klasör yoktur."
fi
```
> **Explanation:**
> 1. `$#` girilen argüman sayısını verir. Eğer argüman sayısı 1'den küçük ise çalışır. (`-lt`: less than)
> 2. `-d` parametresi dizin var mı diye bakar. Eğer girilen argüman dizin ise çalışır.
> 3. `-f` parametresi dosya olup olmadığına bakar.
> 4. `-e` parametresi dosya veya dizin olup olmadığına bakar.

##### Uygulama 4: Positional Arg. - Aritmatik İşlem - fonksiyon
```bash
#!/usr/bin/env bash

function dort_islem() {          # 1
    x=$1
    y=$2

	topla=$((x+y))               # 2
    cikarma=$((x-y))
    carpma=$((x*y))
    bolme=$((x/y))

    echo "$1+$2=$topla"
    echo "$1-$2=$cikarma"
    echo "$1x$2=$carpma"
    echo "$1/$2=$bolme"
}

x=$1                             # 3
y=$2

if [ $# -lt 2 ]; then            # 4
    echo "Lütfen 2 adet sayı giriniz"
    echo "Kullanım şekli: $0 sayı1 sayı2"
	exit 1

elif ! [[ "$x" =~ ^[[:blank:]]*[0-9]*[[:blank:]]*$ ]]; then      # 5
    echo "Hatalı sayı: $x"
    exit 2

elif ! [[ "$y" =~ ^[[:blank:]]*[0-9]*[[:blank:]]*$ ]]; then      # 5
    echo "Hatalı sayı: $y"
    exit 3

else
	dort_islem $x $y        # 6
fi
```

```bash
$ ./app4.sh 10 5
```
> **Explanation:**
> 1. `dort_islem` adında fonksiyon tanımladık
> 2. Aritmetik işlemlerin nasıl yapıldığına dikkat ile inceleyiniz.
> 3. Positional Arg. kullanarak kullanıcıdan girdi alıyoruz.
> 4. `test` komutu ile girilen argüman sayısını kontrol ediyoruz.
> 5. `RegEx` ile birinci argümanın ve ikinci argümanın doğru girildiğini kontrol ediyoruz.
> 6. `dort_islem` adındaki fonksiyonu çağırıp ve parametrelerini fonksiyon veriyoruz. 

##### Uygulama 3: Faktöriyel Hesaplama
```bash
#!/usr/bin/bash

function faktoriyel() {          # 1
    ((i=1))
	((faktoriyel=1))
    while ((i<=$1)); do          # 2 
        ((faktoriyel*=i))        # eş değeri: ((faktoriyel=faktoriyel*i))
	    ((i++))
	done
}


sayi="$1"
if [ $# -lt 1 ]; then            # 3
    echo "Sayı girmediniz"
    echo "Kullanım şekli: $0 sayi"
	exit 1

elif [[ "$sayi" =~ ^[[:blank:]]*[[:digit:]]*[[:blank:]]*$ ]]   # 4
then
	faktoriyel $sayi            # 5

else
    echo "Hatalı sayı: $sayi"
    exit 1
fi

echo "$sayi faktoriyel: $faktoriyel"     # 6
```
> **Explanation:**
> 1. `faktoriyel` adında fonksiyon tanımladık ve görevi faktöriyel hesaplama yapıyor.
> 2. Matematiksel işlemler kullandığımız için `((..))` yapısını kullandık.
> 3. `test` komut ile positional arg. sayısını kontrol ediyoruz.
> 4. Girilen position arg. sayısını `regex` ile doğru yazıldığını kontrol ediyoruz.
> 5. `$faktoriyel` değişkeni ile sonucu ekrana basıyoruz ama dikkat edilmesi gereken nokta bu değişken fonksiyon içerisinde tanımlandığıdır yani değişken global'dir.

##### Uygulama 4: Sayı Tahmin Oyunu
```bash
#!/usr/bin/bash

random=$(( ($RANDOM%100)+1 ))                  # 1

echo "1 ile 100 arasında (1 ve 100 dahil) bir sayı tuttum"
echo "Bil bakalım..."

echo -e "1 ile 100 arasında sayı giriniz: \c"; read tahmin
let tahminSayisi=1                             # 2

while ((tahmin != random)); do

	if ((tahmin > random)); then
		echo "Daha küçük bir sayı giriniz!"
		
	elif ((tahnin < random)); then
		echo "Daha büyük bir sayı giriniz!"
	fi
	echo -e "1 ile 100 arasında sayı giriniz: \c"; read tahmin
	let tahminSayisi++
done

echo "${tahminSayisi}. defada bildiniz."

if [ $tahminSayisi -lt 6 ]; then
	echo "TEBRIKLER"
fi
```
> **Explanation:**
> 1. `$RANDOM` bir sistem değişkeni ve rastgele sayılar üretir ama bu sayılar genelde 3 ile 5 veya daha fazla olabilir bu yüzden `%` operatörü ve 100 ile kalanını alarak 0-99 arasında değerler üretmesini sağlıyoruz. +1 ile aralığı 1-100 arasına çekiyoruz.
> 2. `let` ile değişken tanımlanmıştır. `let` komutu değişken tanımlama, aritmetik işleri hesaplama ve `if` de koşul durumları oluşturma gibi görevleri mevcuttur.
> 	+ `(( ... ))` ile de aynı görevleri yapar.

##### Uygulama 5: Kullanıcı Söz Dizimi Oluşturma
```bash
#!/usr/bin/bash

function adSoyadFonk(){
    local isim="$1"                    # 1
    local digerIsim="$2"               # 1

    if [ -z $isim ]; then              # 2
        echo "İsim boş geçilemez!"
        exit 1
    else
        local loginIsim=$(echo $isim | tr [:upper:] [:lower:])     # 3
        # local loginIsim="${isim,,}"  # Alternatif                # 3

        local tamIsim="$isim"
        if [ ! -z $digerIsim ]; then
            local tamIsim="$isim $digerIsim"
        fi
    fi
    # Return Value
    local varArray=( "$loginIsim" "$tamIsim")   # 4
    echo "${varArray[@]}"                # 5
}

function selectShellFonk() {             # 6
    local shell=$1
    local selShell=""
    if [ -z $shell ]; then
        echo "Shell giriniz"; exit 1
    else
        case "$shell" in
            ksh) selShell=/usr/bin/ksh;;
            bash) selShell=/usr/bin/bash;;
            *) echo "Sadece ksh veya bash girebilirsiniz"; exit 2
        esac
    fi
    # reture value
    echo $selShell
}

function createHomeFonk() {             # 7
    local evetHayir=$1
    local createHome=''
    if [ -z $evetHayir ]; then
        echo "Tercih yapmadınız!"; exit 1
    else
        case "$evetHayir" in
            e ) createHome='-m';;
            h ) createHome=;;
            * ) echo "Sadece evet veya hayır girebilirsiniz"; exit 1
        esac
    fi
    # reture value
    echo $createHome
}

read -p "İsim Giriniz(isim diğerİsim): " isim digerIsim          # 8
read -p "Soyisim Giriniz(soyisim diğerSoyisim): " soyisim digerSoyIsim

loginAdVar=($(adSoyadFonk $isim $digerIsim))                # 9
loginSoyVar=($(adSoyadFonk $soyisim $digerSoyIsim))

loginVar=${loginAdVar[0]}.${loginSoyVar[0]}                  # 10

echo -e "Shell seçiniz:\c"; read shell
selShellVar=$(selectShellFonk $shell)

echo "Home dizini oluşturulsun mu?"
read -p "(evet için e, hayır için h)" evetHayir
createHomeVar=$(createHomeFonk $evetHayir)

comment1="${loginAdVar[@]:0:1} ${loginAdVar[@]:2:3}"          # 11
comment2="${loginSoyVar[@]:0:1} ${loginSoyVar[@]:2:3}"        # 11
echo "Girmeniz Gereken Komut:"
echo "-----------------------"
echo "sudo useradd $createHomeVar -d /home/$loginVar -s $selShellVar \
-c \"$comment1 ${comment2^^}\" $loginVar"
```
> **Explanation:**
> 1. `adSoyadFonk` adında fonksiyon tanımladık ve `local` anahtarını kullanarak 2 değişken tanımladık ve bu değişkenlere fonksiyonun argümanları yükledik.
> 2. `test` komutun `-z` parametresi ile değişkenin boş olup olmadığını kontrol ettik.
> 3. `$isim` adındaki değişkeni harfleri büyük -> küçük dönüştürdük. Bunu `tr` komutu ile veya `${...}` kullanarak yapabiliriz.
> 4. `varArray` adında bir dizi tanımladık ve içerisine değişkenleri yükledik.
> 5. Bash script de `return` programlama dillerindeki gibi çalışmamaktadır. Bu yüzden `echo` komut ile standart çıktıya gönderiyoruz.
> 6. `selectShellFonk` adında bir fonksiyon tanımladık ve görevi hangi kabuğu(shell) seçmemiz noktasında bize yardımcı olmaktadır.
> 7. `createHomeFonk` adında bir fonksiyon ve görevi home dizin altında kullanıcı dizini oluşturup oluşturma konusunda çalışmaktadır.
> 8. `read` komutu ile kullanıcıdan girdi alıyoruz.
> 9. `adSoyadFonk`'undan *geri dönen diziyi(array) bir değişkene nasıl yüklediğimize dikkat ediniz.*
> 10.  `loginAdVar` ve `loginSoyVar` değişkenlerine array yüklemiştik fonksiyonlar ile ve bu array'in sıfırıncı indekslerini alıp birleştirip `loginVar` değişkenine atıyoruz.
> 11. Array yüklü değişkenlerimizi dilimleme(slicing) yaparak array içindeki istediğimiz elemanları alıyoruz. 
> 12. Video Kaynak: [Süleyman ŞEKER](https://youtube.com/watch?v=WEMl6t-yTFo&list=PLeKWVPCoT9e0jHStZlH-z8Gsoo1SBZJlG&index=32)

##### Uygulama 6: Dosyaları Yedekleme
```bash
#!/usr/bin/bash

newFolder="$HOME/backup-$(date +%Y%m%d-%H%M%S)"       # 1

if [ ! -d newFolder ]; then                           # 2
	/usr/bin/mkdir $newFolder
fi

for file in $(ls); do                                 # 3
	if [ -f $file ]; then
		echo "$file kopyalanıyor..."
		/usr/bin/cp -p $file $newFolder               # 4
		sleep 1
	fi
done
```
> **Explanation:**
> 1. `$HOME` sistem değişkenin kullanarak kullanıcı dizin altında `backup` adında ve `date` komut ile birlikte o günün tarih ve saatinde klasör yolunu `newFolder` değişkenine atıyoruz.
> 2. Eğer oluşturulacak klasör dizin yolunda yok ise `newFolder` değişkeni ile klasör oluşturulur.
> 3. `ls` komut ile dizin içeriğini `for` döngüsü ile `file` değişkenine gönderiyoruz.
> 4. Eğer değişken dosya ise `newFolder` değişkenin tutuğu dizine kopyalama yapıyoruz.

##### Uygulama 7:
```bash
#!/usr/bin/bash

# Girilen Sayıların Kıyaslamasını Yapar:
function biggerFonk() {
	if [ $1 -gt $2 ]; then
		echo "$1 daha büyük $2'den"
	else
		echo "$2 daha büyük $1"
	fi
}
# Girilen Argümanların Doğrumu Girildiğini Kontrol eder:
function inputControlFonk() {
	if [ $# -lt 2 ]; then
		echo "2 sayı girmeniz gerekmektedir!"
		echo "Kullanım Şekli: $0 sayi1 sayi2"
		exit 1
	elif ! [[ "$sayi1" =~ ^[[:blank:]]*[0-9]+[[:blank:]]*$ ]]
	then
		echo "Hatalı Sayı: $sayi1"
		exit 1
	elif ! [[ "$sayi2" =~ ^[[:blank:]]*[0-9]+[[:blank:]]*$ ]]
	then
		echo "Hatalı Sayı: $sayi2"
		exit 1
		
	fi
}

sayi1=$1
sayi2=$2

inputControlFonk $sayi1 $sayi2

# biggerFonk fonksiyonda 'Return' yapısı kullanıldı:
MAX=$(biggerFonk $sayi1 $sayi2)
echo "En büyük olan sayı: $MAX"
```
> **Explanation:**
> 

##### Uygulama 8: if - test - regex

```bash
#!/usr/bin/bash

while true; do
    # Kullanıcıdan bir sayı girmesini iste
    echo -e "Bir sayı girin(Çıkmak için 'q' ya da 'quit' yazın : \c"
    read number

    # Çıkış seçeneği kontrolü
    if [[ "$number" == "q" || "$number" == "quit" ]]; then
        echo "Çıkılıyor...";
        sleep 2; break
    fi

    # Girilen değerin bir sayı olup olmadığını kontrol et
    if ! [[ "$number" =~ ^-?[0-9]+$ ]]; then
        echo "Lütfen geçerli bir sayı girin."
        continue
    fi

    # Sayın negatif, pozitif veya sıfır olup olmadığını kontrol et
    if [ "$number" -gt 0 ]; then
        echo "Sayı pozitiftir."
    elif [ "$number" -lt 0 ]; then
        echo "Sayı negatiftir."
    else
        echo "Sayı sıfırdır."
    fi

    echo # Bir satır boşluk bırak
done
```

##### Uygulama 9: case 
```bash
#!/usr/bin/bash

# Kullanıcı dosya adını al
echo -e "Bir dosya adı girin: \c"

# Dosya türüne göre işlem yap
case $1 in
    *.txt)
        echo "Bu bir metin doyası.";;
    *.jpg|*.png)
        echo "Bu bir resim dosyaı.";;
    *.sh)
        echo "Bu bir Bash script dosyası.";;
    *)
        echo "Dosya türü tanımıyor.";;
esac
```
