
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


> [!NOTE]
> ```shell
> cargo new hello-world --vcs none
> ```
> + 🧰 `--vcs none`:
> 	- **VCS (Version Control System)** → sürüm kontrol sistemi (örneğin Git).
> 	- Normalde `cargo new` çalıştırıldığında **otomatik olarak bir Git deposu (`git init`) oluşturur**.
> 	- Ama `--vcs none` dersen, **Git deposu oluşturulmaz** (yani `.git` klasörü eklenmez).
> #### Örnek Fark:
> + **Varsayılan(`cargo new hello-world`)**
> ```shell
> hello-world/
> ├── .git/                ← otomatik oluşturulur
> ├── .gitignore           ← otomatik eklenir
> ├── Cargo.toml
> └── src/
>     └── main.rs
> ```
> + **`--vcs` parametresi(`cargo new hello-world --vcs none`)**
> ```shell
> hello-world/
> ├── Cargo.toml
> └── src/
>     └── main.rs
> ```

+ **`--vcs` Parametresi Seçenekleri:**

| Seçenek        | Açıklama                                                                           |
| -------------- | ---------------------------------------------------------------------------------- |
| `--vcs git`    | Git deposu oluşturur (`.git` klasörü, `.gitignore` dosyası). Bu **varsayılandır.** |
| `--vcs hg`     | **Mercurial (hg)** deposu oluşturur (`.hg` klasörü, `.hgignore` dosyası).          |
| `--vcs pijul`  | **Pijul** adlı daha yeni bir sürüm kontrol sistemiyle başlatır.                    |
| `--vcs fossil` | **Fossil SCM** adlı sistemi kullanır (`.fossil-settings` klasörü ekler).           |
| `--vcs none`   | Hiçbir sürüm kontrol sistemi oluşturmaz (sadece kaynak dosyaları).                 |

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


# 5. İlişkili Verileri Düzenlemek için Struct’ları Kullanmak:


## 5.1. Struct’ları Tanımlama ve Örneklerini (Nesnelerini) Oluşturma:

+ Rust’ta **`struct` (structure)**, kendi veri türünü (custom data type) tanımlamak için kullanılır.
+ Yani, birden fazla veriyi tek bir mantıksal varlık altında toplamanı sağlar -- tıpkı C, C++ veya Go'daki `struct` yada python'daki sınıf(`class`) yapısında benzer şeklinde.

+ `structs`, "`Tuple` Türü" bölümünde tartışılan `tuple`'lara benzer, çünkü her ikisi de birden fazla ilişkili değeri tutar.
+ `Tuple`'lar gibi, bir struct'ın parçaları da farklı tiplerde olabilir.
+ Demetlerden(`Tuple`) farklı olarak, bir struct'da her veri parçasına isim verirsiniz, böylece değerlerin ne anlama geldiği açık olur.

### A. Temel Tanım

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

### B. Field Init Kısaltması:

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

### C. `Struct Update` Sözdizimiyle Diğer Örneklerden Örnekler Oluşturma:

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

### D. Farklı Tipler Oluşturmak İçin `Named Fields` Olmadan `Tuple Structs` Kullanma:

+ Rust ayrıca tuple'lara benzeyen yapıları da destekler, bunlara `tuple yapıları` denir.
+ `Tuple struct`’lar, alanlarıyla (`field`) ilişkilendirilmiş isimlere sahip değildir; bunun yerine sadece alanların türlerinden (type) oluşurlar. Yine de, struct adı sayesinde ek bir anlam kazandırırlar.
+ `Tuple struct`’ları, tüm `tuple`'a bir isim vermek ve tuple'ı diğer tuple'lardan farklı bir tipte(`type`) yapmak istediğinizde ve her alanı(`field`) normal bir yapıda(`struct`) olduğu gibi adlandırmanın ayrıntılı veya gereksiz olacağı durumlarda kullanışlıdır.
+ Bir `tuple struct `tanımlamak için, `struct` anahtar kelimesiyle başlayıp `struct` adını ve ardından `tuple` içindeki türleri yazarsınız. 
+ Örneğin, burada `Color` ve `Point` adında iki tuple struct tanımlayıp kullanıyoruz:

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```


> [!CAUTION]
> + `black` ve `origin` değerlerinin farklı türler(`types`) olduğunu unutmayın çünkü bunlar farklı `tuple struct`'larının örnekleridir(`instance`).
> + Tanımladığınız her `struct`, `struct` içindeki alanlar(`field`) aynı tipte(`type`) olsa bile, kendi tipine(`type`) sahiptir.
> + Örneğin, `Color` türünde(`Color type`) bir parametre alan bir fonksiyon, her iki tür de üç `i32` değerinden oluşmasına rağmen, bir `Point`'i argüman olarak alamaz.
> + Bunun dışında, tuple struct örnekleri (instance’ları), tıpkı tuple’larda olduğu gibi parçalara ayrılarak (destructure edilerek) tek tek bileşenlerine ayrılabilir ve ayrıca belirli bir değere erişmek için nokta (`.`) operatöründen sonra indeks kullanabilirsiniz.
> ```rust
> // Tuple struct tanımları
> struct Color(i32, i32, i32);
> struct Point(f32, f32, f32);
>
> fn main() {
>    let red = Color(255, 0, 0);
>    let point = Point(3.5, 7.2, 1.0);
>
>    // .indeks ile erişim
>    println!("Red color: {}, {}, {}", red.0, red.1, red.2);
>    println!("Point x: {}", point.0);
>
>    // Destructuring (parçalama)
>    let Color(r, g, b) = red;
>    println!("Destructured color: {}, {}, {}", r, g, b);
>}
> ```
> + **Kodu Açıklaması:**
> 	- `Color` ve `Point` isimlerinde `tuple struct`'lar tanımlandı.
> 	- `field` adları yok; sadece türleri var.
> 	- `.0`, `.1`, `.2` şeklinde indeks numarasıyla erişim yapılabilir.
> 	- `let Color(r, g, b) = red;` kısmında olduğu gibi **destructure edilerek** parçalara ayrılabilir.


> [!CAUTION]
> + Demetlerin(`tuple`) aksine, demet yapıları(`tuple struct`), yapıyı parçalara ayırırken(`destucture`) yapının türünü belirtmenizi gerektirir.
> + Örneğin, `origin` içindeki değerleri `x`, `y` ve `z` adlı değişkenlere ayırmak için `let Point(x, y, z) = origin;` şeklinde yazmalıyız.
> ```rust
> // Tuple struct tanımı
> struct Point(i32, i32, i32);
> 
> fn main() {
>    let origin = Point(10, 20, 30);
>
>    // Destructuring yapılırken struct adı belirtilmeli
>    let Point(x, y, z) = origin;
>
>    println!("x: {}, y: {}, z: {}", x, y, z);
> }
> ```
> + **Tuple Stuct vs Tuple**
> + Normal tuple'da şöyle yazabiliriz:
> ```rust
> let (a, b, c) = (1, 2, 3);
> ```
> + Ama tuple struct'ta tür ismi belirtmenden olmaz:
> ```rust
> let Point(x, y, z) = origin; // ✅ Doğru
> // let (x, y, z) = origin;   // ❌ Hatalı
> ```

### E. Herhangi Bir Alanı Olmayan Birim Benzeri Yapılar(Unit-Like Structs):

+ Ayrıca hiçbir alanı(`field`) olmayan yapıları(`struct`) da tanımlayabilirsiniz!
+ Bunlara `unit-like struct` denir çünkü ["Tuple Türü"](https://doc.rust-lang.org/book/ch03-02-data-types.html#the-tuple-type) bölümünde bahsettiğimiz `unit type` olan `()`'ne benzer şekilde davranırlar.
+ Unit benzeri (unit-like) struct’lar, bir tür üzerinde `trait` (özellik) uygulamak istediğinizde ancak bu türün içinde herhangi bir veri saklamanıza gerek olmadığında faydalı olabilir. Yani, Unit-like struct’lar, içinde veri tutmanıza gerek olmayan ama yine de bir `trait`’i uygulamak istediğiniz durumlarda işe yarar.
+ `trait`'leri 10. Bölümde ele alacağız.
+ `AlwaysEqual` adında bir birim yapısının(`unit struct`) bildirilmesi ve örneklendirilmesine(`declaring and instantiating`) dair bir örnek aşağıda verilmiştir:

```rust
struct AlwaysEqual;  // declaring - bildirilmesi

fn main() {
    let subject = AlwaysEqual; // instantiating - örneklenmesi
}
```

> + `AlwaysEqual`'ı tanımlamak için `struct` anahtar kelimesini, istediğimiz ismi(`AlwaysEqual`) ve ardından noktalı virgülü(`;`) kullanırız.
> + Süslü parantezlere veya ayraçlara gerek yok!
> + `AlwaysEqual` türünden bir örneği (`instance`), `subject` değişkenine benzer şekilde atayabiliriz: Tanımladığımız ismi kullanarak, süslü parantez `{}` veya normal parantez `()` olmadan. Yani, `AlwaysEqual` yapısından bir örnek oluşturmak için sadece ismini yazmamız yeterlidir; süslü veya normal parantez kullanmamıza gerek yoktur.
> + Daha sonra bu tür (type) için bir davranış (behavior) uygulayacağımızı hayal edin; öyle ki, `AlwaysEqual` türünün her örneği, başka herhangi bir türün her örneğiyle her zaman eşit olsun — belki de test amaçlı olarak bilinen bir sonuç elde etmek için. Yani, İleride bu tür için, `AlwaysEqual`’ın her örneğinin diğer tüm türlerin örnekleriyle her zaman eşit olacağı bir davranış tanımlayacağımızı düşünün; örneğin testlerde tahmin edilebilir bir sonuç elde etmek için.
> + Bu davranışı uygulamak için hiçbir veriye ihtiyacımız olmayacaktı!
> + 10. bölümde, `unit-like-struct`lar da dahil olmak üzere bu türlere nasıl **`trait`’ler (özellikler)** tanımlayacağınızı ve onları nasıl **uygulayacağınızı (`implement`)** öğreneceksiniz.

#### E.1. Struct Data'ların Sahipliği:
+ Liste 5-1'deki `User` struct tanımında `&str string` dilim türü yerine `owned String` türünü kullandık.
+ Bu bilinçli bir tercihtir çünkü bu `struct`’ın her örneğinin (`instance`’ının) sahip olduğu tüm verilerin mülkiyetine (`ownership`) sahip olmasını ve bu verilerin, `struct` geçerli olduğu sürece geçerli kalmasını istiyoruz.


> [!NOTE]
> #### Ne Anlatılmak İsteniyor:
> Rust’ta **`String`** ve **`&str`** arasında önemli bir fark vardır:
> + `String` → verinin sahibi olan(`owned`) bir string türüdür.
> + `&str` → **başka bir yere ait veriye referans eden (borrowed) bir string dilimidir.**
> ```rust
> struct User {
>    active: bool,
>    username: String,
>    email: String,
>    sign_in_count: u64,
>}
> ```
> + Burada `username` ve `email` alanları **`String`** türünde.
> 	- ➡️ `User` nesnesi oluşturulduğunda, `username` ve `email` verilerinin **sahibi (owner)** `User`’dır.
> 	- ➡️ Yani, `User` bellekte durduğu sürece bu string verileri de geçerli olur.
> 	- ➡️ `User` silinince (`drop` edilince) bu veriler otomatik olarak silinir.
> + Eğer `&str` kullansaydık:
> ```rust
> struct User {
>    username: &str,   // ❌
>    email: &str,      // ❌
>}
> ```
> + bu durumda `User` sadece **başka bir yere ait string’lere referans verirdi.**
> + Yani `User` var olsa bile, o referans ettiği string’ler silinirse program hata verir. (`dangling reference`).
> + Bu da Rust’ın **ownership** ve **lifetime** kurallarına uymadığı için derlenmez.
> #### Özet:
> + `User` struct’ında `String` kullandık çünkü her kullanıcı kendi verilerinin sahibi olmalı.  
> + Böylece o veriler, kullanıcı nesnesi (struct) var olduğu sürece güvenli bir şekilde bellekte kalır.

+ Struct’ların, başka bir şeye ait olan verilere referans (gönderme) yapacak şekilde veri tutması da mümkündür; ancak bunu yapabilmek için, Rust’ın 10. bölümde ele alacağımız _lifetime_ (ömür) özelliğini kullanmak gerekir.
+ Lifetimes, bir struct’ın referans verdiği verilerin, struct geçerli olduğu sürece geçerli kalmasını garanti eder.
+ Diyelim ki, bir struct içinde yaşam sürelerini (lifetimes) belirtmeden bir referans depolamaya çalışıyorsunuz; aşağıdaki örnekte olduğu gibi. Bu işe yaramaz.

**Dosya adı: `src/main.rs`**

```rust
struct User {
    active: bool,
    username: &str,
    email: &str,
    sign_in_count: u64,
}

fn main() {
    let user1 = User {
        active: true,
        username: "someusername123",
        email: "someone@example.com",
        sign_in_count: 1,
    };
}
```

+ Derleyici, yaşam süresi belirteçlerine (`lifetime specifiers`) ihtiyaç duyduğunu belirterek hata verecektir.
+ Yani, bu struct bir **referans** tutuyor ama ben bu referansın **ne kadar süre geçerli olacağını** bilmiyorum.  Lütfen bana bir **lifetime (örneğin `'a`)** belirt.
+ Bu uyarı, Rust’ın **bellek güvenliği** mekanizmasının bir parçasıdır.
+ Derleyici lifetime olmadan referansın **geçerliliğini garanti edemez**, o yüzden kodu derlemez.

```rust
$ cargo run
   Compiling structs v0.1.0 (file:///projects/structs)
error[E0106]: missing lifetime specifier
 --> src/main.rs:3:15
  |
3 |     username: &str,
  |               ^ expected named lifetime parameter
  |
help: consider introducing a named lifetime parameter
  |
1 ~ struct User<'a> {
2 |     active: bool,
3 ~     username: &'a str,
  |

error[E0106]: missing lifetime specifier
 --> src/main.rs:4:12
  |
4 |     email: &str,
  |            ^ expected named lifetime parameter
  |
help: consider introducing a named lifetime parameter
  |
1 ~ struct User<'a> {
2 |     active: bool,
3 |     username: &str,
4 ~     email: &'a str,
  |

For more information about this error, try `rustc --explain E0106`.
error: could not compile `structs` (bin "structs") due to 2 previous errors
```

> + 10. bölümde, bu hataları nasıl düzelteceğimizi ve struct’lar içinde referansların nasıl saklanabileceğini tartışacağız. Ancak şimdilik, bu tür hataları düzeltmek için `&str` gibi referanslar yerine `String` gibi sahip olunan (owned) türleri kullanacağız.
> + Yani şunu söylüyor:
> 	- Şimdilik `&str` (referans) kullanmaya çalışmak yerine, doğrudan `String` (sahip olunan veri) kullan.
> 	- Çünkü `String` veriyi **kendisi sahiplenir** ve **lifetime belirtmeye gerek kalmaz**.
> 	- İleride (10. bölümde) Rust’ta **lifetime** konusunu öğrenince, struct içinde `&str` gibi referansları güvenli şekilde kullanmayı da öğreneceksin.

> [!NOTE]
> #### Ne Anlatılmak İsteniyor?
> + Burada Rust'ın **lifetime**(ömür) kavramına giriş yapılyor.
> + Yani, bir struct’ın içindeki veriler **kendisinin sahibi değilse** (örneğin sadece bir `&str` referansı tutuyorsa), Rust bu referansın **geçerlilik süresini (lifetime)** takip eder.
> + Amaç şudur👇:
> 	- Struct geçerli olduğu sürece, o struct’ın referans verdiği veriler de geçerli olmalı.
> 	- Eğer veri önce silinirse, struct “boş referans” (dangling reference) tutmuş olur — Rust bunu engeller.
> #### 📘 Basit Örnek (ilerideki konudan fikir vermesi için):
> ```rust
> struct User<'a> {
>    username: &'a str, // referans (borrowed data)
>}
>
>fn main() {
>    let name = String::from("Tanju");
>    let user = User { username: &name };
>    println!("{}", user.username);
>}
> ```
> + Burada `'a` lifetime parametresi sayesinde Rust şunu anlar:
> 	- `user` yapısı, `name` değişkeni geçerli olduğu sürece geçerlidir.
> + Yani `user`'ın ömrü, `name`'in ömründen uzun olamaz.
> + Bu da bellek güvenliğini sağlar. ✅


