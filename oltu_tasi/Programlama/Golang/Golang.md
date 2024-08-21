## Fonksiyonlar:
### Named Return Value:
```go
package main

import "fmt"

func main() {
    x, y := 10, 4
    sum, minus, multiple := calculation(x, y)
    rest, division := calculation_named(x, y)

    fmt.Println(sum, minus, multiple)
    fmt.Println(rest, division)
}

func calculation(num1, num2 int) (int, int, int) {                   # 1
    sum := num1 + num2
    minus := num1 - num2
    multiplication := num1 * num2

    return sum, minus, multiplication
}

func calculation_named(num1, num2 int) (rest int, division int) {   # 2
    rest = num1 % num2
    division = num1 / num2
    // return rest, division
    return
}
```
> **Explanation:**
> 1. calculation fonksiyonunda normal bir fonksiyon kullanıyoruz
> 2. named retrun fonksiyon(isimlendirilmiş return değeri) kullanılıyor.
## Hata Yakalama:


> [!NOTE] Not:
> Beklenilmeyen tüm sonuçlara hata(error) denir.

> [!IMPORTANT] Önemli:
> Go dilinde (`Golang`), `nil` bir değeri temsil eden özel bir anahtar kelimedir ve genellikle referans türleri (pointer, slice, map, channel, function, interface) için kullanılır. Bir değişkenin `nil` olması, onun bir değeri olmadığını veya başlangıçta atanmış bir referansı olmadığını gösterir.

###### Örnek 1: Çift sayı kontrolü
```go
package main

import (
    "errors"
    "fmt"
)

func main() {
    // fmt.Println(evenNum(11))
    result, err := evenNum(10)

    if err != nil {
        fmt.Println(err)
    } else {
        fmt.Println("Girdiğiniz sayı:", result)
    }
}

func evenNum(num int) (int, error) {
    if num%2 != 0 {
        return 0, errors.New("HATA: Çift sayı girmediniz")    # 1
    }
    return num, nil
}
```
> **Explanation:**
> Girilen sayın çift olup olmasını kontrol ediyoruz. Eğer çift ise ekrana değeri basar aksi taktirde hata geri dönerek *HATA: Çift sayı girmediniz* ekrana çıktı verir.
> 	1. Burada `error.New` fonksiyonuna bir hata mesajı(*HATA: Çift sayı girmediniz*) veriliyor ve bu mesajla bir `error` nesnesi oluşturuluyor.

###### Örnek 2:  Karakökün değeri kontrolü
```go
package main

import (
    "errors"
    "fmt"
    "math"
)

func main() {
    var value float64 = -16
    var result float64
    var err error

    result, err = sRoot(value)

    if err != nil {
        fmt.Println(err)
    } else {
        fmt.Printf("%v sayısın karakökü: %v\n", value, result)
    }

    fmt.Println(math.Sqrt(-16))          # 1
}

func sRoot(num float64) (float64, error) {
    if num < 0 {
        return 0, errors.New("negatif sayıların karakökü alınamaz")
    }
    return math.Sqrt(num), nil
}
```
> **Explanation:**
> Karakök değerin negatif girmesini kontrol ediyoruz. errors interface'in New yapısı ile nesne üretip geri dönüyoruz.
> 	1. `fmt.Println(math.Sqrt(-16))` ile hata kontrolü yapmadığımızda ne gibi sonuç veriyor buradan görebilirsiniz.(Çıktı: NaN)

###### Örnek 3: Open Fonksiyonun
```go
package main

import (
    "fmt"
    "os"
)

func main() {
    file, err := os.Open("test.txt")

    if err != nil {
        fmt.Println("Hata:", err)
    } else {
        fmt.Println("Dosyamız: ", file)
    }
}
```
> **Explanation:**
> Built-in bir fonksiyon olan os paketinin Open fonksiyonu 2 değer göndermektedir; Birincisi file ve diğeri err. Bu doğrultuda eğer dosya yoksa if bloğunda hatayı ekrana basar aksi taktirde dosyanın(file) pointer'ından dönen adresi ekran basar.

## Girdi Alma:
```go
package main

import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    reader := bufio.NewReader(os.Stdin)            # 1, 2
    fmt.Print("Lütfen bir değer giriniz: ")
    input, err := reader.ReadString('\n')          # 3

    if err != nil {
        fmt.Println(err)
    }
    fmt.Println("Girilen değer:", input)           
}
```
> **Explanation:**
> 1. `bufio`, Go dilinde buffered (ara bellekli) giriş ve çıkış işlemleri için kullanılan bir pakettir. Buffered I/O, girdiyi veya çıktıyı belleğe alarak daha verimli işlemler yapmayı sağlar.
> 2. `os.Stdin`, Go dilinde standart giriş akışını temsil eder. Bu, genellikle terminalden alınan kullanıcı girdisi anlamına gelir.
> 3. `reader.ReadString('\n')` ifadesi, kullanıcıdan bir satır girdi alır ve bu girdiyi bir string olarak döndürür.