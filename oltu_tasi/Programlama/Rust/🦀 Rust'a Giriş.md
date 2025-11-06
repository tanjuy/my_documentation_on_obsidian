
# 🦀 Rust Programlama Nedir?



# Yükleme İşlemleri:


> [!TIP]
> **Yükleme Öncesi yapılması gereken işlemler:**
> 1. `curl` yükleme işlemi
> ```shell
> sudo apt install curl  # Debian/Ubuntu
> ```
> ```shell
> sudo dnf install curl  # Fedora/Rocky/Alma Linux
> ```
> ```shell
> sudo pacman -S curl    # Arch/CachyOS
> ```
> 2. Gerekli paketleri kurulumu:
> ```shell
> sudo apt install build-essential  # Ubuntu/Debian
> ```
> ```shell
> sudo dnf groupinstall "Development Tools"  # Fedora/RHEL/Rocky/AlmaLinux
> ```
> ```shell
> sudo pacman -S base-devel  # Arch/CachyOS/Manjaro
> ```
> ```shell
> sudo zypper install -t pattern devel_basis
> ```



+ Rust’ın resmi yükleyicisi **`rustup`** aracılığıyla yapılır. Bu araç, hem Rust derleyicisini (`rustc`) hem de paket yöneticisini (`cargo`) birlikte yükler.

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

+ Kurulum tamamlanınca Rust araçlarının terminalde çalışması için PATH değişkenine eklenir.
+ Ancak mevcut terminal oturumuna bunu eklemek için şunu çalıştır:

```shell
source $HOME/.cargo/env
```

+ Rust ve Cargo’nun yüklendiğini test et:

```shell
rustc --version
cargo --version
```

+ `rustc` ve `cargo` komut çıktıları:

```shell
rustc 1.90.0 (1159e78c4 2025-09-14)
cargo 1.90.0 (840b83a10 2025-07-30
```

# İlk Rust Programı Oluşurma:

+ Yeni bir proje başlat:

```shell
cargo new hello_world
```

+ `cargo` komut çıktısı:

```shell
    Creating binary (application) `hello_world` package
note: see more `Cargo.toml` keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html
```

+ `cargo new` komutu ile oluşan dizin yapısı:

```shell
hello_world
├── Cargo.toml
└── src
    └── main.rs

2 directories, 2 files
```

+ `cargo new` komutu ile tüm oluşan dizin yapısını görmek istersek:

```shell
hello_world
├── Cargo.toml
├── .git
│   ├── config
│   ├── description
│   ├── HEAD
│   ├── hooks
│   │   ├── applypatch-msg.sample
│   │   ├── commit-msg.sample
│   │   ├── fsmonitor-watchman.sample
│   │   ├── post-update.sample
│   │   ├── pre-applypatch.sample
│   │   ├── pre-commit.sample
│   │   ├── pre-merge-commit.sample
│   │   ├── prepare-commit-msg.sample
│   │   ├── pre-push.sample
│   │   ├── pre-rebase.sample
│   │   ├── pre-receive.sample
│   │   ├── push-to-checkout.sample
│   │   ├── sendemail-validate.sample
│   │   └── update.sample
│   ├── info
│   │   └── exclude
│   ├── objects
│   │   ├── info
│   │   └── pack
│   └── refs
│       ├── heads
│       └── tags
├── .gitignore
└── src
    └── main.rs

11 directories, 21 files
```


> [!CAUTION]
> +  Dikkat ederseniz `cargo new` komutu bize ayrıca `git` dizini de oluşturmaktadır.

# Programı Derle ve Çalıştır:

+ `cargo new` komut ile oluşturduğumuz `hello_world` klasörüne giriş yapalım:

```shell
cd hello_world
```

+ Bu dizin içerisindeyken aşağıdaki komut çalıştıralım:

```shell
cargo run
```

**Çıktı:**

```shell
Hello, world!
```



> [!NOTE]
> **(İsteğe bağlı) Manuel derleme:**
> + İstersen doğrudan `rustc` ile de derleyebilirsin:
> 1. Bir `manual_derleme` adında dizin oluşturalım ve dosya içerisinde girelim.
> ```shell
> mkdir manual_derleme; cd manual_derleme
> ```
> 2. `vim` ile dosyamızı açalım
> ```shell
> vim hello.rs
> ```
> 3. `hello.rs` dosyasını içerisi:
> ```shell
> fn main() {
> 	println!("Hello World!");
> }
> ```
> 4. Yazmış olduğumuz `hello.rs` dosyasını derleyelim
> 	- Rust derleyicisi `rustc` kullanılarak bir binary(ikili) dosya oluşturulabilir.
> ```shell
> rustc hello.rs
> ```
> 5. `rustc` çalıştırılabilen bir `hello` `binary(ikili)` dosyası üretecektir.
> ```shell
> ./hello   # Çıktı: Hello World!
> ```


> [!NOTE]
> + `println!` konsola metin yazdıran bir **makro**dur(`macro`).
> + Sonraki derslerde **makro**'un(`macro`) derinlemesine anlatılacaktır.


# Rust'ı güncelleme  ve Kaldırma:

+ Rust'ı güncellemek için aşağıdaki komut:

```shell
rustup update
```

```shell
info: syncing channel updates for 'stable-x86_64-unknown-linux-gnu'
info: checking for self-update

  stable-x86_64-unknown-linux-gnu unchanged - rustc 1.90.0 (1159e78c4 2025-09-14)

info: cleaning up downloads & tmp directories
```