> [!NOTE] Title
> #### `String` vs `&str` farkıyla:
> #####  1. `String` kullanan struct (verinin sahibi)
> ```rust
> struct User {
 >   username: String, // User bu verinin sahibi
>}
>
>fn main() {
>    let name = String::from("Tanju");
>    let user = User { username: name }; // sahiplik transfer edilir
>
>    // println!("{}", name); ❌ artık name geçersiz (move oldu)
>    println!("{}", user.username); // ✅ user verinin sahibi, kullanabilir
>} // burada user scope dışına çıkar ve String otomatik olarak silinir
> ```
> + `User` struct’ı `username` verisinin **sahibidir (owner)**.
> + `name` değişkeni artık verinin sahibi değildir (ownership `user`’a geçti).
> + `user` silindiğinde `String` verisi de bellekte otomatik temizlenir.
> + Bu yüzden **`lifetime`** belirtmeye gerek yoktur.
> ```rust
> struct User<'a> {
>    username: &'a str, // Bu struct veriyi sadece ödünç alıyor (borrow)
>}
>
>fn main() {
>    let name = String::from("Tanju");
>    let user = User { username: &name }; // name'den ödünç alındı
>
>    println!("{}", user.username);
>} // name ve user aynı anda scope dışına çıktığı için sorun yok
> ```
> + `User` struct'ı verinin sahibi değildir, sadece referansını (`&str`)  tutar.
> + Bu nedenle Rust, `User`’ın ömrü (`'a`) ile `name`’in ömrünü **eşleştirmemizi ister**.  (`'a` lifetime parametresi bunu yapar.)
> + Böylece Rust, `user` geçerli olduğu sürece `name`’in de geçerli olmasını **garanti eder**.
> #### Sonuç:
> + Eğer struct içindeki veri **struct’a ait olacaksa** → `String` kullan.
> + Eğer veri **başka bir yerde tanımlanmışsa ve sadece referans tutmak istiyorsan** → `&str` kullan, ama **lifetime belirtmeyi unutma**.

| Özellik              | `String`                      | `&str`                        |
| -------------------- | ----------------------------- | ----------------------------- |
| Sahiplik (Ownership) | Struct sahip olur             | Struct sadece referans tutar  |
| Bellek yönetimi      | Struct silinince veri silinir | Veri başka yerde tutulur      |
| Lifetime gerekliği   | Gerekmez                      | Gerekir (`'a` ile belirtilir) |
| Bellek güvenliği     | Rust otomatik halleder        | Rust lifetime ile denetler    |

## 5.2. Struct’ları Kullanan Örnek Bir Program:

+ Struct’ları ne zaman kullanmak isteyebileceğimizi anlamak için, bir dikdörtgenin alanını hesaplayan bir program yazalım.
+ Önce tek değişkenler kullanarak başlayacağız, ardından programı **struct** kullanacak şekilde yeniden düzenleyeceğiz (refactor edeceğiz).
	- Başlangıçta **her değeri ayrı değişkenlerde** tutacağız.
	- Sonrasında, bu ilişkili verileri **struct içine toplayarak daha düzenli ve anlamlı** bir hale getireceğiz.
+ Cargo ile piksel cinsinden belirtilen bir dikdörtgenin genişliğini ve yüksekliğini alacak ve dikdörtgenin alanını hesaplayacak **rectangles** adında yeni bir ikili (binary) proje oluşturalım.
	- **Binary project** → Çalıştırılabilir bir program (komut satırından çalıştırabileceğimiz).
	- **Cargo** → Rust’ın proje yönetim ve derleme aracı.
	- Proje adı: **rectangles**
	- Amaç: Genişlik ve yükseklik değerlerini alıp alanı hesaplamak.
+ Liste 5-8, projemizin `src/main.rs` dosyasında tam olarak bunu yapmanın bir yolunu gösteren kısa bir program göstermektedir.

**Dosya adı: `src/main.rs`**

```rust
fn main() {
    let width1 = 30;
    let height1 = 50;

    println!(
        "The area of the rectangle is {} square pixels.",
        area(width1, height1)
    );
}

fn area(width: u32, height: u32) -> u32 {
    width * height
}
```

**Çıktı:**

```bash
The area of the rectangle is 1500 square pixels.
```

> + liste 5-8: Ayrı genişlik ve yükseklik değişkenleriyle belirtilen bir dikdörtgenin alanının hesaplanması

+ Şimdi bu programı `cargo run` kullanarak çalıştıralım:

```shell
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.42s
     Running `target/debug/rectangles`
The area of the rectangle is 1500 square pixels.
```

> + Bu kod, her bir boyutu (genişlik ve yükseklik) ile `area` fonksiyonuna göndererek dikdörtgenin alanını hesaplamayı başarıyor, ancak bu kodu daha **açık** ve **okunabilir** hale getirmek için daha fazlasını yapabiliriz.

+ Bu koddaki sorun, `area` fonksiyonunun imzasında (tanım satırında) açıkça görülmektedir.

```rust
fn main() {
    let width1 = 30;
    let height1 = 50;

    println!(
        "The area of the rectangle is {} square pixels.",
        area(width1, height1)
    );
}

fn area(width: u32, height: u32) -> u32 {
    width * height
}
```

> + `area` fonksiyonu, **bir** dikdörtgenin alanını hesaplamak için tasarlanmıştır; ancak yazdığımız fonksiyonun **iki parametresi** vardır ve bu parametrelerin **birbirleriyle ilişkili** olduğu programımızın hiçbir yerinde açıkça belli değildir.
> + Genişlik (**width**) ve yükseklik (**height**) değerlerini **bir arada gruplamak**, kodu hem **daha okunabilir** hem de **daha kolay yönetilebilir** hale getirecektir.
> + Bunu yapmanın bir yolunu aslında 3. bölümdeki **"[Tuple Türü](https://doc.rust-lang.org/book/ch03-02-data-types.html#the-tuple-type)"** başlığı altında konuşmuştuk:  bunu **tuple’lar** kullanarak yapabiliriz.

### 5.2.1. Tuple’lar ile Yeniden Düzenleme (Refactoring):

+ `Liste 5-9`, **tuple’ları kullanan** programımızın başka bir versiyonunu göstermektedir.

**Dosya Adı: `src/main.rs`**

```rust
fn main() {
    let rect1 = (30, 50);

    println!(
        "The area of the rectangle is {} square pixels.",
        area(rect1)
    );
}

fn area(dimensions: (u32, u32)) -> u32 {
    dimensions.0 * dimensions.1
}
```

> + `Liste 5-9`: Dikdörtgenin genişliğini ve yüksekliğini bir tuple ile belirtme

**Çıktı:**

```bash
The area of the rectangle is 1500 square pixels.
```


> + Bir bakıma, bu program daha iyidir. Tuple’lar bize biraz yapı kazandırır ve artık sadece **tek bir argüman** geçiriyoruz.
> + Ancak diğer yandan, bu versiyon daha az açıktır: Tuple’lar öğelerine isim vermez, bu yüzden tuple’ın bölümlerine **indeks** ile erişmemiz gerekir ve bu da hesaplamayı **daha az anlaşılır** hale getirir.
> 	- Yani `(width, height)` gibi bir tuple kullanıldığında, `width` ve `height` isimleriyle değil, **sıra numaralarıyla** (`rect.0`, `rect.1`) erişilir.
> + Genişlik ve yüksekliği karıştırmak, alan hesabı için önemli olmayabilir; ancak dikdörtgeni ekranda **çizmek istersek**, bu durum önemli hale gelir!
> 	- Yani Tuple kullanıldığında `rect.0` ve `rect.1` gibi isimler belirsizdir; hangisi genişlik, hangisi yükseklik karışabilir.
> 	- Alan hesabında (`width * height`) fark etmez ama **grafiksel çizimde** (örneğin koordinat belirlerken) **doğru alanın ne olduğunu bilmek gerekir**.
> + Genişliğin 0 dizini, yüksekliğin ise 1 dizini olduğunu aklımızda tutmalıyız.
> + Başka birinin bizim kodumuzu kullanması durumunda bunu anlaması ve aklında tutması daha da zor olacaktır.
> + Verilerimizin anlamını kodumuzda aktarmadığımız için artık hata yapmak daha kolay.

### 5.2.2. Yapılarla (Struct’larla) Yeniden Düzenleme: Daha Fazla Anlam Katmak:

+ Verileri etiketleyerek anlama kazandırmak için `struct` kullanıyoruz.
+ Kullandığımız tuple’ı, tamamı için bir isim ve bölümleri için de isimler içeren bir struct’a dönüştürebiliriz; bu, 5-10 numaralı listede gösterilmiştir.
	- Yani burada deniyor ki: elimizdeki tuple’ı daha anlamlı hale getirmek için, hem tüm yapıya bir isim (örneğin `Rectangle`) hem de içindeki parçalara (örneğin `width`, `height`) isimler verebiliriz.

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        area(&rect1)
    );
}

fn area(rectangle: &Rectangle) -> u32 {
    rectangle.width * rectangle.height
}
```

> + `Liste 5-10`: Bir `Rectangle` struct tanımlanması

**Çıktı:**

```shell
The area of the rectangle is 1500 square pixels.
```

> + Burada bir **struct** tanımladık ve ona `Rectangle` adını verdik. Küme parantezleri içinde, alanları `width` ve `height` olarak tanımladık; her ikisinin de türü `u32`.
> + Sonra, `main` içinde genişliği 30 ve yüksekliği 50 olan özel bir `Rectangle` örneği (instance) oluşturduk.
> + Artık `area` fonksiyonumuz **bir parametre** ile tanımlandı; bu parametreye `rectangle` adını verdik ve türü, bir `Rectangle` struct örneğinin **değiştirilemez (immutable) referansı**dir. ⚠️
> + 4. bölümde de bahsedildiği gibi, struct’ın sahipliğini almak yerine **ödünç almak (borrow)** istiyoruz.
> + Böylece `main` fonksiyonu sahipliğini korur ve `rect1`’i kullanmaya devam edebilir. İşte bu yüzden fonksiyon imzasında ve fonksiyonu çağırdığımız yerde `&` kullanıyoruz.
> 	- Burada anlatılmak istenen;
> 		- `rectangle: &Rectangle` → **Rectangle örneğine referans (borrow)** alır, sahipliğini almaz.
> 		- `&rect1` → `rect1`’in adresini gönderir, böylece fonksiyon sadece **okuma izni** kazanır.
> 	- Bu sayede:
> 		- `main` hala `rect1`'i kullanabilir.
> 		- Rust'ın **ownership ve borrowing kuralları** korunmuş olur.
> + `area` fonksiyonu, `Rectangle` örneğinin `width` ve `height` alanlarına erişir (dikkat edin, ödünç alınmış bir struct örneğinin alanlarına erişmek **alan değerlerini taşımaz (move etmez)**; bu yüzden struct’ların sıklıkla ödünç alındığını görürsünüz).
> 	- `rectangle.width` ve `rectangle.height` → alanlara **sadece erişiyoruz**, sahipliği(`ownership`) almıyoruz.
> 	- Bu, Rust’ta **borrow (ödünç alma) ile veri güvenliği** sağlamak için önemlidir.
> 	- Eğer struct yerine alanları doğrudan fonksiyona gönderseydik, değerler **move** olur ve orijinal değişken artık kullanılamazdı.
> + Artık `area` fonksiyonumuzun imzası tam olarak demek istediğimizi ifade ediyor: `Rectangle`’ın alanını, onun `width` ve `height` alanlarını kullanarak hesapla.
> 	- Fonksiyonun imzası (`fn area(rectangle: &Rectangle) -> u32`) açıkça şunu söylüyor:
> 	- Bir `Rectangle` al (ödünç olarak) ve onun alanını hesapla.
> + Bu, genişlik (`width`) ve yüksekliğin (`height`) birbiriyle ilişkili olduğunu ifade eder ve 0 ile 1 gibi tuple indeksleri kullanmak yerine değerlere açıklayıcı isimler verir. Bu da kodun **anlaşılırlığı açısından bir kazançtır.**
> 	- Struct kullanmak, tuple’a göre daha okunaklıdır çünkü:
> 		- `rectangle.width` demek `tuple.0` demekten daha anlamlıdır.
> 		- Böylece kodun **ne yaptığını anlamak** kolaylaşır, hata yapma olasılığı da azalır.

#### HATIRLATMA:

###### 1. `&rect1` nedir?

+ `&rect1` ifadesi, **`rect1` değişkenine ait verinin kendisini değil, ona bir “referans”ı (yani adresini)** gönderir.
+ Yani, `rect1` değişkeninin sahipliğini (`ownership`) **başka bir fonksiyona devretmeden**, sadece **ona erişim izni** verir.
+ ➡️ Rust’ta bu, **borrowing (ödünç alma)** olarak bilinir.
+ Bu sayede:
	- `area` fonksiyonu `rect1`’in değerini kullanabilir,
	- ama `rect1`’in sahipliği (`ownership`) `main` fonksiyonunda kalır,
	- dolayısıyla `rect1`’i sonradan tekrar kullanabilirsin (Rust bunu güvenli kılar).
###### 2. `&Rectangle` nedir?

+ `&Rectangle`, fonksiyonun parametre türüdür.
+ Yani `area` fonksiyonu, **Rectangle yapısına ait bir referans** (adres) bekler.

```rust
fn area(rectangle: &Rectangle) -> u32
```

> + Bu şu anlama gelir:
> 	- Bu fonksiyon, bir `Rectangle`’a ait **referansı** alır ama onun sahipliğini almaz.

###### 3. Neden referans kullanılıyor?

+ Rust’ta eğer biz fonksiyona doğrudan `rect1` gönderseydik (yani `area(rect1)` deseydik), `area` fonksiyonu **rect1’in sahipliğini alırdı**, ve `main` fonksiyonu artık `rect1`’i kullanamazdı.
+ Ama biz sadece **değerini okumak** istiyoruz, değiştirmek değil.
+ Bu nedenle referans (`&`) kullanarak hem güvenli hem verimli bir şekilde erişim sağlıyoruz.

| İfade        | Anlamı            | Açıklama                                            |
| ------------ | ----------------- | --------------------------------------------------- |
| `rect1`      | Değerin kendisi   | `Rectangle` yapısının bir örneği                    |
| `&rect1`     | Değerin referansı | `rect1`’in adresini (referansını) gönderir          |
| `&Rectangle` | Parametre tipi    | Bir `Rectangle` referansı kabul eden fonksiyon türü |
###### 1️⃣ Referans Kullanmazsak (Ownership taşınır):

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle { width: 30, height: 50 };

    println!("Alan: {}", area(rect1)); // ❌ burası hata verir

    println!("Genişlik: {}", rect1.width); // ❌ rect1 artık geçersiz
}

fn area(rectangle: Rectangle) -> u32 {
    rectangle.width * rectangle.height
}
```

> + `area` fonksiyonu parametre olarak **sahipliği** alıyor (`rectangle: Rectangle`).
> + Dolayısıyla `rect1` artık `main` içinde kullanılamaz.
> + Rust bunu **çift serbest bırakmayı önlemek için** engeller.

###### 2️⃣ Referans Kullanırsak (Borrowing):

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle { width: 30, height: 50 };

    println!("Alan: {}", area(&rect1)); // ✅ &rect1 ile referans gönderiyoruz
    println!("Genişlik: {}", rect1.width); // ✅ rect1 hala geçerli
}

