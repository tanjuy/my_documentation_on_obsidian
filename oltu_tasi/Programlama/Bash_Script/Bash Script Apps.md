#Bash_Script


> [!INFO]
> Bash Script Dosyasını çalıştırılabilir hale nasıl getiririz: Örneğin; dosya adı: `apps.sh`
> 1. `$ chmod +x apps.sh`    komut ile çalıştırma izni veriyoruz.
> 2. `ls -ltr` komut ile çalıştırma iznini görebilir.
> 3. `$ ./apps`  komut ile bash script  uygulamayı çalıştırıyoruz.

###### Uygulama 1: shift - Positional Arg
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

###### Uygulama 2: while - Positional Arg - shift
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

###### Uygullama 3: if - test - positional arg
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

###### Uygulama 4: Positional Arg. - Aritmatik İşlem - fonksiyon
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

###### Uygullama 3: Faktöriyel Hesaplama
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

###### Uygulama 4: Sayı Tahmin Oyunu
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