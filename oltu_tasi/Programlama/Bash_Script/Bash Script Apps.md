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

###### Uygulama 4: Positional Arg. - Aritmatik İşlem
```bash
#!/usr/bin/bash

x="$1"
y="$2"

topla=$((x+y))
echo "$x + $y = $topla"
```
> **Explanation:**
> Terminal: `./app4.sh 4 5` ile değerleri girilir. Toplam sonucu ekrana basar.