fn area(rectangle: &Rectangle) -> u32 {
    rectangle.width * rectangle.height
}
```

> + `&rect1` → `rect1`’in **adresini** gönderiyoruz, sahipliğini vermiyoruz.
> + `area` fonksiyonu, parametre olarak `&Rectangle` alıyor → sadece ödünç alıyor.
> + Böylece `rect1` hâlâ `main` içinde kullanılabiliyor.
> + **Hafıza güvenliği** ve **ownership kuralları** korunmuş oluyor.


### 5.2.3. Türetilmiş (derived) trait’lerle kullanışlı işlevler ekleme:

+ Programımızı hata ayıklarken (`debugging` yaparken), bir `Rectangle` örneğini ekrana yazdırabilmek ve tüm alanlarının değerlerini görebilmek faydalı olurdu.
+ Listeleme 5-11, önceki bölümlerde kullandığımız gibi `println!` makrosunu kullanmayı dener. Ancak bu, **çalışmayacaktır.**
	- Yani, Normalde `println!` makrosuyla değişkenleri yazdırabiliyoruz, ama bir `struct` (örneğin `Rectangle`) doğrudan yazdırılamaz.

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {rect1}");
}
```

> + Liste 5-11: Bir `Rectangle` örneğini ekrana yazdırmayı girişimi

+ Bu kodu derlediğimizde, şu temel mesajla birlikte bir hata alırız:

```shell
error[E0277]: `Rectangle` doesn't implement `std::fmt::Display`
```

> + `println!` makrosu birçok farklı biçimlendirme türü yapabilir ve varsayılan olarak süslü parantezler (`{}`), `println!`’a **Display** olarak bilinen biçimlendirmeyi kullanmasını söyler: yani çıktının, doğrudan son kullanıcıya gösterilmesi amaçlanan bir biçimde üretilmesini sağlar.
> 	- Rust’ta `println!("{}", value)` yazdığında `Display` biçimlendirmesi kullanılır.  
> 	- Bu, genellikle **insan tarafından okunabilir** bir çıktı içindir.
> + Şu ana kadar gördüğümüz ilkel (primitive) türler, varsayılan olarak `Display` özelliğini (trait’ini) uygular; çünkü bir `1` sayısını veya başka bir ilkel türü kullanıcıya göstermek için yalnızca tek bir mantıklı yol vardır
> 	- Rust’ta `i32`, `u32`, `bool`, `char` gibi **temel türler**, `println!` ile doğrudan yazdırılabilir çünkü `Display` trait’i onlar için zaten tanımlıdır.
> 	- Ama `struct` gibi özel türlerde bu yoktur; yani, Rust onların **nasıl gösterileceğini** bilemez.
> + Ancak `struct`’larda, `println!` makrosunun çıktıyı nasıl biçimlendirmesi gerektiği o kadar açık değildir, çünkü birden fazla gösterim olasılığı vardır: Virgüller olsun mu olmasın mı? Süslü parantezler yazdırılsın mı? Tüm alanlar gösterilsin mi?
> + Bu belirsizlik nedeniyle Rust, ne istediğimizi tahmin etmeye çalışmaz ve bu yüzden `struct` türleri için `println!` ve `{}` yer tutucusuyla kullanılabilecek bir **`Display`** uygulaması (uyarlaması) varsayılan olarak sağlanmaz.

+ Hataları okumaya devam edersek, şu faydalı notu göreceğiz:
+ Yani derleyicinin verdiği hata mesajının devamında, Rust bize **neden hata olduğunu** ve **nasıl çözülebileceğini** açıklayan bir ek bilgi (not) gösterecektir.

```
   = help: the trait `std::fmt::Display` is not implemented for `Rectangle`
   = note: in format strings you may be able to use `{:?}` (or {:#?} for pretty-print) instead
```

+ Hadi deneyelim!
+ `println!` makrosu artık şöyle görünecek: `println!("rect1 is {rect1:?}");`
+ Süslü parantezlerin içine `:?` belirtecini eklemek, `println!`’a **Debug** adı verilen bir çıktı biçimini kullanmak istediğimizi söyler.
+ **Debug** trait’i, `struct`’ımızı geliştiriciler için faydalı bir biçimde ekrana yazdırmamızı sağlar; böylece kodumuzu hata ayıklarken (debug yaparken) değerini görebiliriz.
+ Bu değişikliği yaptıktan sonra kodu derleyelim. Tüh! Hâlâ bir hata alıyoruz:

```
error[E0277]: `Rectangle` doesn't implement `Debug`
```

+ Ama derleyici yine de bize yardımcı olacak bir not veriyor:

```
   = help: the trait `Debug` is not implemented for `Rectangle`
   = note: add `#[derive(Debug)]` to `Rectangle` or manually `impl Debug for Rectangle`
```

> + Rust, hata ayıklama (debug) bilgilerini ekrana yazdırmak için gerekli işlevselliği içerir, ancak bu özelliğin `struct`’ımız için kullanılabilir hale gelmesi için bunu açıkça etkinleştirmemiz gerekir.
> + Bunu yapmak için, `struct` tanımının hemen öncesine `#[derive(Debug)]` adlı dış özniteliği (outer attribute) ekleriz; bu, 5-12 numaralı listede gösterilmiştir.

**Dosya Adı: `scr/main.rs`**

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {rect1:?}");
}
```

> + `Liste 5-12`: `Debug` özelliğini (trait’ini) türetmek için özniteliğin eklenmesi ve `Rectangle` örneğinin (`instance`’ının) debug biçimlendirmesi kullanılarak yazdırılması.
> + Yani, Bu ifade, “`#[derive(Debug)]` ekleyerek `Debug` trait’ini etkinleştiriyoruz ve ardından `println!("{:?}", rect1)` ile `Rectangle` yapısını ekrana yazdırıyoruz.” anlamına gelir.

**Çıktı:**

```bash
rect1 is Rectangle { width: 30, height: 50 }
```

+ Artık programı çalıştırdığımızda herhangi bir hata almayacağız ve aşağıdaki çıktıyı göreceğiz:

```
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.48s
     Running `target/debug/rectangles`
rect1 is Rectangle { width: 30, height: 50 }
```

> + Güzel! Çıktı çok estetik görünmüyor ama bu örnekteki tüm alanların (field’ların) değerlerini gösteriyor ve bu da kesinlikle hata ayıklama sırasında faydalı olur.
> + Daha büyük struct’larımız olduğunda, çıktının biraz daha okunabilir olması faydalıdır; bu durumlarda, `println!` string’inde `{:?}` yerine `{:#?}` kullanabiliriz.
> 	- `{:?}` → tek satırda ve ham biçimde debug çıktısı verir.
> 	- `{:#?}` → **pretty-print** denilen, daha okunabilir bir biçimde (satır satır ve girintili) debug çıktısı sağlar.
> + Bu örnekte, `{:#?}` stilinin kullanılması aşağıdaki çıktıyı verecektir:

```
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.48s
     Running `target/debug/rectangles`
rect1 is Rectangle {
    width: 30,
    height: 50,
}
```