> + Her hangi bir güncelleme gerçekleşmediği için yukarıdaki çıktıda `unchanged` görünmektedir.

+ Rust'ı sisteminizden kaldırmak için aşağıdaki komut uygulayınız:

```shell
rustup self uninstall
```


# Rust Main Fonksiyonu:

## 1. Programın giriş noktasıdır (entry point):

+ Her programın çalışmaya **nereden başlayacağını** bilmesi gerekir.
+ Rust derleyicisi (`rustc`), derleme sırasında “programın nereden başlayacağını” belirlemek için `main` fonksiyonunu **otomatik olarak giriş noktası (entry point)** olarak kabul eder.

> + Yani, program çalıştırıldığında ilk olarak `main()` fonksiyonunun içindeki kod yürütülür.  Bu, C, C++, Java gibi birçok sistem programlama dilinde de böyledir. 

---
## 2. Derleyici tarafından özel olarak tanımlanmıştır:



# Yorum Satırları(Comments):

+ Herhangi bir program yorum gerektirir ve Rust birkaç farklı çeşidi destekler:

## A. Regular Comments:

+ Normal yorumlar, sadece **kod okuyucular için açıklama eklemek** amacıyla kullanılır.
+ Derleyici (`compiler`) bu yorumları tamamen **yok sayar**, yani programın davranışını etkilemez.


> [!NOTE]
> + Rust doc comments Markdown biçimini destekler, yani:
> + `**kalın**`, `*italik*`, `# başlıklar`, `kod blokları` gibi Markdown yazımı kullanılabilir.


+ Rust’ta iki tür “regular comment” vardır:
### A.1. Tek Satırlık Yorum(Line Comment)

+ `//` ile başlar ve satırın sonuna kadar devam eder.

### A.2. Çok satırlı yorum(Block Comment)

+ `/*` ile başlar ve `*/` ile biter.
## B. Doc Comments:

+ Doc comments, **Rust’ın otomatik dokümantasyon sistemi** olan `[rustdoc](https://doc.rust-lang.org/rustdoc/)` tarafından kullanılır.
+ Bu yorumlar, **kütüphane (crate)**, **modül**, **fonksiyon**, **yapı (struct)** gibi öğelere açıklama ekler.

### B.1. Satır içi dokümantasyon yorumları


# İlkel Tipler(Primitives):

+ Rust programlama dilinde **veri tipleri (data types)**, bir değişkenin bellekte ne tür veri tuttuğunu belirler.
+ Rust **statik tipli (statically typed)** bir dildir; yani her değişkenin tipi **derleme zamanında (compile time)** bellidir.
+ Bu tip ya **otomatik olarak çıkarılır (type inference)** ya da **sen belirtirsin**.

## A. Basit (Scalar) Veri Tipleri

### A.1. Tam sayılar (Integer)

| Tür     | Boyut                              | Aralık             |
| ------- | ---------------------------------- | ------------------ |
| `i8`    | 8 bit                              | -128 → 127         |
| `i16`   | 16 bit                             | -32,768 → 32,767   |
| `i32`   | 32 bit                             | -2^31 → 2^31 - 1   |
| `i64`   | 64 bit                             | -2^63 → 2^63 - 1   |
| `i128`  | 128 bit                            | -2^127 → 2^127 - 1 |
| `isize` | Mimariye göre (32-bit veya 64-bit) | —                  |
| `u8`    | 8 bit                              | 0 → 255            |
| `u16`   | 16 bit                             | 0 → 65,535         |
| `u32`   | 32 bit                             | 0 → 4 milyar       |
| `u64`   | 64 bit                             | —                  |
| `u128`  | 128 bit                            | —                  |
| `usize` | Mimariye göre                      | —                  |

```rust
fn main() {
    let x: i32 = -10;
    let variable = 19i8;
}
```

### A.2. Ondalıklı sayılar (Floating-point):

+ Ondalıklı sayılar IEEE-754 standardına uyar.

| Tür   | Boyut  | Hassasiyet                   |
| ----- | ------ | ---------------------------- |
| `f32` | 32 bit | Tek hassasiyet               |
| `f64` | 64 bit | Çift hassasiyet (varsayılan) |
### A.3. Boolean (Mantıksal):

+ Sadece **true** veya **false** değerlerini alır.

```rust
let aktif: bool = true;
```
### A.4. Character (Karakter):

+ Rust’ta karakterler **Unicode** desteklidir, yani sadece ASCII değil:

```rust
let harf: char = 'A';
let kalp = '❤';
let emoji = '😊'
```
## B. Bileşik (Compound) Veri Tipleri

+ Birden fazla değeri bir arada tutan türlerdir.

### B.1. Tuple(Demet):

+ Farklı türden birden fazla değeri bir arada tutar.

```rust
let kisi: (&str, i32, f64) = ("Ali", 30, 72.5);
println!("İsim: {}, Yaş: {}, Kilo: {}", kisi.0, kisi.1, kisi.2);
```

### B.2. Array(Dizi):

+ Aynı türden sabit uzunlukta elemanları saklar.

```rust
let sayilar: [i32; 4] = [10, 20, 30, 40];
let varsyilan = [0; 5];  // [0, 0, 0, 0, 0]  
```


> [!NOTE]
> + Rust’ta değişken tanımlarken tip genelde çıkarılabilir:
> ```rust
> let x = 5;        // i32 olarak algılanır
> let y = 3.14;     // f64 olarak algılanır
> ```
> + Ama istersen **tip belirtmek** mümkündür:
> ```rust
> let z: f32 = 2.5;
> ```

