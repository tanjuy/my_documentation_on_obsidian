###### Örnek 1: Girdi alma ve if-else

> [!EXAMPLE] Örnek 1:
> Kullanıcı tarafından girilen nota göre geçtiniz veya kaldınız geri dönüşünü yazdırınız

```go
package main

import (
    "bufio"
    "fmt"
    "os"
    "strconv"
    "strings"
)

func main() {
    fmt.Print("Lütfen aldığınız notu giriniz:")
    // Burada hatayı yakalamamıza gerek yok çünkü fonksiyon
    // içerisinde hata yakalanıyor.
    grade, _ := getGrade()                   # 1

    var result string
    if grade >= 50 {
        result = "Geçtin ;)"
    } else {
        result = "Kaldınız!"
    }
    fmt.Println(result)
}

func getGrade() (int, error) {               # 1
    reader := bufio.NewReader(os.Stdin)      # a
    input, err := reader.ReadString('\n')    # a

    if err != nil {
        fmt.Println(err)
    }
    input = strings.TrimSpace(input)         # b
    num, err := strconv.Atoi(input)          # c

    if err != nil {
        fmt.Println(err)
    }
    return num, nil
}
```
> **Explanation:**
> 1. `getGrade` ekrandan girdi alma fonksiyonu ayrıca içerisinde hata kontrolü de yapmaktadır.
> 	a. açıklması: [[Golang#Girdi Alma|Girdi alma]]
> 	b. strings paketindeki TrimSpace fonksiyonu; baştan ve sondan boşlukları silecektir.
> 	c. strconv paketindeki Atoi fonksiyonu string --> int dönüştürür. ParseInt(s, 10, 0) eş değerdir.

###### Örnek 2: fonksiyonlar, Girdi alma, Random
> [!EXAMPLE] Örnek 2:
> 1 ile 100 arasındaki bir sayıyı tahmin etme uygulaması yazınız. Toplam tahmin hakkınız 10 olsun.

```go
package main

import (
    "bufio"
    "fmt"
    "math/rand"
    "os"
    "strconv"
    "strings"
    "time"
)

func main() {
    target := numRandNew(1, 100)
    fmt.Println("1 ile 100 arasındaki sayıyı bulmaya çalışın")

    for attempts := 0; attempts < 10; attempts++ {
        fmt.Println(10-attempts, "hakkınız kaldı")
        fmt.Print("Lütfen tahminizi yapınız: ")

        num, _ := inputData()

        // fmt.Println(target)

        if num > target {
            fmt.Println("Tahminiz daha büyük, daha küçük bir sayı giriniz.")
        } else if num < target {
            fmt.Println("Tahminiz daha küçük, daha büyük bir sayı giriniz.")
        } else {
            fmt.Println("Doğru tahmin", attempts, " seferde bulundunuz")
            break
        }
    }
}

func numRand(min, max int) int {
    // rand.Seed(time.Now().Unix())    Seed -> deprecated
    return rand.Intn(max-min) + min
}

func numRandNew(min, max int) int {
    rand.New(rand.NewSource(time.Now().Unix()))
    return rand.Intn(max-min) + min
}

func inputData() (int, error) {
    reader := bufio.NewReader(os.Stdin)
    input, err := reader.ReadString('\n')
    if err != nil {
        fmt.Println(err)
    }
    input = strings.TrimSpace(input)
    num, err := strconv.Atoi(input)
    if err != nil {
        fmt.Println(err)
    }
    return num, err
}
```

> **Explanation**: [Arin Yazilim Video](https://www.youtube.com/watch?v=fSJ57p5a-L8&list=PL-Hkw4CrSVq96dPr33xTdBjSgn9wKLHPa&index=27)
> 