> + **Debug** (hata ayıklama) formatını kullanarak bir değeri yazdırmanın bir diğer yolu da **`dbg!`** makrosunu kullanmaktır. Bu makro, bir ifadenin **sahipliğini alır** (bu, bir referans alan `println!`'den farklıdır), kodunuzda bu `dbg!` makro çağrısının bulunduğu **dosya ve satır numarasını** ve ayrıca o ifadenin **sonuç değerini** yazdırır ve ardından **değerin sahipliğini geri döndürür**.


> [!NOTE]
> #### `println!`
> + Bir değeri veya ifadeyi **ekrana yazdırmak** için kullanılır.
> + Genellikle kullanıcıya yönelik **temiz ve formatlı çıktı** üretir.
> ```
> let x = 5;
> println!("x: {}", x);  // x: 5
> ```
> + **Referans alır**: Eğer bir struct veya değişken gönderiyorsak, genellikle `&` ile referans göndeririz (`println!("{:?}", &my_struct)`).
> #### `dbg!`
> + Daha çok **hata ayıklama(debugging)** amacıyla kullanılır.
> + Gönderilen ifadeyi değerlendirir, **sahipliğini alır** (ownership), dosya adı ve satır numarasıyla birlikte ekrana yazdırır.
> + Çıktıyı **geliştiriciye yönelik** gösterir (Debug formatı varsayılan).
> + Ayrıca, ifadenin **değerini geri döndürür**, bu yüzden değişkene atayabilirsiniz.
> ```rust
> let x = 5;
> let y = dbg!(x * 2); // [src/main.rs:3] x * 2 = 10
> ```

| Özellik           | `println!`          | `dbg!`                           |
| ----------------- | ------------------- | -------------------------------- |
| Amaç              | Kullanıcıya çıktı   | Geliştirici/debug için çıktı     |
| Referans/Sahiplik | Referans alır (`&`) | Sahipliği alır (ownership)       |
| Ek bilgi          | Yok                 | Dosya ve satır numarası gösterir |
| Geri dönüş        | Yok                 | İfadenin değerini döndürür       |
| Format            | Display veya Debug  | Debug (`{:?}`) varsayılan        |


> [!CAUTION]
> + `dbg!` makrosunu çağırmak, çıktıyı **standart hata (stderr) akışına** yazdırır; oysa `println!`, çıktıyı **standart çıktı (stdout) akışına** yazar.
> 	- **stdout** → normal program çıktıları için kullanılır (ekrana yazdırılır veya yönlendirilir).
> 	- **stderr** → hata mesajları veya debug bilgileri için ayrılmıştır.
> + `stderr` ve `stdout` hakkında daha fazla bilgiyi, 12. bölümdeki “[Hata Mesajlarını Standart Çıktı Yerine Standart Hata Akışına Yazmak](https://doc.rust-lang.org/book/ch12-06-writing-to-stderr-instead-of-stdout.html)” başlıklı bölümde ele alacağız.

+ İşte genişlik alanına atanan değerin yanı sıra rect1'deki tüm yapının değeriyle ilgilendiğimiz bir örnek:
+ Yani, verilen kod örneğinde, sadece **`width`** değişkeninin son değerini değil, aynı zamanda **`rect1`** adındaki **tüm yapı nesnesinin** (örneğin bir dikdörtgenin genişlik, yükseklik ve alan gibi tüm bilgilerinin) değerini de incelemek istiyoruz.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let scale = 2;
    let rect1 = Rectangle {
        width: dbg!(30 * scale),
        height: 50,
    };

    dbg!(&rect1);
}
```

> + `30 * scale` ifadesinin etrafına `dbg!` koyabiliriz ve `dbg!`, ifadenin değerinin sahipliğini(`ownership`) geri verdiği için, `width` alanı `dbg!` çağrısı olmasaydı ne değer alacaktıysa yine aynı değeri alacaktır.
> 	- `dbg!` makrosunu 30 * scale ifadesine uygulasak bile, `dbg!` ifadenin değerini geri verdiğinden `width` alanı normalde alacağı değeri almaya devam eder.
> 	- Yani, `dbg!` makrosunun ifadeyi _değiştirmediği_, sadece onu ekrana bastığıdır. `dbg!` kullanmak programın değerlerini bozmaz.
> + `dbg!` makrosunun `rect1`’in sahipliğini(`ownership`) almasını istemediğimiz için, sonraki çağrıda `rect1`’e bir referans kullanıyoruz. Bu örneğin çıktısı şöyle görünür:
> 	-  Bu cümleyi aşağıdaki "`dbg!(&rect1)` ile `dbg!(rect1)` arasındaki fark" Notu açıklamaktadır.


> [!NOTE]
> #### `dbg!(&rect1)` ile `dbg!(rect1)` arasındaki fark:
> ##### Sahiplik (Ownership) farkı:
>  + `dbg!(rect1)`
> 	- → `dbg!` makrosu **ifadenin sahipliğini alır (takes ownership)**.
> 	- Yani `rect1` değeri `dbg!` içine **taşınır (moved)**.
> 	- Bu yüzden `dbg!` çağrısından **sonra `rect1` artık kullanılamaz**.
> + `dbg!(&rect1)`
> 	- → Burada `rect1`’in **referansını (borrow)** geçiriyorsun.
> 	- Yani `rect1` hâlâ **main fonksiyonunda kullanılabilir durumda kalır**.
> 	- Çünkü sadece **ödünç verilmiştir**, taşınmamıştır.

| Kullanım       | Anlamı                        | Sonrasında `rect1` kullanılabilir mi? |
| -------------- | ----------------------------- | ------------------------------------- |
| `dbg!(rect1)`  | Sahipliği taşır (move)        | ❌ Hayır                               |
| `dbg!(&rect1)` | Referansla borç alır (borrow) | ✅ Evet                                |

```
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.61s
     Running `target/debug/rectangles`
[src/main.rs:10:16] 30 * scale = 60
[src/main.rs:14:5] &rect1 = Rectangle {
    width: 60,
    height: 50,
}
```

> + İlk çıktının, `30 * scale` ifadesini debug ettiğimiz `src/main.rs` dosyasındaki 10. satırdan geldiğini görebiliyoruz ve bu ifadenin sonucu 60’tır (tamsayılar için uygulanmış Debug biçimlendirmesi yalnızca değerlerini yazdırır).
> 	- Yani, İlk çıktının `src/main.rs` dosyasının 10. satırından geldiğini görüyoruz. Burada `30 * scale` ifadesini debug ediyoruz ve sonuç değeri 60 olarak görünüyor. (Tamsayılar için Debug formatı sadece sayısal değerlerini gösterecek şekilde uygulanmıştır.
> + `src/main.rs` dosyasının 14. satırındaki dbg! çağrısı `&rect1` değerini, yani `Rectangle` yapısını çıktı olarak verir.
> + Bu çıktı, `Rectangle` türü için uygulanmış **`pretty Debug`** biçimlendmesini kullanır.
> + `dbg!` makrosu, kodunun ne yaptığını anlamaya çalışırken gerçekten çok yardımcı olabilir!


> [!NOTE]
> #### 📌 Pretty Debug Nedir?
> + Rust’ta **Debug trait**, bir değerin ekrana yazdırılabilmesini sağlar.
> 	- Normal `Debug` → basit, tek satır, minimal bilgi
> 	- Pretty Debug (`{:#?}`) → daha okunabilir, **güzel formatlanmış**, **çok satırlı** çıktı
> ```rust
> #[derive(Debug)]
> struct Rectangle {
>    width: u32,
>    height: u32,
>}
>
> fn main() {
>    let rect1 = Rectangle { width: 60, height: 50 };
>
>    // Normal Debug
>    println!("{:?}", rect1);
>
>    // Pretty Debug
>    println!("{:#?}", rect1);
>}
> ```
> #### Çıktı:
> **Normal Çıktı:**
> ```
> Rectangle { width: 60, height: 50 }
> ```
> **Pretty Debug (`{:#?}`)**
> ```
> Rectangle {
>    width: 60,
>    height: 50,
>}
> ```

> + Debug trait’ine ek olarak, Rust, `derive` özniteliği ile kullanabileceğimiz ve özel (custom) türlerimize faydalı davranışlar ekleyebilen bir dizi trait sağlamıştır.
> + Bu trait’ler ve davranışları  [Appendix C](https://doc.rust-lang.org/book/appendix-03-derivable-traits.html)’de listelenmiştir. Bu trait’leri kendi özel davranışlarımızla nasıl uygulayacağımızı ve kendi trait’lerimizi nasıl oluşturacağımızı Bölüm 10’da ele alacağız.
> + `derive` dışında da birçok öznitelik vardır; daha fazla bilgi için [Rust Reference’taki ‘Attributes’ bölümüne](https://doc.rust-lang.org/reference/attributes.html) bakabilirsiniz.

> + `Area` (alan) fonksiyonumuz oldukça spesifik: yalnızca dikdörtgenlerin alanını hesaplar. 
> + Bu davranışı `Rectangle` yapımıza(`struct`) daha sıkı bağlamak faydalı olur, çünkü başka bir türle çalışmaz. 
> + Şimdi, bu kodu nasıl yeniden düzenleyebileceğimize ve `area` fonksiyonunu `Rectangle` türü üzerinde tanımlanmış bir alan (`area`) **metodu** haline nasıl getirebileceğimize bakalım.


## 5.3. Metot Sözdizimi:

+ Metotlar (methods), fonksiyonlara benzer: `fn` anahtar kelimesi ve bir isimle tanımlanırlar, parametreleri ve bir dönüş değeri olabilir, ve metot başka bir yerden çağrıldığında çalıştırılacak bazı kodları içerirler.
+ Fonksiyonların aksine, metotlar bir struct (veya enum ya da trait nesnesi, bunları sırasıyla Bölüm 6 ve Bölüm 18’de ele alacağız) bağlamı içinde tanımlanır ve ilk parametreleri her zaman `self`’tir; bu `self`, metot çağrısının yapıldığı struct örneğini(`struct instance`) temsil eder.

### 5.3.1. Metotları Tanımlama:

+ Parametre olarak bir `Rectangle` örneği alan `area` fonksiyonunu değiştirelim ve bunun yerine, `Rectangle` struct’ı üzerinde tanımlanmış bir `area` metodu haline getirelim; bunun nasıl yapılacağını 5-13 numaralı listede görebilirsiniz.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

> + Liste 5-13: Rectangle yapısı üzerinde bir area (alan) metodu tanımlamak

+ Fonksiyonu `Rectangle` bağlamında tanımlamak için, `Rectangle` için bir `impl` (`implementation`) bloğu başlatırız. 
+ Bu `impl` bloğunun içindeki her şey `Rectangle` türüyle ilişkilendirilecektir. 
+ Daha sonra `area` fonksiyonunu bu `impl` bloğunun süslü parantezleri içine taşırız ve fonksiyonun imzasındaki ilk (ve bu durumda yalnızca) parametreyi `self` olarak değiştiririz; ayrıca fonksiyonun gövdesindeki tüm kullanımları da buna göre güncelleriz.
+ `main` fonksiyonunda, daha önce `area` fonksiyonunu çağırıp `rect1`’i argüman olarak geçtiğimiz yerde, bunun yerine `Rectangle` örneğimiz üzerinde `area` metodunu çağırmak için metot sözdizimini kullanabiliriz.
+ Metot sözdizimi bir örnekten(`instance`) sonra gelir: örneğin sonuna bir nokta ekleriz, ardından metot adı, parantezler ve varsa argümanlar gelir.
+ `area` metodunun imzasında, `rectangle: &Rectangle` yerine `&self` kullanıyoruz.
+ Aslında `&self`, `self: &Self` ifadesinin kısaltmasıdır.
	- `fn area(&self) -> u32 {...}` ile `fn area(self: &Self) -> u32 {...}` aynıdır.
+ Bir `impl` bloğunun içinde `Self` türü, o `impl` bloğunun tanımlandığı tür için bir takma addır.
+ Metotların ilk parametresi, türü `Self` olan `self` adında bir parametre olmalıdır, bu yüzden Rust size ilk parametre konumunda yalnızca `self` yazarak bunu kısaltma imkânı verir.
+ Ancak, bu metodun `Self` örneğini ödünç aldığını belirtmek için kısaltmanın önüne hâlâ `&` koymamız gerekir; tıpkı `rectangle: &Rectangle` yazdığımız gibi.
+ Metotlar, tıpkı diğer parametrelerde olduğu gibi, `self`’in sahipliğini(`ownership`) alabilir, `self`’i değiştirilemez (`immutably`) ödünç alabilir — burada yaptığımız gibi — veya `self`’i değiştirilebilir (`mutably`) ödünç alabilir.
+ Burada **&self** kullanmayı, fonksiyon versiyonunda **&Rectangle** kullanmamızla aynı sebepten seçtik: **sahipliği almak istemiyoruz** ve **yapı içindeki veriyi sadece okumak istiyoruz, yazmak değil**.
+ Eğer metodun yaptığı işlemin bir parçası olarak, üzerinde çağrıldığı örneği (instance’ı) değiştirmek isteseydik, ilk parametre olarak **&mut self** kullanırdık.
+ Sadece **self** kullanan (yani sahipliği alan) bir metod ise **nadiren kullanılır**; bu teknik genellikle metodun `self`i başka bir şeye dönüştürdüğü ve dönüşümden sonra çağıranın orijinal örneği kullanmasını engellemek istediğiniz durumlarda tercih edilir.
+ Bir türün bir örneğiyle (instance’ıyla) yapabileceğimiz tüm işlemleri tek bir **impl bloğu** içine yerleştiririz; böylece kodumuzu kullanan kişiler, `Rectangle` ile ilgili yetenekleri (neler yapabileceğini) kütüphanemizin farklı yerlerinde aramak zorunda kalmazlar.
+ Dikkat edin: Bir metoda, yapının alanlarından (`field`) biriyle aynı ismi vermeyi seçebiliriz.  
+ Örneğin, `Rectangle` üzerinde `width` adıyla bir alan olmasına rağmen, aynı zamanda `width` adında bir metot da tanımlayabiliriz.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn width(&self) -> bool {
        self.width > 0
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    if rect1.width() {
        println!("The rectangle has a nonzero width; it is {}", rect1.width);
    }
}
```

> + Burada, `width` metodunun, örneğin(`instance`) `width` alanındaki(`width field`) değer 0’dan büyükse `true`, 0 ise `false` döndürmesini seçiyoruz: aynı isme sahip bir metodun içinde o alanı (`field`) istediğimiz amaçla kullanabiliriz.  
> + `main` fonksiyonunda `rect1.width` ifadesinden sonra parantez kullanırsak, Rust bunun `width` metodu olduğunu anlar.
> + Parantez kullanmazsak, Rust bunun `width` alanı (`field`) olduğunu anlar.

> + Çoğu zaman (ama her zaman değil), bir metoda bir alanla (field) aynı ismi verdiğimizde, yalnızca o alandaki değeri döndürmesini ve başka hiçbir şey yapmamasını isteriz.
> + Bu tür metotlara _getter_ denir ve bazı dillerin aksine Rust, struct alanları için getter metotlarını otomatik olarak oluşturmaz.
> + `Getter`'lar faydalıdır çünkü alanı (`field`) `private` yapabilir, metodu ise `public` yapabilirsiniz. Böylece bu alan için yalnızca okuma (`read-only`) erişimi sağlayarak türün `public API`’sine dahil etmiş olursunuz.
> + Alanların ve metotların `public` veya private olmasının ne anlama geldiğini ve bunların nasıl belirtileceğini **7. bölümde** tartışacağız.
	- Aşağıdaki Not yukarıdaki paragrafları açıklamaktadır(chatGPT):

> [!NOTE]
> + Rust’ta bir `impl` bloğunun içinde yazdığın **Self** kelimesi aslında **o struct’ın adıyla aynı şeyi ifade eder**.
> + Yani;
> 	- Struct’ın adı: `Rectangle`
> 	- `impl Rectangle` içinde `Self` yazarsan → **`Rectangle` ile tamamen aynı anlamdadır.**
> 	- `Self` = `Rectangle`
> + Bu, sadece yazımı kolaylaştırmak ve okunabilirliği arttırmak için kullanılır.
> ```rust
> struct Rectangle {
 >   width: u32,
>    height: u32,
>}
>
>impl Rectangle {
>    fn new(width: u32, height: u32) -> Self {
>        Self { width, height }
>    }
>}
> ```
> + Burada:
> 	- `fn new(...) -> Self` aslında **`-> Rectangle`** demektir.
> 	- `Self { width, height }` aslında **`Rectangle { width, height }`** demektir.
> + Yani aşağıdaki iki kod tamamen aynıdır:
> ```rust
> fn new(width: u32, height: u32) -> Self { ... }
> ```
> ve
> ```rust
> fn new(width: u32, height: u32) -> Rectangle { ... }
> ```


> [!NOTE]
> #### Neden `Self` kullanılır?
> + ✔ Kod daha okunabilir olur.
> 	- Özellikle generic yapılarda veya uzun struct isimlerinde çok işine yarar.
> + ✔ Refactoring kolaylaşır.
> 	- Struct’ın adı değişse bile `Self` olduğundan kod bozulmaz.
> + ✔ Rust topluluğunda **standart yazım şeklidir**

#### 5.3.1.1. `Self` ile `self` arasında fark:

**🟥 1. **Self (büyük S)** → Türün kendisi**

+ `Self` bir tip(type) anlamına gelir. Yani, `struct` adının yerine kullanılır.

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn new(w: u32, h: u32) -> Self {
        Self { width: w, height: h }
    }
}
```

🟦 2. **self (küçük s)** → Metotun aldığı örnek (instance)

+ `self`,  metodu çağıran nesnenin kendisidir.

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}
```

> + Buradaki:
> 	- `self` → `rect1`, `rect2` gibi bir örnektir.
> 	- Yani **`Self`’in örneğidir.**

**Örneğini Oluşturma:**

```rust
let rect1 = Rectangle { width: 10, height: 20 };
rect1.area();
```

> + Burada `rect1.area()` çağrıldığında:
> 	- `self` = `rect1`

|Yazım|Anlam|Açıklama|
|---|---|---|
|**Self**|Tür|`Rectangle` demek|
|**self**|Nesne (instance)|`rect1`, `rect2` gibi|
**Self = Tür, self = Nesne**

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // Self → Tür (Rectangle)
    fn new(width: u32, height: u32) -> Self {
        Self { width, height }
    }

    // self → nesne (örnek)
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle::new(10, 20); // Self burada Rectangle

    println!("Area: {}", rect1.area()); // self burada rect1
}
```

#### 5.3.1.2. self sahiplenme (ownership)

+ `self` sahipliği alır

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {

	// Self ile constructor gibi fonksiyon
    fn new(w: u32, h: u32) -> Self {
        Self {width: w, height: h}
    }

    fn area(self: &Self) -> u32 {
        self.width * self.height
    }

    fn destory(self) {
        println!(
            "Rectangle yok edildi: {}x{}", self.width, self.height
            );
    }
}

fn main() {

    let rect1 = Rectangle::new(10,20);
    println!("{}",rect1.area());

    rect1.destory();  // self burada rect (tüm ownership geçti)
    println!("{}",rect1.area());  // HATA verir.
}
```

> + Bu metot `self` alıyor → yani **nesnenin sahipliğini alıyor**.
> + `&self` değil → artık rect kullanılamaz.

#### 5.3.1.3. self mut olarak borrow

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {

    fn new(w: u32, h: u32) -> Self {
        Self {width: w, height: h}
    }

    fn area(self: &Self) -> u32 {
        self.width * self.height
    }

    fn destory(self) {
        println!(
            "Rectangle yok edildi: {}x{}", self.width, self.height
            );
    }

    fn grow(&mut self, amount: u32) {
        self.width += amount;
        self.height += amount;
    }
}


fn main() {

    let mut rect1 = Rectangle::new(10,20);
    rect1.grow(5); // +5
    println!("+5 Ek: {} {}", rect1.width, rect1.height);
}
```

**Çıktı:**

```
+5 Ek: 15x25
```

> + `&mut self` → nesne üzerinde değişiklik yapma izni

| Yazım         | Anlam                          | Ne için kullanılır?               |
| ------------- | ------------------------------ | --------------------------------- |
| **Self**      | Türün kendisi                  | `Rectangle` oluşturmak, döndürmek |
| **&self**     | Nesnenin borçlanmış hali       | Okuma işlemleri                   |
| **&mut self** | Nesnenin değiştirilebilir hali | Alan değiştirme                   |
| **self**      | Nesnenin sahipliğini alan hali | Nesneyi tüketen işlemler          |

+ Metotları fonksiyonlar yerine kullanmanın temel nedeni — metot söz dizimini sağlamanın ve her metodun imzasında self türünü tekrar tekrar yazmak zorunda olmamanın yanı sıra — **düzen sağlamaktır**.
	1. Bu yüzden `Rectangle` türünü **tekrar tekrar yazmak zorunda kalmazsın**.
	2. **Her defasında `&Rectangle` yazmak yerine sadece `&self` yazarsın.**

> [!NOTE]
> ##### Her metodun imzasında self türünü tekrar tekrar yazmak zorunda olmamak
> + Eğer metot değil de **fonksiyon** yazarak devam etseydin, her fonksiyonun imzasında Rectangle türünü yazmak zorundaydın:
> ```rust
> fn area(rect: &Rectangle) -> u32
> fn width(rect: &Rectangle) -> u32
> fn height(rect: &Rectangle) -> u32
> fn can_hold(rect1: &Rectangle, rect2: &Rectangle) -> bool
> ```
> + Her defasında **&Rectangle** yazmak zorundaydın.
> + Ama **metot** kullandığında:
> ```rust
> impl Rectangle {
 >   fn area(&self) -> u32
>    fn width(&self) -> u32
>    fn height(&self) -> u32
>    fn can_hold(&self, other: &Rectangle) -> bool
>}
> ```
> + Burada
> 	- `self` → zaten Rectangle türüdür (Self)
> 	- `&self` → `&Rectangle` yazmanın kısa hali
> + Bu yüzden `Rectangle` türünü **tekrar tekrar yazmak zorunda kalmazsın**.

---

> [!NOTE]
> #### `->` operatörü nerede? Rust’ta neden yok?
> + C ve C++’ta, metot çağırmak için iki farklı operatör kullanılır:
> 	- **nesnenin kendisi üzerinde** bir metot çağırıyorsanız `.` kullanırsınız,
> 	- **nesnenin bir pointer’ı üzerinde** metot çağırıyorsanız ve önce pointer’ı dereference etmeniz gerekiyorsa `->` kullanırsınız.
> + Başka bir deyişle, eğer `object` bir pointer ise, **`object->something()` ifadesi, `(*object).something()` ifadesine benzer.**
> + Rust’ta `->` operatörüne eşdeğer bir şey yoktur; onun yerine Rust’ta **otomatik referans ve dereference** (automatic referencing and dereferencing) adı verilen bir özellik vardır.
> + Metot çağırmak(`->` benzer şekilde), Rust’ta bu davranışın görüldüğü nadir durumlardan biridir.
> + Here’s how it works: when you call a method with `object.something()`, Rust automatically adds in `&`, `&mut`, or `*` so `object` matches the signature of the method. Tıpkı aşağıdaki kod gibi;
> ```rust
> #![allow(unused)]
> fn main() {
> #[derive(Debug,Copy,Clone)]
> struct Point {
>    x: f64,
>    y: f64,
>}
>
> impl Point {
>   fn distance(&self, other: &Point) -> f64 {
>       let x_squared = f64::powi(other.x - self.x, 2);
>       let y_squared = f64::powi(other.y - self.y, 2);
>
>       f64::sqrt(x_squared + y_squared)
>   }
>}
>let p1 = Point { x: 0.0, y: 0.0 };
>let p2 = Point { x: 5.0, y: 6.5 };
>p1.distance(&p2);  // 1. Yöntem
>(&p1).distance(&p2); // 2. Yöntem
>} 
> ```
> + İlk yöntem çok daha temiz görünüyor.
> + Bu otomatik referans ekleme davranışı, metodların net bir alıcıya (receiver) sahip olmasından dolayı çalışır—yani `self` tipi.
> + Bir metodun alıcısı ve adı bilindiğinde, Rust metodun **okuma yaptığını (`&self`)**, **değişiklik yaptığını (`&mut self`)** veya **sahipliği devraldığını (`self`)** kesin olarak belirleyebilir.
> + Rust’ın metod alıcıları için `borrowing`’i (ödünç alma) otomatik yapması, `ownership` (sahiplik) kavramını pratikte kullanışlı ve rahat hale getiren önemli bir etkendir.


> [!NOTE]
> #### Rust’ta `->` operatörü yok çünkü
> + Rust, **pointer ve referansları otomatik olarak dereference eder**. Yani, C/C++’taki gibi elle `*` veya `->` yazmana gerek yoktur.
> #### Örnek: C++
> ```Cpp
> struct Rectangle {
>    int width;
>    int height;
>    int area() { return width * height; }
>};
>
>Rectangle rect;
>Rectangle* ptr = &rect;
>
>rect.area();     // . ile çağır
>ptr->area();     // -> ile pointer üzerinden çağır
>(*ptr).area();   // veya dereference ederek çağırabilirsin
> ```
> #### Aynı Örnek Rust
> ```rust
> struct Rectangle {
>    width: u32,
>    height: u32,
>}
>
>impl Rectangle {
>    fn area(&self) -> u32 {
>        self.width * self.height
>    }
>}
>
>fn main() {
>    let rect = Rectangle { width: 10, height: 20 };
>    let rect_ref = &rect;
>
>    println!("{}", rect.area());      // doğrudan nesne
>    println!("{}", rect_ref.area());  // referans üzerinden çağrı, Rust otomatik deref yapar
>}
>```
>+ `rect_ref.area()` çağrısı **`&rect`** bir referans olmasına rağmen sorunsuz çalışır.
>+ Rust otomatik olarak `*rect_ref` yapar ve metodu çağırır.
>+ Bu yüzden **C++’taki `->` operatörüne gerek yoktur.**

| Dil   | Pointer üzerinden metot çağırma        |
| ----- | -------------------------------------- |
| C/C++ | `ptr->method()` veya `(*ptr).method()` |
| Rust  | `&instance.method()` (otomatik deref)  |
#### 5.3.1.4 Rust otomatik olarak `&`, `&mut` veya `*` ekler:

+ Rust’ta bir metot bir **referans**, **mutable referans** veya **owned değer** alacak şekilde tanımlanabilir:

```rust
struct MyStruct {
    value: i32,
}

impl MyStruct {
    // self referansı immutable
    fn read(&self) -> i32 {
        self.value
    }

    // self referansı mutable
    fn increment(&mut self) {
        self.value += 1;
    }

    // self'i sahiplenir (move)
    fn consume(self) -> i32 {
        self.value
    }
}
```

+ Metot çağırırken Rust sizin yerinize uygun işareti ekler:

```rust
fn main() {
    let mut obj = MyStruct { value: 10 };

    // read() metodu &self alıyor, Rust otomatik olarak &obj koyar
    println!("{}", obj.read()); // -> Rust bunu obj.read() yerine (&obj).read() gibi yorumlar

    // increment() metodu &mut self alıyor, Rust otomatik olarak &mut obj koyar
    obj.increment(); // -> Rust bunu (&mut obj).increment() gibi yorumlar

    // consume() metodu self alıyor, yani obj'in sahipliğini alır
    let v = obj.consume(); // -> obj artık kullanılamaz, çünkü sahipliği consume() aldı
}
```

> + **Özet:** Rust, metot çağrılarında sizin yerinize `&`, `&mut` veya `*` ekleyerek çağırdığınız objeyi metot imzasına uydurur. Yani sizin `&obj` ya da `&mut obj` yazmanız çoğu zaman gerekmez.
### 5.3.2 Daha Fazla Parametreler ile Metotlar:

+ Metotları kullanma pratiği yapalım: Rectangle yapısında ikinci bir metot daha implemente edeceğiz.
+ Bu sefer `Rectangle`’ın bir örneğinin(`instance`), başka bir `Rectangle` örneğini(`instance`) alıp, ikinci `Rectangle`’ın tamamen `self` (birinci `Rectangle`) içine sığıp sığamayacağını kontrol etmesini istiyoruz.
+ Eğer sığıyorsa `true`, aksi halde `false` döndürmeli.
+ Yani `can_hold` metodunu tanımladıktan sonra, `Listing 5-14`’te gösterilen programı yazabilmek istiyoruz.

**Dosya Adı:`src/main.rs`**

```rust
fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```

> + `Listing 5-14`: Henüz yazılmamış olan `can_hold` metodunu kullanmak

+ Beklenen çıktı aşağıdaki gibi olacaktır; çünkü `rect2`’nin her iki boyutu da `rect1`’in boyutlarından küçüktür, ancak rect3 rect1’den daha geniştir.

```shell
Can rect1 hold rect2? true
Can rect1 hold rect3? false
```

+ Bir metot tanımlamak istediğimizi biliyoruz, bu yüzden `impl Rectangle` bloğu içinde olacak.
+ Metot adı `can_hold` olacak ve parametre olarak başka bir `Rectangle`’ın değiştirilemez bir ödünç(`immutable borrow`) alacak.
+ Parametrenin türünün(type) ne olacağını, metodu çağıran koda bakarak anlayabiliriz: `rect1.can_hold(&rect2)` ifadesi, `Rectangle` örneği olan `rect2`’nin değiştirilemez bir ödünç(`immutable borrow`) alımını (`&rect2`) geçiriyor.
+ Bu mantıklıdır çünkü `rect2`’yi sadece okumamız gerekiyor (eğer yazmamız gerekseydi değiştirilebilir bir borç—`mutable borrow`—gerekirdi) ve `can_hold` metodunu çağırdıktan sonra `main` fonksiyonunun `rect2`’nin sahipliğini elinde tutmasını istiyoruz, böylece onu tekrar kullanabiliriz.
	- Yani `rect2`, `can_hold` metoduna **geçici olarak ödünç verilsin**,  ama sonra **hala main fonksiyonunda kullanılabilir kalsın**.
+ `can_hold` metodunun dönüş değeri `Boolean (bool)` olacak ve `implementasyonu`, `self`’in genişlik ve yüksekliğinin, diğer `Rectangle`’ın genişlik ve yüksekliğinden büyük olup olmadığını kontrol edecek.
+ Şimdi `Listing 5-13`’teki `impl` bloğuna yeni `can_hold` metodunu ekleyelim; bu, `Listing 5-15`’te gösterilmiştir

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```

> + `Listing 5-15`: Parametre olarak başka bir `Rectangle` örneği(`Rectangle instance`) alan `can_hold` metodunun `Rectangle` üzerinde uygulanması

```shell
Can rect1 hold rect2? true  
Can rect1 hold rect3? false
```

> + Bu kodu` Listing 5-14’`teki main fonksiyonuyla birlikte çalıştırdığımızda istediğimiz çıktıyı elde ederiz.
> + Metotlar, self parametresinden sonra imzaya eklediğimiz birden fazla parametre alabilir ve bu parametreler, fonksiyonlardaki parametreler gibi çalışır.
> 	- **Rust'ta bir metot (method) tanımlarken, ilk parametre her zaman `self` olur.**  
> 	- Bu, metodun **hangi nesne üzerinde çalıştığını** gösterir.
> 	- Ama **`self`'ten sonra** metota **istediğin kadar ek parametre** yazabilirsin.
> 	- Ve bu parametreler, normal bir fonksiyondaki parametreler gibi çalışır:


> [!NOTE]
> #### İmza(Signature) nedir?
> + Rust, C, C++, Java, Python gibi birçok dilde bir fonksiyonun veya metodun:
> 	- adı
> 	- parametre listesi
> 	- parametre tipleri
> 	- dönüş tipi
> + gibi tanımlayıcı özelliklerinin tamamına "signature" yani imza denir.
> + Yani Bir fonksiyonun/metodun **nasıl çağrılacağını belirleyen bölüm demektir.**
> ```rust
> fn can_hold(&self, other: &Rectangle) -> bool
> ```
> + Buradaki satır komple **metodun imzasıdır.**
> 
> **İçerisinde:**
> + metodun adı: `can_hold`
> + parametreler:
> 	- `&self`
> 	- `other: &Rectangle`
> + dönüş tipi: `bool`
> + Bunların hepsi bir arada → **imza (signature)**
> #### Neden "imza" deniyor?
> + Çünkü bir fonksiyonu tanımlayan şey budur.
> + Bir insanı nasıl imzasıyla tanıyorsan, bir fonksiyonu da "signature" yani imzasıyla tanırsın.
> + Derleyici de fonksiyonları bu imza üzerinden ayırt eder.

### 5.3.3. Associated Fonksiyonlar:

+ Bir `impl` bloğu içinde tanımlanan tüm fonksiyonlara, `impl` anahtar sözcüğünden sonra adı yazılan türle ilişkili oldukları için ‘ilişkili fonksiyonlar’ (`associated functions`) denir.
+ Bu fonksiyonların ilk parametreleri `self` olmak zorunda değildir (dolayısıyla metot değildirler); çünkü çalışmak için o türe ait bir örneğe ihtiyaç duymazlar.
+ Daha önce buna bir örnek kullandık: `String` türü üzerinde tanımlanmış olan `String::from` fonksiyonu.
+ Metot olmayan ilişkili fonksiyonlar (`associated functions`) genellikle `struct`’ın yeni bir örneğini(`instance`) döndürecek `constructor` olarak kullanılır.
+ Bunlara genellikle `new` adı verilir, ancak `new` özel bir isim değildir ve dilin içine gömülü değildir.
+ Örneğin, bir ilişkili fonksiyon(`associated function`) olarak `square` adını seçebiliriz; bu fonksiyon tek bir boyut parametresi alır ve hem genişlik hem yükseklik için kullanır.
+ Böylece kare bir `Rectangle` oluşturmak, aynı değeri iki kez belirtmek zorunda kalmaktan daha kolay hale gelir

**Dosya Adı:`scr/main.rs`**

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn square(size: u32) -> Self {
        Self {
            width: size,
            height: size,
        }
    }
}

fn main() {
    let sq = Rectangle::square(3);
}
```

> + Fonksiyonun dönüş tipinde ve gövdesinde kullanılan `Self` anahtar kelimesi, `impl` anahtar kelimesinden sonra yazılan türün takma adıdır; bu örnekte bu tür `Rectangle`’dır.

> + Bu ilişkili fonksiyonu çağırmak için struct adıyla birlikte `::` sözdizimini kullanırız; örneğin `let sq = Rectangle::square(3);`.
> + Bu fonksiyon `struct` tarafından isim alanına (`namespace`) alınmıştır: `::` sözdizimi hem ilişkili fonksiyonlar(`associated function`) hem de modüller tarafından oluşturulan isim alanları(`namespace`) için kullanılır.
> + **Modülleri Bölüm 7’de tartışacağız.**


> [!NOTE]
> + Rust’ta bir **associated function** (ilişkili fonksiyon) doğrudan bir struct’a bağlıdır. Yani:
> 	- Fonksiyon **`global scope`**’ta değil, `struct`’ın “isim alanı” (`namespace`) içinde tanımlanır.
> 	- Bu yüzden fonksiyonu çağırırken **struct adını** kullanmak zorundayız.
> + `square` fonksiyonu **Rectangle struct’ının namespace’inde** yer alır.
> + Bu nedenle çağırırken:
> ```rust
> let sq = Rectangle::square(3);
> ```
> + Sadece `square(3)` yazamayız, çünkü `global scope`’ta böyle bir fonksiyon yoktur.
> + Rust, fonksiyonun hangi struct’a ait olduğunu **namespace aracılığıyla** bilir.


> [!NOTE]
> + Rust’ta `::` operatörü **bir öğenin hangi isim alanına (namespace) ait olduğunu belirtmek için kullanılır**.
> 
> **Associated Fonksiyonlarda**
> ```rust
> Rectangle::square(3)
> ```
> + Burada `square` fonksiyonu `Rectangle` `struct`’ına ait. `::` operatörü ile “bu fonksiyon `Rectangle` isim alanının(`Rectangle namespace`) içinde” deniyor.
> 
>  **Modüllerde**
>  ```rust
>  std::io::stdin()
>  ```
>  + Burada `stdin` fonksiyonu `std::io` modülünün içinde. Yani modüller de kendi isim alanlarını oluşturur ve `::` ile erişilir.



### 5.3.4 Method ve Associated Fonksiyonlar:

+ Rust’ta **`associated function` (bağlı fonksiyon)** ve **method (metot)** birbirine benzeyen ama önemli farklara sahip iki kavramdır.
+ Bunlar `impl` blokları içinde tanımlanır ama kullanım şekilleri farklıdır.
#### 5.3.4.1. 🟦 Associated Function (Bağlı Fonksiyon) Nedir?

+ **Associated function**, bir **struct**, **enum** veya **trait** ile ilişkilendirilmiş fonksiyondur ama **self parametresi almaz**.
+ Yani bir nesne üzerinde çalışmaz.


> [!NOTE]
> ✔ **Özellikler**
> + `self`, `&self` veya `&mut self` ALMAZ.
> + Genelde **yapıcı fonksiyon (constructor)** gibi kullanılır.
> + Çağrılırken **tip adı üzerinden çağrılır**: `Type::function()`

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // Associated function -> çünkü self almıyor
    fn new(width: u32, height: u32) -> Rectangle {
        Rectangle { width, height }
    }
}

fn main() {
    let rect = Rectangle::new(30, 50);
}
```

> + `new()` bir associated function’dır, metot değildir.

#### 5.3.4.2. 🟩 Method (Metot) Nedir?

+ **Method**, bir struct örneği (instance) üzerinde çalışan fonksiyondur.
+ Bu yüzden mutlaka **self**, `&self` veya `&mut self` parametresi alır.

> [!NOTE]
> ✔ Özellikler
> + Bir **örnek** üzerinde çalışır.
> + Çağrılırken **nokta kullanılır**: `instance.method()`

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect = Rectangle { width: 30, height: 50 };
    println!("Alan: {}", rect.area());
}
```

> + `area()` bir metottur, çünkü `&self` alıyor.

🟥 **Associated Function ve Method Arasındaki Fark**

|Özellik|Associated Function|Method|
|---|---|---|
|**self alır mı?**|❌ Hayır|✔ Evet|
|**Nereden çağrılır?**|Tip adıyla: `Type::function()`|Örnek ile: `value.method()`|
|**Ne işe yarar?**|Genelde constructor, yardımcı fonksiyon|Nesne üzerinde işlem yapar|
|**Instance gerekir mi?**|❌ Hayır|✔ Evet|
#### 5.3.4.3. 🟧 Son Kıyas Örneği

```rust
impl Rectangle {
    // associated function
    fn square(size: u32) -> Rectangle {
        Rectangle { width: size, height: size }
    }

    // method
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let sq = Rectangle::square(10);  // Associated function çağrısı
    println!("{}", sq.area());       // Method çağrısı
}
```

### 5.3.5. Birden Fazla impl Bloğu:

+ Her struct’ın birden fazla `impl` bloğuna sahip olmasına izin verilir.
+ `Liste 5-15`, her metodu kendi `impl` bloğunda bulunduran `Liste 5-16`'da gösterilen koda eşdeğerdir.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```

> + `Liste 5-16`: Birden fazla `impl` bloğu kullanarak `Liste 5-15`'i yeniden yazma

> + Buradaki metotları birden fazla `impl` bloğuna ayırmak için bir sebep yok, ancak bu geçerli bir sözdizimidir. 
> + Birden fazla `impl` bloğunun işe yaradığı bir durumu, genel tipler (`generics`) ve `trait`’leri ele aldığımız **10. Bölümde** göreceğiz.

#### 5.3.6. Özet:

+ Struct’lar, alanınıza (problem alanınıza - domain) uygun, anlamlı özel türler oluşturmanıza olanak tanır.
+ Struct kullanarak birbirleriyle ilişkili veri parçalarını bir arada tutabilir ve her parçaya bir isim vererek kodunuzu daha anlaşılır hale getirebilirsiniz.
+ `impl` bloklarında, türünüzle ilişkili fonksiyonlar tanımlayabilirsiniz;
+ metotlar ise struct örneklerinin(`instance`) nasıl davranacağını belirlemenizi sağlayan bir tür ilişkili fonksiyondu.
+ Ancak özel türler(`custom types`) oluşturmanın tek yolu struct’lar değildir; alet çantamıza(`toolbox`) bir başka araç eklemek için şimdi Rust’ın `enum` özelliğine bakalım.

# 6. Enum’lar ve Desen Eşleme (Pattern Matching):

+ Bu bölümde, **enumeration**'ları (numaralandırmalar) inceleyeceğiz, kısaca **enum**'lar olarak adlandırılırlar.
+ Enum’lar, bir türün sahip olabileceği olası varyantları sıralayarak bir tür tanımlamanıza olanak tanır.
+ Önce bir enum tanımlayıp kullanarak enum’ların nasıl hem anlam hem de veri içerebildiğini göstereceğiz.
	- Rust enum’ları sadece bir isimden ibaret değildir; bir varyantın içinde ekstra veri tutabilir ve böylece hem **ne** olduğunu (anlam), hem de **ilgili bilgiyi** (veri) tek bir yapıda taşıyabilir.
+ Ardından, bir değerin ya bir şey olabileceğini ya da hiçbir şey olmayabileceğini ifade eden, Option adı verilen özellikle kullanışlı bir enum’u inceleyeceğiz.
+ Daha sonra, `match` ifadesindeki **pattern matching** (desen eşleme) özelliğinin, bir `enum`'un farklı değerleri için farklı kodlar çalıştırmayı nasıl kolaylaştırdığına bakacağız.
+ Son olarak, `if let` yapısının kodunuzdaki enum'ları yönetmek için mevcut olan başka bir kullanışlı ve özlü ifade biçimi olduğunu ele alacağız.

## 6.1. Bir `enum` tanımlama:

+  Struct’lar, bir Rectangle’ın genişliği ve yüksekliği gibi birbiriyle ilişkili alanları ve verileri bir araya getirmenizi sağlarken, enum’lar bir değerin belirli olası değerlerden biri olduğunu ifade etmenize olanak tanır.
+ **Örneğin, Rectangle’ın Circle (daire) ve Triangle (üçgen) gibi çeşitli şekillerden biri olduğunu söylemek isteyebiliriz. Bunu yapmak için Rust, bu olasılıkları bir enum olarak ifade etmemize izin verir.**
	- Bu cümleyi aşağıdaki Note açıklamıştır.


> [!NOTE]
> #### 1. Struct ve Enum Arasındaki Fark Ne?
> ##### 1. Struct → Birbiriyle ilişkili verileri gruplayan yapı
> + Struct; bir nesnenin **özelliklerini** bir araya toplamak için kullanılır.
> ```rust
> struct Rectangle {
>    width: u32,
>    height: u32,
>}
> ```
> 
> Burada Rectangle, **iki parçadan oluşan bir veri paketidir**:
> + genişlik
> + yükseklik
> Burada Rectangle, **iki parçadan oluşan bir veri paketidir**:
> ---
> ##### 2. Enum → Bir değerin birden fazla mümkün durumdan biri olduğunu söyleyen yapı
> + Enum ise bir nesnenin **hangi türde/şekilde/durumda olduğunu** belirtmek içindir.
> 
> Örneğin;
> + Rectangle
> + Circle
> + Triangle
> bunların hepsi birer şekildir
> ```rust
> enum Shape {
>    Rectangle,
>    Circle,
>    Triangle,
>}
> ```
> + Yani **enum = bir değerin bir seçenekler kümesinden biri olduğu**.

+ Kodla ifade etmek isteyebileceğimiz bir duruma bakalım ve bu durumda neden `enum`’ların yararlı ve `struct`’lara göre daha uygun olduğunu görelim.
+ Diyelim ki IP adresleriyle çalışmamız gerekiyor. Günümüzde IP adresleri için iki ana standart kullanılıyor: sürüm dört ve sürüm altı.
+ Programımızın karşılaşacağı bir IP adresi için tek olasılıklar bunlar olduğundan, tüm olası varyantları sıralayabiliriz; numaralandırmanın adı da buradan gelir.
	- Yani, Programımızın karşılaşabileceği IP adresleri yalnızca bu iki olasılıktan oluştuğu için, tüm olası varyantları tek tek sıralayabiliriz; işte `enumeration` (enumerasyon) adı da buradan gelir.
+ Her IP adresi ya sürüm dört ya da sürüm altı olabilir, ancak aynı anda ikisi birden olamaz.
+ IP adreslerinin bu özelliği, enum veri yapısını uygun hâle getirir çünkü bir enum değeri yalnızca kendi varyantlarından biri olabilir.
+ Hem sürüm dört hem de sürüm altı adresler temelde birer IP adresidir; bu nedenle, kod herhangi bir IP adresi türü için geçerli durumu ele alırken, bunlar aynı tür olarak değerlendirilmelidir.



> [!NOTE]
> #### 2. Struct ve Enum Arasındaki Fark Ne?
> + IP adreslerinin iki türü vardır:
> 	- IPv4
> 	- IPv6
> + Bir IP adresi **aynı anda ikisi birden olamaz** — ya IPv4’tür ya da IPv6.
> 
> Bu özellik tam olarak enum’ların çalışma şekline uyar:
> - Bir enum değeri **bir seçenekler kümesinden sadece bir tanesi** olabilir.
> 
> Bu yüzden Rust’ta IP adreslerini şöyle bir enum ile ifade etmek **doğru ve mantıklı** olur:
> ```rust
> enum IpAddrKind {
>    V4,
>    V6,
>}
> ```
> ##### Peki neden struct değil?
> + Struct birden fazla veriyi aynı anda tutmak içindir.
> + Ama burada IP adresi **aynı anda hem IPv4 hem IPv6 olamaz**, dolayısıyla struct doğru model olmaz.
> + Enum ise **“bu seçeneklerden biridir”** demek için tasarlanmıştır.

+ Bu kavramı kodda ifade etmek için bir `IpAddrKind enum`’u tanımlayıp bir IP adresinin alabileceği olası türleri — V4 ve V6 — listeleyebiliriz. Bunlar `enum`’un varyantlarıdır.

```rust
enum IpAddrKind {               // <---
    V4,                         // <--- 
    V6,                         // <---
}                               // <---

fn main() {
    let four = IpAddrKind::V4;
    let six = IpAddrKind::V6;

    route(IpAddrKind::V4);
    route(IpAddrKind::V6);
}

fn route(ip_kind: IpAddrKind) {}
```

> + `IpAddrKind` artık kodumuzun başka yerlerinde kullanabileceğimiz özel bir veri türüdür.

### 6.1.1. Enum Değerleri:

+ `IpAddrKind`’in iki varyantının her birinden örnekleri(`instances`) şu şekilde oluşturabiliriz:

```rust
enum IpAddrKind {
    V4,
    V6,
}

fn main() {
    let four = IpAddrKind::V4;     // <---  1. instance
    let six = IpAddrKind::V6;      // <---  2. instance

    route(IpAddrKind::V4);
    route(IpAddrKind::V6);
}

fn route(ip_kind: IpAddrKind) {}
```


> [!CAUTION]
> + Enum’un varyantlarının kendi tanımlayıcısı (ismi) altında ad alanına(`namespace`) alındığını ve ikisini ayırmak için çift iki nokta (`::`) kullandığımızı unutmayın
> 	- Yani, Enum içindeki seçenekler (varyantlar), enum’un adıyla bir ad alanı(`namespace`) içinde bulunur ve bunlara erişirken `::` kullanırız.
> + Bu, kullanışlıdır çünkü artık `IpAddrKind::V4` ve `IpAddrKind::V6` değerlerinin her ikisi de aynı türdendir: `IpAddrKind`.
> + Böylece, örneğin, herhangi bir `IpAddrKind` alan bir fonksiyon tanımlayabiliriz.

```rust
enum IpAddrKind {
    V4,
    V6,
}

fn main() {
    let four = IpAddrKind::V4;
    let six = IpAddrKind::V6;

    route(IpAddrKind::V4);
    route(IpAddrKind::V6);
}

fn route(ip_kind: IpAddrKind) {}   // <--- 
```

+ Ve bu fonksiyonu şu iki varyanttan biriyle çağırabiliriz:

```rust
enum IpAddrKind {
    V4,
    V6,
}

fn main() {
    let four = IpAddrKind::V4;
    let six = IpAddrKind::V6;

    route(IpAddrKind::V4); // 1. Varyant
    route(IpAddrKind::V6); // 2. Varyant
}

fn route(ip_kind: IpAddrKind) {}
```

> + Enum kullanmanın daha da fazla avantajı vardır.
> + IP adresi türümüz hakkında biraz daha düşündüğümüzde, şu anda gerçek IP adresi verisini saklayabileceğimiz(depolayabileceğimiz) bir yolumuz olmadığını fark ediyoruz; sadece hangi türde olduğunu biliyoruz.
> + 5. bölümde yeni öğrendiğiniz yapıları (_struct_) düşündüğünüzde, bu problemi 6-1 numaralı listede gösterildiği gibi struct kullanarak çözmeye çalışmak isteyebilirsiniz.

```rust
fn main() {
    enum IpAddrKind {
        V4,
        V6,
    }

    struct IpAddr {
        kind: IpAddrKind,
        address: String,
    }

    let home = IpAddr {
        kind: IpAddrKind::V4,
        address: String::from("127.0.0.1"),
    };

    let loopback = IpAddr {
        kind: IpAddrKind::V6,
        address: String::from("::1"),
    };
}
```

> + `Liste 6-1:` Bir IP adresinin verisini ve `IpAddrKind` varyantını bir struct kullanarak saklamak

> Burada iki alanı olan bir **IpAddr** struct’ı tanımladık:
> + **kind** alanı, daha önce tanımladığımız **IpAddrKind** enum türündedir.
> + **address** alanı ise **String** türündedir.
> 
> Bu struct’tan iki örnek oluşturduk.
> + İlk örnek **`home`**’dur ve **`IpAddrKind::V4`** değerini `kind` olarak taşır; buna karşılık gelen adres verisi **`"127.0.0.1"`**’dir.
> + İkinci örnek **loopback**’tir. Bu örnekte `kind` değeri olarak `enum`’ın diğer varyantı olan **V6** kullanılmıştır ve buna karşılık gelen adres verisi **"::1"** şeklindedir.
> + Bu şekilde, bir struct kullanarak **IP adresinin türünü** ve **adres değerini** bir arada tutmuş olduk; yani artık tür (V4 veya V6) ile adres verisi birlikte saklanıyor.

+ Ancak aynı kavramı yalnızca bir **`enum`** kullanarak ifade etmek çok daha sade bir yapıdır:
	- Bir `struct` içinde `enum` kullanmak yerine, veriyi doğrudan `enum` varyantlarının içine koyabiliriz.
	- **`IpAddr`** `enum`’ının bu yeni tanımı, hem **`V4`** hem de **`V6`** varyantlarının kendilerine bağlı birer **`String`** değeri taşıyacağını belirtmektedir.

```rust
fn main() {
    enum IpAddr {
        V4(String),
        V6(String),
    }

    let home = IpAddr::V4(String::from("127.0.0.1"));

    let loopback = IpAddr::V6(String::from("::1"));
}
```

> + Verileri her bir `enum` varyantına doğrudan ekliyoruz, bu yüzden ekstra bir `struct`’a ihtiyaç kalmıyor.
> + Ayrıca burada `enum`’ların nasıl çalıştığıyla ilgili başka bir detayı da görmek daha kolay: tanımladığımız her enum varyantının adı, aynı zamanda `enum`’ın bir örneğini oluşturan bir fonksiyon hâline gelir.
> + Yani, `IpAddr::V4()` bir `String` argümanı alan ve `IpAddr` türünün bir örneğini döndüren bir fonksiyon çağrısıdır.
> + **Bu kurucu fonksiyonu (`constructor`) `enum`’ı tanımladığımız anda otomatik olarak elde ederiz.**
> 	- Yani, Enum'u tanımlamamızın sonucunda bu constructor fonksiyonunu otomatik olarak elde ederiz.



> [!NOTE]
> #### 📌 Enum Varyantları Nasıl Fonksiyon Oluyor?
> Aşağıdaki enum’ı ele alalım:
> ```rust
> enum IpAddr {
>    V4(String),
>    V6(String),
>}
> ```
> Burada
> + `V4` **bir fonksiyon gibi davranır**.
> + `V6` **bir fonksiyon gibi davranır**.
> 
> Rust derleyicisi, sen bu enum’ı tanımladığın anda otomatik olarak şu imzaları üretmiş olur:
> ```rust
> fn V4(arg: String) -> IpAddr
> fn V6(arg: String) -> IpAddr
> ```
> 
> Tabii bunlar `IpAddr` ad alanı (namespace) altındadır, yani tam hâli:
> ```rust
> IpAddr::V4(String) -> IpAddr
> IpAddr::V6(String) -> IpAddr
> ```
> ---
> #### Örnek Kullanım:
> ```rust
> fn main() {
>    let home = IpAddr::V4(String::from("127.0.0.1"));
>    let loopback = IpAddr::V6(String::from("::1"));
>
>    println!("IPv4: {:?}", home);
>    println!("IPv6: {:?}", loopback);
>}
> ```
> 
> Burada olan
> + `IpAddr::V4("127.0.0.1".to_string())`
> 	→ bir **fonksiyon çağrısıdır**, ve `IpAddr::V4` varyantını içeren bir `IpAddr` döndürür.
> + `IpAddr::V6("::1".to_string())`
> 	→ yine bir **fonksiyon çağrısıdır**, ve `IpAddr` döndürür.

+ `Enum` kullanmanın, `struct` kullanmaya göre başka bir avantajı daha vardır: her bir varyant farklı türlerde ve farklı miktarlarda veri içerebilir. 
+ Örneğin, IPv4 adresleri her zaman 0 ile 255 arasında değer alan dört sayısal bileşenden oluşur. 
+ IPv4 adreslerini dört adet `u8` değeri olarak saklamak, ancak IPv6 adreslerini tek bir `String` olarak ifade etmek isteseydik, bunu bir `struct` ile yapamazdık. 
+ `Enum`’lar ise bu durumu kolayca çözebilir:

```rust
fn main() {
    enum IpAddr {
        V4(u8, u8, u8, u8),
        V6(String),
    }

    let home = IpAddr::V4(127, 0, 0, 1);

    let loopback = IpAddr::V6(String::from("::1"));
}
```

> + Dördüncü ve altıncı versiyon IP adreslerini saklamak için veri yapıları tanımlamanın birkaç farklı yolunu gösterdik.
> + Ancak görünen o ki, IP adreslerini saklamak ve hangi türden olduklarını kodlamak o kadar yaygın bir ihtiyaç ki, [standart kütüphanede kullanabileceğimiz hazır bir tanım var!](https://doc.rust-lang.org/std/net/enum.IpAddr.html)
> + Gelin standart kütüphanenin `IpAddr`'ı nasıl tanımladığına bakalım: bizim tanımlayıp kullandığımız `enum` ve varyantların tıpatıp aynısına sahip, ancak adres verisini varyantların içine, her varyant için farklı şekilde tanımlanmış iki ayrı `struct` biçiminde gömüyor:

```rust
#![allow(unused)]
fn main() {
struct Ipv4Addr {
    // --snip--
}

struct Ipv6Addr {
    // --snip--
}

enum IpAddr {
    V4(Ipv4Addr),
    V6(Ipv6Addr),
}
}
```

> + Bu kod, bir `enum` varyantının içine her türlü veriyi koyabileceğinizi gösteriyor: örneğin `string`'ler, sayısal tipler veya `struct`'lar. 
> + Hatta başka bir `enum` bile ekleyebilirsiniz! Ayrıca, standart kütüphane tipleri çoğu zaman sizin aklınıza gelebilecek çözümlerden çok daha karmaşık değildir.


> [!CAUTION]
> + Standart kütüphane `IpAddr` için bir tanım içerse bile, standart kütüphanenin tanımını kendi kapsamımıza(`scope`) dahil etmediğimiz için çakışma olmadan kendi tanımımızı(`scope`) oluşturup kullanabileceğimizi unutmayın. 
> + Türleri kapsama(`scope`) dahil etme konusunu 7. Bölüm'de daha ayrıntılı ele alacağız.

+ `Liste 6-2`'deki başka bir `enum` örneğine bakalım: bu örnekte varyantların içine gömülmüş çok çeşitli tipler bulunuyor.

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn main() {}
```

> Liste 6-2: Varyantlarının her biri farklı miktarda ve tipte değer saklayan bir `Message` `enum`'u

> Bu `enum`'un farklı tiplere sahip dört varyantı var:
> + `Quit`: Kendisiyle ilişkili hiçbir veri yok
> + `Move`: Tıpkı bir `struct` gibi isimlendirilmiş alanlara sahip
> + `Write`: Tek bir `String` içeriyor.
> + `ChangeColor`: Üç adet `i32` değeri içeriyor

+ `Liste 6-2`'deki gibi varyantlara sahip bir `enum` tanımlamak, farklı türde `struct` tanımlamaya benzer; tek fark `enum`'un `struct` anahtar kelimesini kullanmaması ve tüm varyantların `Message` tipi altında bir arada gruplanmış olmasıdır. 
+ Aşağıdaki `struct`'lar, önceki `enum` varyantlarının tuttuğu verilerin aynısını tutabilir:

```rust
struct QuitMessage; // unit struct
struct MoveMessage {
    x: i32,
    y: i32,
}
struct WriteMessage(String); // tuple struct
struct ChangeColorMessage(i32, i32, i32); // tuple struct

fn main() {}
```

+ Ancak her biri kendi tipine sahip farklı `struct`'lar kullansaydık, `Liste 6-2`'de tanımlanan ve tek bir tip olan `Message` `enum`'u ile yapabildiğimiz kadar kolay bir şekilde bu mesaj türlerinden herhangi birini alan bir fonksiyon tanımlayamazdık.
	- Yani `enum`'un avantajı: farklı veri yapılarını tek bir tip altında toplayarak, hepsini aynı fonksiyona parametre olarak geçirebilmeni sağlaması.

+ `Enum`'lar ve `struct`'lar arasında bir benzerlik daha var: tıpkı `impl` kullanarak `struct`'lar üzerinde metodlar tanımlayabildiğimiz gibi, `enum`'lar üzerinde de metodlar tanımlayabiliriz.

```rust
fn main() {
    enum Message {
        Quit,
        Move { x: i32, y: i32 },
        Write(String),
        ChangeColor(i32, i32, i32),
    }

    impl Message {
        fn call(&self) {
            // method body would be defined here
        }
    }

    let m = Message::Write(String::from("hello"));
    m.call();
}
```

> + Metodun gövdesi, metodu çağırdığımız değeri almak için `self`'i kullanacaktır.
> + Bu örnekte, `Message::Write(String::from("hello"))` değerine sahip `m` adında bir değişken oluşturduk ve `m.call()` çalıştığında `call` metodunun gövdesindeki `self` işte bu değer olacaktır.
> + Standart kütüphanede çok yaygın ve kullanışlı olan başka bir `enum`'a bakalım: `Option`.

### 6.1.2. `Option` Enum'u ve Null Değerlere Göre Avantajları:

+ Bu bölüm, standart kütüphane tarafından tanımlanan başka bir `enum` olan `Option`'ın bir vaka çalışmasını inceler. 
+ `Option` tipi, bir değerin bir şey olabileceği veya hiçbir şey olamayacağı çok yaygın senaryoyu kodlar.
	- Yani, _Option_ türü, bir değerin bazen bir şey olabileceği bazen ise hiç olmayabileceği çok yaygın senaryoyu ifade eder.


> [!CAUTION]
> + Örneğin, boş olmayan bir listeden ilk elemanı isterseniz bir değer elde edersiniz. Boş bir listeden ilk elemanı isterseniz hiçbir şey elde etmezsiniz.
> + Bu konsepti tip sistemi açısından ifade etmek, derleyicinin ele almanız gereken tüm durumları ele alıp almadığınızı kontrol edebileceği anlamına gelir; bu işlevsellik, diğer programlama dillerinde son derece yaygın olan hataları önleyebilir.
> + ❌ **Diğer dillerde (ör: Python, Java, JS…)**
> + Eğer liste boşsa:
> ```text
> NullPointerException
> IndexError
> undefined erişimi
> runtime error
> ```
> + Hata program çalışırken patlar.

+ Programlama dili tasarımı genellikle hangi özellikleri dahil ettiğiniz açısından düşünülür, ancak hariç tuttuğunuz özellikler de önemlidir.
+ Rust, birçok diğer dilin sahip olduğu `null` özelliğine sahip değildir. `Null`, orada hiçbir değer olmadığı anlamına gelen bir değerdir.
+ `Null` olan dillerde, değişkenler her zaman iki durumdan birinde olabilir: `null` veya null-olmayan.


> [!NOTE]
> Tony Hoare, null'ın mucidi, 2009'daki "Null Referanslar: Milyar Dolarlık Hata" sunumunda şunları söyledi:
> 
> Buna benim milyar dolarlık hatam diyorum. O zamanlar, nesne yönelimli bir dilde referanslar için ilk kapsamlı tip sistemini tasarlıyordum. Amacım, tüm referans kullanımlarının kesinlikle güvenli olmasını sağlamak ve kontrolün derleyici tarafından otomatik olarak yapılmasını sağlamaktı. Ancak null referans ekleme cazibesine karşı koyamadım, çünkü uygulaması çok kolaydı. Bu, son kırk yılda muhtemelen milyar dolarlık acıya ve hasara neden olan sayısız hataya, güvenlik açığına ve sistem çökmesine yol açtı.

+ `Null` değerlerle ilgili sorun şu ki, bir `null` değeri null-olmayan(`not-null`) bir değer olarak kullanmaya çalışırsanız, bir tür hata alırsınız.
+ Bu `null` veya null-olmayan(`not-null`) özellik her yerde olduğu için, bu tür bir hatayı yapmak son derece kolaydır.
+ Ancak, `null`'ın ifade etmeye çalıştığı konsept hala faydalı bir konsepttir: `null`, bir nedenden ötürü şu anda geçersiz veya mevcut olmayan bir değerdir.
+ Sorun aslında konseptin kendisiyle değil, özel implementasyonla(uygulanmasıyla) ilgilidir.
+ Bu nedenle, Rust'ta `null`'lar yoktur, ancak bir değerin mevcut olması veya olmaması konseptini kodlayabilen bir `enum` vardır.
+ Bu enum `Option<T>`'dir ve [standart kütüphane tarafından](https://doc.rust-lang.org/std/option/enum.Option.html) şu şekilde tanımlanır:

```rust
#![allow(unused)]
fn main() {
enum Option<T> {
    None,
    Some(T),
}
}
```

+ `Option<T>` `enum`'u o kadar kullanışlıdır ki prelude'a bile dahil edilmiştir; onu açıkça kapsama dahil etmenize gerek yoktur. Varyantları da prelude'a dahildir: `Some` ve `None`'ı doğrudan `Option::` öneki olmadan kullanabilirsiniz.`Option<T>` enum'u yine de sadece normal bir `enum`'dur ve `Some(T)` ile `None`, hala `Option<T>` tipinin varyantlarıdır.
+ Yani, `Option<T>` enum'u o kadar faydalıdır ki, Rust'ın prelude'una (otomatik olarak her programa dahil edilen standart kütüphane bölümüne) dahil edilmiştir; yani onu açıkça içe aktarmanıza (import etmenize) gerek yoktur. Varyantları da prelude'a dahildir: `Some` ve `None`'ı `Option::` öneki koymadan doğrudan kullanabilirsiniz. Bununla birlikte, `Option<T>` enum'u yine de sıradan bir enum'dur ve `Some(T)` ile `None` hala `Option<T>` tipine ait varyantlardır.
+ **Yani kısaca:** Normalde bir enum'u kullanmak için önce `use` ile içe aktarman gerekir. Ama `Option` o kadar yaygın kullanılır ki, Rust onu otomatik olarak her programa dahil ediyor. Bu yüzden direkt `Some(5)` veya `None` yazabiliyorsun, `Option::Some(5)` yazmana gerek kalmıyor.

> [!NOTE]
> #### Prelude Nedir?
> + **Prelude**, Rust'ın her programa otomatik olarak dahil ettiği standart kütüphane öğelerinin bir koleksiyonudur.
> + Yani, Normalde bir kütüphaneden bir şey kullanmak istediğinde önce onu içe aktarman gerekir:
> ```rust
> use std::collections::HashMap; // Bunu yazmak zorundasın
>
> fn main() {
>    let map = HashMap::new();
>}
> ```
> + Ama bazı şeyler o kadar sık kullanılır ki, Rust der ki "bunları her seferinde `use` ile yazmana gerek yok, ben otomatik olarak dahil ediyorum." 
> + İşte bu otomatik dahil edilen şeylere **prelude** denir.
> ##### Prelude'da neler var?
> - `Option<T>` ve varyantları (`Some`, `None`)
> - `Result<T, E>` ve varyantları (`Ok`, `Err`)
> - `Vec<T>` (vektör)
> - `String`
> - Yaygın trait'ler (`Clone`, `Copy`, `Debug`, vb.)
> - Makrolar (`println!`, `vec!`, vb.)
> ```rust
> fn main() {
>    // Bunların hiçbirini import etmene gerek yok:
>    let x = Some(5);        // Option prelude'da
>    let y = None;           // None prelude'da
>    let v = vec![1, 2, 3];  // vec! makrosu prelude'da
>    println!("Merhaba");    // println! prelude'da
>}
> ```
> + Yani **prelude = Rust'ın "bunları çok kullanacaksın, hep hazır olsun" dediği temel araç seti.**

+ `<T>` sözdizimi, henüz bahsetmediğimiz bir Rust özelliğidir. Bu, jenerik tip parametresidir ve jenerikleri 10. Bölüm'de daha detaylı inceleyeceğiz.
+ Şimdilik bilmeniz gereken tek şey, `<T>` ifadesinin Option enum’undaki `Some` varyantının herhangi bir türden bir adet veri tutabileceği anlamına geldiğidir.
+ Ayrıca, `T` yerine kullanılan her somut türün, ortaya çıkan `Option<T>`yi tamamen farklı bir tür yaptığıdır.

> [!NOTE]
> + Her somut tip, farklı bir `Option` tipi oluşturur:
> ```rust
> let x: Option<i32> = Some(5);      // Bu Option<i32> tipi
> let y: Option<String> = Some(String::from("hey"));  // Bu Option<String> tipi
> ```
> + `Option<i32>` ile `Option<String>` **farklı tiplerdir**. Birbirinin yerine kullanamazsın:
> ```rust
> let x: Option<i32> = Some(5);
> let y: Option<String> = x;  // HATA! Tipler uyuşmuyor
> ```

+ Aşağıda sayı ve karakter türlerini tutmak için `Option` değerlerinin nasıl kullanılacağına dair örnekler bulunmaktadır.

```rust
fn main() {
    let some_number = Some(5);
    let some_char = Some('e');

    let absent_number: Option<i32> = None;
}
```

> + `some_number`'ın tipi `Option<i32>`'dir. `some_char`'ın tipi `Option<char>`'dır, bu da farklı bir tiptir. 
> + Rust bu tipleri çıkarım yapabilir(Rust'ın tipi otomatik olarak anlayabilmesi demektir.) çünkü `Some` varyantının içinde bir değer belirttik. 
> + `absent_number` için ise Rust, genel `Option` tipini belirtmemizi ister: 
> + derleyici, sadece bir `None` değerine bakarak karşılık gelen `Some` varyantının tutacağı tipi çıkarım yapamaz. 
> + Burada Rust'a `absent_number`'ın `Option<i32>` tipinde olmasını kastettiğimizi söylüyoruz.


> [!NOTE]
> **Rust'ın tipi otomatik olarak anlayabilmesi**
> ```rust
> let some_number = Some(5);
> ```
> + Burada 5 yazdığımızda Rust der ki: "5 bir `i32` sayısı, o halde `some_number`'ın tipi `Option<i32>` olmalı." Biz açıkça `: Option<i32>` yazmasak bile Rust bunu **kendisi anlar veya çıkarım yapar.**
> 
> **Çıkarım Yapma Durumu(tip belirtmeye gerek yok)**
> ```rust
> let some_number = Some(5);        // Rust: "5 gördüm, demek ki Option<i32>"
> let some_char = Some('z');        // Rust: "'z' gördüm, demek ki Option<char>"
> ```
> 
>  **Çıkarım Yapamama Durumu(tip belirtme gerekir)**
>  ```rust
>  let absent_number = None;  // HATA! Rust: "None görüyorum ama ne tipi?"
>  ```
>  + `None` içinde değer yok, bu yüzden Rust "bu `Option<i32>` mi, `Option<String>` mi, yoksa başka bir şey mi?" bilemez. Geliştiricin söylemesi gerekir:
>  ```rust
>  let absent_number: Option<i32> = None;  // Şimdi Rust anladı: Option<i32>
>  ```


> [!NOTE]
> **Option türünü _manuel olarak_ belirleme:**
> 
> ```rust
> let a: Option<i32> = Some(5);
> let b: Option<String> = Some(String::from("hello"));
> let c: Option<f64> = None;
> ```

+ Bir `Some` değerine sahip olduğumuzda, bir değerin mevcut olduğunu ve bu değerin `Some` içinde tutulduğunu biliriz.
+ Bir `None` değerine sahip olduğumuzda, bir anlamda bu `null` ile aynı şey demektir: geçerli bir değerimiz yoktur.
+ Peki `Option<T>`'ye sahip olmak, `null`'a sahip olmaktan neden daha iyidir?
+ Kısacası, `Option<T>` ve `T` (burada `T` herhangi bir tip olabilir) farklı tipler olduğu için, derleyici bir `Option<T>` değerini kesinlikle geçerli bir değermiş gibi kullanmamıza izin vermez.
+ Örneğin, bu kod derlenmeyecektir, çünkü bir `i8`'i bir `Option<i8>`'e eklemeye çalışıyor:

```rust
fn main() {
    let x: i8 = 5;
    let y: Option<i8> = Some(5);

    let sum = x + y;
}
```

> Bu kodu çalıştırdığımızda aşağıdaki gibi bir hata mesajı alırız:

```
$ cargo run
   Compiling enums v0.1.0 (file:///projects/enums)
error[E0277]: cannot add `Option<i8>` to `i8`
 --> src/main.rs:5:17
  |
5 |     let sum = x + y;
  |                 ^ no implementation for `i8 + Option<i8>`
  |
  = help: the trait `Add<Option<i8>>` is not implemented for `i8`
  = help: the following other types implement trait `Add<Rhs>`:
            `&i8` implements `Add<i8>`
            `&i8` implements `Add`
            `i8` implements `Add<&i8>`
            `i8` implements `Add`

For more information about this error, try `rustc --explain E0277`.
error: could not compile `enums` (bin "enums") due to 1 previous error
```

+ **Yoğun bir durum!** Aslında bu hata mesajı bize şunu söylüyor: Rust, bir `i8` ile bir `Option<i8>` toplamanın nasıl yapılacağını anlamıyor, çünkü bunlar **farklı türler**.
+ Rust’ta elimizde `i8` gibi bir türden bir değer varsa, derleyici her zaman geçerli (valid) bir değere sahip olduğumuzu garanti eder.
+ Bu nedenle, bu değeri kullanmadan önce “acaba null mı?” diye kontrol etmemiz gerekmez.
+ Ancak elimizde bir `Option<i8>` (veya hangi türle çalışıyorsak onun `Option`’ı) varsa, **değerin bulunmama ihtimali** vardır ve işte bu durumda derleyici, değeri kullanmadan önce bu olasılığı doğru şekilde ele almanızı zorunlu kılar.


> [!NOTE]
> Paragrafı **çok net bir örnekle** açıklayayım.
> #### 📌 Option ile i8’in Farkı — Yukarıdaki Kod
> Temel fikir:
> - `i8` → **Her zaman bir sayı vardır.**
> - `Option<i8>` → **Ya bir sayı vardır (`Some`), ya da hiç yoktur (`None`).**
> - Rust, bu iki türü karıştırmaz ve karıştırmanı da engeller. Yani, `i8` ile `Option<i8>` toplayamazsın.
> - Çünkü;
> 	+ `x` → kesin bir sayı (i8).
> 	+ `y` → sayı olabilir ama olmayabilir; Rust bunu **sana zorla kontrol ettiriyor.**
> #### ✔️ Doğru kullanım:
> ```rust
> fn main() {
>    let x: i8 = 5;
>    let y: Option<i8> = Some(5);
>
>    let result = match y {
>        Some(value) => x + value,
>        None => x, // ya da başka bir işlem
>    };
>
>    println!("{}", result);
>}
> ```
>  + **Dikkat:** `match` anahtar kelimesi sonraki konuda anlatılacaktır.
> #### 🔍 Ne oluyor burada?
> - Eğer `y = Some(3)` → sonuç `5 + 5 = 10`
> - Eğer `y = None` → sayı yok, Rust seni bunu düşünmeye zorluyor

+ **Başka bir deyişle,** bir `Option<T>` üzerinde çalışmadan önce onu mutlaka bir `T` türüne dönüştürmen gerekir; ancak ondan sonra `T` türüne ait işlemleri yapabilirsin.
+ Genel olarak bu, null ile ilgili en yaygın sorunlardan birini yakalamaya yardımcı olur:  **Bir şeyin null olmadığını varsaymak ama aslında null olması.**


> [!NOTE]
> **Cümlede anlatılmak istenen şey tam olarak şu:**
> + Rust, seni `Option<T>` değerini önce işleyip içindeki gerçek `T` değerini _güvenli şekilde çıkarmaya_ zorluyor.
> + Böylece diğer dillerdeki şu klasik hatayı engelliyor:
> 	- "Ben burada değer vardır diye düşündüm ama aslında yokmuş! (`null` hatası)"
> + Rust buna asla izin vermiyor.

+ Null olmayan(`not-null`) bir değeri yanlışlıkla `null` olarak varsayma riskinin ortadan kaldırılması, kodunuzda daha emin olmanızı sağlar.
+ Bir değerin **muhtemelen null olabileceğini** ifade etmek istiyorsanız, bunu açıkça belirtmeniz gerekir: yani değerin türünü `Option<T>` olarak tanımlamalısınız.
+ Sonra bu değeri kullandığınızda, derleyici sizi **değerin null olabileceği durumu açıkça ele almaya** zorlar.
+ Bir değerin türü `Option<T>` değilse, o değerin **null olmadığını güvenle varsayabilirsiniz**.

+ **Peki, elinizde bir `Option<T>` değeri olduğunda ve bu değer `Some` varyantındaysa, içindeki `T` değerini nasıl çıkarıp kullanabilirsiniz?**
+ `Option<T>` `enum`’unun, farklı durumlarda çok kullanışlı olabilecek **birçok metodu** vardır; bunları [belgelerinde](https://doc.rust-lang.org/std/option/enum.Option.html) inceleyebilirsiniz.
+ `Option<T>` üzerindeki metodlara hakim olmak, Rust ile yolculuğunuzda **son derece faydalı** olacaktır.

+ Genel olarak, bir `Option<T>` değerini kullanabilmek için, `enum`’un **her iki varyantını da ele alan** bir koda ihtiyacınız vardır.
	- **`Some(T)`** olduğu durumda çalışacak bir koda ihtiyaç duyarsınız ve bu kod, içindeki **T değerini** kullanabilir.
	- **`None`** olduğu durumda çalışacak farklı bir koda ihtiyaç duyarsınız ve bu durumda kullanabileceğiniz bir **T değeri yoktur**.
+ `match` ifadesi, özellikle `enum`’larla birlikte kullanıldığında, tam olarak bunu yapan bir kontrol akışı yapısıdır: Hangi `enum` varyantının kullanıldığına bağlı olarak **farklı kodların çalışmasını sağlar** ve eşleşen varyantın içindeki veriyi kullanmanıza olanak tanır.



## 6.2. `match` Kontrol Akışı Yapısı

+ Rust, bir değeri çeşitli desenlerle (`pattern`) karşılaştırmanıza ve hangi desenle eşleştiğine göre kod çalıştırmanıza imkân tanıyan **son derece güçlü bir kontrol akışı yapısı** olan `match` ifadesine sahiptir.
+ Desenler; **sabit değerlerden**, **değişken isimlerinden**, **joker karakterlerden (`wildcards`)** ve daha birçok şeyden oluşabilir.
+ Bu desen çeşitlerinin tamamı ve ne işe yaradıkları **Bölüm 19'da** ayrıntılı şekilde ele alınmaktadır.
+ `match` ifadesini güçlü yapan şey, desenlerin ifade gücü ve **derleyicinin tüm olası durumların ele alındığını doğrulamasıdır**.

> [!NOTE]
> #### Match neden güçlü?
> + Tüm enum varyantlarını **ele almanı** zorunlu kılar.
> + Rust garantiler: "Her olasılığı kontrol etmiş misin?"
> 
> Bu da daha güvenli kod demektir.

+ Bir `match` ifadesini, **bozuk para ayırma makinesi** gibi düşünebilirsiniz:
	- Paralar, çeşitli boyutlarda deliklerin bulunduğu bir kanaldan kayar ve her para, karşılaştığı ilk deliğe uyarak içinden düşer.
+ Aynı şekilde, bir `match` ifadesinde değerler de her deseni sırayla kontrol eder ve **değerin “uyduğu” ilk desende**, değer ilgili kod bloğuna düşer ve çalıştırma sırasında o blokta kullanılır.
+ Bozuk paralardan söz etmişken, **`match`** kullanımını göstermek için onları örnek olarak kullanalım!
+ Bilinmeyen bir ABD bozuk parasını alan ve tıpkı bozuk para sayma makinesi gibi, **bu paranın hangi tür olduğunu belirleyip değerini sent cinsinden döndüren** bir fonksiyon yazabiliriz. Bu, **`Liste 6-3`**’te gösterilmiştir.

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,   // return 1
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

fn main() {}
```

> Liste 6-3: Bir enum ve enum'un varyantlarını desen olarak kullanan bir match ifadesi

> + **`value_in_cents`** fonksiyonundaki **`match`** ifadesini parçalara ayıralım.
> + Önce **match** anahtar kelimesini ve ardından bir ifade yazarız; bu örnekte ifade **coin** değeridir.
> + Bu, `if` ile kullanılan koşullu ifadeye çok benziyor gibi görünür, ancak büyük bir fark var:
> 	- **`if`** ifadesinde koşulun `Boolean (true/false)` bir değeri değerlendirilmesi gerekir,
> 	- **ama `match` ifadesinde koşul herhangi bir tür olabilir.**
> + Bu örnekteki `coin`'in tipi, ilk satırda tanımladığımız `Coin enum`'udur.

> + Sırada **`match` kolları (arms)** vardır.  Bir kolun iki parçası bulunur: **bir desen (`pattern`)** ve **bazı kodlar**.
> + Buradaki ilk kolun deseni **`Coin::Penny`** değeridir ve ardından, deseni çalıştırılacak koddan ayıran **`=>`** operatörü gelir.
> 	- Bu durumda kod sadece `1` değeridir.
> + Her bir kol, bir sonrakinden **virgül** ile ayrılır.


> [!NOTE]
> #### Bir match kolu (arm) nedir?
> Bir kol iki parçadan oluşur:
> ```rust
> Coin::Penny => 1,
   ^ desen       ^ kod
> ```
> 
> + **Desen (pattern)**: `Coin::Penny`
> 	→ Eğer `coin` değişkeni Penny ise…
> + **Kod (expression/block)**: `1`
> 	→ Bu kol seçilir ve `1` değeri return edilir.
> 
> Her match kolu, bir eşleştirme deseni (Penny, Nickel, Dime...) ve bu eşleşme gerçekleştiğinde çalıştırılacak koddan (1, 5, 10...) oluşur.

+ `Match` ifadesi çalıştığında, ortaya çıkan değer her bir kolun (`arm`’ın) deseniyle sırayla karşılaştırılır.
+ Eğer bir desen değerle eşleşirse, o desenle ilişkili kod çalıştırılır.
+ Eğer desen değerle eşleşmezse, tıpkı bir bozuk para ayıklama makinesinde olduğu gibi yürütme bir sonraki kola geçmeye devam eder.
+ İhtiyacımız olduğu kadar çok `match` kolu kullanabiliriz: 6-3 numaralı listede, `match` ifademizde dört tane kol bulunmaktadır.
+ Her kol ile ilişkili kod bir **ifadedir (`expression`)** ve eşleşen kolun ifadesinin **oluşan değeri**, tüm `match` ifadesinin döndürdüğü değer olur.
	- `match`’in her kolundaki kod bir ifade olup, o kol eşleştiğinde o ifade çalışır ve `match`’in **sonucu olarak döner**.


> [!NOTE]
> Burada **ifade (expression)** kısmı **`1`**’dir, yani match kolunun sağ tarafındaki değer veya kod bloğu.
> 
> - `Coin::Penny` → Bu **desen (pattern)**’dir, yani eşleşme için kontrol edilen kısmı gösterir.
> - `1` → Bu **ifade (expression)**’dir, yani eşleşme gerçekleşirse çalıştırılan ve match’in sonucu olan kısımdır.
> ```rust
> Coin::Penny => 1,
> ```
> 
> Yani özetle:
> + **`Coin::Penny`** → desendir (hangi duruma uyduğunu kontrol eder)
> + **1** → ifadedir (eşleşirse döndürülecek değer)

+ Genellikle, `match` kolundaki kod kısa ise süslü parantez `{}` kullanmayız; tıpkı **6-3 numaralı listede** olduğu gibi, her kol sadece bir değer döndürüyorsa.
+ Eğer bir `match` kolunda **birden fazla satır kod çalıştırmak** istiyorsanız, süslü parantez kullanmanız gerekir ve bu durumda kolun sonundaki virgül isteğe bağlıdır.
+ Örneğin, aşağıdaki kod, her `Coin::Penny` ile çağrıldığında **“Lucky penny!”** yazdırır, ancak yine de bloğun son değerini, yani **1**’i döndürür.

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1 // return 1;
        }
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

fn main() {}
```

### 6.2.1. Değerlere Bağlanan Desenler:

+ `Match` kollarının bir diğer yararlı özelliği, desenle eşleşen değerlerin parçalarına bağlanabilmeleridir. Enum varyantlarından değerleri bu şekilde çıkarabiliriz.
+ Örnek olarak, enum varyantlarımızdan birini içinde veri tutacak şekilde değiştirelim. 1999'dan 2008'e kadar, Amerika Birleşik Devletleri bir yüzünde 50 eyaletin her biri için farklı tasarımlara sahip çeyreklik paralar bastı. Başka hiçbir madeni para eyalet tasarımı almadı, bu yüzden sadece çeyrekliklerin bu ekstra değeri var. Bu bilgiyi `Quarter` varyantını, içinde saklanan bir `UsState` değeri içerecek şekilde değiştirerek `enum`'umuza ekleyebiliriz; bunu Liste 6-4'te yaptık.

```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn main() {}
```

> Liste 6-4: `Quarter` varyantının aynı zamanda bir `UsState` değeri de tuttuğu bir `Coin enum`'u


> [!NOTE]
> #### Örnek: ABD eyalet çeyreklik paraları
> + 1999-2008 yılları arasında ABD, her eyalet için özel tasarımlı çeyreklik paralar basmıştı. Diyelim ki Quarter paralarının hangi eyalete ait olduğunu saklamak istiyoruz:
> ```rust
> #[derive(Debug)] // println! ile yazdırabilmek için
>enum UsState {
>    Alabama,
>    Alaska,
>    // ... diğer eyaletler
>}
>
>enum Coin {
>    Penny,
>    Nickel,
>    Dime,
>    Quarter(UsState),  // Quarter'ın içinde eyalet bilgisi var!
>}
>
>fn value_in_cents(coin: Coin) -> u8 {
>    match coin {
>        Coin::Penny => 1,
>        Coin::Nickel => 5,
>        Coin::Dime => 10,
>        Coin::Quarter(state) => {  // state değişkenine eyalet bilgisi bağlanır
>            println!("Bu quarter {:?} eyaletinden!", state);
>            25
>        }
>    }
>}
>
>fn main() {
>    let coin = Coin::Quarter(UsState::Alaska);
>    let value = value_in_cents(coin);
>    println!("Değer: {} cent", value);
>}
>```
>
>**Çıktı:**
>```
>Bu quarter Alaska eyaletinden!
>Değer: 25 cent
> ```
> #### Ne oldu burada?
> 1. `Quarter(UsState::Alaska)` oluşturduk - içinde Alaska bilgisi var
> 2.  `Match`'te `Coin::Quarter(state)` yazdık
> 3.  `state` değişkeni otomatik olarak `UsState::Alaska` değerini aldı
> 4. Artık `state`'i kullanabiliyoruz!

+ Arkadaşımızın tüm 50 eyalet quarters(çeyreklik) koleksiyonunu tamamlamaya çalıştığını hayal edelim. Bozukluklarımızı madeni para türüne göre ayırırken, aynı zamanda her quarter’ın üzerinde yazan eyaletin adını da söyleyelim ki eğer arkadaşımızın koleksiyonunda olmayan bir eyalet varsa, onu koleksiyonuna ekleyebilsin.
+ Bu kod için yazdığımız `match` ifadesinde, `Coin::Quarter` varyantıyla eşleşen desene `state` adında bir değişken ekliyoruz. Bir `Coin::Quarter` değeri eşleştiğinde, `state` değişkeni o quarter’ın(çeyrekliğin) temsil ettiği eyalet değerine bağlanır. Daha sonra bu `state` değişkenini ilgili kolun (arm) içindeki kodda kullanabiliriz. Aşağıdaki gibi:

```rust
#[derive(Debug)]
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {state:?}!");
            25
        }
    }
}