## İpucu:

+ [Rust By Example](https://doc.rust-lang.org/rust-by-example/primitives.html) sayfasında “**Primitives**” (ilkel türler) başlığı altında sadece `i32`, `f64`, `bool`, `char` gibi _scalar_ türler değil, aynı zamanda `tuple` ve `array` gibi **compound types** (bileşik türler) de anlatılıyor.
+ Bu durum ilk bakışta kafa karıştırıcı görünebilir ama aslında Rust’ın **dil tasarımı felsefesiyle** alakalı.

#### 1. “Primitive” terimi Rust’ta “basit” değil, “yerleşik” anlamındadır:

+ Rust’ta “primitive types” dendiğinde, “**dilin çekirdeğinde yer alan, standart kütüphaneye bağlı olmadan çalışan türler**” anlamı kastedilir.
+ Yani bu türler:
	 - Derleyici (compiler) tarafından **doğrudan tanınır**,
	 - Ek bir `use` ifadesine veya crate’e gerek duymaz,
	 - **Temel yapı taşlarıdır (building blocks)**.
+ Dolayısıyla Rust’ta şu türlerin hepsi **primitive** kabul edilir:
	- Scalar types: `i32`, `u8`, `f64`, `bool`, `char`
	- Scalar types: `i32`, `u8`, `f64`, `bool`, `char`

#### 2. Compound types da aslında dil seviyesinde tanımlı:

+ Hem `tuple` hem `array` tipi Rust dilinin **temel (built-in)** parçalarıdır; bunlar `std` kütüphanesi tarafından değil, doğrudan **dilin sözdizimi (syntax)** tarafından sağlanır.
+ Bu yüzden Rust By Example bunları “primitive types” içinde gösterir.

```rust
let t = (1, true, 3.5); // tuple literal
let a = [1, 2, 3, 4];   // array literal
```

+ Bunlar tamamen **derleyici tarafından anlaşılan yapılar**, başka bir modül ya da trait gerektirmiyorlar.
# Değişken Bağlamaları:

+ Rust’ta **“variable bindings”** (değişken bağlamaları), bir **ismi (identifier)** bir **değere (value)** **bağlama** işlemine verilen isimdir.
+ **Yani aslında “değişken tanımlama” dediğimiz şeyin Rust’taki teknik terimidir.**
+ Rust, **statik tip kontrolü** kullanarak **tür güvenliği** sağlar.
	- Yani, her değişkenin tipi **derleme zamanında** (program çalışmadan önce) bellidir.
	- Bu, hataların erkenden fark edilmesini sağlar.
	- Örneğin: `let x: i32 = 10;` (burada `x` bir tamsayıdır, başka bir tür atanamaz).

## A. Immutable (Değiştirilemez):

```rust
fn main() {
    let x = 10;
    println!("x değişkeninin değeri: {}", x);
}
```

```shell
cargo run
```

**Çıktı:**

```shell
   Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.68s
     Running `target/debug/hello_world`
x değişkeninin değeri: 10
```


## B. Mutable(Değiştirilebilir):

+ 

```rust
fn main() {
    let mut x = 5;
    println!("x'in ilk değeri: {}", x);

    x = 10;
    println!("x'in yeni değeri: {}", x);
}
```

```shell
cargo run
```

**Çıktı:**

```shell
   Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.30s
     Running `/home/ottoman/rustDersleri/hello_world/target/debug/hello_world`
x'in ilk değeri: 5
x'in yeni değeri: 10
```

## C. Shadowing(Gölgeleme):

+ Rust’ta **shadowing** (Türkçesiyle “gölgeleme”) kavramı, **aynı isimli bir değişkenin yeni bir değerle yeniden tanımlanması** anlamına gelir.
+ Bu durumda yeni değişken, **önceki değişkeni "gölgeler"** yani artık önceki tanıma erişilemez — ama teknik olarak eski değişken ortadan kalkmaz, sadece yeni tanım onu gizler.

|Özellik|Shadowing (`let x = ...`)|Mutable değişken (`let mut x = ...`)|
|---|---|---|
|Tür değiştirilebilir|✅ Evet|❌ Hayır|
|Aynı isimli yeni binding oluşturur|✅ Evet|❌ Hayır|
|Bellekte yeni yer ayrılır|✅ Evet|❌ Hayır|
|Kullanım amacı|Dönüştürme, geçici yeniden tanımlama|Değer güncelleme|

### Örnek 1:

```rust
fn main() {
    let x = 5;
    println!("x'in ilk değeri: {}", x);

    let x = x + 1; // shadowing
    println!("x'in yeni değeri: {}", x);

    {
        let x = x * 2; // inner scope shadowing
        println!("iç bloktaki x: {}", x);
    }
    println!("Dış bloktaki x: {}", x);
}
```

> 1. `let x = 5;` → `x` isimli bir değişken tanımlanıyor.
> 2. `let x = x + 1;` → Yeni bir `x` oluşturuluyor, önceki `x`’i **gölgeliyor**.
> 3. İç blokta (`{}` içinde) tekrar `let x = x * 2;` diyerek o blokta geçerli **yeni bir x** oluşturuluyor.

+ Her yeni `let` ifadesiyle **yeni bir binding** (bağlantı) oluşur, öncekini değiştirmez — sadece **üzerine yazar gibi görünür.**

**Çıktı:**

```text
   Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.99s
     Running `target/debug/hello_world`
x'in ilk değeri: 5
x'in yeni değeri: 6
iç bloktaki x: 12
Dış bloktaki x: 6
```

### Örnek 2: Tür değiştirme

```rust
fn main() {

    let spaces = "     ";       // string slice
    let spaces = spaces.len();  // integer (yeni değişken)

    println!("spaces: {}", spaces);
}
```

> + Burada `spaces` önce bir **`&str (string slice)`**, sonra bir **u32 (tamsayı)** oluyor.
> + Bunu `mut` ile yapamazdık çünkü tür değişikliğine izin verilmez.

**Çıktı:**

```text
   Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.81s
     Running `target/debug/hello_world`
spaces: 5
```
## İpuçları:

### Kullanılmayan Değişken:

```rust
let variable = 19i8;
```

**Çıktı:**

```shell
   Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
warning: unused variable: `variable`
 --> src/main.rs:4:9
  |
4 |     let variable = 19i8;
  |         ^^^^^^^^ help: if this is intentional, prefix it with an underscore: `_variable`
  |
  = note: `#[warn(unused_variables)]` on by default

warning: `hello_world` (bin "hello_world") generated 1 warning
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.37s
     Running `target/debug/hello_world`
```

> + Bu satırda `y` değişkenini tanımlıyorsun ama sonra programın hiçbir yerinde `variable`’ı **kullanmıyorsun**.
> + Rust, kullanılmayan değişkenleri varsayılan olarak **uyarı** olarak gösterir, çünkü bu genellikle gereksiz veya unutulmuş bir kod parçası anlamına gelir.
> + `^^^^^^^^ help: if this is intentional, prefix it with an underscore: _variable`
> 	- Eğer gerçekten `y`’yi **bilerek** kullanmıyorsan (örneğin geçici bir değişken olarak), Rust’a bunu belirtmek için ismini `_` ile başlatabilirsin:
> + `let _variable = 19i8` 
> 	- Bu durumda uyarı **kaybolur**, çünkü Rust `_` ile başlayan değişkenlerin **bilerek kullanılmadığını** varsayar.

### Tür Bildirimi(type annotation):


# Fonksiyonlar:


# Sahiplik(Ownership) Nedir?

+ Sahiplik, bir Rust programının belleği nasıl yöneteceğini belirleyen bir dizi kuraldır.
+ Tüm programlar çalışırken bilgisayarın belleğini nasıl kullanacaklarını yönetmek zorundadır.


> [!NOTE]
> #### Sahilik Kuralları:
> Öncelikle sahiplik kurallarına(ownership rules) bir göz atalım. Örnekleri incelerken bu kuralları aklınızda bulundurun:
> 1. Her değerin yalnızca **bir sahibi** vardır.
> 2. Sahiplik kapsam(Scope) dışına çıktığında, değer otomatik olarak **drop** edilir (yani bellekten sillinir).
> 3. Sahiplik başka bir değişkene **taşınabilir (move)**, ama aynı anda iki sahip olamaz.

##  A. Taşıma(move):

```rust
fn main() {
    let s1 = String::from("Merhaba");
    let s2 = s1; // s1'in sahipliği s2'ye geçer (move edilir)

    // println!("{}", s1); // ❌ Hata! s1 artık geçerli değil
    println!("{}", s2); // ✅ s2 artık sahibidir
}
```

> + 👉 Burada `String` heap üzerinde bir veri tutar.
> + `s1` → `s2` aktarımı bir **kopyalama (copy)** değil, **taşıma (move)** işlemi olur.
> + Bu nedenle `s1` artık geçersiz hale gelir.

## B. Kopyalama(Copy):

+ Bazı türler (örneğin ilkel türler(Primitive) – integer, bool, char, vb.)
+ **stack üzerinde saklandıkları için taşınmak yerine kopyalanırlar.**

```rust
fn main() {
    let x = 5;
    let y = x; // burada x kopyalanır, çünkü i32 Copy trait'ine sahiptir

    println!("x = {}, y = {}", x, y); // ✅ her ikisi de geçerli
}
```

### Copy Trait nedir?

+ Rust'ta `Copy trait` bir değerin sahipliği taşınmadan (move olmadan) otomatik olarak kopyalanabileceğini belirtir.
+ Yani, bir tür `Copy trait`'ini destekliyorsa, o türün değerleri **taşımak yerine kopyalanır.**

#### Basit Açıklama:

+ Normalde;

```rust
let s1 = String::from("Linux is Awesome");
let s2 = s1;    // move olur
```

> + Burada, `String`, `Copy trait`'ini **desteklemez**.
> + Dolayısıyla `s1` artık geçersiz hale  gelir(move gerçekleşir.)

+ Ama;

```rust
let x = 5;
let y = x;
```

> + Burada `i32` `Copy trait`'ine sahiptir.
> + yani, x'in değeri **yeni bir kopya olarak y'ye kopyalanır,** `x` hala geçerlidir.

#### `Copy Trait`'in Mantığı:

`Copy trait`'in etkin olduğu türler:
+ Stack üzerinden depolanan,
+ Karmaşık heap verisi içermeyen,
+ Küçük, basit türlerdir


> [!NOTE]
> **✅ Copy olabilen tür örnekleri:**
> + Bütün sayılar(`i32`, `u8`, `usize`, vs)
> + Ondalıklı sayılar(`f32`, `f64`)
> + `char`
> + `bool`
> + Bu türlerin sabit uzunluktaki dizileri, örneğin `[i32; 3]`


> [!NOTE]
> **❌ Copy olamayan türler:**
> + `String`, `Vec<T>`, `Box<T>`, `HashMap<K, V>`
> + Heap üzerinde veri tutan veya `Drop trait`'i uygulayan türler.

##### Örnek: Copy vs Move Farkı

```rust
fn main() {
    let a = 10;     // i32 -> Copy trait'i var
    let b = a;      // kopyalanır
    println!("a: {}, b: {}", a, b); // ✅ her ikisi de geçerli

    let s1 = String::from("Rust");
    let s2 = s1;    // move edilir
    // println!("{}", s1); // ❌ hata! s1 artık geçerli değil
    println!("{}", s2);
}
```


| Özellik           | `Copy` Türleri           | `Move` Türleri              |
| ----------------- | ------------------------ | --------------------------- |
| Sahiplik aktarımı | Kopyalanır               | Taşınır                     |
| Heap verisi       | Yok                      | Var                         |
| Geçerli kalma     | Eski değişken geçerlidir | Eski değişken geçersiz olur |
| Örnek             | `i32`, `bool`, `char`    | `String`, `Vec<T>`          |


## C. Borrowing(Ödünç Alma):

+ Bir değeri **taşımadan** (move etmeden) başka bir fonksiyona ya da değişkene **geçici erişim** vermek istiyorsan, **referans (&)** kullanırsın.
+ Bu işleme **borrowing** denir.

```rust
fn main() {
    let s1 = String::from("Selam");
    let len = string_length(&s1); // & ile ödünç(Borrowing) veriyoruz

    println!("'{}' uzunluğu {} karakterdir.", s1, len);
}

fn string_length(s: &String) -> usize {
    s.len() // sadece okuma(readonly) izni var
}
```

> + `&s1` → `s1`’in referansını gönderir, sahipliği devretmez.
> + `string_uzunlugu` fonksiyonu değeri **okuyabilir**, ama **değiştiremez**.

## D. ✏️Mutable Borrowing (Değiştirilebilir Ödünç Alma):

+ Bir değeri **değiştirmek** istiyorsan, `&mut` kullanman gerekir.
+ Ama aynı anda yalnızca bir mutable referans olabilir.

```rust
fn main() {
    let mut s = String::from("Hey");
    ekle(&mut s);

    println!("{}", s);
}

fn ekle(s: &mut String) {
    s.push_str(", nasılsın?");
}

// Kod Çıktısı: Hey, nasılsın?
```

> **Kurallar:**
> 1. Aynı anda **bir tane mutable referans** olabilir.
> 2. Mutable ve immutable referanslar **aynı anda var olamaz**.


> [!CAUTION]
> #### Örnek Hata(Çakışan Borrow):
> ```rust
> fn main() {
>    let mut s = String::from("Selam");
>
>    let r1 = &s;     // immutable Borrowing
>    let r2 = &s;     // immutable Borrowing
>    let r3 = &mut s; // ❌ Hata! immutable referanslar varken mutable olamaz
>
>    println!("{}, {}, {}", r1, r2, r3);
>}
> ```
> **Çıktısı:**
> ```rust
>    Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
> error[E0502]: cannot borrow `s` as mutable because it is also borrowed as immutable
> --> src/main.rs:7:14
>    |
>5  |     let r1 = &s;
>    |              -- immutable borrow occurs here
>6  |     let r2 = &s;
>7  |     let r3 = &mut s;
>    |              ^^^^^^ mutable borrow occurs here
>8  |
>9  |     println!("{} {} {}", r1, r2, r3);
>    |                          -- immutable borrow later used here
>
> For more information about this error, try `rustc --explain E0502`.
> error: could not compile `hello_world` (bin "hello_world") due to 1 previous error
> FAIL
> ```


> [!NOTE]
> #### Ownership ve Bellek Yönetimi:
> Rust, bu kurallar sayesinde;
> 1. Çift serbest bırakma(**double free**) hataları önler.
> 2. Boş referans(**dangling pointer**) hatalarını engeller.
> 3. Veri yarışlarını (**date race**) derleme zamanında yakalar.
# String Tanımlama:

## A. `&str` (string slice):

+ Bu, **değiştirilemez** (immutable) bir **string dilimidir**.
+ Genellikle **sabit metinler (literal)** bu türdedir.

```rust
fn main() {
    let s: &str = "Merhaba Rust!";
    println!("{}", s);
}
```

> + `"Merhaba Rust!"` Programın sabit belleğinde(stack) tutulur.
> + `$str` veriye **referans** eder (yani kendi başına sahip değildir).
> + **Değiştirilemez** → içeriğini değiştiremezsin.

## B. `String` (heap-allocated string):

+ Bu, **sahip olunan (owned)** ve **değiştirilebilir** (mutable) string türüdür.
+ Heap üzerinde tutulur.

```rust

```


# Kontrol Akışı(Control Flow):

## A. If Koşulu(If Expressions):

## B. Dögüler(Repetition with Loops):

+ Bir kod bloğunu birden fazla kez çalıştırmak çoğu zaman faydalıdır.
+ Rust, döngü gövdesinin içindeki kodu sonuna kadar çalıştıracak ve ardından hemen başa dönerek devam edecek birkaç döngü sağlar.
+ Döngülerle denemeler yapmak için `loops` adında yeni bir proje yapalım.

### B.1. Loop ile Kod Tekarı(Repeating Code with loop):


# Tuple(Demet):

+ Rust’ta **tuple (demet)**, birden fazla değeri **tek bir yapıda bir araya getiren** bir veri tipidir.
+ Tuple’lar genellikle **farklı türlerdeki** değerleri birlikte tutmak için kullanılır.
---
+ Bir tuple, farklı tiplerdeki değerlerin bir araya gelmesiyle oluşan bir koleksiyondur.
+ Tuple'lar parantez () kullanılarak oluşturulur ve her tuple'ın kendisi (T1, T2, ...) tür imzasına sahip bir değerdir; burada T1, T2 üyelerinin türleridir.


> [!CAUTION]
> + Bu soru Rust’ın **türü güvenli (`type-safe`)** yapısına dokunuyor çünkü Rust’ta `tuple` üzerinde doğrudan `for` döngüsü **yapılamaz**. Yani, farklı veri tiplerini barındırdığı için `loop` kullanılamaz.
> #### Tuple Üzerinde `for` Döngüsü Neden Olmaz?
> + Rust’ta `for` döngüsü yalnızca **iterable** (yani `IntoIterator` trait’ini uygulayan) veri tipleriyle çalışır:
> + Örneğin; `Vec<T>` (vektör), `array` (`[T; N]`), `range` (`0..10` gibi)
> + Ancak **tuple** (`(a, b, c, ...)`) bu trait’i **uygulamaz**.
> ```rust
> fn main() {
>    let tup = (1, 2, 3);
>
>    for x in tup {  // ❌ hata!
> 	  println!("{}", x);
>    }
>}
> ```
> #### Tür Güvenliği Sayesinde Bellek Hataları Azalır:
> + Bazı dillerde (örneğin C), bir değişkeni yanlış türde kullanırsan **bellek sızıntısı** veya **program çökmesi** olabilir.  Ama Rust buna derleme aşamasında izin vermez.
> ```rust
> let t = (10, 3.14, "Rust");
> ```
> + Bu tuple üzerinde `for` döngüsü yapmak istersen Rust şöyle der:
> 	- "Bu tuple’da farklı türler var, ben bunu teker teker döngüye sokamam."
> + Bu da Rust’ın **type-safe** olmasından kaynaklanır.
> 	- Yani, Rust _ne yaptığını bilmeden_ türleri karıştıramaz.


## Söz dizimi:

+ Bir **tuple**, değerlerin **parantez içinde** ve **virgülle ayrılarak** yazılmasıyla tanımlanır:

```rust
let tuple_name = (value_1, value_2, value_3);
```

## Örnek 1:

```rust
fn main() {
    let kişi = ("Ahmet", 25, 1.75);

    println!("İsim: {}", kişi.0);
    println!("Yaş: {}", kişi.1);
    println!("Boy: {}", kişi.2);
}
```

> + `("Ahmet", 25, 1.75)` bir tuple’dır.
> + `kişi.0`, `kişi.1`, `kişi.2` sırasıyla tuple’ın **0., 1. ve 2.** elemanlarına erişir. (Tuple indeksleri 0’dan başlar.)

## Tür Belirtme:

+ Tuple’ların türleri **içindeki elemanların türlerinden** oluşur:

```rust
fn main() {

    let veri: (i32, f64, &str) = (42, 3.14, "Rust");

    println!("{}", veri.0);
    println!("{}", veri.1);
    println!("{}", veri.2);
}
```



# Struct(Structure):

+ Rust’ta **`struct` (structure)**, kendi veri türünü (custom data type) tanımlamak için kullanılır.
+ Yani, birden fazla veriyi tek bir mantıksal varlık altında toplamanı sağlar -- tıpkı C, C++ veya Go'daki `struct` yada python'daki sınıf(`class`) yapısında benzer şeklinde.

+ `structs`, "`Tuple` Türü" bölümünde tartışılan `tuple`'lara benzer, çünkü her ikisi de birden fazla ilişkili değeri tutar.
+ `Tuple`'lar gibi, bir struct'ın parçaları da farklı tiplerde olabilir.
+ Demetlerden(`Tuple`) farklı olarak, bir struct'da her veri parçasına isim verirsiniz, böylece değerlerin ne anlama geldiği açık olur.

## A. Temel Tanım

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {}
```


> [!NOTE]
> #### `fields`(alanlar) nedir?
> + Rust’ta **`fields` (alanlar)**, bir `struct`’ın **içinde tanımlanan veri parçalarıdır**.
> + Yani bir `struct`’ın “özellikleri” veya “veri bileşenleridir.”
> #### Örnek:
> + Bir `struct` tanımlarken, **alanların (fields)** her biri bir **isim (identifier)** ve bir **tür (type)** içerir.
> ```rust
> struct Person {
> 	name: String,
> 	age: u8,
> 	is_student: bool
> }
> ```
> Burada,
> + `name`, `age` ve `is_student` — **alan adlarıdır (fields)**
> + `String`, `u8` ve `bool` — **alanların türleridir (types)**
> +  Bu alanlar birlikte `Person` yapısını (struct’ını) oluşturur.

---

+ Bir yapıyı(`struct`) tanımladıktan sonra kullanmak için, her alan için somut değerler belirterek o yapının(`struct`) bir örneğini(`instance`) oluştururuz.
+ Yapının(`struct`) adını belirterek bir örnek(`instance`) oluşturuyoruz ve ardından `key:value` çiftlerini süslü parantezler içerisine ekliyoruz; burada anahtarlar(`key`), alanların(`fields`) isimleri ve değerler(`value`), bu alanlarda depolamak istediğimiz verilerdir.
+ Alanları(`fields`) yapıda(`struct`) tanımladığımız sırayla belirtmemize gerek yok.
+ Başka bir deyişle, struct tanımı tür için genel bir şablon gibidir ve örnekler(`instances`), türün veya tipin değerlerini oluşturmak için bu şablonu belirli verilerle doldurur.

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    let user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };
}
```

---

+ Bir yapıdan(`struct`) belirli bir değeri almak için nokta işaretini kullanırız.
+ Örneğin, bu kullanıcının e-posta adresine erişmek için `user1.email` adresini kullanıyoruz.
+ Eğer örnek(`instance`) değiştirilebilir ise, nokta işareti ile değeri değiştirebiliriz ve belirli alan(`field`) içerisine atma yapabiliriz.
+ Aşağıdaki kod, değiştirilebilir bir Kullanıcı örneğinin(`instance`) e-posta alanındaki(`email field`) değerin nasıl değiştirileceğini gösterir.

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    let mut user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };

    user1.email = String::from("anotheremail@example.com");
}
```


