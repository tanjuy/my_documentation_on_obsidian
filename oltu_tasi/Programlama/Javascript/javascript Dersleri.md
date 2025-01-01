### Javascript html dosyasına bağlama:

#### 1. Yöntem:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Javascript Öğreniyorum</title>
</head>
<body>
    <script>
        console.log("Merhaba Dünya")
    </script>
</body>
</html>
```
> **Explanation:**
> javascript kodları ==index.html== dosyasında çalıştırıyoruz.

#### 2. Yöntem:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Javascript Öğreniyorum</title>
</head>
<body>
    <script src="index.js"></script>
</body>
</html>
```

> **Explanation:** index.html
> ==index.html== dosyası oluşturup ==index.js== dosyamızı entegrasyonu
>  (`<script src="index.js"></script>`) yapıyoruz.

### Yorum Satırı:
> [!INFO] Bilgi:
> Javascript de yorum satırı: 
> `// Bu tek satırlık yorum satırı` 
>```
> /*
> 	Bu birden çok satırlı yorum satırı
>*/
> ```

> [!IMORTANT] Önemli:
> Tüm metotları ekrana basmak için: `console.log(window)`
> document özelliği o pencerede yüklenen DOM document işaret eder. Yani window nesnesin içerisindeki document özeliği DOM document'ine referans eder.


### Ekrana Çıktı Verme:
```js
console.log("Merhaba Dünya");
console.log("Linux is", "awesome");
```
veya
```js
window.alert("Hello World!");
// alert("Hello World!");
```

### Değişken:
**Syntax:**
```javascript
scope_key variable_name = variable_value
```
> **Explanation:**
> + `scope_key` : kapsam anahtarı yani `var`, `let` ve `const` anahtar kelimelerini alır. Örneğin; `let`
> + `variable_name` : programınıza uygun bir isimlendirme. Örneğin; distro
> + `variable_value`: değişkenin tutacağı değer. Örneğin; ubuntu
> + Sonuç olarak; `let distro = ubuntu` k

### Scope (Kapsam):
> [!INFO] Bilgi:
> Javascript de 3 tane scope alanı vardır:
> 1. Global Scope
> 	+ En geniş scope'dur ve her yerden bu değişken değere ulaşılabilir.
> 	+ window objesi de global scope'dur.
> 	+ Eğer dosya düzeyinde *let* ile değişken tanımlarsak global scope da çalışır değişkenimiz. [[javascript Dersleri#Örnek 2|let global]]
> 2. Function Scope
> 	+ Fonksiyonların kendi scope'ları mevcuttur. Aynı dosya düzeyinde tanımlan değişkenler gibi.
> 3. Block Scope
> 	+ if-else, while loop ve for loop block scope'dır.
> 	+ *let* ile değişken tanımladığımızda değişken *block scope* alanında etkin olunur. Block scope dışına çıkıldığında değişken yok olur.

#### 1.Global Scope:

+ **Global değişken**, programın herhangi bir yerinden **erişilebilen** ve **kapsamı (scope)** sınırlı olmayan bir değişkendir.
+ Bu tür değişkenler, belirli bir fonksiyon ya da blokla sınırlı değildir; programın tamamında kullanılabilir.


> [!CAUTION]
> + Tarayıcıda çalışan bir JavaScript kodunda **tüm global değişkenler, fonksiyonlar ve nesneler** aslında `window` nesnesinin bir özelliği olarak depolanır.
> + Eğer bir değişken veya fonksiyon global olarak tanımlandıysa, ona `window.değişkenAdı` ya da `window.fonksiyonAdı` şeklinde erişebilirsiniz.
> + *var ile oluşturulan değişkenler window scope alanında oluşurlar.* Örneğin; `var distro = linux;` distro değişkeni window scope da oluşur. Eğer `console.log(window)` baktığımızda window nesnesi içerisinde görebiliriz. 
> + window nesinesin kendisi bir global scope'dur.


> [!WARNING]
> `var distro = linux` ile `distro = linux` aynıdır. Varsayılan *var* anahtar kelimesidir. 

##### Global: var key ile
```javascript
var variable_1 = 'javascript'

console.log('variable_1:',variable_1)
console.log('windows.variable_1:', window.variable_1)
```

**Çıktı:**
```console
variable_1: javascript
windows.variable_1: javascript
```
> **Explanation:**
> + Dosya düzeyinde ve `var` anahtar kelimesi ile tanımlan `variable_1` değişkeni global bir değişken olmaktadır.
> + Çünkü, `var` anahtar kelimesi değişkeni global düzeye taşımaktadır. Ayrıca dosya düzeyindeki değişkenlerde değişkenleri global yapmaktadır.
> + `window` nesnesi ile değişkene ulaştığımız için bu değişkenin global olduğunu göstermektedir.




---
###### Örnek 1: var block
```js
if (true) {
    var distro = 12
}
console.log(distro)
```
> **Explanation:**
> + if bir block scope ama `var` ile değişken tanımlandığı için *distro* değişkeni *window* objesinde oluştuğu için global bir değişken oluşturmuş oluyoruz her yerden ulaşabiliriz.




###### Örnek 2: let global
```js
// Global Scope
let a = "let anathar kelimesi";       // 1

if (true) {                           // 2
    // Block Scope
    console.log('Block Scope:',a);    
}

test2();                              // 3

function test2 () {                   // 4
    // function Scope
    console.log('Function Scope:',a);
}
```
> **Explanation:**
> 1. dosya düzeyinde değişken tanımlanmıştır. Bu yüzden global seviyedir.
> 2. `if` de bir block scope alanıdır. `a değişkeni` dosya düzeyinde olduğu için ekrana çıktı verecektir.
> 3.  4. basamakta fonksiyon tanımladık ve çalışması için çağırıyoruz.
> 4. `a değişkeni` dosya düzeyin de olduğun için fonksiyon içerisinden de ekrana çıktı verebiliyoruz.


#### 2.Function Scope:

#### 3.Block Scope:

