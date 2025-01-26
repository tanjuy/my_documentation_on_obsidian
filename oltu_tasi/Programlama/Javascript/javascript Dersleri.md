## Javascript html dosyasına bağlama:

### 1. Yöntem:
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

### 2. Yöntem:
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

## Yorum Satırı:
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


## Ekrana Çıktı Verme:
```js
console.log("Merhaba Dünya");
console.log("Linux is", "awesome");
```
veya
```js
window.alert("Hello World!");
// alert("Hello World!");
```

## Değişken:
**Syntax:**
```javascript
scope_key variable_name = variable_value
```
> **Explanation:**
> + `scope_key` : kapsam anahtarı yani `var`, `let` ve `const` anahtar kelimelerini alır. Örneğin; `let`
> + `variable_name` : programınıza uygun bir isimlendirme. Örneğin; distro
> + `variable_value`: değişkenin tutacağı değer. Örneğin; ubuntu
> + Sonuç olarak; `let distro = ubuntu` k

## Let - Const - Var:
### Let:
+ `let` anahtar sözcüğü ES6'da (2015) tanıtıldı.
+ 

#### Kaynak:
+ [JS Let](https://www.w3schools.com/js/js_let.asp)

## Scope (Kapsam):


> [!INFO] Bilgi:
> Javascript de 3 tane scope alanı vardır:
> 1. Global Scope
> 	+ En geniş scope'dur ve her yerden bu değişken değere ulaşılabilir.
> 	+ window objesi de global scope'dur.
> 	+ Dosya düzeyinde `let` ve `const` anahtarları ile tanımlan değişkenlerde global kapsama girmektedir. Çünkü, burada oluşturulan değişkenlere fonksiyon veya if else bloklarından ulaşabiliyoruz ve program sonlandığında değişken de sonlanıyor.
> 1. Function Scope
> 	+ Fonksiyonların kendi scope'ları mevcuttur. Aynı dosya düzeyinde tanımlan değişkenler gibi.
> 2. Block Scope
> 	+ if-else, while loop ve for loop block scope'dır.
> 	+ *let* ile değişken tanımladığımızda değişken *block scope* alanında etkin olunur. Block scope dışına çıkıldığında değişken yok olur.

### 1.Global Scope:

+ **Global değişken**, programın herhangi bir yerinden **erişilebilen** ve **kapsamı (scope)** sınırlı olmayan bir değişkendir.
+ Bu tür değişkenler, belirli bir fonksiyon ya da blokla sınırlı değildir; programın tamamında kullanılabilir.


> [!CAUTION]
> + Tarayıcıda çalışan bir JavaScript kodunda **tüm global değişkenler, fonksiyonlar ve nesneler** aslında `window` nesnesinin bir özelliği olarak depolanır.
> + Eğer bir değişken veya fonksiyon global olarak tanımlandıysa, ona `window.değişkenAdı` ya da `window.fonksiyonAdı` şeklinde erişebilirsiniz.
> + *var ile oluşturulan değişkenler window scope alanında oluşurlar.* Örneğin; `var distro = linux;` distro değişkeni window scope da oluşur. Eğer `console.log(window)` baktığımızda window nesnesi içerisinde görebiliriz. 
> + window nesinesin kendisi bir global scope'dur.


> [!WARNING]
> `var distro = linux` ile `distro = linux` aynıdır. Varsayılan *var* anahtar kelimesidir. 

#### Global: var key ile
```javascript
var variable_1 = 'javascript'

console.log('variable_1:',variable_1)
console.log('window.variable_1:', window.variable_1)
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
> + `var` ile tanımlanan değişkenler **global alanda tanımlanırsa**, otomatik olarak `window` nesnesinin bir özelliği haline gelir. Bu nedenle `window.variable` erişilebilir olur ve `'javascript'` değerini döner.

#### Global: let key ile
+ `let` ile tanımlanan değişkenler, **block scope**'a sahiptir. Yani sadece tanımlandıkları blok içerisinde geçerlidir ve **global objeye (örneğin, tarayıcı ortamında `window` nesnesine)** eklenmez.

```javascript
let variable = 'javascript'

console.log('variable:', variable)
console.log('window.variable:', window.variable)
```

**Çıktı:**
```console
variable: javascript
windows.variable_1: undefined
```
> **Explanation:**
> + `let` anahtar kelimesi bulunduğu kapsam(scope) alanında geçerlidir. Yani bulunduğu kapsamda ve onun alt kapsamlarında geçerli olacaktır.
> + `let` kullanıldığı için, bu değişken **global objeye (`window`)** eklenmez.
> + **`console.log('variable:', variable);`** Bu, `variable` değişkenini mevcut kapsamdan çağırır. Değişken tanımlı olduğu için `javascript` çıktısını verir.
> + **`console.log('window.variable:', window.variable);`** Burada, global `window` nesnesinin bir özelliği olarak `variable` değişkenini kontrol ediyorsunuz. Ancak `let` ile tanımlandığı için `window` nesnesine eklenmemiştir. Bu yüzden `undefined` döner.

#### Global: const key ile
+ **Sabit değerli (constant)** değişkenler tanımlamak için kullanılır.


> [!WARNING]
> +  `const` ile bir değişken tanımladığınızda, ona hemen bir değer atamanız gerekir. Aksi halde bir **`SyntaxError`** alırsınız.  Örneğin; `const x; // Hata: Missing initializer in const declaration`
> + Bir kez değer atanmışsa, bu değeri sonradan değiştiremezsiniz.


```javascript
const variable = 'javascript'

console.log('variable:',variable)
console.log('window.variable:', window.variable)
```

```console
variable: javascript
window.variable: undefined
```
> **Explanation:**
> + Global anlamda `const` anahtar kelimesi `let` anahtar kelimesi ile aynı şekilde davranır ama `const` ile tanımlanmış değişkenler daha sonrasında değiştirilemez.
#### Global: Automatically Global
+ JavaScript de `automatically global` terimi, bir değişkenin açıkça tanımlanmadan global bir değişken haline gelmesi durumunu ifade eder.
+ Bu, genellikle bir değişkenin `var`, `let` veya `const` anahtar kelimeleri kullanılmadan atanmasıyla gerçekleşir.
+ Böyle bir durumda, değişken otomatik olarak global kapsamda tanımlanır, bu da genellikle istenmeyen bir durumdur.

```javascript
function globalVariable() {
	myVar = "Bu bir global bir değişken oldu!";
}

globalVariable();
console.log(myVar);
```
> **Explanation:**
> + fonksiyon içerisindeki `myVar` adlı değişkeni `var`, `let` ve `const` anahtar kelimeleri ile tekrar deneyiniz.
> + Örneğin; `var myVar = "Bu bir global bir değişken oldu!"`  veya `let myVar = "Bu bir global bir değişken oldu!"` gibi

#### Global: Automatically Global(Strict Mode):

+ JavaScript'in **"strict mode"** (katı mod) kullanımı, bu tür hataların önüne geçer. Strict mode, `var`, `let` veya `const` kullanmadan bir değişken tanımlamayı yasaklar.
+ *Böyle bir durumda bir hata alırsınız.*

```javascript
"use strict";             // <------- 

function globalVariable() {
	myVar = "Bu bir global bir değişken oldu!";     // <-----   
}

globalVariable();
console.log(myVar);
```
> **Explanation:**
> + globalVariable içerisinde tanımlamış olduğumuz `myVar` değişkenini bu şekilde tanımladığımızda hata verecektir.
> + `let myVar`, `var myVar` veya `const myVar` şeklinde tanımlamaya zorlamaktadır.


### 2.Function Scope:
+ JavaScript fonksiyon kapsamına(`scope`) sahiptir. Her fonksiyon yeni bir kapsam(`scope`) yaratır.
+ Bir fonksiyon içerisinde tanımlanan değişkenlere fonksiyon dışından erişilemez (görünmez).
+ `var`, `let` ve `const` ile tanımlanan değişkenler, bir fonksiyon içerisinde tanımlandıklarında oldukça benzerdir.

#### Fonksiyon: var key ile
```javascript
function myFunction() {
	var carName = "Javascript";      // Function Scope
	console.log("Fonksiyon içerisi:", carName);
}

myFunction()
console.log("Fonksiyon Dışı:", carName)
```
> **Explanation:**
> + Fonksiyon içerisinde `var` anahtar ile oluşturulan `carName` adındaki değişken fonksiyon içerisinde geçerli olacaktır. Çünkü her fonksiyon kendi kapsamı(`scope`) oluşturacaktır.

**Çıktısı:**
```console
Fonksiyon içerisi: Javascript
Uncaught ReferenceError: carName is not defined
```

#### Fonksiyon: let key ile
```javascript
function myFunction() {
	let carName = "Javascript";      // Function Scope
	console.log("Fonksiyon içerisi:", carName);
}

myFunction()
console.log("Fonksiyon Dışı:", carName)
```
> **Explanation:**
> + `var` anahtar kelimesi ile aynı şekilde çalışır.

```console
Fonksiyon içerisi: Javascript
Uncaught ReferenceError: carName is not defined
```

#### Fonksiyon: const key ile
```javascript
function myFunction() {
	const carName = "Javascript";      // Function Scope
	console.log("Fonksiyon içerisi:", carName);
}

myFunction()
console.log("Fonksiyon Dışı:", carName)
```
> **Explanation:**
> + `var` anahtar kelimesi ile aynı şekilde çalışır.

**Çıktısı:**
```console
Fonksiyon içerisi: Javascript
Uncaught ReferenceError: carName is not defined
```
### 3.Block Scope:

+ ES6 (2015) öncesinde JavaScript değişkenlerinin yalnızca `Global Scope` ve `Function Scope` vardı.
+ ES6 iki önemli yeni JavaScript anahtar sözcüğünü tanıttı: `let` ve `const`.
+ Bu iki anahtar kelime JavaScript'te `Blok Scope` sağlar.
+ if statement içerisinde `let` ve `const` ile tanımlan değişkenler block Scope olarak geçmektedir.
+ { } bloğu içerisinde tanımlanan değişkenlere bloğun dışından erişilemez:

#### Block: let key ile
```javascript
{
    let x = 3;
}

// x değişkeni burada kullanılamaz.
console.log(x);
```
> **Explanation:**
> + `x` değişkenin geçerlilik süresi `{ ... }` içerisinde olmaktadır.
> + `console.log(x)`  fonksiyonu `Uncaught ReferenceError: x is not defined` şekilde bir hata verecektir.

#### Block: var key ile
```javascript
if (true) {
    var x = 3;
}
// x değişkenini burada kullanabiliriz.

console.log("x :", x);
console.log("window.x :", window.x);
```
> **Explanation:**
> + Bu kez `block scope` düzeyinde `if statement` kullanıyoruz. if block scope içerisinde `var` anahtar kelimesi ile tanımladığımız için `x` değişkeni *global değişken* olmaktadır.
> + `var` anathar kelimesinden dolayı `window` objesin içerisinde görebiliriz.

#### Block: const key ile

```javascript

```

### Özetle:

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

### Dikkat: var - let - const


> [!CAUTION]
> + `var` anahtar ile tanımlamış bir değişkeni tekrar tanımlayabiliriz!


```javascript
var variable = 10;
var variable = 12;
console.log('Variable:', variable);
```

```console
Variable: 12
```


> [!CAUTION]
> + `let` anahtar ile tanımlanmış bir değişkeni tekrardan tanımlayamazsınız!

```javascript
let variable = 10;
let variable = 12;
console.log('Variable:', variable);
```

```console
Uncaught SyntaxError: Identifier 'variable' has already been declared
```



> [!CAUTION]
> + `const` anahtar ile tanımlanmış bir değişkeni tekrardan tanımlayamazsınız!

```javascript
const variable = 10;
const variable = 12;
console.log('Variable:', variable);
```

```console
Uncaught SyntaxError: Identifier 'variable' has already been declared
```