> [!CAUTION]
> + Unutma, örneğin tamamının değiştirilebilir (mutable) olması gerekir; Rust yalnızca belirli alanların (field’ların) değiştirilebilir olarak işaretlenmesine izin vermez.
> + Yani, Bir struct’ın sadece belirli alanlarını (fields) `mutable` yapamazsın. Eğer herhangi bir alanını değiştirmek istiyorsan, struct örneğinin tamamı `mutable` olmalıdır.
> ```rust
> let mut user1 = User {
> 	...
> }
> ```
> + Burada `user1` değişkeni `let mut` ile tanımlandığı için **struct'ın tamamı mutabledir.**
> ```rust
> let user1 = User {
>	...
> }
> ```
> + Burada rust `field` üzerinde herhangi değişiklik yapılmasına izin vermeyecektir!

---

+ Her ifadede olduğu gibi, fonksiyon gövdesindeki son ifade olarak yeni bir struct örneği oluşturabiliriz; böylece o örnek, açıkça `return` yazmadan dolaylı (implicit) olarak geri döndürülmüş olur.
+ Yani, Rust dilinde **fonksiyonların son ifadesi**, eğer noktalı virgül (`;`) ile bitmiyorsa, otomatik olarak (implicit) geri döndürülür. Yani `return` yazmak zorunda değilsin.
+ Aşağıda, verilen e-posta(`email`) ve kullanıcı adı(`username`) ile bir `User` örneği döndüren bir `build_user` fonksiyonunu gösterir.
+ `active` alan(field) true değerini alır ve `sign_in_count` ise `1` değerini alır.

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username: username,
        email: email,
        sign_in_count: 1,
    } // ← Bu satır return yazmadan otomatik olarak döner
}

