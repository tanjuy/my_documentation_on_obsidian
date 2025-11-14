
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