fn main() {
    value_in_cents(Coin::Quarter(UsState::Alaska));
    // Çıkısı: State quarter from Alaska!
}
```

> + Eğer `value_in_cents(Coin::Quarter(UsState::Alaska))` çağrısını yapsaydık, `coin` değeri `Coin::Quarter(UsState::Alaska)` olurdu.
> + Bu değeri her bir `match` koluyla karşılaştırdığımızda, `Coin::Quarter(state)` koluna gelene kadar hiçbiri eşleşmez.
> + Bu noktada `state` değişkenine bağlanacak olan değer `UsState::Alaska` olur.
> + Ardından bu bağlamayı `println!` ifadesinde kullanabiliriz, böylece `Quarter` için `Coin` `enum` varyantının içindeki eyalet değerini çıkarmış oluruz.
> 	- Yani, Rust, `match` ile bir `Coin::Quarter` değerinin içindeki eyalet bilgisini çıkarıp kullanmamıza izin verir.


> [!NOTE]
> #### Kodda olan durum:
> ```rust
> enum Coin {
>    Penny,
>    Nickel,
>    Dime,
>    Quarter(UsState),
>}
> ```
> + `Quarter` varyantı bir değer taşır: `UsState`.
> + Yani bir çeyrek (Quarter) paranın hangi eyalete ait olduğunu içerir.
> ```rust
> Coin::Quarter(UsState::Alaska)
> ```
> + Bu, “Alaska eyaletine ait bir Quarter” demektir.
> #### `match` içerisindeki şu kısım:
> ```rust
> Coin::Quarter(state) => {
>    println!("State quarter from {:?}", state);
>    25
>}
> ```
> Burada `state` adlı değişken **Quarter varyantının içindeki veriye bağlanıyor**.
> + Eğer gelen değer `Coin::Quarter(UsState::Alaska)` ise 
> 	- → `state` değişkenine `UsState::Alaska` atanır.
> 
> Böylece:
> ```rust
> println!("State quarter from {:?}", state);
> ```
> + satırında artık **Quarter içindeki gerçek değere**, yani `UsState::Alaska`'ya erişmiş oluruz.
> 
> Rust, `match` ile bir `Coin::Quarter` değerinin içindeki eyalet bilgisini çıkarıp kullanmamıza izin verir.

### 6.2.2. `Option<T>` ile Eşleştirme


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