fn main() {
    let user1 = build_user(
        String::from("someone@example.com"),
        String::from("someusername123"),
    );
}
```


> [!CAUTION]
> + `User { ... }` ifadesi fonksiyonun **son satırı**.
> + Bu ifadenin **sonunda noktalı virgül yok!**
> + Bu nedenle Rust, **bunu otomatik olarak fonksiyonun dönüş değeri kabul eder.**
> + Yani, `return User { ... }` yazmana gerek kalmaz.
> + **Peki Noktalı Virgül Olsaydı Ne Olurdu?**
> ```rust
> fn build_user( ... ) -> User {
> 	User {
> 		...
> 	}; // ← Noktalı virgül koyarsan bu artık bir “ifade” değil, bir “statement” olur.
> } // Ve fonksiyon hiçbir şey döndürmez → hata verir! 
> ```
> + Neden? Çünkü artık bu satırın dönüş değeri yoktur, sadece çalışır ve biter.
> + Struct oluşturmak da bir **ifadedir (expression)**.

> + Fonksiyon parametrelerini yapı alanlarıyla(struct field) aynı isimle adlandırmak mantıklıdır, ancak `mail` ve `username` alan(filed) adlarını ve değişkenlerini tekrarlamak biraz sıkıcıdır.
> + Eğer yapı(`struct`) daha fazla alana(field) sahip olsaydı, her ismi tekrarlamak daha da can sıkıcı olurdu.

## B. Field Init Kısaltması:

+ Parametre adları ve yapı alanı(struct field) adları aşağıdaki koda tam olarak aynı olduğundan, build_user'ı yeniden yazmak için `field init shorthand` sözdizimini kullanabiliriz.
+ Aşağıdaki koda gösterildiği gibi, tam olarak aynı şekilde davranır ancak `username` adı ve `email` tekrarı yoktur.

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username,
        email,
        sign_in_count: 1,
    }
}

fn main() {
    let user1 = build_user(
        String::from("someone@example.com"),
        String::from("someusername123"),
    );
}
```

> + Burada, `email` adında bir alana(`fiedl`)sahip olan User yapısının(`User struct`) yeni bir örneğini(`instance`) oluşturuyoruz.
> + `email` alanının(`field`) değerini `build_user` fonksiyonunun `email` parametresindeki değere ayarlamak istiyoruz.
> + `email` alanı(`field`) ve `email` parametresi aynı ada sahip olduğundan `email: email` yerine sadece `email` yazmamız yeterli olacaktır.

## C. `Struct Update` Sözdizimiyle Diğer Örneklerden Örnekler Oluşturma:

+ Aynı tipteki başka bir örneğin(`instance`) değerlerinin çoğunu içeren, ancak bazılarını değiştiren bir yapının(`struct`) yeni bir örneğini(`instance`) oluşturmak genellikle yararlıdır.
+ Bunu `struct update` sözdizimini kullanarak yapabilirsiniz.
+ Öncelikle aşağıdaki `user2`'de `update syntax` olmadan düzenli olarak yeni bir `User` örneğinin(`instance`) nasıl oluşturulacağını gösteriyoruz.
+ `email` için yeni bir değer belirledik ancak bunun dışında aşağıdaki koda oluşturduğumuz `user1`'deki aynı değerleri kullanıyoruz.

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    // --snip--

    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    let user2 = User {
        active: user1.active,
        username: user1.username,
        email: String::from("another@example.com"),
        sign_in_count: user1.sign_in_count,
    };
}
```

> + `struct update syntax` kullanarak, yukarıdaki koda gösterildiği gibi daha az kodla aynı etkiyi elde edebiliriz.
> + `..` sözdizimi, açıkça ayarlanmamış kalan alanların(`fields`), verilen örnekteki(`instance`) alanlarla(`fields`) aynı değere sahip olması gerektiğini belirtir.

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    // --snip--

    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    let user2 = User {
        email: String::from("another@example.com"),
        ..user1  // <<------------------------------ Update Syntax
    };
}
```

> + İlk koda, `user2`'de `email` için farklı bir değere sahip ancak user1'deki `username`, `active` ve `sign_in_count` alanları(`fields`) için aynı değerlere sahip bir örnek(`instance`) oluşturur.

> [!CAUTION]
> + `..user1`, kalan alanların(`fields`) değerlerini user1'deki karşılık gelen alanlardan(`fields`) almasını belirtmek için en sona gelmelidir, ancak yapının(`struct`) tanımındaki alanların(fields) sırasına bakılmaksızın istediğimiz kadar alan için herhangi bir sırada değer belirtmeyi seçebiliriz.

> + `struct update syntax`'in = işaretini atama gibi kullandığını unutmayın; bunun nedeni, ["Move ile Etkileşimde Bulunan Değişkenler ve Veriler"](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#variables-and-data-interacting-with-move) bölümünde gördüğümüz gibi, verileri taşımasıdır.
> + Eğer `user2`'ye hem `email` hem de `username` için yeni `String` değerleri vermiş olsaydık ve böylece sadece `user1`'den gelen `active` ve `sign_in_count` değerlerini kullansaydık, `user2` oluşturulduktan sonra `user1` hala geçerli olurdu.
> + Hem `active` hem de `sign_in_count`, Kopyalama özelliğini(`Copy trait`) uygulayan türlerdir, bu nedenle ["Yığın-Yalnızca Veriler: Kopyalama"](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#stack-only-data-copy) bölümünde tartıştığımız davranış geçerli olacaktır.
> + Bu örnekte `user1.email`'i de kullanabiliriz çünkü değeri `user1`'den dışarı taşınmadı.

## E. Farklı Tipler Oluşturmak İçin `Named Fields` Olmadan `Tuple Structs` Kullanma:

+ Rust ayrıca tuple'lara benzeyen yapıları da destekler, bunlara `tuple yapıları` denir.
+ Tuple struct’lar, alanlarıyla (`field`) ilişkilendirilmiş isimlere sahip değildir; bunun yerine sadece alanların türlerinden (type) oluşurlar. Yine de, struct adı sayesinde ek bir anlam kazandırırlar.
# Packages, Crates ve Modules:

## A. Paketler ve Crates:

+ Modül sisteminin ilk olarak ele alacağımız kısımları `packages`(paketler) ve `crates`'dır. (kasalardır).
+ `Crate`, Rust derleyicisinin bir seferde dikkate aldığı en küçük kod miktarıdır.
+ Cargo yerine rustc çalıştırsanız ve tek bir kaynak kod dosyası geçirseniz bile (Bölüm 1'deki "Rust Programı Yazma ve Çalıştırma"da yaptığımız gibi), derleyici bu dosyayı bir kasa olarak kabul eder.
+ Bir `crate` iki biçimde olabilir: `binary crate` veya `library crate`.
### A.1. Binary crate:



### A.2. Library crate:


### Crate Nedir?

+ **Crate**, Rust’ta **derlenebilir en küçük birimdir**.
+ “Crate”, Rust derleyicisinin **tek seferde derlediği tüm kod birimidir.**  Bu bir **dosya** olabilir (`main.rs`) veya bir **dosyalar kümesi** (modüllerle birlikte).

> [!NOTE]
> Bir crate şunlardan biri olabilir:
> 1. **İkili (binary) crate:** Çalıştırılabilir bir program üretir (örnek: `main.rs` dosyası içeren projeler).
> 2. **Kütüphane (library) crate:** Başka projeler tarafından kullanılabilen bir kütüphane üretir (örnek: `lib.rs` içeren projeler).



```rust


```

## B.  Modüller(Modules):

+ Modüller ve modül sisteminin diğer parçaları hakkında konuşacağız, özellikle de öğelere(items) isim vermenizi sağlayan yollar(paths); kapsama(scope) bir yol getiren `use` anahtar sözcüğü; ve öğeleri(items) herkese açık hale getiren `pub` anahtar sözcüğü.
+ Ayrıca as anahtar sözcüğünü, harici paketleri ve glob operatörünü de ele alacağız.

## Kaynak:

+ [READ THE BOOK!](https://doc.rust-lang.org/book/ch05-01-defining-structs.html)