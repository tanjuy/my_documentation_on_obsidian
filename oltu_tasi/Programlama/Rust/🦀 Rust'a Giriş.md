#programlama  #rust
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

> Liste 6-3: Bir `enum` ve `enum`'un varyantlarını desen olarak kullanan bir match ifadesi

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

+ Önceki bölümde, `Option<T>` kullanırken `Some` durumunun içindeki `T` değerini almak istemiştik; `Option<T>`‘yi de tıpkı `Coin enum`’unda yaptığımız gibi `match` kullanarak ele alabiliriz! Madeni paraları karşılaştırmak yerine `Option<T>` varyantlarını karşılaştıracağız, ancak `match` ifadesinin çalışma şekli aynı kalır.
+ Diyelim ki bir `Option<i32>` alan bir fonksiyon yazmak istiyoruz ve eğer içinde bir değer varsa, bu değere 1 eklesin. Eğer içinde bir değer yoksa, fonksiyon `None` döndürsün ve herhangi bir işlem yapmaya kalkışmasın.
+ Bu fonksiyonu yazmak match sayesinde çok kolaydır ve 6-5 numaralı listede gösterildiği gibi görünecektir.

```rust
fn main() {
    fn plus_one(x: Option<i32>) -> Option<i32> {
        match x {
            None => None,
            Some(i) => Some(i + 1),
        }
    }

    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
}
```

> Liste 6-5: `Option<i32>` üzerinde bir `match` ifadesi kullanan bir fonksiyon.

+ `plus_one` fonksiyonunun ilk çalışmasını daha ayrıntılı inceleyelim.
+ `plus_one(five)` çağrısını yaptığımızda, `plus_one` fonksiyonunun içindeki `x` değişkeni `Some(5)` değerine sahip olacaktır.
+ Daha sonra bunu her bir `match` koluyla karşılaştırırız:

```rust
fn main() {
    fn plus_one(x: Option<i32>) -> Option<i32> {
        match x {
            None => None,     // <=======================
            Some(i) => Some(i + 1),
        }
    }

    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
}
```

+ `Some(5)` değeri `None` desenine (`pattern`’ine) uymadığı için bir sonraki kola geçeriz:

```rust
fn main() {
    fn plus_one(x: Option<i32>) -> Option<i32> {
        match x {
            None => None,
            Some(i) => Some(i + 1),  // <=======================
        }
    }

    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
}
```

+ Peki `Some(5)`, `Some(i)` desenine uyar mı? Uyar! Aynı varyanta sahibiz.  `i` değişkeni, `Some` içindeki değere bağlanır, yani `i` değeri 5 olur.  Ardından bu kola ait kod çalıştırılır; böylece `i` değerine 1 ekleriz ve içinde toplam 6 olan yeni bir `Some` değeri oluştururuz.
+ Şimdi de `Liste 6-5`’teki `plus_one` fonksiyonunun ikinci çağrısını ele alalım; burada `x` değeri `None`’dır.  `match` ifadesine gireriz ve ilk kola göre karşılaştırma yaparız:

```rust
fn main() {
    fn plus_one(x: Option<i32>) -> Option<i32> {
        match x {
            None => None,     // <=======================
            Some(i) => Some(i + 1),
        }
    }

    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
}
```

+ Eşleşti!(`None` ile eşleştiğini bahis etmektedir!) Ekleyebileceğimiz bir değer olmadığı için program durur ve `=>` işaretinin sağındaki `None` değerini döndürür.
+ `Match` ile `enum`’ları birleştirmek birçok durumda faydalıdır. Rust kodunda bu deseni sıkça göreceksiniz: bir `enum` ile `match` yapılır, içindeki verilere bir değişken bağlanır ve ardından buna göre kod çalıştırılır. 
+ İlk başta biraz karmaşık gelebilir, ama alıştıktan sonra keşke tüm dillerde bu özellik olsaydı diyeceksiniz. Kullanıcılar arasında sürekli favori bir yöntemdir.

### 6.2.3. `Match`’ler Tüm Olasılıkları Kapsar:

+ `Match` ifadesiyle ilgili ele almamız gereken bir diğer konu: kolların desenleri (`patterns`) tüm olasılıkları kapsamalıdır.
+ Aşağıdaki `plus_one` fonksiyonunun bu sürümünü ele alalım; bu sürümde bir hata var ve derlenmeyecektir:

```rust
fn main() {
    fn plus_one(x: Option<i32>) -> Option<i32> {
        match x {
            Some(i) => Some(i + 1),
        }
    }

    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
}
```

+ None durumunu ele almadık, bu yüzden bu kod bir hataya yol açacaktır. Neyse ki, bu Rust’un yakalayabileceği bir hata. 
+ Bu kodu derlemeye çalışırsak, şu hatayı alırız:

```
$ cargo run
   Compiling enums v0.1.0 (file:///projects/enums)
error[E0004]: non-exhaustive patterns: `None` not covered
 --> src/main.rs:3:15
  |
3 |         match x {
  |               ^ pattern `None` not covered
  |
note: `Option<i32>` defined here
 --> /rustc/4eb161250e340c8f48f66e2b929ef4a5bed7c181/library/core/src/option.rs:572:1
 ::: /rustc/4eb161250e340c8f48f66e2b929ef4a5bed7c181/library/core/src/option.rs:576:5
  |
  = note: not covered
  = note: the matched value is of type `Option<i32>`
help: ensure that all possible cases are being handled by adding a match arm with a wildcard pattern or an explicit pattern as shown
  |
4 ~             Some(i) => Some(i + 1),
5 ~             None => todo!(),
  |

For more information about this error, try `rustc --explain E0004`.
error: could not compile `enums` (bin "enums") due to 1 previous error
```

> + Rust, tüm olası durumları kapsamadığımızı ve hatta hangi deseni unuttuğumuzu bile bilir! 
> + Rust’taki `match` ifadeleri kapsayıcıdır (`exhaustive`): Kodun geçerli olabilmesi için tüm olasılıkları tüketmemiz gerekir. 
> + Özellikle `Option<T>` durumunda, Rust’ın `None` durumunu açıkça ele almayı unutmamıza izin vermemesi, elimizde bir değer olduğunu varsayıp aslında `null` olabileceği durumlara düşmemizi engeller 
> 	- Yani, Rust seni yanlış varsayımlardan koruyor. Bir değerin her zaman var olduğunu sanmana izin vermiyor; `None` ihtimalini mutlaka düşünmeni sağlıyor.
> + ve böylece daha önce bahsedilen milyar dolarlık hatanın ortaya çıkmasını imkânsız hâle getirir.


### 6.2.4. `Catch-All` Desenler ve `_` Placeholder(Yer Tutucusu)

+ Enum’ları kullanarak yalnızca birkaç özel değer için özel işlemler yapabilir, fakat diğer tüm değerler için de varsayılan bir işlem gerçekleştirebiliriz.
+ Bir oyun geliştirdiğimizi hayal edin: Eğer zar attığınızda 3 gelirse oyuncu ilerlemez, bunun yerine yeni ve havalı bir şapka kazanır. Eğer 7 gelirse oyuncu havalı bir şapkasını kaybeder.
+ Diğer tüm değerlerde ise oyuncu zarın gösterdiği sayı kadar oyun tahtası üzerinde ilerler. Aşağıdaki `match` ifadesi bu mantığı uygular.
+ Zar sonucu rastgele bir değer yerine doğrudan sabit bir sayı olarak verilmiştir ve diğer tüm işlemler, örneğin fonksiyonlar, örnek dışında kalması için gövdesiz olarak temsil edilmiştir:
	- Yani, Bu örnekte zar atma gerçek değil; sabit bir sayı yazıldı. Ayrıca fonksiyonların içi doldurulmadı çünkü örneğin amacı sadece `match` kullanımını göstermek.

```rust
fn main() {
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        other => move_player(other),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
    fn move_player(num_spaces: u8) {}
}
```

> + İlk iki kolda (arm) kullanılan desenler, 3 ve 7 olan literal (doğrudan yazılmış) değerlerdir. Diğer tüm olası değerleri kapsayan son kolda ise desen olarak _other_ adını verdiğimiz bir değişken kullanılır. Bu son kolda çalışan kod, bu _other_ değişkenini alıp `move_player` fonksiyonuna göndererek kullanır.

> + Bu kod derlenir, çünkü her ne kadar bir `u8`’in alabileceği tüm olası değerleri tek tek yazmamış olsak da, son desen (catch-all) özel olarak listelenmeyen tüm değerlerle eşleşir. Bu _catch-all_ deseni, `match` ifadesinin kapsamlı (`exhaustive`) olma zorunluluğunu karşılar.

> + Dikkat edilmelidir ki, bu _catch-all_ kolunu en sona koymak zorundayız; çünkü desenler sırayla değerlendirilir. Eğer _catch-all_ kolunu daha önce koyarsak, diğer kollar asla çalıştırılamaz. Bu nedenle, Rust eğer bir _catch-all_ kolundan sonra başka kollar eklemeye çalışırsak bize uyarı verir!


> [!CAUTION]
> ```rust
> fn main() {
>    let dice_roll = 9;
>    match dice_roll {
>        3 => add_fancy_hat(),
>        7 => remove_fancy_hat(),
>        // other => move_player(other),
>    }
>
>    fn add_fancy_hat() {}
>    fn remove_fancy_hat() {}
>    // fn move_player(num_spaces: u8) {}
>}
> ```
> + Eğer `other` kolunu kapatıp derlenirse konu daha net anlarsınız:
> ```shell
> cargo clippy
> ```
> + Çıktısı:
> ```
>     Checking hello-world v0.1.0 (/home/veritabani/rustDersleri/hello-world)
>error[E0004]: non-exhaustive patterns: `i32::MIN..=2_i32`, `4_i32..=6_i32` and `8_i32..=i32::MAX` not covered
> --> src/main.rs:6:10
>   |
>6 |    match dice_roll {
>   |          ^^^^^^^^^ patterns `i32::MIN..=2_i32`, `4_i32..=6_i32` and `8_i32..=i32::MAX` not covered
>   |
>   = note: the matched value is of type `i32`
>help: ensure that all possible cases are being handled by adding a match arm with a wildcard pattern, a match arm with multiple or-patterns as shown, or mul
>tiple match arms
>   |
>8 ~        7 => remove_fancy_hat(),
>9 ~        i32::MIN..=2_i32 | 4_i32..=6_i32 | 8_i32..=i32::MAX => todo!(),
>   |
>
>For more information about this error, try `rustc --explain E0004`.
>error: could not compile `hello-world` (bin "hello-world") due to 1 previous error
> ```

> + Rust’ta, bir _catch-all_ (her şeyi yakalayan) desen kullanmak istediğimizde fakat bu desende eşleşen değeri kullanmak istemediğimizde kullanabileceğimiz özel bir desen daha vardır: `_`.
> + `_` özel bir desendir; herhangi bir değerle eşleşir ancak bu değeri bir değişkene bağlamaz.
> + Bu, Rust’a o değeri kullanmayacağımızı söyler; bu nedenle Rust bize “kullanılmayan değişken” uyarısı vermez.

> + Oyunun kurallarını değiştirelim: artık, zar atıp 3 veya 7 dışında bir şey gelirse tekrar zar atmanız gerekiyor.
> + Artık catch-all (her şeyi yakalayan) değeri kullanmamıza gerek yok, bu yüzden other adlı değişkeni kullanmak yerine kodumuzu `_` kullanacak şekilde değiştirebiliriz:

```rust
fn main() {
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        _ => reroll(),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
    fn reroll() {}
}
```

+ Bu örnek aynı zamanda kapsamlılık (`exhaustiveness`) gereksinimini de karşılar çünkü son kolda (arm) diğer tüm değerleri açıkça görmezden geliyoruz; hiçbir şeyi unutmamış olmuyoruz.
+ Son olarak, oyunun kurallarını bir kez daha değiştireceğiz; artık 3 veya 7 dışında bir şey atarsanız, sıranızda(sıra sizdeyken) başka hiçbir şey olmayacak.
+ Bunu, `_` koluna (arm) karşılık gelen kod olarak birim değeri (boş tuple türü, "[Tuple Türü](https://doc.rust-lang.org/book/ch03-02-data-types.html#the-tuple-type)" bölümünde bahsetmiştik) kullanarak ifade edebiliriz.

```rust
fn main() {
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        _ => (),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
}
```

> + Burada Rust’a açıkça şunu söylemiş oluyoruz: Önceki kollarda (arm) eşleşmeyen herhangi bir değeri kullanmayacağız ve bu durumda hiçbir kod çalıştırmak istemiyoruz.

> + Desenler (`patterns`) ve eşleştirme (matching) ile ilgili daha öğrenecek çok şey var; bunları [19. bölümde](https://doc.rust-lang.org/book/ch19-00-patterns.html) ele alacağız.
> + Şimdilik, match ifadesinin biraz uzun olduğu durumlarda kullanışlı olabilen `if let` sözdizimine geçeceğiz.

## 6.3. if let ve let else ile Kısa ve Öz Kontrol Akışı:

+ `if let` sözdizimi, `if` ve `let`'i birleştirerek daha az ayrıntılı/sözcüklü bir şekilde bir desene uyan değerleri ele almanıza, diğerlerini ise görmezden gelmenize olanak tanır.
	- Yani, Rust’ta `if let` yapısı, belirli bir desenle eşleşen değerleri kontrol etmek ve o duruma özgü kodu çalıştırmak için kullanılır. Normalde `match` ile bütün varyantları tek tek kontrol etmeniz gerekirken, `if let` sayesinde yalnızca ilgilendiğiniz varyant için kısa ve okunaklı bir kod yazabilirsiniz. Geri kalan varyantları yok sayabilirsiniz; onları ayrıca belirtmenize gerek yok.
+ Liste 6-6’daki programı düşünün: `config_max` değişkenindeki `Option<u8>` değerine bakıyor, ancak yalnızca değer `Some` varyantı olduğunda kodu çalıştırmak istiyor.

```rust
fn main() {
    let config_max = Some(3u8);
    match config_max {
        Some(max) => println!("The maximum is configured to be {max}"),
        _ => (),
    }
}
```

> `Liste 6-6`: Yalnızca değer Some olduğunda kodu çalıştıran bir `match` ifadesi

> + Eğer değer `Some` ise, desendeki değeri `max` değişkenine bağlayarak `Some` içindeki değeri yazdırıyoruz. `None` değeri ile ilgili herhangi bir işlem yapmak istemiyoruz.
> + Ancak `match` ifadesini geçerli kılmak için, yalnızca bir varyantı işledikten sonra `_ => ()` eklememiz gerekiyor; bu da eklenmesi zorunlu ve can sıkıcı bir tekrar kodu oluşturuyor.

+ Bunun yerine, bunu **`if let`** kullanarak daha kısa bir şekilde yazabiliriz.  Aşağıdaki kod, `Liste 6-6`’daki `match` ifadesiyle aynı şekilde davranır.

```rust
fn main() {
    let config_max = Some(3u8);
    if let Some(max) = config_max {
        println!("The maximum is configured to be {max}");
    }
}
```

**Kod Çıktııs:**

```shell
The maximum is configured to be 3
```


> [!CAUTION]
> + `match config_max { ..` ile çalıştırdığımızda rust derleyicisi bize uyarı vermektedir:
> ```shell
> cargo clippy
> ```
> + Çıktısı:
> ```
>     Checking hello-world v0.1.0 (/home/veritabani/rustDersleri/hello-world)
>warning: you seem to be trying to use `match` for destructuring a single pattern. Consider using `if let`
>  --> src/main.rs:6:5
>   |
> 6 | /     match config_max {
> 7 | |         Some(max) => {
> 8 | |             println!("The maximum is configured to be {max}");
> 9 | |         },
>10 | |         _ => (),
>11 | |     }
>   | |_____^
>   |
>   = help: for further information visit https://rust-lang.github.io/rust-clippy/rust-1.91.0/index.html#single_match
>   = note: `#[warn(clippy::single_match)]` on by default
>help: try
>   |
> 6 ~     if let Some(max) = config_max {
> 7 +         println!("The maximum is configured to be {max}");
> 8 +     }
>   |
>
>warning: `hello-world` (bin "hello-world") generated 1 warning (run `cargo clippy --fix --bin "hello-world"` to apply 1 suggestion)
>    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.32s
> ``` 

> + **`if let` sözdizimi**, bir kalıp (`pattern`) ve bir ifadeyi (`expression`) eşittir işaretiyle ayırır.  
> + Bu yapı, bir ifadeyi `match`’e vermek ve kalıbı da `match`’in ilk kolu (`arm`’ı) olarak kullanmakla aynı şekilde çalışır.(`liste: 6-6`)
> + Bu durumda kalıp **`Some(max)`**’tir ve **`max`**, `Some` içindeki değere(`3u8`) bağlanır. 
>+ Daha sonra, tıpkı `match` ifadesindeki ilgili kolda yaptığımız gibi, `if let` bloğunun içinde `max` değişkenini kullanabiliriz.
>+ `if let` bloğundaki kod yalnızca değer kalıpla eşleştiğinde çalışır.

> + **`if let` kullanmak**, daha az yazım, daha az girinti (`indentation`) ve daha az gereksiz (`boilerplate`) kod demektir.
> + Ancak, `match` ifadesinin sağladığı _tüm olasılıkları kapsama_ (`exhaustive checking`) kontrolünü kaybedersiniz; yani herhangi bir durumu ele almayı unutmamanızı garanti eden kontrol ortadan kalkar.
> + **`match` ve `if let` arasında seçim yapmak**, bulunduğunuz duruma göre değişir.  Daha kısa ve temiz bir sözdizimi kazanmak adına _tüm durumları kapsama kontrolünü kaybetmenin_ uygun bir değiş-tokuş olup olmadığına bağlıdır.
	- **Hangi yapıyı kullanacağınız**, ihtiyacınıza göre değişir.  Kısalık uğruna, `match`’in sağladığı **tüm durumların ele alındığından emin olma** güvencesini bırakmaya hazır olup olmadığınıza bakmalısınız.

> + **Başka bir deyişle, `if let`’i; değerin bir desene uyduğu durumda kod çalıştıran ve diğer tüm değerleri yok sayan bir `match` ifadesinin sözdizimsel şekeri (kolaylaştırılmış hali) olarak düşünebilirsiniz.**

>+ Bir `if let` ifadesine bir `else` bloğu ekleyebiliriz. 
>+ `else` ile birlikte gelen kod bloğu,` if let` ve `else` yapısına eşdeğer olan `match` ifadesindeki `_` durumu ile ilişkili kod bloğuyla aynıdır.
>	- `else` ifadesi `match` ifadesi de olan `_` ile aynı görevi yapabilir.
>+ `Liste 6-4`’teki `Coin enum` tanımını hatırlayın; *Quarter(Çeyreklik)* çeşidi aynı zamanda bir `UsState` değeri de içeriyordu.
>+ Eğer gördüğümüz tüm *quarter* olmayan paraları saymak ve aynı zamanda *quarter* olanların eyaletini duyurmak isteseydik, bunu aşağıdaki gibi bir `match` ifadesiyle yapabilirdik:

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

fn main() {
    let coin = Coin::Penny;
    let mut count = 0;
    match coin {
        Coin::Quarter(state) => println!("State quarter from {state:?}!"),
        _ => count += 1,
    }
}
```

+ Veya bunu bir `if let` ve `else` ifadesi kullanarak da yapabiliriz, şöyle:

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

fn main() {
    let coin = Coin::Penny;
    let mut count = 0;
    if let Coin::Quarter(state) = coin {
        println!("State quarter from {state:?}!");
    } else {
        count += 1;
    }
}
```

###  6.3.1 `let...else` ile “Mutlu Yol”da Kalmak

+ Yaygın kullanım deseni, bir değer mevcut olduğunda bazı hesaplamalar yapmak ve aksi takdirde varsayılan bir değer döndürmektir.
+ `UsState` değerine sahip madeni paralar örneğimize devam edecek olursak, quarter'ın (çeyreğin) üzerindeki eyaletin ne kadar eski olduğuna bağlı olarak eğlenceli bir şey söylemek veya yapmak isteseydik, bir eyaletin yaşını kontrol etmek için `UsState` üzerinde şu şekilde bir metot tanımlayabiliriz:

```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

impl UsState {                                    // <========= metot
    fn existed_in(&self, year: u16) -> bool {     // <========= metot
        match self {                              // <========= metot
            UsState::Alabama => year >= 1819,     // <========= metot
            UsState::Alaska => year >= 1959,      // <========= metot
            // -- snip --                         // <========= metot
        }                                         // <========= metot
    }                                             // <========= metot
}                                                 // <========= metot

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn describe_state_quarter(coin: Coin) -> Option<String> {
    if let Coin::Quarter(state) = coin {
        if state.existed_in(1900) {
            Some(format!("{state:?} is pretty old, for America!"))
        } else {
            Some(format!("{state:?} is relatively new."))
        }
    } else {
        None
    }
}

fn main() {
    if let Some(desc) = describe_state_quarter(Coin::Quarter(UsState::Alaska)) {
        println!("{desc}");
    }
}
```

+ Daha sonra madeni paranın türü üzerinde eşleştirme yapmak için `if let` kullanabiliriz ve `Liste 6-7`'de olduğu gibi koşulun gövdesi içinde bir `state` değişkeni tanıtabiliriz.

```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

impl UsState {
    fn existed_in(&self, year: u16) -> bool {
        match self {
            UsState::Alabama => year >= 1819,
            UsState::Alaska => year >= 1959,
            // -- snip --
        }
    }
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

// if let - state -------------------------------------------
fn describe_state_quarter(coin: Coin) -> Option<String> {        
    if let Coin::Quarter(state) = coin {
        if state.existed_in(1900) {
            Some(format!("{state:?} is pretty old, for America!"))
        } else {
            Some(format!("{state:?} is relatively new."))
        }
    } else {
        None
    }
}
// if let - state --------------------------------------------

fn main() {
    if let Some(desc) = describe_state_quarter(Coin::Quarter(UsState::Alaska)) {
        println!("{desc}");
    }
}
```

> `Liste 6-7`: `if let` içine iç içe yerleştirilmiş koşullarla bir eyaletin 1900'de mevcut olup olmadığını kontrol etme.

+ Bu işimizi görür, ancak yapılacak işi `if let` ifadesinin gövdesine taşımış olur ve yapılacak iş daha karmaşık olursa, üst düzey dalların (`branch`'lerin) birbiriyle nasıl ilişkili olduğunu takip etmek zor olabilir.
	- Üst düzey dallar (Top-level branches) → kodun en üst seviyedeki büyük karar noktalarıdır.
+ Ayrıca, ifadelerin bir değer ürettiği gerçeğinden faydalanarak, `if let`’ten eyaleti (`state`) elde etmek veya erken dönmek için bunu kullanabiliriz; bunun bir örneği `Liste 6-8`’de gösterilmiştir. (Benzer bir şeyi `match` ile de yapabilirsiniz.)

> [!NOTE]
> #### Bu Cümle Ne Anlatıyor?
> ##### 1. `if let` içinde işlem yapmak kodu karmaşıklaştırabilir:
> + Eğer `if let` bloğunun içi çok dolu olursa:
> ```rust
> if let Coin::Quarter(state) = coin {
> 	// Burada çok iş yapılırsa
> } else {
> 	// Başka bir yol
> }
> ```
> 
> Bu çoğaldıkça:
> - Mantık dalları (branch’ler) _gizlenir_
> - Kodun “üst seviyedeki mantığını” okumak zorlaşır.
> - Dizayn dağılır
> 
> Yani,
> + `if let` içindeki iş büyüdükçe kodun akışı bozulur, okunabilirlik azalır.


```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

impl UsState {
    fn existed_in(&self, year: u16) -> bool {
        match self {
            UsState::Alabama => year >= 1819,
            UsState::Alaska => year >= 1959,
            // -- snip --
        }
    }
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

// bu değer(coin: Coin) fonksiyona move edilerek veriliyor
fn describe_state_quarter(coin: Coin) -> Option<String> {       // <==
    let state = if let Coin::Quarter(state) = coin {            // <==
        state // ← if bloğunun dönüş değeri                     // <==
    } else {
	    return None; // → Fonksiyondan çık, None döndür ✓       // <==
    };                                                          // <==

    if state.existed_in(1900) {                                 // <==
        Some(format!("{state:?} is pretty old, for America!"))  // <==
    } else {                                                    // <==
        Some(format!("{state:?} is relatively new."))           // <==
    }
}

fn main() {
					// bu değer(coin: Coin) fonksiyona move edilerek veriliyor
    if let Some(desc) = describe_state_quarter(Coin::Quarter(UsState::Alaska)) {
        println!("{desc}");
    }
}
```

> `Liste 6-8`: `if let` kullanarak ya bir değer üretmek ya da erken dönmek(Fonksiyondan erken çıkış).

> [!NOTE]
> ##### 2. Rust’ta ifadeler (`expressions`) değer üretebildiği için, bu özellik daha temiz kod yazmamızı sağlar:
> + Rust’ta `if`, `match`, blok `{}` hepsi **değer üretebilir**.
> + Bu yüzden şöyle yapabiliriz:
> 	- ❌ İş yükünü `if let` içinde yapmak yerine
> 	- ✔️ `if let` bir değer (`state`) üretsin
> 	- ✔️ Geri kalan iş blok dışında yapılsın
> ```rust
> let state = if let Coin::Quarter(state) = coin {
>     state
> } else {
> 	return None;
> }
> ```
> ##### Bu Kod Ne Yapıyor?
> + Eğer `coin` bir `Quarter` ise, içindeki `state` değerini çıkart
> + Eğer `Quarter` **değilse** (örneğin `Penny`, `Nickel`, `Dime` ise), fonksiyondan hemen `None` döndür ve çık.
> + Bu bir **erken dönüş** (`early return`) örneğidir.


> [!tip]
> + `state` yazınca **`if` bloğundan değer döner** ve `let state = ...` atamasına gider.
> + `return state` yazarsak **fonksiyondan çıkış** yapar, `let` ataması hiç gerçekleşmez!


> [!NOTE]
> + **Eğer borrowing olsaydı şöyle olurdu:**
> ```rust
> ...
> ...
> ...
> fn describe_state_quarter(coin: &Coin) -> Option<String> {  // <== Borrowing
>    let state = if let Coin::Quarter(state) = coin {
>        state
>    } else {
>        return None;
>    };
>
>    if state.existed_in(1900) {
>        Some(format!("{state:?} is pretty old, for America!"))
>    } else {
>        Some(format!("{state:?} is relatively new."))
>    }
>}
>
>fn main() {
>    if let Some(desc) = describe_state_quarter(&Coin::Quarter(UsState::Alaska)) {  // <==
>        println!("{desc}");
>    }
>}
> ```

> + Bu da kendine özgü bir şekilde biraz can sıkıcı! `if let`'in bir dalı değer döndürürken, diğeri fonksiyonun tamamından çıkıyor.

> + Bu yaygın deseni daha güzel ifade edebilmek için Rust, `let...else` yapısını sunar.
> + `let...else` sözdizimi, sol tarafında bir desen (`pattern`) ve sağ tarafında bir ifade (`expression`) alır; `if let`’e çok benzer, ancak bir `if` dalı yoktur, yalnızca bir `else` dalı vardır.
> + Eğer desen eşleşirse, desendeki değer dıştaki kapsamda bağlanır (`bind` edilir).
> + Eğer desen eşleşmezse, program `else` dalına girer ve bu dal mutlaka fonksiyondan dönüş yapmak zorundadır.

> + `Liste 6-9`’da, `Liste 6-8`’in `if let` yerine `let...else` kullanıldığında nasıl göründüğünü görebilirsiniz.

```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

impl UsState {
    fn existed_in(&self, year: u16) -> bool {
        match self {
            UsState::Alabama => year >= 1819,
            UsState::Alaska => year >= 1959,
            // -- snip --
        }
    }
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn describe_state_quarter(coin: Coin) -> Option<String> {
    let Coin::Quarter(state) = coin else {
        return None;
    };

    if state.existed_in(1900) {
        Some(format!("{state:?} is pretty old, for America!"))
    } else {
        Some(format!("{state:?} is relatively new."))
    }
}

fn main() {
    if let Some(desc) = describe_state_quarter(Coin::Quarter(UsState::Alaska)) {
        println!("{desc}");
    }
}
```

> `Liste 6-9` : `let...else` ile fonksiyon akışını daha anlaşılır hale getirmek.

> + Dikkat edersen, bu şekilde fonksiyonun ana gövdesinde ‘mutlu yol’da (happy path) kalıyor; `if let` kullanıldığında olduğu gibi iki dal arasında önemli ölçüde farklı bir kontrol akışı oluşturmuyor.


> [!info]
> + Yukarıdaki cümle ne demek istiyor:
> + **"Happy path" (mutlu yol)** yazılımda çok sık kullanılan bir terimdir.
> #### Happy Path nedir?
> Bir fonksiyonun, işlemin veya algoritmanın en ideal, en sorunsuz, beklendiği gibi ilerleyen akışına "happy path" denir.
> Yani,
> + Hiç hata yoktur.
> + İstenmeyen durumlarla karşılaşılmaz.
> + Mantık akışı düzgün şekilde ilerler.
> + Kod _esas yapılmak istenen işlemi_ kesintisiz yapar.
> 
> Buna karşılık, hata durumları, beklenmeyen durumlar, boş değerler, başarısızlıklar vs. **“unhappy path”** veya **“error path”** olarak geçer.

+ Eğer programınızdaki mantık `match` kullanarak ifade etmek için fazla karmaşıksa, `if let` ve `let...else`'in de Rust alet çantanızda olduğunu aklınızda tutun.


> [!info]
> #### Domain (Etki Alanı / İş Alanı) Nedir?
> + Yazılım dünyasında, bir uygulamanın üzerine kurulduğu ve modellemeye çalıştığı özel uzmanlık alanıdır.
> + Örneğin:
> 	- **E-ticaret domain'i:** Sipariş, Ürün, Sepet, Ödeme, Kargo gibi kavramları içerir.
> 	- **Oyun domain'i:** Oyuncu, Can Puanı, Silah, Seviye, Skor gibi kavramları içerir.
> 	- **Muhasebe domain'i:** Hesap, Bilanço, Gelir/Gider, Fatura gibi kavramları içerir.
> #### Cümlenin anlamı:
> + Artık Rust programlarınız, **çalıştığınız özel iş alanındaki** kavramları (örneğin: 'Müşteri', 'Fatura', 'Stok' gibi) `struct` ve `enum` yapıları kullanarak temsil edebilirsiniz.
> #### Örnek:
> + Diyelim ki bir **okul yönetim sistemi** yazıyorsunuz (domain: eğitim yönetimi).
> + Bu domain'deki kavramları Rust'ta şöyle ifade edersiniz:
> ```rust
> // Domain kavramlarını struct ve enum ile modellemek:
>enum DersTipi {
>    Zorunlu,
>    Secmeli,
>}
>
>struct Ogrenci {
>    id: u32,
>    ad: String,
>    kayitli_dersler: Vec<Ders>,
>}
>
>struct Ders {
>    kod: String,
>    ad: String,
>    tip: DersTipi,
>}
> ```
> 
> Yani **domain**, programınızın dilini ve mantığını şekillendiren **gerçek hayat bağlamıdır**. Rust'ın güçlü tür sistemi sayesinde bu kavramları güvenli ve anlaşılır bir şekilde kodlayabilirsiniz.


> [!info]
> #### API nedir?
>  + **Dikkat:** Burada bahsedilen **API**, web API'si değil, çok daha genel bir kavram
> + API = Application Programming Interface
> + **Yani:** Bir programcının sizin yazdığınız kodu kullanırken **etkileşime girdiği kısım**.
> + **API = Kodunuzun "dışarıya açık" kısmı**
> 	- ✅ `pub` ile işaretlenmiş fonksiyonlar, `struct`'lar, `enum`'lar
> 	- ✅ Başka programcıların kullanabileceği şeyler
> 	- ❌ Private/gizli implementasyon detayları **API değil**

> [!summary]
> + Şimdi `enum`'ları kullanarak, numaralandırılmış bir değerler kümesinden biri olabilen özel tipler oluşturmayı ele aldık. 
> 	- `Enum`'lar, kendi tanımladığınız yeni bir veri türüdür (custom type).
> 	- Bu özel tür, **önceden tanımlanmış sabit seçenekler kümesinden** yalnızca birini alabilir.
> 	- "Enumerated values" = "Numaralandırılmış değerler" = Sabit, belirli seçenekler.
> + Standart kütüphanenin `Option<T>` tipinin, hataları önlemek için tip sistemini nasıl kullanmanıza yardımcı olduğunu gösterdik.
> 	- Yani, `Option<T>` sayesinde "değer olmayabilir" durumunu Rust derleyici seviyesinde kontrol eder. Diğer dillerdeki `null` hatalarını önler çünkü `None` durumunu **mutlaka** ele almanız gerekir.
> + `Enum` değerlerinin içinde veri olduğunda, kaç durumu ele almanız gerektiğine bağlı olarak bu değerleri çıkarmak ve kullanmak için `match` veya `if let` kullanabilirsiniz.
> ---
> + Rust programlarınız artık alan adınızdaki (domain) kavramları `struct`'lar ve `enum`'lar kullanarak ifade edebilir. API'nizde kullanmak üzere özel tipler oluşturmak tip güvenliğini sağlar: derleyici, fonksiyonlarınızın yalnızca her bir fonksiyonun beklediği tipteki değerleri almasını garanti eder.
> ---
> + Kullanıcılarınıza kullanımı kolay olan ve tam olarak kullanıcılarınızın ihtiyaç duyacağı şeyleri ortaya koyan, iyi organize edilmiş bir API sunmak için, şimdi Rust'ın modüllerine geçelim.

# 7. Büyüyen Projeleri Paketler, Crate’ler ve Modüller ile Yönetmek:

+ Büyük programlar yazdıkça, kodunuzu düzenlemek giderek daha önemli hale gelecektir. İlgili işlevleri gruplayarak ve farklı özelliklere sahip kodları ayırarak, belirli bir özelliği uygulayan kodun nerede bulunacağını ve bir özelliğin nasıl çalıştığını değiştirmek için nereye gidileceğini daha net hale getireceksiniz.
+ Şu ana kadar yazdığımız programlar tek bir dosyada, tek bir modül içindeydi. Bir proje büyüdükçe, kodu birden fazla modüle ve ardından birden fazla dosyaya bölerek düzenlemelisiniz.
+ Bir paket, birden fazla `binary crate` ve isteğe bağlı olarak bir `library crate` içerebilir.


> [!NOTE]
> #### ✔️ Bir Rust paketi, aynı anda:
> + Birden fazla binary crate içerebilir
> 	- Yani bir paketten birden fazla çalıştırılabilir program (örneğin birden fazla `main.rs`) üretebilirsin.
> + İsteğe bağlı olarak bir tane library crate içerebilir
> 	- Yani paket isterse bir kütüphane (`lib.rs`) da sağlayabilir. Ama bu zorunlu değildir.
> #### 🎯 Ne demek oluyor?
> Bir Rust projesi (package):
> + Hem birden fazla “uygulama / komut satırı aracı” üretebilir 
> 	-  (örneğin: `cargo run --bin server`, `cargo run --bin client`)
> + Hem de tüm bu uygulamaların ortak kullandığı bir kütüphane sunabilir (`src/lib.rs`)
> #### 📌 Örnek senaryo:
> Diyelim ki bir proje yapıyorsun:
> + `server` adında bir program
> + `client` adında bir program
> + Ortak kullanılan veri yapıları ve fonksiyonlar için bir kütüphane (`lib.rs`)
> 
> Bunların hepsi **tek bir package içinde bulunabilir**.

+ Bir paket büyüdükçe, bazı bölümleri ayırıp harici bağımlılık haline gelen ayrı crate’lere dönüştürebilirsiniz.

> [!NOTE]
> #### ✔️ Proje büyüdükçe, bazı bölümleri ayırıp **ayrı crate’ler** haline getirebilirsin
> Yani başlangıçta tek bir package içinde yazılan kodlar zamanla çok büyürse veya daha karmaşık hale gelirse:
> + Bazı parçaları **ayrı projelere (crate’lere)** bölebilirsin.
> + Bu yeni crate’ler artık **harici bağımlılık (external dependency)** olur.
> + Ana proje bu yeni crate’leri `Cargo.toml` içinde **dependency** olarak kullanır.
> #### 🧪 Örnek açıklama
> Başta tek bir projede her şeyi yazıyorsun:
> ```shell
> my_project/
>  src/
>    main.rs
>    utils.rs
>    parser.rs
>    network.rs
> ```
> + Projede `parser` çok büyüdü ve başka projelerde de kullanmak istiyorsun.
> #### 🔽 Ne yaparsın?
> + `parser` modülünü alıp **ayrı bir crate** olarak dışarı çıkarırsın:
> ```shell
> my_parser/
>   src/lib.rs
> ```
> + Sonra ana projende bunu bağımlılık yaparsın:
> ```toml
> # my_project/Cargo.toml
>[dependencies]
>my_parser = "1.0"
> ```
> Artık `parser` kodu:
> + Ayrı bir crate’tir
> + Ana proje için **harici bağımlılık** haline gelmiştir

+ Bu bölüm tüm bu teknikleri kapsar. Birlikte gelişen birbiriyle ilişkili paketler kümesinden oluşan çok büyük projeler için Cargo, workspace'ler sağlar; bunu Bölüm 14'teki "[Cargo Workspace'leri](https://doc.rust-lang.org/book/ch14-03-cargo-workspaces.html)" kısmında ele alacağız.

+ Ayrıca, uygulama detaylarını kapsüllemeyi (`encapsulation`) de ele alacağız. Bu sayede kodu daha üst seviyede yeniden kullanabilirsiniz: Bir işlemi bir kez uyguladıktan sonra, diğer kodlar, bu işlemin nasıl çalıştığını bilmeden, sizin oluşturduğunuz herkese açık (public) arayüz üzerinden bu kodu çağırabilir.Kodunuzu yazma şekliniz, hangi bölümlerin başka kodların kullanması için herkese açık olacağını, hangi bölümlerin ise yalnızca size ait olup değişiklik yapma hakkını saklı tuttuğunuz özel (private) uygulama detayları olacağını belirler. Bu da zihninizde tutmanız gereken detayların miktarını azaltmanın başka bir yoludur.
+ İlgili bir kavram da scope'tur (kapsam): kodun yazıldığı iç içe geçmiş bağlamın, "scope içinde/scope da" olarak tanımlanmış bir dizi ismi vardır. Kod okurken, yazarken ve derlerken, programcıların ve derleyicilerin belirli bir yerdeki belirli bir ismin bir değişkene, fonksiyona, struct'a, enum'a, modüle, sabite veya başka bir öğeye mi atıfta bulunduğunu ve bu öğenin ne anlama geldiğini bilmesi gerekir. Scope'lar oluşturabilir ve hangi isimlerin scope içinde veya dışında olduğunu değiştirebilirsiniz. Aynı scope içinde aynı isme(değişken) sahip iki öğeye sahip olamazsınız; isim(değişken) çakışmalarını çözmek için araçlar mevcuttur.
+ Rust, kodunuzun organizasyonunu yönetmenize olanak tanıyan bir dizi özelliğe sahiptir; bunlar arasında hangi detayların açığa çıkarıldığı, hangi detayların private olduğu ve programlarınızdaki her scope'ta hangi isimlerin bulunduğu yer alır. Bazen toplu olarak modül sistemi olarak adlandırılan bu özellikler şunları içerir:
	- **Packages (Paketler)** - Cargo özelliği, crate'leri oluşturmanıza, test etmenize ve paylaşmanıza olanak tanır.
	- **Crates (Sandıklar)** - Bir kütüphane veya çalıştırılabilir dosya üreten modül ağacı
	- **Modules (Modüller)** ve **use** anahtar kelimesi - Kodun organizasyonunu, kapsamını (scope) ve yolların (paths) gizliliğini kontrol etmenizi sağlar
	- **Paths (Yollar)** - Bir öğeyi (`struct`, fonksiyon, modül vb.) isimlendirme yolu


> [!NOTE] Title
> #### Modül ağacı" ne demek?
> + Bir crate, içinde birden fazla modülün (kod dosyalarının) hiyerarşik olarak düzenlendiği bir yapıdır. Tıpkı bir ağaç gibi:
> ```bash
> crate (kök)
>  ├── modül1
>  │   ├── alt_modül1
>  │   └── alt_modül2
>  └── modül2
> ```

+ Bu bölümde, tüm bu özellikleri ele alacağız, nasıl etkileşime girdiklerini tartışacağız ve `scope`'u (kapsamı) yönetmek için bunları nasıl kullanacağınızı açıklayacağız. Sonunda, modül sistemi hakkında sağlam bir anlayışa sahip olmalı ve `scope`'larla bir profesyonel gibi çalışabilmelisiniz!

## 7.1. Package'ler and Crate'ler

+ Ele alacağımız modül sisteminin ilk kısımları paketler ve crate'lerdir.
+ Crate, Rust derleyicisinin bir seferde dikkate aldığı en küçük kod miktarıdır. Cargo yerine `rustc`'yi çalıştırsanız ve tek bir kaynak kod dosyası geçseniz bile (Bölüm 1'deki "Bir Rust Programı Yazma ve Çalıştırma" kısmında yaptığımız gibi), derleyici o dosyayı bir crate olarak kabul eder. Crate'ler modüller içerebilir ve modüller, ilerleyen bölümlerde göreceğimiz gibi, crate ile birlikte derlenen diğer dosyalarda tanımlanmış olabilir.
+ Bir crate iki biçimden birinde olabilir: binary crate veya library crate.
+ Binary crate'ler, komut satırı programı veya sunucu gibi, çalıştırılabilir bir dosyaya derleyebileceğiniz programlardır.
	- Yani, Binary crate’ler, bir çalıştırılabilir dosyaya derlenebilen ve çalıştırabileceğiniz programlardır; örneğin bir komut satırı uygulaması veya bir sunucu üzerinde.
+ Her birinin, çalıştırılabilir dosya çalıştığında ne olacağını tanımlayan **main** adında bir fonksiyonu olmalıdır.
	- Her **binary crate**, çalıştırılabilir dosya çalıştığında ne olacağını tanımlayan `main` adlı bir fonksiyona sahip olmalıdır.
+ Şimdiye kadar oluşturduğumuz tüm crate'ler binary crate'ler olmuştur.
---
+ Library crate'lerin main fonksiyonu yoktur ve çalıştırılabilir bir dosyaya derlenmezler. Bunun yerine, birden fazla projeyle paylaşılması amaçlanan işlevselliği(fonksiyonilite) tanımlarlar. Örneğin, Bölüm 2'de kullandığımız rand crate'i, rastgele sayılar üreten işlevsellik sağlar. Rustacean'lar "crate" dediklerinde çoğu zaman library crate'i kastederler ve "crate" kelimesini genel programlama kavramı olan "library" (kütüphane) ile birbirinin yerine kullanırlar.

+ Crate root, Rust derleyicisinin başladığı ve crate'inizin kök modülünü oluşturan bir kaynak dosyadır (modülleri "Kapsam ve Gizliliği Kontrol Etmek İçin Modülleri Tanımlama" bölümünde derinlemesine açıklayacağız).
	- Yani, Crate kökü (crate root), Rust derleyicisinin derlemeye başladığı kaynak dosyasıdır ve crate’inizin kök modülünü oluşturur.

> [!NOTE]
> + **Crate root**, bir Rust projesinde derleyicinin işe başladığı **ana kaynak dosyadır**.
> + **Hangi dosya crate root'tur?**
> ##### 1. **Binary crate için:** `src/main.rs`
> + Derleyici buradan başlar
> + `main()` fonksiyonu burada olmalıdır.
> ##### 2. Library crate için: `src/lib.rs`
> - Derleyici buradan başlar
> - Kütüphanenin genel yapısı burada tanımlanır
> ##### Neden root(kök) denir?
> + Çünkü bu dosya, crate'inizin **modül ağacının kökünü** oluşturur. Tıpkı bir ağacın kökünden dalların çıkması gibi, diğer tüm modüller bu ana dosyadan türetilir veya buradan referans edilir.
> ```shell
> my_project/
>  └── src/
>      ├── main.rs      # ← Binary crate'in root'u
>      ├── lib.rs       # ← Library crate'in root'u (varsa)
>      └── helper.rs    # ← Alt modül (root değil)
> ```

+ Bir package (paket), bir dizi işlevsellik sağlayan bir veya daha fazla crate'in bir araya getirilmesidir.
+ Bir package, bu crate'lerin nasıl oluşturulacağını açıklayan bir Cargo.toml dosyası içerir.
	- **Bir paket, içindeki crate’lerin nasıl derleneceğini tanımlayan bir _Cargo.toml_ dosyası içerir.**
+ Cargo aslında, kodunuzu oluşturmak için kullandığınız komut satırı aracı için binary crate içeren bir package'dir.
	- **Aslında Cargo’nun kendisi de bir pakettir:**
+ Cargo package'i ayrıca binary crate'in bağımlı olduğu bir library crate de içerir.
+ Diğer projeler, Cargo komut satırı aracının kullandığı mantığı kullanmak için Cargo library crate'ine bağımlı olabilir.

---
+ Bir package istediğiniz kadar binary crate içerebilir, ancak en fazla yalnızca bir library crate içerebilir. Bir package, ister library ister binary crate olsun, en az bir crate içermelidir.
+ Bir package oluşturduğumuzda ne olduğunu inceleyelim. Önce `cargo new my-project` komutunu giriyoruz:

```shell
$ cargo new my-project
     Created binary (application) `my-project` package
$ ls my-project
Cargo.toml
src
$ ls my-project/src
main.rs
```

> + `cargo new my-project` komutunu çalıştırdıktan sonra, Cargo’nun neler oluşturduğunu görmek için `ls` komutunu kullanırız.
> + Proje dizininde, bize bir paket sağlayan bir `Cargo.toml` dosyası bulunur. Ayrıca içinde `main.rs` dosyasının yer aldığı bir `src` dizini vardır.


> [!CAUTION]
> + Metin düzenleyicinizde `Cargo.toml` dosyasını açın; `src/main.rs` dosyasından bahsedilmediğini fark edeceksiniz.
> + Cargo bir geleneği takip eder:
> 	- `src/main.rs`, paketin ismiyle aynı isme sahip **binary crate**’in _crate root_ dosyasıdır.
> 	- Aynı şekilde, paket dizininde `src/lib.rs` varsa, paket yine ismiyle aynı isme sahip bir **library crate** içerir ve `src/lib.rs` onun _crate root_’udur.
> + Cargo, bu crate root dosyalarını **rustc** derleyicisine göndererek ilgili library veya binary crate’i oluşturur.
> ```toml
> [package]
> name = "my-project"  ← Bu crate'in adıdır
> version = "0.1.0"
> edition = "2021"
> ```
> + Crate'in adı `Cargo.toml` dosyasındaki `[package]` bölümündeki `name` alanında tanımlıdır. `main.rs` veya `lib.rs` sadece dosya adlarıdır, crate'in kendisinin adı değildir.

+ Burada, yalnızca `src/main.rs` içeren bir `package`'imiz var, bu da yalnızca `my-project` adında bir *binary crate* içerdiği anlamına gelir.
+ Bir package `src/main.rs` ve `src/lib.rs` içeriyorsa, iki crate'e sahiptir: bir *binary* ve bir *library*, her ikisi de package(paket) ile aynı ada sahiptir.
+ Bir package(paket), `src/bin` dizinine dosyalar yerleştirerek birden fazla *binary crate*'e sahip olabilir: her dosya ayrı bir *binary crate* olacaktır.

## 7.2. Scope ve Privacy'yi Kontrol Etmek İçin Modülleri Tanımlama:

+ Bu bölümde modüllerden ve modül sisteminin diğer parçalarından bahsedeceğiz; özellikle, öğelere (items) isim vermenizi sağlayan yolları (paths), bir yolu kapsam(`scope`) içine almak için kullanılan `use` anahtar kelimesini ve öğeleri herkese açık yapmak için kullanılan `pub` anahtar kelimesini ele alacağız. Ayrıca `as` anahtar kelimesini, harici paketleri ve `glob` operatörünü de inceleyeceğiz.

### 7.2.1. Modüller Hızlı Rehberi

+ Modüller ve yolların (paths) ayrıntılarına geçmeden önce, burada modüllerin, yolların(path'lerin), `use` anahtar sözcüğünün ve `pub` anahtar sözcüğünün derleyicide nasıl çalıştığına ve çoğu geliştiricinin kodunu nasıl organize ettiğine dair hızlı bir referans sunuyoruz. Bu kuralların her birinin örneklerini bu bölüm boyunca inceleyeceğiz, ancak modüllerin nasıl çalıştığını hatırlamak için burası harika bir başvuru noktasıdır.
+ **Modül bildirme:** Crate root dosyasında yeni modüller bildirebilirsiniz; diyelim ki `mod garden;` ile bir **"garden"** modülü bildirdiniz. Derleyici modülün kodunu şu yerlerde arayacaktır:
	- Satır içi (inline), `mod garden`'ı takip eden noktalı virgülün yerine geçen süslü parantezler içinde
	- `src/garden.rs` dosyasında
	- `src/garden/mod.rs` dosyasında


> [!NOTE]
> #### Noktalı virgülle vs Süslü parantezle:
> ##### 1. Noktalı Virgülle(Ayrı Dosyalarda):
> ```rust
> mod garden;  // ← Noktalı virgül var
> ```
> + Bu durumda derleyici `garden` modülünün kodunu **başka bir dosyada** arar (`src/garden.rs` veya `src/garden/mod.rs`)
> ##### 2. Süslü Parantezle(Satır içi/inline):
> ```rust
> mod garden {  // ← Noktalı virgül YOK, süslü parantez VAR
>    // Modülün kodu buraya yazılır
>    pub fn plant() {
>        println!("Bitki ektim!");
>    }
>}
> ```
> + Bu durumda modülün kodu **aynı dosyanın içinde**, süslü parantezler arasında yazılır.

+ **Alt modül bildirme:** Crate kök dosyası dışındaki herhangi bir dosyada alt modüller tanımlayabilirsiniz. Örneğin `src/garden.rs` dosyasında `mod vegetables;` yazdığınızı düşünelim. Bu durumda derleyici alt modülün kodunu, üst modülün adına sahip klasör içinde şu yerlerde arar:
	- Noktalı virgül yerine süslü parantez içinde doğrudan `mod vegetables` satırının hemen altında (**inline**)
	- `src/garden/vegetables.rs` dosyasında
	- `src/garden/vegetables/mod.rs` dosyasında


> [!NOTE]
> Ama **crate kök dosyası dışında** olduğunuz için (yani `src/main.rs` veya `src/lib.rs` içinde değil, örneğin `src/garden.rs` içindeyseniz):
> + Yazdığınız `mod vegetables;` satırı **alt modül (submodule)** oluşturur.
> + Bu alt modülün kodu, **üst modülün klasörü içinde** aranır.
> #### 🔍 Örnek ile açıklayalım:
> + Diyelim ki dosya yapınız şöyle:
> ```css
> src/
>  main.rs         (crate root)
>  garden.rs       (buradayız)
> ```
> + `garden.rs` içinde şunu yazdınız:
> ```rust
> mod vegetables;
> ```
> Bu durumda derleyici şunu düşünür:
> + "Bu `vegetables` bir **alt modül**, o halde kodu _garden_ modülünün klasöründe olmalı."
> Ve şu yerlerde arar:
> 1. `src/garden/vegetables.rs`
> 2. `src/garden/vegetables/mod.rs`
> 3. Inline(Süslü parantezle yazılmış mod)
> 
> **Inline nedir?**
> ```rust
> // src/garden.rs
> mod vegetables {
> 	// Kod burada
> }
> ``` 
> **Dosya Yapısı:**
> ```shell
> src/ 
> ├── main.rs 
> ├── garden.rs           ← garden modülü 
> └── garden/             ← garden için dizin 
> 	└── vegetables.rs   ← vegetables alt modülü
> ```

+ **Modüllerdeki koda giden yollar:**  Bir modül crate’inizin parçası olduktan sonra, gizlilik (privacy) kuralları izin verdiği sürece, crate’in herhangi bir yerinden o modüldeki koda modül yolunu kullanarak erişebilirsiniz. Örneğin, `garden::vegetables` modülindeki bir `Asparagus` tipi şu yolda bulunur: 

```rust
crate::garden::vegetables::Asparagus
```

> [!NOTE]
> #### Mutlak ve Göreceli Yol:
> Rust'ta bir path yazarken **nereden başladığınızı** belirtmeniz gerekir:
> ##### 1. `crate::`- Mutlak Yol(Absolute Path):
> ```rust
> crate::garden::vegetables::Asparagus
> ```
> + Mevcut crate'in kökünden başla
> + `src/main.rs` veya `src/lib.rs`'den başlar
> + Her yerden aynı şekilde çalışır
> + `crate::` kelimesi, "bu crate'in en başından (root'undan) başlayarak şu yolu takip et" demektir. Bu sayede kodunuzun nerede olduğuna bakmaksızın her yerden aynı yolu kullanabilirsiniz.
> ##### 2. Göreceli Yol(Relative Path):
> ```rust
> garden::vegetables::Asparagus
> ```
> - Bulunduğum yerden başla
> - Hangi dosyada olduğuna bağlı olarak değişir.
> ```shell
> src/ 
> ├── main.rs 
> └── garden/ 
> 	└── vegetables.rs
> ```
> `main.rs`'den `Asparagus`'a ulaşmak için:
> ```rust
> // Mutlak yol (her zaman aynı)
>use crate::garden::vegetables::Asparagus;
>
>// Veya göreceli yol (main.rs'deyseniz)
>use garden::vegetables::Asparagus;
> ```

+ **Özel (private) ve genel (public):** Bir modül içindeki kod, varsayılan olarak üst modüllerinden gizlidir (private).
+ Bir modülü public yapmak için, mod yerine pub mod ile bildirin. Public bir modül içindeki öğeleri de public yapmak için, bildirimlerinin önünde pub kullanın.
	- Yani, Bir modülü public(genel) yapmak için `mod` yerine `pub mod` yazmanız gerekir. Benzer şekilde, public(genel) bir modül içindeki elemanları da public(genel) yapmak istiyorsanız bildirimlerinin başına `pub` eklemeniz gerekir.
+ **`use` anahtar kelimesi:** Bir scope içinde, use anahtar kelimesi uzun path'lerin tekrarını azaltmak için öğelere kısayollar oluşturur.
+ `crate::garden::vegetables::Asparagus`'a başvurabilen veya erişilebilen herhangi bir scope'ta, `use crate::garden::vegetables::Asparagus`; ile bir kısayol oluşturabilirsiniz ve bundan sonra o scope'ta bu türü kullanmak için sadece Asparagus yazmanız yeterlidir.
+ Burada, bu kuralları gösteren backyard adında bir binary crate oluşturuyoruz. Yine backyard adındaki crate'in dizini, şu dosya ve dizinleri içerir:

```shell
backyard
├── Cargo.lock
├── Cargo.toml
└── src
    ├── garden
    │   └── vegetables.rs
    ├── garden.rs
    └── main.rs
```

+ Bu durumda crate root dosyası src/main.rs'dir ve şunları içerir:

**Dosya Adı:** `src/main.rs`

```rust
use crate::garden::vegetables::Asparagus;

pub mod garden;

fn main() {
    let plant = Asparagus {};
    println!("I'm growing {plant:?}!");
}
```

+ `pub mod garden;` satırı, derleyiciye `src/garden.rs` dosyasında bulduğu kodu dahil etmesini söyler; bu dosyanın içeriği ise şudur:

**Dosya Adı:** `src/garden.rs`

```rust
pub mod vegetables;
```

+ Burada, `pub mod vegetables;` ifadesi `src/garden/vegetables.rs` içindeki kodun da dahil edildiği anlamına gelir. Bu dosyanın içeriği ise şöyledir:

```rust
#[derive(Debug)]
pub struct Asparagus {}
```

+ Şimdi bu kuralların detaylarına girelim ve onları uygulamalı olarak gösterelim!

### 7.2.2. İlişkili Kodu Modüllerde Gruplandırma:

+ Modüller, okunabilirlik ve kolayca yeniden kullanım için bir crate içindeki kodu düzenlememize olanak tanır. Modüller ayrıca öğelerin gizliliğini kontrol etmemizi de sağlar çünkü bir modül içindeki kod varsayılan olarak **private**'tır. **Private** öğeler, dışarıdan kullanıma açık olmayan dahili(iç) uygulama detaylarıdır. Modülleri ve içlerindeki öğeleri public(genel) yapmayı seçebiliriz, bu da onları harici kodun kullanmasına ve onlara bağımlı olmasına izin verecek şekilde açığa çıkarır.
+ Örnek olarak, bir restoranın işlevselliğini sağlayan bir library crate yazalım. Fonksiyonların imzalarını tanımlayacağız ancak gövdelerini boş bırakacağız, böylece bir restoranın uygulamasından ziyade kodun organizasyonuna odaklanacağız.
+ Restoran endüstrisinde, bir restoranın bazı bölümleri front of house (ön bölüm), diğerleri ise back of house (arka bölüm) olarak adlandırılır. Front of house, müşterilerin bulunduğu yerdir; bu, ev sahiplerinin müşterileri oturttuğu, garsonların sipariş ve ödeme aldığı ve barmenların içki hazırladığı yerleri kapsar. Back of house, şeflerin ve aşçıların mutfakta çalıştığı, bulaşıkçıların temizlik yaptığı ve yöneticilerin idari işleri yaptığı yerdir.
---
+ Crate’imizi bu şekilde yapılandırmak için, fonksiyonlarını **iç içe (nested) modüller** içine organize edebiliriz.
+ `cargo new restaurant --lib` komutunu çalıştırarak **restaurant** adlı yeni bir kütüphane (library) oluşturun.
+ Ardından, modülleri ve fonksiyon imzalarını tanımlamak için Liste 7-1’deki kodu **src/lib.rs** dosyasına ekleyin; bu kod, restoranın **front of house** (müşteri alanı) kısmını temsil eder.

```rust
mod front_of_house {
    mod hosting {
        fn add_to_waitlist() {}

        fn seat_at_table() {}
    }

    mod serving {
        fn take_order() {}

        fn serve_order() {}

        fn take_payment() {}
    }
}
```

> `Liste 7-1`: Diğer modülleri ve onların içinde fonksiyonları barındıran bir `front_of_house` modülü

+ Bir modülü, `mod` anahtar sözcüğünü ve ardından modülün adını (bu örnekte `front_of_house`) yazarak tanımlarız. Modülün gövdesi ise süslü parantezler içine yazılır. Modüllerin içinde başka modüller de koyabiliriz; bu örnekte `hosting` ve `serving` modüllerinde olduğu gibi. Modüller ayrıca `struct`, `enum`, sabit (`constant`), `trait` ve `Liste 7-1`’de olduğu gibi fonksiyon tanımları gibi başka öğeleri de barındırabilir.
+ Modülleri kullanarak ilgili tanımları bir araya toplayabilir ve neden ilişkili olduklarını ifade eden bir isim verebiliriz. Bu kodu kullanan programcılar, tüm tanımları tek tek okumak zorunda kalmadan sadece ilgili gruplara bakarak kod içerisinde kolayca gezinebilir; bu da aradıkları tanımları bulmalarını kolaylaştırır. Koda yeni işlev ekleyecek programcılar da düzeni bozmadan bu işlevleri nereye koymaları gerektiğini bilirler.


> [!NOTE]
> #### 1. İlgili tanımları bir araya gruplandırmak:
> + Birbiriyle ilişkili kod parçalarını (fonksiyonlar, struct'lar vb.) aynı modül altında toplayabilirsiniz.
> + Burada:
> 	- `add_to_waitlist` ve `seat_at_table` → müşteri karşılama ile ilgili → `hosting` modülünde
> 	- `take_order` ve `serve_order` → servis ile ilgili → `serving` modülünde
> #### 2. Neden ilişkili olduklarını isimlendirmek:
> + Modül adı, içindeki kodların **neden bir arada olduğunu** açıklar.
> 	- `hosting` → "Bu fonksiyonlar müşteri karşılama (`hosting`) işleriyle ilgili"
> 	- `serving` → "Bu fonksiyonlar servis işleriyle ilgili"
> 
> **Özetle:** Modüller hem ilgili kodları **bir araya toplar** hem de onlara **anlamlı bir isim vererek** neden birlikte olduklarını belirtir. Böylece kod daha düzenli ve anlaşılır olur.

+ Daha önce `src/main.rs` ve `src/lib.rs`'nin *crate root*'ları olarak adlandırıldığından bahsetmiştik. İsimlerinin nedeni, bu iki dosyadan herhangi birinin içeriğinin, modül ağacı(`module tree`) olarak bilinen crate'in modül yapısının kökünde crate adında bir modül oluşturmasıdır.
+ Listeleme 7-2, Listeleme 7-1'deki yapıya ait modül ağacını göstermektedir.

```shell
crate
 └── front_of_house
     ├── hosting
     │   ├── add_to_waitlist
     │   └── seat_at_table
     └── serving
         ├── take_order
         ├── serve_order
         └── take_payment
```

> `Liste 7-2`: `Liste 7-1`’deki kodun modül ağacı

> [!NOTE]
> + Bu iki dosyadan birinin içeriği, otomatik olarak **`crate` adında bir modül** oluşturur ve bu modül **modül ağacının en üstünde** (kökünde) bulunur.
> #### Modül Ağacı nedir?
> + Rust'taki tüm modüller bir **ağaç yapısı** oluşturur:
> ```shell
> crate  ← Kök (root), src/lib.rs veya src/main.rs
> └── front_of_house
>      ├── hosting
>      │    ├── add_to_waitlist
>      │    └── seat_at_table
>      └── serving
>           ├── take_order
>           └── serve_order
> ```
> #### Neden "crate root" denir?
> Çünkü:
> 1. `src/main.rs` veya `src/lib.rs` dosyasının içeriği → `crate` modülünü oluşturur
> 2. Bu `crate` modülü → ağacın kökü (root) konumundadır
> 3. Diğer tüm modüller bu kökün altında dallanır


> [!NOTE]
> #### Crate Modülü Soyut Bir Kavram mı?
> + Rust derleyicisi, `src/main.rs` veya `src/lib.rs` dosyasını okurken **otomatik olarak** şu modül ağacını oluşturur:
> ```rust
> // src/lib.rs dosyası
>  mod front_of_house { 
> 	 mod hosting {} 
> }
> ```
> + **Derleyicinin gördüğü yapı:**
> ```shell
> crate ← Rust bunu otomatik ekler (görünmez ama var)
>  └── front_of_house 
> 	 └── hosting
> ```
> + `crate` modülü kodda yazılmasa da, Rust derleyicisi onu **arka planda otomatik olarak oluşturur**.
> #### Kanıt: `crate::` kullanımı:
> + Kodda `crate::` yazdığınızda, bu gerçekten çalışır:
> ```rust
> // src/lib.rs
> mod front_of_house {
>    pub mod hosting {
>        pub fn add_to_waitlist() {}
>    }
>}
>
>pub fn eat_at_restaurant() {
>    // crate:: kullanarak başlıyoruz
>    crate::front_of_house::hosting::add_to_waitlist();
>}
> ```
> + Eğer `crate` sadece soyut bir kavram olsaydı, bu kod çalışmazdı. Ama çalışıyor çünkü **Rust gerçekten `crate` adında bir kök modül oluşturuyor**.
> #### Sonuç:
> + Eğer `crate` sadece soyut bir kavram olsaydı, bu kod çalışmazdı. Ama çalışıyor çünkü **Rust gerçekten `crate` adında bir kök modül oluşturuyor**.
> +  **Görünmez ama var:** Kodda yazmıyoruz ama `crate::` ile erişebiliyoruz.
> + **"Crate root" ifadesi:** Hem fiziksel dosyayı hem de derleyicinin oluşturduğu kök modülü ifade eder.

+ Bu ağaç, bazı modüllerin diğer modüllerin içinde nasıl iç içe geçtiğini gösterir; örneğin, hosting, front_of_house'un içinde iç içe geçmiştir. Ağaç ayrıca bazı modüllerin kardeş (sibling) olduğunu da gösterir, yani aynı modül içinde tanımlanmışlardır; hosting ve serving, front_of_house içinde tanımlanmış kardeşlerdir. Eğer A modülü B modülünün içinde yer alıyorsa, A modülünün B modülünün çocuğu (child) olduğunu ve B modülünün A modülünün ebeveyni (parent) olduğunu söyleriz. Tüm modül ağacının, crate adlı örtük (implicit) modülün altında köklendiğine dikkat edin.
+ Modül ağacı size bilgisayarınızdaki dosya sisteminin dizin ağacını hatırlatabilir; bu çok uygun bir karşılaştırmadır! Tıpkı bir dosya sistemindeki dizinler gibi, kodunuzu düzenlemek için modülleri kullanırsınız. Ve tıpkı bir dizindeki dosyalar gibi, modüllerimizi bulmak için bir yola ihtiyacımız vardır.
	- Yani, Tıpkı bilgisayarınızda bir dosyayı bulmak için yolunu bilmeniz gerektiği gibi, Rust'ta da bir fonksiyonu veya yapıyı kullanmak için **hangi modülde olduğunu** (yolunu) bilmeniz gerekir.
	- Modüllere erişmek için onların *adresini* (path'ini) yazmamız gerekir, tıpkı dosya sisteminde dosyalara erişmek gibi.

## 7.3. Modül ağacındaki öğelere erişim yolları:

+ Rust’a, modül ağacında bir öğenin (item’ın) nerede olduğunu göstermek için, bir dosya sisteminde gezinirken kullandığımız yola (path’e) benzer bir yol kullanırız. Bir fonksiyonu çağırmak için onun yolunu bilmemiz gerekir.
+ Bir yol iki biçimde olabilir:
1. **Mutlak yol (absolute path)**, Kök krate’ten(`crate root`) başlayan tam yoldur; harici bir crate'ten gelen kod için mutlak yol, crate adıyla başlar ve mevcut crate'ten gelen kod için literal crate(`crate::`) ile başlar.


> [!NOTE]
> Rust’ta bir fonksiyon, struct veya modüle erişirken **mutlak yol (absolute path)** kullanıyorsan
> #### 1. Eğer erişeceğin kod _başka bir crate_ içindeyse:
> + Mutlak yol **crate’in kendi adıyla** başlar.
> ```rust
> rand::thread_rng();
> ```
> + Burada `rand` dış bir crate’dir → mutlak yol `rand` ile başlar.
> #### 2. Eğer erişeceğin kod *kendi crate’inin* içindeyse:
> + Mutlak yol **crate** kelimesiyle başlar (literal “crate”).
> ```rust
> crate::front_of_house::hosting::add_to_waitlist();
> ```
> + Burada `crate` → "bu projedeki crate’in kökü" anlamına gelir.
> + Yani `crate::` = `src/lib.rs` veya `src/main.rs` dosyasının kök modülü.


2. **Göreceli yol (relative path)**, mevcut modülden başlar ve `self`, `super` veya mevcut modüldeki bir tanımlayıcı (identifier) kullanır.

> [!NOTE]
> Göreceli yol, "bulunduğunuz yerden" başlar ve üç farklı şekilde yazılabilir:
> #### 1. `self` - mevcut modül:
> + Bulunduğunuz modülün içindeki bir şeye erişmek için:
> ```rust
> mod front_of_house {
>    pub mod hosting {
>        pub fn add_to_waitlist() {}
>        
>        pub fn seat() {
>            // self = bu modül (hosting)
>            self::add_to_waitlist();
>        }
>    }
>}
> ``` 
> + `self` = "bulunduğum modül" (`hosting`)
> #### 2. `super` - bir üst modül (parent):
> + Bir üst seviyedeki modüle erişmek için:
> ```rust
> mod front_of_house {
>    pub fn greet() {}
>    
>    pub mod hosting {
>        pub fn welcome() {
>            // super = bir üst modül (front_of_house)
>            super::greet();
>        }
>    }
>}
> ```
> + `super` = "bir üst modül" (parent), tıpkı dosya sistemindeki `../` gibi
> #### 3. Doğrudan tanımlayıcı(identifier):
> + Mevcut seviyede veya alt modülde bir şeyi direkt adıyla çağırma:
> ```rust
> mod front_of_house {
>    pub mod hosting {
>        pub fn add_to_waitlist() {}
>    }
>    
>    pub fn eat() {
>        // "hosting" tanımlayıcısını doğrudan kullanıyoruz
>        hosting::add_to_waitlist();
>    }
>}
> ```

| Rust       | Dosya Sistemi       |
| ---------- | ------------------- |
| `crate::`  | `/` (kök dizin)     |
| `self::`   | `./` (mevcut dizin) |
| `super::`  | `../` (üst dizin)   |

+ Hem mutlak hem de göreceli yollar, çift iki nokta üst üste (::) ile ayrılmış bir veya daha fazla tanımlayıcı ile takip edilir.


> [!NOTE]
> Hem mutlak hem de göreceli yollarda **modül/fonksiyon adları `::` ile birbirinden ayrılır**.
> ##### Mutlak Yol:
> ```rust
> crate::front_of_house::hosting::add_to_waitlist()
>  ↑       ↑            ↑         ↑
>  └───────┴────────────┴─────────┴─ Bunlar "tanımlayıcılar" (identifiers)
>      └──────┴──────┴─── Bunlar :: ile ayrılıyor
> ```
> ##### Göreceli Yol:
> ```rust
> front_of_house::hosting::add_to_waitlist()
>     ↑           ↑           ↑
>     └───────────┴───────────┴─ Tanımlayıcılar
>         └──────┴─── :: ile ayrılıyor
> ```

+ `Liste 7-1`’e geri dönersek, diyelim ki `add_to_waitlist` fonksiyonunu çağırmak istiyoruz.  Bu, şu soruyu sormakla aynıdır: **`add_to_waitlist` fonksiyonunun yolu (path’i) nedir?**  `Liste 7-3`, `Liste 7-1`’in bazı modül ve fonksiyonlarının çıkarılmış hâlini içerir.
+ `add_to_waitlist` fonksiyonunu, **crate root**’ta tanımlanan yeni bir fonksiyon olan `eat_at_restaurant` içinden çağırmanın iki yolunu göstereceğiz. Bu yollar doğrudur, ancak bu örneğin olduğu gibi derlenmesini engelleyecek başka bir sorun daha vardır. Bu sorunun nedenini birazdan açıklayacağız.
+ `eat_at_restaurant` fonksiyonu, kütüphane crate’imizin **herkese açık API’sinin** bir parçasıdır; bu yüzden onu `pub` anahtar sözcüğüyle işaretliyoruz.  `pub` hakkında daha fazla detaya Exposing Paths with the pub Keyword (`pub` Anahtar Kelimesi ile Path'leri Herkese Açma) bölümünde gireceğiz.

**Dosya Adı:** `src/lib.rs`

```rust
mod front_of_house {
    mod hosting {
        fn add_to_waitlist() {}
    }
}

pub fn eat_at_restaurant() {
    // Absolute path
    crate::front_of_house::hosting::add_to_waitlist();

    // Relative path
    front_of_house::hosting::add_to_waitlist();
}
```

> `Liste 7-3:` Mutlak ve göreceli yollar kullanarak `add_to_waitlist` fonksiyonunu çağırma

+ `eat_at_restaurant` fonksiyonu içinde `add_to_waitlist` fonksiyonunu ilk çağırışımızda **mutlak (absolute) bir yol** kullanıyoruz.
+ `add_to_waitlist` fonksiyonu, `eat_at_restaurant` ile **aynı crate içinde** tanımlandığı için mutlak bir yol başlatmak amacıyla `crate` anahtar kelimesini kullanabiliriz.  Daha sonra, `add_to_waitlist` fonksiyonuna ulaşana kadar sırayla tüm modülleri ekleriz.
+ Aynı yapıya sahip bir dosya sistemi hayal edebilirsiniz: `add_to_waitlist` adlı bir programı çalıştırmak için şu yolu belirtirdik:

```shell
/front_of_house/hosting/add_to_waitlist
```

+ Crate kökünden (crate root) başlamak için `crate` adını kullanmak, dosya sistemi kökünden başlamak için `/` kullanmaya benzer.
---
+ `eat_at_restaurant` fonksiyonu içinde `add_to_waitlist` fonksiyonunu ikinci kez çağırdığımızda, bu sefer **göreceli (relative) bir yol** kullanıyoruz. Yol, `eat_at_restaurant` ile modül ağacında aynı seviyede tanımlanmış olan `front_of_house` modülünün adıyla başlıyor.
+ Dosya sistemi benzetmesine göre, burada kullanılan yol şu şeklinde olurdu;

```bash
front_of_house/hosting/add_to_waitlist
```

+ Bir yolun bir modül adıyla başlaması, o yolun **göreceli bir yol** olduğunu gösterir.
---
+ Göreceli (relative) ya da mutlak (absolute) yol kullanmayı seçmek, projenize göre vereceğiniz bir karardır ve bir öğenin tanımını, o öğeyi kullanan koddaki yerinden ayrı mı yoksa birlikte mi taşıma olasılığınıza bağlıdır.
+ Örneğin, `front_of_house` modülünü ve `eat_at_restaurant` fonksiyonunu `customer_experience` adında bir modülün içine taşırsak, `add_to_waitlist` için kullandığımız **mutlak yolu** güncellememiz gerekir; ancak **göreceli yol** hâlâ geçerli olur.
+ Buna karşılık, `eat_at_restaurant` fonksiyonunu tek başına `dining` adında bir modüle taşırsak, `add_to_waitlist` için kullandığımız **mutlak yol aynı kalır**, fakat **göreceli yolu** güncellememiz gerekir.

> [!NOTE]
>  ##### Durum 1: İlk Hali
>  ```rust
>  crate
> ├── front_of_house
> │    └── hosting (fn add_to_waitlist)
> └── eat_at_restaurant  ← buradayız
>  ```
>  ##### Durum 2: eat_at_restaurant başka bir modüle taşınıyor
>  ```rust
>  crate
> ├── front_of_house
> │    └── hosting (fn add_to_waitlist)
> └── dining
>      └── eat_at_restaurant  ← artık buradayız!
>  ```

+ Hadi 7-3 numaralı listeyi derlemeyi deneyelim ve henüz neden derlenmediğini öğrenelim! Alacağımız hatalar 7-4 numaralı listede gösterilmiştir.

```rust
$ cargo build
   Compiling restaurant v0.1.0 (file:///projects/restaurant)
error[E0603]: module `hosting` is private
 --> src/lib.rs:9:28
  |
9 |     crate::front_of_house::hosting::add_to_waitlist();
  |                            ^^^^^^^  --------------- function `add_to_waitlist` is not publicly re-exported
  |                            |
  |                            private module
  |
note: the module `hosting` is defined here
 --> src/lib.rs:2:5
  |
2 |     mod hosting {
  |     ^^^^^^^^^^^

error[E0603]: module `hosting` is private
  --> src/lib.rs:12:21
   |
12 |     front_of_house::hosting::add_to_waitlist();
   |                     ^^^^^^^  --------------- function `add_to_waitlist` is not publicly re-exported
   |                     |
   |                     private module
   |
note: the module `hosting` is defined here
  --> src/lib.rs:2:5
   |
2  |     mod hosting {
   |     ^^^^^^^^^^^

For more information about this error, try `rustc --explain E0603`.
error: could not compile `restaurant` (lib) due to 2 previous errors
```

> `Liste 7-4`: `Liste 7-3`’teki kodu derlerken alınan derleyici hataları

+ Hata mesajları, hosting modülünün private olduğunu söylüyor. Başka bir deyişle, `hosting` modülü ve `add_to_waitlist` fonksiyonu için doğru yollara sahibiz, ancak Rust bunları kullanmamıza izin vermiyor çünkü private bölümlere erişimi yok. Rust'ta, tüm öğeler (fonksiyonlar, metodlar, `struct`'lar, `enum`'lar, modüller ve sabitler) varsayılan olarak üst modüllere karşı private'tır. Bir fonksiyon veya `struct` gibi bir öğeyi private yapmak istiyorsanız, onu bir modüle koyarsınız.
+ Bir üst modüldeki öğeler, alt modüllerin içindeki private öğeleri kullanamaz, ancak alt modüllerdeki öğeler, ata modüllerindeki öğeleri kullanabilir. Bunun nedeni, alt modüllerin uygulama detaylarını sarıp gizlemesi, ancak alt modüllerin tanımlandıkları bağlamı görebilmeleridir. Metaforumuza devam edersek, gizlilik kurallarını bir restoranın arka ofisi gibi düşünün: orada olan şeyler restoran müşterileri için private'tır, ancak ofis yöneticileri işlettikleri restoranda her şeyi görebilir ve yapabilir.


> [!NOTE]
> #### Üst Modül(Parent) ile Alt Modül(Child) Arasından Erişim:
> ##### 1. Üst modül → Alt modüle ERİŞEMEZ (varsayılan olarak)
> ```rust
> mod parent {
>    fn parent_function() {
>        // HATA! child_function private
>        child::child_function(); // ❌
>    }
>   
>    mod child {
>        fn child_function() {} // private
>    }
>}
> ```
> + Üst modül, alt modülün private öğelerini göremez.
> ##### 2. Alt modül → Üst modüle ERİŞEBİLİR
> ```rust
> mod parent {
>    fn parent_function() {} // private ama child erişebilir
>    
>    mod child {
>        fn child_function() {
>            // ✅ Çalışır! Üst modüldeki fonksiyona erişebildik
>            super::parent_function();
>        }
>    }
>}
> ```
> + Alt modül, üst modülün öğelerini görebilir.
> #### Neden Böyle?
> + **"alt modüller uygulama detaylarını gizler"** → Alt modül kendi içinde ne yaptığını gizler (kapsülleme)
> + **"alt modüller tanımlandıkları bağlamı görür"** → Ama bulunduğu ortamı (üst modülü) görebilir

+ Rust, modül sisteminin bu şekilde işlemesini seçti, böylece iç uygulama detaylarını gizlemek varsayılan olur. Bu şekilde, dış kodu bozmadan iç kodun hangi kısımlarını değiştirebileceğinizi bilirsiniz. Ancak, Rust size `pub` anahtar kelimesini kullanarak bir öğeyi public yaparak alt modüllerin kodunun iç kısımlarını dış ata modüllere açma seçeneği sunar.

### 7.3.1. `pub` Anahtar Kelimesi ile Path'leri Herkese Açma:

+ Hata aldığımız 7-4 numaralı listeye dönelim; bu hata bize `hosting` modülünün özel (`private`) olduğunu söylüyordu. Üst (parent) modülde bulunan `eat_at_restaurant` fonksiyonunun, alt (child) modülde bulunan `add_to_waitlist` fonksiyonuna erişebilmesini istiyoruz. Bu nedenle, 7-5 numaralı listede gösterildiği gibi `hosting` modülünü `pub` anahtar kelimesiyle işaretliyoruz (public yapıyoruz).

**Dosya Adı:**

```rust
mod front_of_house {
    pub mod hosting {
        fn add_to_waitlist() {}
    }
}

// -- snip --
pub fn eat_at_restaurant() {
    // Absolute path
    crate::front_of_house::hosting::add_to_waitlist();

    // Relative path
    front_of_house::hosting::add_to_waitlist();
}
```

> `Liste 7-5`: `eat_at_restaurant`'tan(`eat_at_restaurant` içerisinde) kullanmak için `hosting` modülünü `pub` olarak bildirme

+ Ne yazık ki, `Liste 7-5`'teki kod hala `Liste 7-6`'da gösterildiği gibi derleyici hatalarıyla sonuçlanıyor.

```
$ cargo build
   Compiling restaurant v0.1.0 (file:///projects/restaurant)
error[E0603]: function `add_to_waitlist` is private
  --> src/lib.rs:10:37
   |
10 |     crate::front_of_house::hosting::add_to_waitlist();
   |                                     ^^^^^^^^^^^^^^^ private function
   |
note: the function `add_to_waitlist` is defined here
  --> src/lib.rs:3:9
   |
3  |         fn add_to_waitlist() {}
   |         ^^^^^^^^^^^^^^^^^^^^

error[E0603]: function `add_to_waitlist` is private
  --> src/lib.rs:13:30
   |
13 |     front_of_house::hosting::add_to_waitlist();
   |                              ^^^^^^^^^^^^^^^ private function
   |
note: the function `add_to_waitlist` is defined here
  --> src/lib.rs:3:9
   |
3  |         fn add_to_waitlist() {}
   |         ^^^^^^^^^^^^^^^^^^^^

For more information about this error, try `rustc --explain E0603`.
error: could not compile `restaurant` (lib) due to 2 previous errors

```

> `Liste 7-6`: Liste 7-5’teki kodu derlerken oluşan derleyici hataları

+ Ne oldu? mod hosting'in önüne pub anahtar kelimesini eklemek, modülü public yapar. Bu değişiklikle, front_of_house'a erişebilirsek, hosting'e de erişebiliriz. Ancak hosting'in içeriği hala private'tır; modülü public yapmak, içeriğini public yapmaz. Bir modül üzerindeki pub anahtar kelimesi, yalnızca ata modüllerindeki kodun ona başvurmasına izin verir, iç koduna erişmesine değil. Modüller birer kapsayıcı olduğundan, sadece modülü public yaparak yapabileceğimiz pek bir şey yoktur; daha ileri gitmeli ve modül içindeki öğelerden bir veya daha fazlasını da public yapmayı seçmeliyiz.
+ `Liste 7-6`'daki hatalar, `add_to_waitlist` fonksiyonunun *private* olduğunu söylüyor. Gizlilik kuralları, modüllerin yanı sıra `struct`'lar, `enum`'lar, fonksiyonlar ve metodlar için de geçerlidir.
+ Şimdi, **`Liste 7-7`’de olduğu gibi**, `add_to_waitlist` fonksiyon tanımının önüne `pub` anahtar kelimesini ekleyerek bu fonksiyonu da public (herkese açık) yapalım.

**Dosya Adı:** `src/lib.rs`

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

// -- snip --
pub fn eat_at_restaurant() {
    // Absolute path
    crate::front_of_house::hosting::add_to_waitlist();

    // Relative path
    front_of_house::hosting::add_to_waitlist();
}
```

> `Liste 7-7`: `mod hosting` ve `fn  add_to_waitlist`'e `pub` anahtar kelimesini eklemek, fonksiyonu `eat_at_restaurant`'tan çağırmamıza izin verir.

+ Artık kod derlenecek! `pub` anahtar kelimesini eklemenin, gizlilik kurallarına göre `eat_at_restaurant` içinde bu yolları kullanmamıza neden izin verdiğini görmek için mutlak ve göreceli yollara bakalım.
+ **Mutlak yolda**, crate'imizin modül ağacının kökü olan crate ile başlarız. `front_of_house` modülü, `crate root`'ta tanımlanmıştır. `front_of_house` `public`(herkese açık) olmasa da, `eat_at_restaurant` fonksiyonu `front_of_house` ile aynı modülde tanımlandığı için (yani, `eat_at_restaurant` ve `front_of_house` kardeştir), `eat_at_restaurant`'tan `front_of_house`'a başvurabiliriz. Sıradaki, `pub` ile işaretlenmiş `hosting` modülüdür. `hosting`'in üst modülüne erişebiliriz, dolayısıyla `hosting`'e erişebiliriz. Son olarak, `add_to_waitlist` fonksiyonu `pub` ile işaretlenmiştir ve üst modülüne erişebiliriz, bu nedenle bu fonksiyon çağrısı çalışır!
+ **Göreceli yolda**, mantık mutlak yolla aynıdır, ilk adım dışında: `crate root`'tan başlamak yerine, yol `front_of_house`'tan başlar. `front_of_house` modülü, `eat_at_restaurant` ile aynı modül içinde tanımlanmıştır, dolayısıyla `eat_at_restaurant`'ın tanımlandığı modülden başlayan göreceli yol çalışır. Ardından; `hosting` ve `add_to_waitlist`, `pub` ile işaretlendiği için, yolun geri kalanı çalışır ve bu fonksiyon çağrısı geçerlidir!
+ Library crate'inizi diğer projelerin kodunuzu kullanabilmesi için paylaşmayı planlıyorsanız, public API'niz, crate'inizi kullanan kullanıcılarla yaptığınız ve kodunuzla nasıl etkileşime girebileceklerini belirleyen sözleşmedir. İnsanların crate'inize bağımlı olmasını kolaylaştırmak için public API'nizdeki değişiklikleri yönetmeyle ilgili birçok husus vardır. Bu hususlar bu kitabın kapsamı dışındadır; bu konuyla ilgileniyorsanız, [The Rust API Guidelines](https://rust-lang.github.io/api-guidelines/)'a bakın.


> [!tip]
> #### Binary ve Kütüphane İçeren Paketler İçin En İyi Pratikler
> + Bir paketin hem src/main.rs binary crate root'u hem de `src/lib.rs` library crate root'u içerebileceğinden ve her iki crate'in de varsayılan olarak paket adına sahip olacağından bahsetmiştik.
> + Tipik olarak, hem library hem de binary crate içeren bu modele sahip paketler, binary crate'te library crate'te tanımlanan kodu çağıran bir çalıştırılabilir dosyayı başlatmak için yeterli miktarda kod içerecektir.
> + Bu, diğer projelerin paketin sağladığı işlevselliğin çoğundan faydalanmasını sağlar çünkü library crate'in kodu paylaşılabilir.
> ---
> + Modül ağacı **src/lib.rs** içinde tanımlanmalıdır. Bu sayede, tüm public öğeler (public items) binary crate içinde, yol isimlendirmesi paketin adıyla başlatılarak kullanılabilir. 
> + Binary crate, kütüphane crate’in bir kullanıcısı hâline gelir; tıpkı tamamen harici bir crate’in kütüphane crate’i kullanması gibi. Binary crate yalnızca public API’ye erişebilir. Bu durum, iyi bir API tasarlamanıza yardımcı olur; çünkü hem yazar hem de müşteri siz olursunuz!
> ---
> + Bölüm 12'de,, hem *binary crate* hem de *library crate* içeren bir komut satırı programı üzerinden bu organizasyon yaklaşımını *uygulamalı olarak* göstereceğiz.

### 7.3.2. `super` ile Göreli (Relative) Yolları Başlatmak:

+ Geçerli (current) modül veya crate kökü yerine, **üst (parent) modülden başlayan göreli yolları**, yolun başında `super` kullanarak oluşturabiliriz. Bu, dosya sisteminde **üst dizine çıkmak** anlamına gelen `..` söz dizimiyle bir yol başlatmaya benzer.
+ `super` kullanımı, bir öğenin üst modülde bulunduğunu bildiğimiz durumlarda ona referans vermemizi sağlar. Bu da, modül üst modülüyle yakından ilişkiliyse fakat ileride üst modülün modül ağacı içinde başka bir yere taşınması ihtimali varsa, **modül ağacını yeniden düzenlemeyi daha kolay hâle getirir**.
+ `Liste 7-8`’deki kodu ele alalım: Bu kod, bir şefin yanlış bir siparişi düzelttiği ve siparişi bizzat müşteriye götürdüğü durumu modellemektedir. `back_of_house` modülü içinde tanımlanan `fix_incorrect_order` fonksiyonu, **üst modülde** tanımlı olan `deliver_order` fonksiyonunu çağırır. Bunu yaparken, `deliver_order`’a giden yolu `super` ile başlatarak belirtir.

**Dosya Adı:** `src/lib.rs`

```rust
fn deliver_order() {}

mod back_of_house {
    fn fix_incorrect_order() {
        cook_order();
        super::deliver_order();
    }

    fn cook_order() {}
}
```

> `Liste 7-8`: `super` ile başlayan göreli(`relative`) bir yol kullanarak bir fonksiyon çağırma

+ `fix_incorrect_order` fonksiyonu `back_of_house` modülünün içindedir, bu yüzden `super` kullanarak `back_of_house` modülünün üst (ebeveyn) modülüne geçebiliriz. Bu durumda ebeveyn modül `crate`, yani kök modüldür. Buradan `deliver_order` fonksiyonunu ararız ve buluruz. Başarılı!
+ `back_of_house` modülü ile `deliver_order` fonksiyonunun büyük olasılıkla birbirleriyle olan bu ilişkiyi koruyacağını ve crate’in modül ağacını yeniden düzenlemeye karar verdiğimizde birlikte taşınacaklarını düşünüyoruz. Bu nedenle `super` kullandık; böylece ileride bu kod farklı bir modüle taşınırsa, güncellememiz gereken yerlerin sayısı daha az olur.
### 7.3.3. Struct'ları ve Enum'ları Public Yapma:

+ `Struct` ve `enum`’ları da **pub** anahtar kelimesiyle herkese açık (public) olarak tanımlayabiliriz; ancak **struct** ve **enum**’lar için **pub** kullanımında dikkat edilmesi gereken bazı ek ayrıntılar vardır.
+ Bir **struct** tanımının başına **pub** koyarsak, struct’ın kendisi public olur; ancak **struct’ın alanları (fields) varsayılan olarak hâlâ private** kalır. Her bir alanın public olup olmayacağını **ayrı ayrı** belirleyebiliriz.
+ `Liste 7-9`’da, **`back_of_house::Breakfast`** adlı public bir `struct` tanımladık. Bu `struct` içinde **toast** alanı(field) public iken, **seasonal_fruit** alanı private’tır. Bu durum, bir restorandaki şu senaryoyu modellemektedir: Müşteri, yemeğin yanında hangi ekmeğin (toast) geleceğini seçebilir; ancak yemeğe eşlik edecek meyveye şef karar verir. Şef bu kararı, mevsime ve stok durumuna göre verir. Mevcut meyveler sık sık değiştiği için müşteriler meyveyi seçemez, hatta hangi meyvenin geleceğini önceden göremez.

**Dosya Adı:** `src/lib.rs`

```rust
mod back_of_house {
    pub struct Breakfast {
        pub toast: String,
        seasonal_fruit: String,
    }

    impl Breakfast {
        pub fn summer(toast: &str) -> Breakfast {
            Breakfast {
                toast: String::from(toast),
                seasonal_fruit: String::from("peaches"),
            }
        }
    }
}

pub fn eat_at_restaurant() {
    // Order a breakfast in the summer with Rye toast.
    let mut meal = back_of_house::Breakfast::summer("Rye");
    // Change our mind about what bread we'd like.
    meal.toast = String::from("Wheat");
    println!("I'd like {} toast please", meal.toast);

    // The next line won't compile if we uncomment it; we're not allowed
    // to see or modify the seasonal fruit that comes with the meal.
    // meal.seasonal_fruit = String::from("blueberries");
}
```

> `Liste 7-9:` Bazı alanları (field) public, bazı alanları `private` olan bir `struct`

+ `back_of_house::Breakfast` yapısındaki **`toast`** alanı (field) public olduğu için, **`eat_at_restaurant`** fonksiyonu içinde nokta gösterimi (dot notation) kullanarak **`toast`** alanını hem okuyabilir hem de yazabiliriz. Dikkat ederseniz, **`seasonal_fruit`** alanını **`eat_at_restaurant`** içinde kullanamayız; çünkü **`seasonal_fruit`** private’tır. **`seasonal_fruit`** alanının değerini değiştiren satırın yorumunu kaldırmayı deneyin; hangi hatayı aldığınızı göreceksiniz.
+ Ayrıca şuna dikkat edin: **`back_of_house::Breakfast`** yapısının private bir alanı olduğu için, bu `struct` bir **public ilişkili fonksiyon** (associated function) aracılığıyla bir **`Breakfast`** örneği oluşturmak zorundadır (biz bu fonksiyona burada **`summer`** adını verdik). Eğer **`Breakfast`** böyle bir fonksiyon sağlamasaydı, **`eat_at_restaurant`** içinde bir **`Breakfast`** örneği oluşturamazdık; çünkü **`seasonal_fruit`** alanı private olduğu için bu alanın değerini **`eat_at_restaurant`** içinde ayarlayamazdık.
+ Buna karşılık, bir **`enum`**’u public yaparsak, onun **tüm varyantları (variants)** da otomatik olarak public olur. Bunun için yalnızca **`enum`** anahtar kelimesinin önüne **`pub`** yazmamız yeterlidir; `Liste 7-10`’da gösterildiği gibi.

**Dosya Adı:** `src/lib.rs`

```rust
mod back_of_house {
    pub enum Appetizer {
        Soup,
        Salad,
    }
}

pub fn eat_at_restaurant() {
    let order1 = back_of_house::Appetizer::Soup;
    let order2 = back_of_house::Appetizer::Salad;
}
```

> `Liste 7-10`: Bir `enum`’u public olarak tanımlamak, onun tüm varyantlarını (variantlarını) da `public` yapar.

+ `Appetizer` `enum`'unu public yaptığımız için, `eat_at_restaurant` içinde `Soup` ve `Salad` varyantlarını kullanabiliriz.
+ `Enum`'lar, varyantları public olmadıkça pek kullanışlı değildir; her durumda tüm `enum` varyantlarını `pub` ile işaretlemek zorunda kalmak can sıkıcı olurdu, bu nedenle `enum` varyantları için varsayılan durum `public` olmaktır. `Struct`'lar genellikle alanları public olmadan da kullanışlıdır, bu nedenle `struct` alanları(fields), `pub` ile işaretlenmedikçe her şeyin varsayılan olarak private olması genel kuralını takip eder.
+ Henüz ele almadığımız `pub` ile ilgili bir durum daha var ve bu bizim son modül sistemi özelliğimizdir: `use` anahtar kelimesi. Önce `use`'u tek başına ele alacağız, ardından `pub` ve `use`'u nasıl birleştireceğimizi göstereceğiz.

## 7.4. `use` Anahtar Kelimesi ile Yolları(Path) Kapsama(Scope) Alma:

+ Fonksiyonları çağırmak için yolları (path’leri) sürekli yazmak zahmetli ve tekrarlı gelebilir. Liste 7-7’de, `add_to_waitlist` fonksiyonunu çağırmak için ister mutlak (absolute) ister göreli (relative) yolu seçmiş olalım, her seferinde `front_of_house` ve `hosting` bölümlerini de belirtmek zorunda kalıyorduk. Neyse ki bu süreci basitleştirmenin bir yolu vardır: `use` anahtar sözcüğünü kullanarak bir yol için bir kez kısayol oluşturabilir ve ardından aynı kapsam (scope) içinde her yerde bu daha kısa adı kullanabiliriz.
+ Liste 7-11’de, `eat_at_restaurant` fonksiyonunun kapsamına `crate::front_of_house::hosting` modülünü dahil ediyoruz. Böylece `eat_at_restaurant` içinde `add_to_waitlist` fonksiyonunu çağırmak için yalnızca `hosting::add_to_waitlist` ifadesini kullanmamız yeterli oluyor.

**Dosya Adı:** `src/lib.rs`

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

> `Liste 7-11`: `use` ile bir modülün kapsama(scope) alınması

+ Bir kapsam (scope) içinde `use` ve bir yol (path) eklemek, dosya sisteminde sembolik bir bağlantı (symbolic link) oluşturmaya benzer. Kasa (crate) kökünde `use crate::front_of_house::hosting` ifadesini eklediğimizde, `hosting` artık o kapsamda geçerli bir isim olur; sanki `hosting` modülü doğrudan crate kökünde tanımlanmış gibi davranır. `use` ile kapsama alınan yollar, diğer tüm yollar gibi gizlilik (privacy) kurallarına da tabidir.
+ Unutulmamalıdır ki `use`, yalnızca tanımlandığı kapsama özel bir kısayol oluşturur. Liste 7-12’de `eat_at_restaurant` fonksiyonu `customer` adlı yeni bir alt modüle taşınmıştır. Bu durum, `use` bildiriminin bulunduğu kapsamdan farklı bir kapsam oluşturduğu için, fonksiyon gövdesi derlenmez.


**Dosya Adı:** `src/lib.rs`

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting;

mod customer {
    pub fn eat_at_restaurant() {
        hosting::add_to_waitlist();
    }
}
```


> `Liste 7-12`: Bir `use` ifadesi yalnızca bulunduğu kapsamda(`scope`) geçerlidir.

+ Derleyici hatası, kısayolun artık `customer` modülü içinde geçerli olmadığını gösteriyor:

```
$ cargo build
   Compiling restaurant v0.1.0 (file:///projects/restaurant)
error[E0433]: failed to resolve: use of undeclared crate or module `hosting`
  --> src/lib.rs:11:9
   |
11 |         hosting::add_to_waitlist();
   |         ^^^^^^^ use of undeclared crate or module `hosting`
   |
help: consider importing this module through its public re-export
   |
10 +     use crate::hosting;
   |

warning: unused import: `crate::front_of_house::hosting`
 --> src/lib.rs:7:5
  |
7 | use crate::front_of_house::hosting;
  |     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(unused_imports)]` on by default

For more information about this error, try `rustc --explain E0433`.
warning: `restaurant` (lib) generated 1 warning
error: could not compile `restaurant` (lib) due to 1 previous error; 1 warning emitted
```

+ Ayrıca use ifadesinin artık kendi kapsamında kullanılmadığına dair bir uyarı olduğuna dikkat edin! Bu sorunu düzeltmek için, use ifadesini customer modülünün içine taşıyın veya alt modül olan customer içinde super::hosting ile üst modüldeki kısayola referans verin.


> [!NOTE]
> **Bu sorunu düzeltmek için**
> ##### 1. Yöntem: `super`
> ```rust
>mod front_of_house {
>    pub mod hosting {
>        pub fn add_to_waitlist() {}
>    }
>}
>
>use crate::front_of_house::hosting;
>
>mod customer {
>    pub fn eat_at_restaurant() {
>        super::hosting::add_to_waitlist();
>    }
>}
> ```
> ##### 2. Yöntem:  `use`'u `customer` içerisine taşıma
> ```rust
>mod front_of_house {
>    pub mod hosting {
>        pub fn add_to_waitlist() {}
>    }
>}
>
>mod customer {
>    use crate::front_of_house::hosting;
>    pub fn eat_at_restaurant() {
>        hosting::add_to_waitlist();
>    }
>}
> ```

### 7.4.1. Rust’a Özgü (İdiyomatik) `use` Path’leri Oluşturma:

+ `Liste 7-11`’de, aynı sonucu elde etmek için `Liste 7-13`’te olduğu gibi `use` yolunu doğrudan `add_to_waitlist` fonksiyonuna kadar belirtmek yerine, neden `use crate::front_of_house::hosting` ifadesini kullandığımızı ve ardından `eat_at_restaurant` içinde `hosting::add_to_waitlist` çağrısını yaptığımızı merak etmiş olabilirsiniz.

**Dosya Adı:** `src/lib.rs`

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting::add_to_waitlist;

pub fn eat_at_restaurant() {
    add_to_waitlist();
}
```

> `Liste 7-13`: `use` ile `add_to_waitlist` fonksiyonunu kapsama almak (idiyomatik olmayan bir kullanım)


> [!NOTE]
> #### İdiyomatik nedir?
> Programlama bağlamında **idiyomatik**, bir dilin:
> + Topluluk tarafından **benimsenmiş**
> + Resmî dokümantasyonlarda **önerilen**
> + Okunabilirliği ve niyeti **en iyi yansıtan**
> + "Bu dili bilen biri böyle yazar" denilen
> 
> **doğal ve doğru kullanım biçimini** ifade eder.
> + Yani “çalışıyor mu?” sorusundan çok, **“Bu dilde doğru ve yerleşik şekilde mi yazılmış?”** sorusunun cevabıdır.


> [!tip]
> + Liste 7-11 ve Liste 7-13 her ikisi de aynı işi yapıyor olsa da, bir fonksiyonu `use` ile kapsama almanın idiyomatik yolu Liste 7-11’de gösterilmiştir. Fonksiyonun ait olduğu üst (parent) modülü `use` ile kapsama almak, fonksiyonu çağırırken bu üst modülü belirtmemizi gerektirir. Fonksiyon çağrısında üst modülün belirtilmesi, fonksiyonun yerel olarak tanımlanmadığını açıkça gösterirken, tam yolun tekrar edilmesini de en aza indirir. Liste 7-13’teki kodda ise `add_to_waitlist` fonksiyonunun nerede tanımlandığı net değildir.
> + Öte yandan, `use` ile struct’lar, enum’lar ve diğer öğeler kapsama alınırken, tam yolun belirtilmesi idiyomatik kabul edilir. Liste 7-14, standart kütüphanedeki `HashMap` struct’ını bir ikili (binary) crate’in kapsamına almanın idiyomatik yolunu göstermektedir.

**Dosya Adı:** `src/main.rs`

```rust
use std::collections::HashMap;

fn main() {
    let mut map = HashMap::new();
    map.insert(1, 2);
}
```

> `Liste 7-14`: `HashMap`’i idiyomatik bir şekilde kapsama almak

+ Bu deyimin arkasında güçlü bir neden yoktur: Bu sadece ortaya çıkmış bir gelenektir ve insanlar Rust kodunu bu şekilde okumaya ve yazmaya alışmışlardır.
+ Bu idiyomun bir istisnası, `use` ifadeleriyle aynı ada sahip iki öğeyi kapsama almaya çalıştığımız durumdur; çünkü Rust buna izin vermez. Liste 7-15, aynı ada sahip ancak farklı üst (parent) modüllere ait iki `Result` türünün kapsama nasıl alındığını ve bunlara nasıl referans verildiğini göstermektedir.

**Dosya Adı:** `src/lib.rs`

```rust
use std::fmt;
use std::io;

fn function1() -> fmt::Result {
    // --snip--
    Ok(())
}

fn function2() -> io::Result<()> {
    // --snip--
    Ok(())
}
```

> L`iste 7-15`: Aynı ada sahip iki türü aynı kapsama(scope) almak, üst (parent) modüllerinin kullanılmasını gerektirir.

+ Gördüğünüz gibi, üst (parent) modülleri kullanmak iki `Result` türünü birbirinden ayırt eder. Eğer bunun yerine `use std::fmt::Result` ve `use std::io::Result` ifadelerini kullansaydık, aynı kapsam içinde iki farklı `Result` türü bulunmuş olurdu ve `Result` ismini kullandığımızda Rust hangisini kastettiğimizi bilemezdi.

### 7.4.2. `as` Anahtar Sözcüğü ile Yeni Adlar Verme:

+ `use` ile aynı ada sahip iki türü aynı kapsama alma problemine başka bir çözüm daha vardır: Yolun (path) ardından `as` anahtar sözcüğünü kullanarak tür için yeni bir yerel ad, yani bir takma ad (alias) tanımlayabiliriz. Liste 7-16, Liste 7-15’teki kodun, iki `Result` türünden birini `as` kullanarak yeniden adlandırma yoluyla yazılmış başka bir hâlini göstermektedir.

```rust
use std::fmt::Result;
use std::io::Result as IoResult;

fn function1() -> Result {
    // --snip--
}

fn function2() -> IoResult<()> {
    // --snip--
}
```

> `Liste 7-16`: `as` anahtar sözcüğü ile kapsama(scope) alınırken bir türün yeniden adlandırılması

+ İkinci `use` ifadesinde, `std::io::Result` türü için **IoResult** adında yeni bir isim seçtik. Bu isim, kapsama aldığımız `std::fmt` içindeki `Result` ile çakışmayacaktır. Liste 7-15 ve Liste 7-16 idiyomatik kabul edilir; dolayısıyla hangisini seçeceğiniz size kalmıştır.

### 7.4.3. `pub use` ile İsimlerin Yeniden Dışa Aktarılması:

+ Bir ismi `use` anahtar sözcüğü ile kapsama aldığımızda, bu isim yalnızca içe aktarıldığı kapsama özeldir (private). Bu kapsamın dışındaki kodun, sanki bu isim o kapsamda tanımlanmış gibi ona başvurabilmesini sağlamak için `pub` ve `use` anahtar sözcüklerini birlikte kullanabiliriz. Bu tekniğe **yeniden dışa aktarma (re-exporting)** denir; çünkü bir öğeyi kapsama alırken, aynı zamanda bu öğeyi başkalarının da kendi kapsamlarına alabilmesi için erişilebilir hâle getirmiş oluruz.
+ `Liste 7-17`, kök (root) modüldeki `use` ifadesi `pub use` olarak değiştirilmiş hâliyle `Liste 7-11`’deki kodu göstermektedir.

**Dosya Adı:** `src/lib.rs`

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

> `Liste 7-17`: `pub use` kullanarak bir ismi, yeni bir kapsamdan tüm kodlar için erişilebilir kılma

+ Bu değişiklikten önce, dışarıdaki kodun `add_to_waitlist` fonksiyonunu çağırabilmesi için `restaurant::front_of_house::hosting::add_to_waitlist()` yolunu kullanması gerekiyordu; bu da `front_of_house` modülünün `pub` olarak işaretlenmesini zorunlu kılıyordu. Şimdi ise bu `pub use` ifadesi, `hosting` modülünü kök (root) modülden yeniden dışa aktardığı için, dışarıdaki kod `restaurant::hosting::add_to_waitlist()` yolunu kullanabilir.

> [!NOTE]
> Buradaki Örnek yukarıdaki cümleyi daha netleştirmektedir:
> #### `pub use` ve sadece `use` arasındaki fark şöyle:
> ##### `use` (sadece)
> - Bir öğeyi **sadece o modül içinde** kullanılabilir hale getirir
> - Öğe **private** (özel) kalır
> - Dış modüller bu öğeye erişemez
> ```rust
> mod my_module {
>    use std::collections::HashMap;  // Sadece my_module içinde kullanılabilir
>    
>    pub fn do_something() {
>        let map = HashMap::new();  // Burada kullanılabilir
>    }
>}
>
>// Dışarıdan HashMap'e erişilemez
> ```
> ##### `pub use` (yeniden dışa aktarma)
> + Bir öğeyi hem o modülde kullanılabilir yapar
> + Hem de **dışarıya açar** (public yapar)
> + Başka modüller bu öğeyi sizin modülünüzden alabilir
> ```rust
> mod my_module {
>    pub use std::collections::HashMap;  // Hem içerde hem dışarıda kullanılabilir
>    
>    pub fn do_something() {
>        let map = HashMap::new();
>    }
>}
>
> // Dışarıdan erişilebilir:
>use my_module::HashMap;  // HashMap'i my_module'den alabiliriz
> ```
> ##### Özet:
> + **`use`**: "Bunu sadece ben kullanacağım"
> + **`pub use`**: "Bunu hem ben kullanacağım, hem başkalarına sunacağım"
> 
> `pub use` özellikle kütüphane yazarken çok kullanışlıdır - iç yapıyı gizleyip kullanıcılara daha basit bir API sunmak için kullanılır.

+ Yeniden dışa aktarma (`re-exporting`), kodunuzun iç yapısı ile kodunuzu çağıran programcıların alanı (domain) nasıl düşündüğü birbirinden farklı olduğunda oldukça faydalıdır. Örneğin bu restoran benzetmesinde, restoranı işleten kişiler "ön taraf" (*front of house*) ve "arka taraf" (*back of house*) şeklinde düşünür. Ancak restorana gelen müşteriler, restoranın bölümlerini muhtemelen bu şekilde kavramsallaştırmaz. `pub use` sayesinde, kodumuzu bir yapıyla yazıp, dışarıya farklı bir yapı sunabiliriz. Bu yaklaşım, hem kütüphane üzerinde çalışan programcılar hem de kütüphaneyi kullanan programcılar için düzenli ve anlaşılır bir yapı sağlar.
+ Bölüm 14’teki **“Kullanışlı Bir Açık API Dışa Aktarma ([Exporting a Convenient Public API](https://doc.rust-lang.org/book/ch14-02-publishing-to-crates-io.html#exporting-a-convenient-public-api))”** başlığında, `pub use`’un başka bir örneğini ve bunun crate belgelerinizi (documentation) nasıl etkilediğini inceleyeceğiz.

### 7.4.4. Harici Paketleri Kullanma:

+ Bölüm 2'de, rastgele sayılar üretmek için **rand** adlı harici bir paketi kullanan bir tahmin oyunu (*guessing game*) projesi yazmıştık. Projemizde **rand**’i kullanabilmek için, `Cargo.toml` dosyasına aşağıdaki satırı eklemiştik:

**Dosya Adı:** `Cargo.toml`

```toml
rand = "0.8.5"
```

+ `Cargo.toml` dosyasına **rand**’i bir bağımlılık (dependency) olarak eklemek, Cargo’ya **rand** paketini ve onun tüm bağımlılıklarını **crates.io** üzerinden indirip projeye dahil etmesini ve **rand**’i projemiz için kullanılabilir hâle getirmesini söyler.
+ Ardından, **`rand`**’in tanımlarını paketimizin *kapsamına almak* için, crate adını (**rand**) temel alan bir `use` satırı ekleyerek kapsama almak istediğimiz öğeleri listeledik. 2. Bölüm’deki **“Rastgele Bir Sayı Üretme (Generating a Random Number)”** kısmını hatırlayacak olursak, `Rng` `trait`’ini *kapsama almış* ve `rand::thread_rng` fonksiyonunu çağırmıştık:

```rust
use std::io;

use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    println!("The secret number is: {secret_number}");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}
```


> [!TIP]
> ##### 1. `rand`’in tanımlarını paketimizin kapsamına almak:
> + `rand` kütüphanesinin içindeki fonksiyonları, struct'ları, trait'leri kendi kodumuza dahil etmek anlamına gelir. Böylece onları kullanabiliriz.
> ##### 2. crate adını (`rand`) temel alan bir `use` satırı:
> + Şu şekilde bir satır yazdık demek:
> ```rust
> use rand::...;
> ```
> + `rand` dış pakettir (crate), önce onun adını yazıyoruz.
> ##### 3. kapsama almak istediğimiz öğeleri listeledik:
> + `rand` paketinin içinden sadece ihtiyacımız olan şeyleri seçtik. Örneğin:
> ```rust
> use rand::Rng;    // Rng trait'ini getirdik
> ```

+ Rust topluluğu üyeleri, **crates.io** üzerinde pek çok paketi kullanıma sunmuştur. Bu paketlerden herhangi birini kendi paketimize dahil etmek de aynı adımları izlemeyi gerektirir: paketi, paketimizin `Cargo.toml` dosyasında listelemek ve ardından o crate içindeki öğeleri kapsama almak için `use` anahtar sözcüğünü kullanmak.
+ Standart **`std`** kütüphanesinin de paketimize **harici (external)** bir crate olduğunu unutmayın. Ancak standart kütüphane Rust diliyle birlikte dağıtıldığı için, **`std`**’yi eklemek amacıyla `Cargo.toml` dosyasında herhangi bir değişiklik yapmamıza gerek yoktur. Buna rağmen, **`std`** içindeki öğeleri paketimizin kapsamına alabilmek için `use` ile ona referans vermemiz gerekir. Örneğin, `HashMap` için şu satırı kullanırız:

```rust
#![allow(unused)]
fn main() {
use std::collections::HashMap;
}
```

+ Bu, standart kütüphane crate’inin adı olan `std` ile başlayan mutlak (*absolute*) bir yoldur.

### 7.4.5. `use` Listelerini Sadeleştirmek için İç İçe (*Nested*) Yollar Kullanımı:

+ Aynı crate veya aynı modül içinde tanımlanmış birden fazla öğeyi kullanıyorsak, her bir öğeyi ayrı bir `use` satırında listelemek dosyalarımızda oldukça fazla dikey alan kaplayabilir. Örneğin, `Liste 2-4`’teki tahmin oyunu (*guessing game*) örneğinde yer alan şu iki `use` ifadesi, `std` içindeki öğeleri kapsama almaktadır:

**Dosya Adı:** `src/main.rs`

```rust
use rand::Rng; 
// --snip-- 
use std::cmp::Ordering; 
use std::io; 
// --snip--

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    println!("The secret number is: {secret_number}");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    let guess: u32 = guess.trim().parse().expect("Please type a number!");

    println!("You guessed: {guess}");

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```

+ Bunun yerine, aynı öğeleri tek bir satırda kapsama almak için iç içe (nested) yolları kullanabiliriz. Bunu, yolun ortak kısmını belirtip ardından iki nokta üst üste (`::`) koyarak ve farklılık gösteren yol kısımlarını küme parantezleri (`{}`) içinde listeleyerek yaparız. Bu kullanım, Liste 7-18’de gösterilmektedir.

**Dosya Adı:** `src/main.rs`

```rust
use rand::Rng;
// --snip--
use std::{cmp::Ordering, io};
// --snip--

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    println!("The secret number is: {secret_number}");

    println!("Please input your guess. ");
	
    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    let guess: u32 = guess.trim().parse().expect("Please type a number!");

    println!("You guessed: {guess}");

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```

> `Liste 7-18`: Aynı öneke (prefix’e) sahip birden fazla öğeyi kapsama almak için iç içe (nested) bir yolun belirtilmesi


> [!tip]
> + `trim()`: Boşlukları ve newline karakterini temizler.
> + `parse()`: String'i sayıya çevirir.
> + `expect()`: Hata olursa panic yapar

+ Daha büyük programlarda, aynı crate veya modülden birçok öğeyi içeri almak için iç içe (nested) yollar kullanmak, gereken ayrı `use` ifadelerinin sayısını önemli ölçüde azaltabilir.
+ Bir yolun (path) herhangi bir seviyesinde iç içe yol kullanabiliriz. Bu, ortak bir alt yolu paylaşan iki `use` ifadesini birleştirirken oldukça faydalıdır. Örneğin, Liste 7-19’da iki `use` ifadesi gösterilmektedir: biri `std::io`’yu kapsama alanına getirir, diğeri ise `std::io::Write`’ı kapsama alanına getirir.

**Dosya Adı:** `src/main.rs`

```rust
use std::io;
use std::io::Write;
```

> `Liste 7-19`: Birinin diğerinin alt yolu (subpath’i) olduğu iki adet `use` ifadesi

+ Bu iki yolun ortak kısmı `std::io`’dur ve bu, aynı zamanda ilk yolun tamamıdır. Bu iki yolu tek bir `use` bildirimi hâline getirmek için, iç içe (*nested*) yolda `self` anahtar kelimesini kullanabiliriz; bu durum `Liste 7-20`’de gösterilmektedir.

**Dosya Adı:** `src/main.rs`

```rust
use std::io::{self, Write};
```

> `Liste 7-20`: `Liste 7-19`’daki yolların tek bir `use` bildirimi içinde birleştirilmesi

+ Bu satır sayesinde `std::io` modülü ile `std::io::Write` türü (trait’i) mevcut kapsamda(into scope) kullanılabilir hâle gelir.

### 7.4.6. `Glob` Operatörü ile Öğeleri İçe Aktarma:

+ İstediğimiz bir yol (path) altında tanımlanmış **tüm public öğeleri** kapsama (scope) almak istersek, bu yolun sonuna `*` **glob operatörünü** ekleyebiliriz:

```rust
#![allow(unused)]
fn main() {
use std::collections::*;
}
```

+ Bu `use` ifadesi, `std::collections` içinde tanımlı olan **tüm public öğeleri** mevcut kapsama alır. Ancak **glob operatörünü kullanırken dikkatli olunmalıdır**. *Glob* kullanımı, hangi isimlerin kapsamda olduğunu ve programınızda kullanılan bir ismin nerede tanımlandığını anlamayı zorlaştırabilir. Ayrıca, bağımlı olduğunuz bir crate tanımlarını değiştirirse, sizin içe aktardığınız öğeler de değişmiş olur. Örneğin, bağımlılık aynı kapsama sizin tanımlarınızla **aynı isme sahip** yeni bir tanım eklerse, bu durum bağımlılığı güncellediğinizde **derleme (compiler) hatalarına** yol açabilir.
+ Glob operatörü çoğunlukla **test yazarken** kullanılır; test edilen her şeyi `tests` modülü içine almak için tercih edilir. Bu konu, Bölüm 11’deki **["How to Write Tests"](https://doc.rust-lang.org/book/ch11-01-writing-tests.html#how-to-write-tests)** başlığında ele alınacaktır. Ayrıca glob operatörü bazen **prelude deseni**nin bir parçası olarak da kullanılır. Bu desen hakkında daha fazla bilgi için [standart kütüphane dokümantasyonuna](https://doc.rust-lang.org/std/prelude/index.html#other-preludes) bakabilirsiniz.


> [!NOTE] Title
> #### Prelude Nedir?
> + **Prelude**, Rust’ta **çok sık kullanılan tür, trait ve fonksiyonların**, kullanıcı tarafından `use` yazılmasına gerek kalmadan **otomatik olarak scope’a alınması** anlamına gelir.
> + Yani, “Rust programı yazarken neredeyse her zaman lazım olan şeyler, zahmetsizce hazır gelsin”  mantığıyla oluşturulmuş bir yaklaşımdır.
> ##### Standart Prelude (std prelude):
> + Rust, her crate’e otomatik olarak şu modülü ekler:
> 	- `Option`, `Result`
> 	- `Some`, `None`, `Ok`, `Err`
> 	- `Vec`, `String`
> 	- `Copy`, `Clone`
> 	- `Drop`
> 	- `Iterator`
> 	- `ToString`
> ```rust
> std::prelude::v1
> ```
> + Bu yüzden şunları **hiç import etmeden** kullanabiliyoruz:
> ```rust
> let x: Option<i32> = Some(5);
> let v: Vec<i32> = Vec::new();
> ```
> + Ama şunu yazmıyoruz:
> ```rust
> use std::option::Option;
> use std::vec::Vec;
> ```
> + Çünkü bunlar **prelude sayesinde zaten scope’ta**.

> [!NOTE]
> #### Prelude deseni (pattern) ne demek?
> + Prelude deseni, **kendi kütüphanende** de benzer bir yapı kurman demektir.
> + Yani;
> 	- Kullanıcıların **en sık ihtiyaç duyacağı şeyleri**
> 	- Tek bir modülde toplayıp
> 	- Kullanıcıya tek satırda import ettirmek
> ##### Örnek: Kendi prelude’unu yazmak
> ```rust
> // lib.rs
> pub mod prelude {
>    pub use crate::config::Config;
>    pub use crate::errors::MyError;
>    pub use crate::utils::init;
>}
> ```
> + Kütüphaneyi kullanan kişi:
> ```rust
> use my_crate::prelude::*;
> ```
> + Ve artık şunları **tek tek import etmeden** kullanabilir:
> ```rust
> let cfg = Config::new();
> init();
> ```
> + İşte burada `*` (glob) operatörü **bilinçli ve kontrollü** kullanılmış olur.

## 7.5. Modülleri Farklı Dosyalara Ayırma:

+ Şimdiye kadar bu bölümdeki tüm örneklerde, birden fazla modül tek bir dosya içinde tanımlanmıştı. Ancak modüller büyüdükçe, kodun okunmasını ve içinde gezinmeyi kolaylaştırmak için modül tanımlarını **ayrı bir dosyaya taşımak** isteyebilirsiniz.
+ Örneğin, birden fazla restoran modülü içeren **Liste 7-17**’deki koddan başlayalım. Bu kez tüm modülleri crate root dosyasında tanımlamak yerine, modülleri ayrı dosyalara ayıracağız. Bu durumda crate root dosyası `src/lib.rs`’dir; ancak aynı yöntem crate root dosyası `src/main.rs` olan binary crate’ler için de geçerlidir.
+ İlk olarak `front_of_house` modülünü kendi dosyasına çıkaracağız. `front_of_house` modülünün süslü parantezleri (`{}`) içindeki kodu kaldırıp yalnızca `mod front_of_house;` bildiriminin kalmasını sağlayacağız. Böylece `src/lib.rs`, **Liste 7-21**’de gösterilen kodu içerecektir. Bu noktada kod **derlenmeyecektir**, çünkü **Liste 7-22**’de gösterildiği gibi `src/front_of_house.rs` dosyasını henüz oluşturmadık.

**Dosya Adı:** `src/lib.rs`

```rust
mod front_of_house;

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
}
```

> `Liste 7-21`: Gövdesi `src/front_of_house.rs` dosyasında yer alacak olan `front_of_house` modülünün tanımlanması

+ Ardından, süslü parantezlerin (`{}`) içinde yer alan kodu **`src/front_of_house.rs`** adlı yeni bir dosyaya taşıyın; bu durum **Liste 7-22**’de gösterilmektedir. Derleyici, crate root dosyasında `front_of_house` adlı modül bildirimiyle karşılaştığı için, bu modülün içeriğini **bu dosyada araması gerektiğini bilir**.

**Dosya Adı:** `src/front_of_house.rs`

```rust
pub mod hosting {
    pub fn add_to_waitlist() {}
}
```

> `liste 7-22`: `src/front_of_house.rs` dosyasındaki `front_of_house` modülü içindeki tanımlar

+ Şunu unutmayın: Bir dosyayı mod bildirimi (`mod`) ile **modül ağacınıza yalnızca bir kez** yüklemeniz yeterlidir. Derleyici, dosyanın projenin bir parçası olduğunu öğrendikten sonra (ve `mod` ifadesini nereye koyduğunuza bakarak kodun modül ağacında **hangi konumda** yer aldığını bildiği için), projedeki diğer dosyalar bu yüklü dosyadaki koda, **bildirildiği yere giden bir yol (path)** kullanarak erişmelidir. Bu konu, **Paths for Referring to an Item in the Module Tree(7.3. Modül ağacındaki öğelere erişim yolları)"** bölümünde ele alınmıştır. Başka bir deyişle, `mod` anahtar kelimesi, bazı diğer programlama dillerinde görmüş olabileceğiniz bir **"nclude" (dosya ekleme)** işlemi değildir.


> [!NOTE] Title
> #### Kritik nokta: `mod` ne yapar, ne yapmaz?
> +  ✅ `mod` ne yapar?
> 	- Bir dosyayı projeye **tanıtır**
> 	- O dosyanın **modül ağacındaki yerini belirler**
> 	- Derleyiciye “Bu modül burada” der.
> +  ❌ `mod` ne yapmaz?
> 	- Dosyayı kopyalayıp başka yerlere yapıştırmaz.
> 	- C/C++’taki `#include` gibi **her kullanıldığında tekrar eklemez**
> #### Artık başka dosyalarda ne olur?
> + Diyelim ki `front_of_house` içinde bir fonksiyon var:
> ```rust
> pub mod hosting {
>    pub fn add_to_waitlist() {}
>}
> ```
> + Başka bir yerde **şunu yapmazsın:**
> ```rust
> mod front_of_house; // ❌ yanlış, tekrar etmiyorsun
> ```
> + Bunun yerine **path kullanırsın**:
> ```rust
> fn eat_at_restaurant() {
>    crate::front_of_house::hosting::add_to_waitlist();
>}
> ```
> + Çünkü;
> 	- Derleyici bu modülün **zaten projede olduğunu biliyor**
> 	- Nerede durduğunu da biliyor.
> 	- Sen sadece **adresini söylüyorsun**

+ Şimdi `hosting` modülünü kendi dosyasına ayıracağız. Bu süreç biraz farklıdır; çünkü `hosting`, kök (root) modülün değil, `front_of_house` modülünün **alt (child) modülüdür**. Bu nedenle `hosting` için olan dosyayı, modül ağacındaki üst modüllerin adını taşıyan yeni bir dizin içine koyacağız; bu durumda dizin adı **`src/front_of_house`** olacaktır.
+ `hosting` modülünü taşımaya başlamak için, `src/front_of_house.rs` dosyasını yalnızca `hosting` modülünün bildirimini içerecek şekilde değiştiririz:

**Dosya Adı:** `src/front_of_house.rs`

```rust
pub mod hosting;
```

+ Daha sonra, `hosting` modülüne ait tanımların yer alması için `src/front_of_house` adlı bir klasör ve bu klasörün içinde `hosting.rs` adlı bir dosya oluştururuz.

**Dosya Adı:** `src/front_of_house/hosting.rs`

```rust
pub fn add_to_waitlist() {}
```

+ Eğer bunun yerine `hosting.rs` dosyasını `src` dizinine koysaydık, derleyici `hosting.rs` içindeki kodun crate root’ta bildirilen bir `hosting` modülüne ait olmasını beklerdi; `front_of_house` modülünün bir alt modülü olarak bildirilmiş olmasını değil. Derleyicinin hangi modülün kodu için hangi dosyalara bakacağına dair kuralları, dizin ve dosya yapısının modül ağacına daha yakından uymasını sağlar.
+ Yani, `hosting.rs` dosyasını doğrudan `src` dizinine koyarsak, derleyici bu dosyayı kök modülde tanımlı bir `hosting` modülü olarak yorumlar. Oysa burada `hosting`, `front_of_house` modülünün alt modülüdür. Rust derleyicisinin dosya–modül eşleme kuralları, klasör ve dosya yapısının modül ağacıyla uyumlu olmasını amaçlar.


> [!NOTE]
> #### Alternatif Dosya Yolları
> Şimdiye kadar Rust derleyicisinin kullandığı **en yaygın (idiomatic)** dosya yollarını ele aldık; ancak Rust, **daha eski bir dosya yolu stilini** de destekler. Crate root’ta bildirilen `front_of_house` adlı bir modül için derleyici, modülün kodunu şu konumlarda arar:
>
> - `src/front_of_house.rs` (ele aldığımız yöntem)
>    
> - `src/front_of_house/mod.rs` (eski stil, hâlâ desteklenmektedir)
>    
>
> `front_of_house` modülünün bir alt modülü olan `hosting` adlı bir modül için ise derleyici, modülün kodunu şu konumlarda arar:
> 
> - `src/front_of_house/hosting.rs` (ele aldığımız yöntem)
>    
> - `src/front_of_house/hosting/mod.rs` (eski stil, hâlâ desteklenmektedir)
>    
>
> Aynı modül için **her iki stili birden** kullanırsanız, derleyici hatası alırsınız. Aynı proje içinde **farklı modüller için** bu iki stilin karışık şekilde kullanılması mümkündür; ancak bu durum projede gezinen kişiler için kafa karıştırıcı olabilir.
>
> `mod.rs` adlı dosyaları kullanan stilin temel dezavantajı şudur: Projenizde çok sayıda `mod.rs` dosyası oluşabilir ve bunları editörde aynı anda açık tuttuğunuzda hangisinin hangi modüle ait olduğunu ayırt etmek zorlaşabilir.

+ Her modülün kodunu ayrı bir dosyaya taşıdık ve **modül ağacı (module tree)** aynı şekilde kaldı. Tanımlar artık farklı dosyalarda bulunsa bile, `eat_at_restaurant` içindeki fonksiyon çağrıları **hiçbir değişiklik yapılmadan** çalışmaya devam eder. Bu teknik, modüller boyut olarak büyüdükçe onları yeni dosyalara taşımanıza olanak tanır.
+ Ayrıca `src/lib.rs` içindeki `pub use crate::front_of_house::hosting` ifadesi de değişmemiştir ve `use` anahtar kelimesinin, crate’in bir parçası olarak **hangi dosyaların derleneceği üzerinde hiçbir etkisi yoktur**. Modülleri tanımlayan anahtar kelime `mod`’dur ve Rust, bir modül için gerekli kodu bulmak üzere, modül ile **aynı ada sahip** dosyaya bakar.

### 7.5.1. Özet:

+ Rust, bir paketi birden fazla crate’e(*bir veya birden fazla binary crate ve bir tane library crate* ), bir crate’i ise modüllere ayırmanıza olanak tanır(package → crate → module). Böylece bir modülde tanımlanmış öğelere başka bir modülden erişebilirsiniz. Bunu **mutlak (absolute)** veya **göreli (relative)** yollar belirterek yapabilirsiniz. Bu yollar, `use` ifadesiyle kapsama alınabilir; böylece aynı kapsam içinde bir öğeyi birden fazla kez kullanırken daha kısa yollar tercih edebilirsiniz. Modül içindeki kodlar varsayılan olarak **özel (private)**tir, ancak tanımları **public** yapmak için `pub` anahtar kelimesini ekleyebilirsiniz.
+ Bir sonraki bölümde, düzgün şekilde organize edilmiş kodunuzda(modüler, crate, `use` ve `pub` dosya yapısın düzenlenmesi) kullanabileceğiniz standart kütüphanedeki bazı **koleksiyon veri yapıları**nı inceleyeceğiz.

# 8. Yaygın Koleksiyonlar

+ Rust’un standart kütüphanesi, **koleksiyonlar** olarak adlandırılan, son derece kullanışlı birçok veri yapısını içerir. Diğer veri türlerinin çoğu tek bir değeri temsil ederken, koleksiyonlar **birden fazla değeri** barındırabilir. 


> [!caution]
>
> + Yerleşik dizi (array) ve demet (tuple) türlerinden farklı olarak, bu koleksiyonların işaret ettiği veriler **heap** üzerinde saklanır. Bu da veri miktarının derleme zamanında bilinmesini gerektirmez; program çalışırken **büyüyebilir veya küçülebilir**.

+ Her koleksiyon türünün kendine özgü yetenekleri ve maliyetleri vardır; bulunduğunuz duruma uygun olanı seçmek ise zamanla geliştireceğiniz bir beceridir. Bu bölümde, Rust programlarında **çok sık kullanılan üç koleksiyonu** ele alacağız:


> [!NOTE]
> + **Bir vektör (vector)**, değişken sayıda(yani, eleman sayısı **derleme zamanında sabit değildir**) değeri **yan yana** saklamanıza(**bellekte ardışık (contiguous)** olarak saklanma) olanak tanır.
> + **Bir string**, karakterlerden oluşan bir koleksiyondur. Daha önce `String` türünden bahsetmiştik; ancak bu bölümde onu **ayrıntılı olarak** ele alacağız.
> + **Bir hash map**, belirli bir anahtarla (key) bir değeri ilişkilendirmenizi sağlar. Bu yapı, **map (eşleme)** olarak adlandırılan daha genel bir veri yapısının özel bir uygulamasıdır.
> + Yani,
> 	- Map = genel fikir
> 	- HashMap = bu fikrin **belirli bir teknikle** (hash) hayata geçirilmiş hâli
> + Aynı map fikri farklı şekillerde de uygulanabilir:
> 	- HashMap (hash tabanlı)
> 	- TreeMap / BTreeMap (ağaç tabanlı)
> 	- OrderedMap (sıralı)

+ Standart kütüphanenin sunduğu diğer koleksiyon türleri hakkında bilgi edinmek için [belgelere (dokümantasyona)](https://doc.rust-lang.org/std/collections/index.html) bakabilirsiniz.
+ Bu bölümde; vektörlerin, string’lerin ve hash map’lerin nasıl oluşturulup güncellendiğini ve her birini özel kılan özelliklerin neler olduğunu ele alacağız.

## 8.1. Vektörler Kullanarak Değer Listelerinin Saklanması:

+ İnceleyeceğimiz ilk koleksiyon türü `Vec<T>`’dir; buna vektör de denir. Vektörler, birden fazla değeri bellekte yan yana yerleştiren tek bir veri yapısı içinde saklamanıza olanak tanır. Vektörler yalnızca aynı türdeki değerleri saklayabilir. Bir dosyadaki metin satırları ya da bir alışveriş sepetindeki ürün fiyatları gibi, bir öğe listesiniz olduğunda vektörler oldukça kullanışlıdır.

### 8.1.1. Yeni bir Vektör Oluşturma:

+ Yeni, boş bir vektör oluşturmak için `Liste 8-1`’de gösterildiği gibi `Vec::new` fonksiyonunu çağırırız.

```rust
fn main() {
    let v: Vec<i32> = Vec::new();
}
```

> `Liste 8-1`: `i32` türündeki değerleri tutmak için yeni, boş bir vektör oluşturma

+ Burada bir **tür belirtimi (type annotation)** eklediğimize dikkat edin. Bu vektöre herhangi bir değer eklemediğimiz için, Rust hangi türden elemanlar saklamak istediğimizi bilemez. Bu önemli bir noktadır.
+ Vektörler **generic (genel)** yapılar kullanılarak uygulanmıştır; generic’lerin kendi türlerinizle nasıl kullanılacağını 10. Bölüm’de ele alacağız.
+ Şimdilik şunu bilmeniz yeterlidir: standart kütüphane tarafından sağlanan `Vec<T>` tipinin herhangi bir tipi tutabileceğini bilin.
+ Belirli bir tipi tutacak bir vector oluşturduğumuzda, tipi açılı parantezler(`<>`) içinde belirtebiliriz.
+ `Liste 8-1`’de, `v` değişkenindeki **`Vec<T>`**’nin `i32` türünde elemanlar tutacağını Rust’a söylemiş olduk.
+ Çoğu zaman, başlangıçta değerler içeren bir **`Vec<T>`** oluşturursunuz ve Rust hangi türde değer saklamak istediğinizi **kendisi çıkarır (type inference)**; bu nedenle genellikle bu tür belirtimine ihtiyaç duymazsınız. Rust, bu işi kolaylaştırmak için **`vec!` makrosunu** sağlar. Bu makro, verdiğiniz değerleri içeren yeni bir vektör oluşturur. `Liste 8-2`, 1, 2 ve 3 değerlerini tutan yeni bir **`Vec<i32>`** oluşturur. Tamsayı türü `i32`’dir çünkü 3. Bölüm’deki **"[Veri Türleri](https://doc.rust-lang.org/book/ch03-02-data-types.html#data-types)"** kısmında da bahsettiğimiz gibi, varsayılan tamsayı türü `i32`’dir.

```rust
fn main() {
    let v = vec![1, 2, 3];
}
```

> `Liste 8-2`: İçinde değerler bulunan yeni bir vektörün oluşturulması

+ Başlangıçta `i32` türünde değerler verdiğimiz için, Rust `v` değişkeninin türünün `Vec<i32>` olduğunu çıkarım yoluyla belirleyebilir ve ayrıca bir tür belirtimine gerek kalmaz. Bir sonraki adımda, bir vektörün nasıl değiştirileceğine bakacağız.

### 8.1.2. Bir Vektörü Güncelleme:

+ Bir vektör oluşturup daha sonra içine elemanlar eklemek için, Liste 8-3’te gösterildiği gibi `push` metodunu kullanabiliriz.

```rust
fn main() {
    let mut v = Vec::new();

    v.push(5);
    v.push(6);
    v.push(7);
    v.push(8);
}
```

> `Liste 8-3`: Bir vektöre değerler eklemek için `push` metodunun kullanılması

+ Her değişkende olduğu gibi, değerini değiştirebilmek istiyorsak `mut` anahtar kelimesini kullanarak onu değiştirilebilir (`mutable`) yapmamız gerekir; bu konu 3. Bölümde ele alınmıştı. İçine koyduğumuz sayıların tamamı `i32` türündedir ve Rust bu bilgiyi verilerden kendisi çıkardığı için `Vec<i32>` şeklinde bir tür belirtimine `(type annotation`) ihtiyaç duymayız.
+ Bir vektörde saklanan bir değere başvurmanın (erişmenin) iki yolu vardır: indeksleme yoluyla ya da `get` metodunu kullanarak. Aşağıdaki örneklerde, daha fazla açıklık sağlamak için bu fonksiyonlardan dönen değerlerin türlerini özellikle belirtmiş bulunuyoruz.”
+ `Liste 8-4`, bir vektördeki bir değere erişmenin her iki yöntemini de göstermektedir: indeksleme sözdizimi ve `get` metodu.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];

    let third: &i32 = &v[2];
    println!("The third element is {third}");

    let third: Option<&i32> = v.get(2);
    match third {
        Some(third) => println!("The third element is {third}"),
        None => println!("There is no third element."),
    }
}
```

> `Liste 8-4`: Bir vektördeki bir öğeye erişmek için indeksleme sözdizimini ve `get` metodunu kullanma

**Çıktısı:**

```rust
The third element is 3  
The third element is 3
```


> [!CAUTION]
> + Burada birkaç detaya dikkat edelim.
> + Üçüncü elemana erişmek için indeks değeri olarak **2** kullanıyoruz; çünkü vektörler sıfırdan başlayarak numaralandırılır.
> + `&` ve `[]` kullanımı, bize verilen indeks değerindeki elemana bir **referans** verir.
> + `get` metodunu, indeksi argüman olarak vererek kullandığımızda ise `match` ile kullanabileceğimiz bir `Option<&T>` elde ederiz


+ Rust, bir elemana referans vermek için bu iki farklı yolu sunar; böylece mevcut elemanların aralığı dışında bir indeks değeri kullanmaya çalıştığınızda programın nasıl davranacağını seçebilirsiniz. **Örnek olarak**, beş elemanlı bir vektörümüz olduğunu ve ardından her iki teknikle de indeks değeri **100** olan bir elemana erişmeye çalıştığımızda ne olacağını görelim. Bu durum, **`Liste 8-5`**’te gösterilmektedir.

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];

    let does_not_exist = &v[100];
    let does_not_exist = v.get(100);
}
```

> `Liste 8-5`: Beş eleman içeren bir vektörde, indeks değeri 100 olan elemana erişmeye çalışma

+ Bu kodu çalıştırdığımızda, ilk yöntem olan `[]` **programın panic yapmasına** neden olur; çünkü var olmayan bir elemana referans vermektedir. Bu yöntem, vektörün sonunu aşan bir elemana erişilmeye çalışıldığında programın **çökmesini istediğiniz** durumlarda kullanmak için en uygunudur.
+ `get` metoduna ise vektörün sınırları dışında bir indeks verildiğinde, panic oluşturmadan **`None` döndürür**. Bu yöntemi, normal koşullar altında zaman zaman vektörün aralığı dışındaki bir elemana erişme ihtimali varsa kullanırsınız. Bu durumda kodunuz, **Bölüm 6’da anlatıldığı gibi**, `Some(&element)` veya `None` durumlarını ele alacak bir mantığa sahip olur.  Örneğin, indeks değeri bir kullanıcının girdiği bir sayıdan geliyor olabilir. Kullanıcı yanlışlıkla çok büyük bir sayı girerse ve program `None` değeri alırsa, kullanıcıya mevcut vektörde kaç eleman olduğunu söyleyebilir ve geçerli bir değer girmesi için ona bir şans daha verebilirsiniz. Bu yaklaşım, bir yazım hatası nedeniyle programın çökmesinden çok daha **kullanıcı dostudur**.
+ Program geçerli bir referansa sahip olduğunda, **borrow checker**, sahiplik ve ödünç alma kurallarını (**Bölüm 4’te ele alınmıştır**) uygulayarak bu referansın ve vektörün içeriğine ait diğer tüm referansların geçerli kalmasını sağlar. Aynı kapsam içinde hem **mutable** hem de **immutable** referanslara sahip olamayacağınızı belirten kuralı hatırlayın. Bu kural, **Liste 8-6**’da geçerlidir; burada bir vektörün ilk elemanına immutable bir referans tutarken, vektörün sonuna yeni bir eleman eklemeye çalışırız. Eğer fonksiyonun ilerleyen kısmında bu elemana tekrar referans vermeye çalışırsak, bu program çalışmaz.

```rust
fn main() {
    let mut v = vec![1, 2, 3, 4, 5];

    let first = &v[0];   // immutable referans

    v.push(6);           // v üzerinde mutable işlem

    println!("The first element is: {first}");
}
```

> Liste 8-6: Bir elemana referans varken vektöre yeni bir eleman ekleme girişimi

+ Bu kodun derlenmesi şu hataya yol açacaktır:

```rust
$ cargo run
   Compiling collections v0.1.0 (file:///projects/collections)
error[E0502]: cannot borrow `v` as mutable because it is also borrowed as immutable
 --> src/main.rs:6:5
  |
4 |     let first = &v[0];
  |                  - immutable borrow occurs here
5 |
6 |     v.push(6);
  |     ^^^^^^^^^ mutable borrow occurs here
7 |
8 |     println!("The first element is: {first}");
  |                                     ------- immutable borrow later used here

For more information about this error, try `rustc --explain E0502`.
error: could not compile `collections` (bin "collections") due to 1 previous error
```


+ **Liste 8-6’daki kod**, ilk bakışta çalışması gerekiyormuş gibi görünebilir: Vektörün ilk elemanına alınmış bir referans, neden vektörün sonundaki değişikliklerle ilgilensin ki?
+ Bu hatanın nedeni, **vektörlerin çalışma şeklidir**. Vektörler, değerleri bellekte **yan yana (ardışık)** olarak sakladıkları için, vektörün sonuna yeni bir eleman eklemek; eğer vektörün şu anda bulunduğu yerde tüm elemanları yan yana koyacak kadar alan yoksa, **yeni bir bellek alanı ayırmayı** ve eski elemanları bu yeni alana **kopyalamayı** gerektirebilir.
+ Bu durumda, ilk elemana ait referans **artık serbest bırakılmış (deallocate edilmiş) belleği** işaret ediyor olurdu. **Ödünç alma (borrowing) kuralları**, programların bu tür bir duruma düşmesini engellemek için vardır.


> [!tip]
> + Not: `Vec<T>` tipinin nasıl uygulandığına dair daha fazla ayrıntı için [The Rustonomicon](https://doc.rust-lang.org/nomicon/vec/vec.html) belgesine bakın.

### 8.1.3. Bir vektördeki değerler üzerinde dolaşma(Iterasyon):

+ Bir vektördeki her bir elemana sırasıyla erişmek için, tek tek indeksler kullanmak yerine tüm elemanlar üzerinde **iterasyon (yineleme)** yaparız. **Liste 8-7**, `i32` değerlerinden oluşan bir vektördeki her elemana **immutable referanslar** alarak bunları yazdırmak için bir `for` döngüsünün nasıl kullanılacağını göstermektedir.

```rust
fn main() {
    let v = vec![100, 32, 57];
    for i in &v {
        println!("{i}");
    }
}
```

> `Liste 8-7`: Bir vektördeki her bir elemanı, `for` döngüsü kullanarak elemanlar üzerinde iterasyon yapıp yazdırma

+ Ayrıca, **mutable(`mut v`)** bir vektördeki her bir elemana **mutable referanslar(`&mut v`)** üzerinden iterasyon yaparak tüm elemanlarda değişiklik de yapabiliriz. **Liste 8-8**’deki `for` döngüsü, her bir elemana 50 eklemektedir.

```rust
let mut v = vec![100, 32, 57];
for i in &mut v {
    *i += 50;
}
```

> `Liste 8-8`: Bir vektördeki elemanlara mutable referanslar(`&mut v`) üzerinden iterasyon yapma

+ Mutable referansın işaret ettiği değeri değiştirebilmek için, `+=` operatörünü kullanmadan önce `i` içindeki değere ulaşmak amacıyla **`*` dereference (çözümleme) operatörünü** kullanmamız gerekir. *Dereference* operatörü hakkında daha fazla bilgiyi **Bölüm 15’teki "[Referansı Takip Ederek Değere Ulaşma](https://doc.rust-lang.org/book/ch15-02-deref.html#following-the-pointer-to-the-value-with-the-dereference-operator)"** başlığında ele alacağız.
+ Bir vektör üzerinde ister immutable ister mutable şekilde iterasyon yapmak, **borrow checker** kuralları sayesinde güvenlidir. **`Liste 8-7`** ve **`Liste 8-8`**’deki `for` döngülerinin gövdelerinde eleman eklemeye ya da çıkarmaya çalışsaydık, **`Liste 8-6`**’daki koda benzer bir derleyici hatası alırdık. Bunun nedeni, `for` döngüsünün vektör üzerinde tuttuğu referansın, vektörün tamamının aynı anda değiştirilmesini engellemesidir.

### 8.1.4. Birden çok türü depolamak için bir enum kullanılması:

+ Vektörler yalnızca **aynı türden** değerleri saklayabilir. Bu durum bazen kullanışsız olabilir; çünkü **farklı türlerde öğelerden oluşan bir listeyi** saklama ihtiyacı olan pek çok kullanım senaryosu vardır. Neyse ki, bir `enum`’un varyantları **aynı enum türü** altında tanımlanır. Bu nedenle, farklı türlerde elemanları temsil etmek için tek bir türe ihtiyaç duyduğumuzda, bir `enum` tanımlayıp kullanabiliriz.

+ Örneğin, bir elektronik tablodaki (spreadsheet) bir satırdan değerler almak istediğimizi düşünelim. Bu satırdaki bazı sütunlar tamsayılar, bazıları kayan noktalı sayılar ve bazıları da metin (string) içerebilir. Bu farklı değer türlerini tutacak varyantlara sahip bir `enum` tanımlayabiliriz ve tüm bu varyantlar **aynı tür**, yani enum’un kendisi olarak kabul edilir. Daha sonra, bu enum’u tutan bir vektör oluşturabiliriz; böylece sonuç olarak **farklı türlerde değerleri** tek bir vektör içinde saklamış oluruz. Bu yaklaşım **Liste 8-9**’da gösterilmektedir.

```rust
fn main() {
    enum SpreadsheetCell {
        Int(i32),
        Float(f64),
        Text(String),
    }

    let row = vec![
        SpreadsheetCell::Int(3),
        SpreadsheetCell::Text(String::from("blue")),
        SpreadsheetCell::Float(10.12),
    ];
}
```

> `Liste 8-9`: Farklı türlerdeki değerleri tek bir vektörde saklamak için bir `enum` tanımlama

+ Rust, bir vektörün içinde hangi türlerin bulunacağını **derleme zamanında** bilmek zorundadır; böylece her bir elemanı saklamak için **heap üzerinde tam olarak ne kadar bellek ayrılması gerektiğini** hesaplayabilir. Ayrıca, bu vektörde **hangi türlere izin verildiğini** açıkça belirtmemiz gerekir.
+ Eğer Rust, bir vektörün herhangi bir türde değeri tutmasına izin verseydi, vektör elemanları üzerinde yapılan işlemler sırasında bu türlerin bir veya birkaçının **hata üretme ihtimali** olurdu.
+ Bir `enum` ile birlikte `match` ifadesi kullanmak, **Bölüm 6’da tartışıldığı gibi**, Rust’ın tüm olası durumların derleme zamanında ele alındığından emin olmasını sağlar.,
+ Eğer bir programın çalışma zamanında bir vector'de depolamak için alacağı tiplerin tam listesini bilmiyorsanız, `enum` tekniği işe yaramayacaktır. Bunun yerine, Bölüm 18'de ele alacağımız bir `trait` nesnesi kullanabilirsiniz.
+ Artık vektörlerin en yaygın kullanım yollarından bazılarını ele aldığımıza göre, standart kütüphanenin `Vec<T>` üzerinde tanımladığı pek çok faydalı metot için **[API dokümantasyonunu](https://doc.rust-lang.org/std/vec/struct.Vec.html)** incelemeniz faydalı olacaktır. Örneğin, `push` metoduna ek olarak, `pop` metodu da son elemanı kaldırır ve geri döndürür.

### 8.1.5. Bir vektör düşürüldüğünde, elemanları da düşürülür:

+ Diğer tüm `struct`’larda olduğu gibi, bir vektör de kapsam (scope) dışına çıktığında serbest bırakılır; bu durum `Liste 8-10`’da gösterilmektedir.

```rust
fn main() {
    {
        let v = vec![1, 2, 3, 4];

        // do stuff with v
    } // <- v goes out of scope and is freed here
}
```

> `Liste 8-10`: Vektörün ve içindeki elemanların nerede düşürüldüğünü (drop edildiğini) gösterme

+ Vektör düşürüldüğünde (drop edildiğinde), içindeki tüm içerik de düşürülür; yani tuttuğu tamsayılar bellekten temizlenir. **Borrow checker**, bir vektörün içeriğine ait tüm referansların(*yani, içeriğine yapılan referansların*), yalnızca vektörün kendisi geçerli olduğu sürece kullanılmasını garanti eder.
+ Şimdi bir sonraki koleksiyon türüne geçelim: **String**!

## 8.2. UTF-8 Kodlamalı Metinlerin Dizeler İçinde Saklanması:

+ 4. Bölümde string’lerden bahsetmiştik, ancak şimdi onları daha ayrıntılı olarak inceleyeceğiz.
+ Yeni Rust kullanıcıları (Rustacean’lar) genellikle string’ler konusunda zorlanır; bunun üç temel nedeni vardır:
	1. Rust’ın olası hataları açıkça ortaya koyma eğilimi,
	2. string’lerin birçok programcının sandığından daha karmaşık bir veri yapısı olması
	3. ve UTF-8 kodlaması.
+ Bu faktörler bir araya geldiğinde, özellikle diğer programlama dillerinden gelenler için konu zorlayıcı hâle getirebilir.
+ String’leri koleksiyonlar bağlamında ele alıyoruz, çünkü string’ler baytların (bytes) bir koleksiyonu olarak uygulanmıştır ve bu baytlar metin olarak yorumlandığında kullanışlı işlevsellik sağlayan bazı metotlarla birlikte gelir.
+ Bu bölümde, her koleksiyon türünde bulunan `String` üzerindeki işlemleri ele alacağız; örneğin oluşturma, güncelleme ve okuma işlemleri.
+ Ayrıca `String`’in diğer koleksiyonlardan farklı olduğu noktaları da tartışacağız; özellikle insanların ve bilgisayarların string verisini yorumlama biçimleri arasındaki farklar nedeniyle, bir `String` üzerinde indeksleme yapmanın neden karmaşık olduğunu açıklayacağız.

### 8.2.1. String’leri Tanımlama:

+ Öncelikle string terimi ile ne demek istediğimizi tanımlayalım. Rust'ın temel dilinde sadece bir string tipi vardır: genellikle ödünç alınmış formu `&str` olarak görülen `string slice str`.(`String Slice => &str`)


> [!tip]
> + Rust dilinin temelinde yalnızca `str` adlı bir string türü vardır ve bu tür pratikte hep referans (`&str`) olarak kullanılır; `String` ise bunun üzerine inşa edilmiş, heap’te saklanan ayrı bir standart kütüphane yapısıdır.

```rust
// "merhaba" bellekte bir yerlerde saklanıyor
// &str → o yeri gösteren bir işaretçi

let s: &str = "merhaba";
//     ^^^^
//     Bu bir referans (pointer)
//     Gerçek veriyi gösteriyor
```

```rust
BELLEK:
┌─────────────────┐
│ "merhaba" ← str │  ← Gerçek veri (str tipi)
└─────────────────┘
        ↑
        │
    ┌───┴────┐
    │  &str  │  ← İşaretçi (referans)
    └────────┘
```


+ Bölüm 4'te, başka bir yerde depolanan UTF-8 kodlamalı *string* verilerine referanslar olan *string slice*'ları tartışmıştık. Örneğin, *string literal*'leri programın *binary*'sinde saklanır ve bu yüzden *string slice*'lardır.

+ **String türü**, Rust’ın çekirdek dilinin bir parçası olarak kodlanmış değil, **standart kütüphane tarafından sağlanan**; **büyüyebilen (growable)**, **değiştirilebilir (mutable)**, **sahipliği olan (owned)** ve **UTF-8 kodlamalı** bir string türüdür.

+ Rust geliştiricileri (“Rustacean”lar) Rust’ta “string” ifadesini kullandıklarında, yalnızca tek bir türü değil; **String** veya **string slice (`&str`)** türlerinden herhangi birini kastediyor olabilirler.

+ Bu bölüm büyük ölçüde **String** türü üzerine odaklansa da, Rust’ın standart kütüphanesinde her iki tür de yoğun biçimde kullanılır ve hem **String** hem de **string slice** türleri **UTF-8 kodlamalıdır**.


**Bellek Düzeni:**

```rust
PROGRAM BINARY (Disk'te):
┌──────────────────┐
│ "merhaba" literal│  ← Compile-time'da buraya yerleştirilir
└──────────────────┘
        ↑
        │
    ┌───┴────┐
    │  &str  │  ← Programın ömrü boyunca geçerli (&'static str)
    └────────┘

HEAP (Çalışma zamanında):
┌─────────────────────┐
│ String("merhaba")   │  ← Runtime'da oluşturulur
└─────────────────────┘
        ↑
        │
    ┌───┴────┐
    │  &str  │  ← String yaşadığı sürece geçerli
    └────────┘
```

### 8.2.2. Yeni bir String Oluşturma:

+ `Vec<T>` ile mevcut olan birçok işlem, String ile de mevcuttur çünkü String aslında, bazı ek garantiler, kısıtlamalar ve yeteneklerle birlikte bir bayt vektörü(*vector of bytes*) çevresine uygulanmış bir sarmalayıcıdır(*wrapper*). `Vec<T>` ve String ile aynı şekilde çalışan bir fonksiyon örneği, Liste 8-11'de gösterilen bir örnek oluşturmak için kullanılan `new` fonksiyonudur.


> [!tip]
> + Bu paragraf, Rust programlama dilinde `String` tipinin dahili olarak bir `Vec<u8>` (bayt vektörü) üzerine inşa edildiğini ve bu nedenle vektörlerle benzer metodlara sahip olduğunu açıklıyor. 
> + `new()` fonksiyonu her ikisinde de boş bir örnek oluşturmak için kullanılır. Metindeki "wrapper" terimi, "sarmalayıcı" veya "kapsayıcı" olarak çevrilebilir; burada String'in temelde bir vektör olduğu ama ek kurallar (örneğin geçerli UTF-8 kodlaması zorunluluğu) getirdiği vurgulanıyor.


```rust
fn main() {
    let mut s = String::new();
}
```

> `Liste 8-11`: Yeni, boş bir `String` oluşturma

+ Bu satır, daha sonra içine veri yükleyebileceğimiz **`s` adlı yeni ve boş bir string** oluşturur.
+ Çoğu zaman string’i başlatırken kullanmak istediğimiz **bazı başlangıç verileri** olur. Bunun için, **string literal’lerin de uyguladığı `Display` trait’ini** uygulayan herhangi bir tür üzerinde kullanılabilen **`to_string`** metodunu kullanırız.
	- Bu cümlede denmek istenen şudur: String’i boş oluşturmak yerine, `Display` trait’ini uygulayan (örneğin string literal gibi) bir değeri `to_string()` ile doğrudan `String` olarak başlatabiliriz.

+  **Liste 8-12**, bununla ilgili iki örnek göstermektedir.

```rust
fn main() {
    let data = "initial contents";

    let s = data.to_string();

    // The method also works on a literal directly:
    let s = "initial contents".to_string();
}
```

> `Liste 8-12`: Bir *string literal*’den `to_string` metodu kullanarak bir `String` oluşturma

+ Bu kod, “initial contents” içeriğine sahip bir `String` oluşturur.

> [!NOTE]
> #### 1. `Display` trait burada neden geçiyor?
> + Rust’ta `to_string()` **her türde otomatik olarak yoktur**.
> + Bir türde `to_string()` kullanılabilmesi için:
> 	- O türün **`Display` trait’ini uygulaması gerekir**
> 	- Yani, Bu tür ekrana yazdırılabiliyor mu?
> 	- Eğer cevap **evet** ise: Rust onu string’e çevirebilir.
> #### 2. Sadece string’ler mi `to_string()` kullanabilir?
> + Hayır. `Display` uygulayan **her şey** kullanabilir.
> ```rust
> let a = 10.to_string();        // i32 → String
> let b = 3.14.to_string();     // f64 → String
> let c = true.to_string();     // bool → String
> ```
> + Hepsi çalışır çünkü: `i32`, `f64`, `bool` → `Display` uygular
> #### 3. Neden böyle bir sistem var?
> + Rust şunu ister:
> 	- Rastgele türlerin string’e çevrilmesini engellemek
> 	- Sadece **mantıklı biçimde yazdırılabilen** türlere izin vermek

+ Bir string literal’den `String` oluşturmak için `String::from` fonksiyonunu da kullanabiliriz. Liste 8-13’teki kod, `to_string` kullanan Liste 8-12’deki kod ile eşdeğerdir.

```rust
fn main() {
    let s = String::from("initial contents");
}
```

> `Liste 8-13`: Bir *string literal*’den `String` oluşturmak için `String::from` fonksiyonunun kullanılması

+ String’ler çok farklı amaçlarla kullanıldığından, string’ler için birçok farklı genel (generic) API kullanabiliriz; bu da bize pek çok seçenek sunar. Bazıları gereksiz veya tekrarlı gibi görünebilir, ancak hepsinin kendine özgü bir yeri vardır. Bu bağlamda, `String::from` ile `to_string` aynı işi yapar; dolayısıyla hangisini seçeceğiniz, daha çok stil ve okunabilirlik meselesidir.


> [!TIP]
> #### Genel(Generic) API nedir?
> +  **Tanım:** tek bir somut tipe bağlı olmayan, birden fazla türle çalışabilecek şekilde tasarlanmış fonksiyonlar, metodlar veya arayüzlerdir.
> + Bu fonksiyon sadece tek bir türle sınırlı değil.
> ```rust
> let s = "Hello".to_string();
> let n = 5.to_string();
> ```
> + **İki farklı tür**, ama **aynı metot** çalışıyor.
> + **Özet:** Genel (generic) API, Rust’ta bir fonksiyonun veya metodun tek bir türe bağlı kalmadan, belirli bir davranışı (trait’i) sağlayan tüm türlerle çalışabilmesini sağlayan tasarım yaklaşımıdır



+ String’lerin UTF-8 kodlamalı olduğunu unutmayın; bu nedenle, `Liste 8-14`’te gösterildiği gibi, uygun şekilde kodlanmış her türlü veriyi string’lerin içinde tutabiliriz.

```rust
fn main() {
    let hello = String::from("السلام عليكم");
    let hello = String::from("Dobrý den");
    let hello = String::from("Hello");
    let hello = String::from("שלום");
    let hello = String::from("नमस्ते");
    let hello = String::from("こんにちは");
    let hello = String::from("안녕하세요");
    let hello = String::from("你好");
    let hello = String::from("Olá");
    let hello = String::from("Здравствуйте");
    let hello = String::from("Hola");
}
```

> `Liste 8-14`: Farklı dillerdeki selamlaşma ifadelerinin string’lerde saklanması

+ Bunların hepsi geçerli (`valid`) `String` değerleridir.

### 8.2.3. Bir String'i Güncelleme:

+ Bir `String`, içine daha fazla veri eklendiğinde boyut olarak büyüyebilir ve içeriği değişebilir; tıpkı bir `Vec<T>`’nin içeriğinin değişebilmesi gibi.
+ Ayrıca, `String` değerlerini birleştirmek (*concatenate*) için `+` operatörünü veya `format!` makrosunu pratik bir şekilde kullanabilirsiniz.


#### 8.2.3.1. `push_str` ya da `push` kullanarak String’e veri ekleme:

+ `Liste 8-15`'te gösterildiği gibi, bir *string slice*(`&str`) eklemek için `push_str` metodunu kullanarak bir String'i büyütebiliriz.

```rust
fn main() {
    let mut s = String::from("foo");
    s.push_str("bar");
}
```

> Liste 8-15: `push_str` metodunu kullanarak bir String’e *string slice*(`&str`)  ekleme

+ Bu iki satırdan sonra `s`, `foobar` içeriğine sahip olacaktır. `push_str` metodu bir `string slice` (`&str`) alır; çünkü parametrenin sahipliğini (*ownership*) almamız gerekmez.

> [!TIP]
> + `push_str` metodunun imzası:
> ```rust
>  pub fn push_str(&mut self, string: &str) {
> ```
> + Metot **`String` değil `&str` alır**
> + Yani **sahiplik devri yoktur**, sadece **ödünç alma (borrowing)** vardır

+ Örneğin, `Liste 8-16`’daki kodda, `s2`’nin içeriğini `s1`’e ekledikten sonra `s2`’yi hâlâ kullanabilmek istiyoruz.

```rust
fn main() {
    let mut s1 = String::from("foo");
    let s2 = "bar";
    s1.push_str(s2);
    println!("s2 is {s2}");
}
```

> `Liste 8-16`: Bir `string slice`'nın içeriğini bir `String`’e ekledikten sonra onu kullanmaya devam etmek

**Çıktısı:**

```
s2 is bar
```

+ Eğer `push_str` metodu `s2`'nin sahipliğini alsaydı, son satırda onun değerini yazdıramazdık. Ancak bu kod, beklediğimiz şekilde çalışmaktadır.
----
+ `push` metodu tek bir karakteri parametre olarak alır ve bu karakteri `String`’e ekler. `Liste 8-17`'de, `push` metodu kullanılarak bir `String`’e `l` harfi eklenmektedir.

```rust
fn main() {
    let mut s = String::from("lo");
    s.push('l');
}
```

> `Liste 8-17`: `push` kullanarak bir `String` değerine tek bir karakter ekleme

+ Sonuç olarak, `s` değişkeni `lol` değerini içerecektir.
#### 8.2.3.2. `+` operatörü ya da `format!` makrosu kullanılarak *string* birleştirme:

+ Çoğu zaman, var olan iki *string*’i birleştirmek isteyeceksiniz. Bunu yapmanın bir yolu, `Liste 8-18`’de gösterildiği gibi **`+` operatörünü** kullanmaktır.

```rust
fn main() {
	let s1 = String::from("Hello, ");
	let s2 = String::from("world!");
	let s3 = s1 + &s2; // s1’in burada taşındığına (move edildiğine) ve artık kullanılamayacağına dikkat edin
}
```

> `Liste 8-18`: `+` operatörünü kullanarak iki `String` değerini yeni bir `String` değeri hâline getirme

+ `s3` string’i `"Hello, world!"` değerini içerecektir. 
+ Toplama işleminden sonra `s1`’in artık geçerli olmamasının nedeni ve `s2` için neden bir referans kullandığımız, `+` operatörünü kullandığımızda çağrılan metodun imzasıyla ilgilidir.
+ `+` operatörü, `add` metodunu kullanır ve bu metodun imzası kabaca şu şekildedir:

```rust
fn add(self, s: &str) -> String {
```

+ Standart kütüphanede `add` metodu, jenerikler (*generics*) ve ilişkili tipler (*associated types*) kullanılarak tanımlanmıştır.
+ Burada ise somut tipleri yerleştirdik; bu da metodu `String` değerleriyle çağırdığımızda olan şeydir.
	- Yani, Rust standart kütüphanesinde `add` metodu **jenerik** olarak tanımlıdır. Yani gerçek tipler yerine **genel (soyut) tipler** kullanılır. Ancak sen bu metodu gerçek bir kodda çağırdığında, Rust bu genel tiplerin yerine **gerçek (somut) tipleri(concrete types)** koyar.
	- Biz burada jenerik tanımı değil, `String` ile çağrıldığında ortaya çıkan gerçek (somut) hâlini gösteriyoruz
+ Generic'leri Bölüm 10'da tartışacağız.
+ Bu imza bize + operatörünün zor kısımlarını anlamak için ihtiyacımız olan ipuçlarını verir.
+ Ancak bir durun—`&s2`’nin tipi `&String`tir, `add` fonksiyonunun ikinci parametresinde belirtilen `&str` değildir. O hâlde Liste 8-18 neden derleniyor?
+ `add` çağrısında `&s2`’yi kullanabilmemizin sebebi, derleyicinin `&String` argümanını otomatik olarak `&str`’ye **zorlayabilmesidir (coerce)**.
+ `add` metodunu çağırdığımızda Rust, burada `&s2`’yi `&s2[..]` hâline dönüştüren bir **deref coercion** (dereference zorlaması) uygular.
+ Deref coercion konusunu Bölüm 15’te daha ayrıntılı ele alacağız. `add` metodu `s` parametresinin sahipliğini almadığı için, bu işlemden sonra `s2` hâlâ geçerli bir `String` olarak kalır.
+ Rust, burada `&s2`’yi `&s2[..]` hâline dönüştüren bir **deref coercion** (dereference zorlaması) uygular.
+ *Deref coercion* konusunu Bölüm 15’te daha ayrıntılı ele alacağız. `add` metodu `s` parametresinin sahipliğini almadığı için, bu işlemden sonra `s2` hâlâ geçerli bir `String` olarak kalır.
+ İkinci olarak, fonksiyon imzasında `add` metodunun `self` parametresinin başında `&` olmadığını görürüz. Bu, `add`’in `self`’in **sahipliğini aldığını** gösterir. Bu nedenle `Liste 8-18`’deki `s1`, `add` çağrısına taşınır (*move* edilir) ve bu çağrıdan sonra artık geçerli olmaz.
+ Dolayısıyla `let s3 = s1 + &s2;` ifadesi, her iki string’i de kopyalayıp yeni bir string oluşturuyormuş gibi görünse de, gerçekte olan şudur:
+ `s1`’in sahipliği alınır, `s2`’nin içeriğinin bir kopyası buna(`$1`) eklenir ve ardından ortaya çıkan sonucun sahipliği geri döndürülür.
+ Başka bir deyişle, çok fazla kopyalama yapıyormuş gibi görünse de, aslında durum böyle değildir; bu uygulama kopyalamaya kıyasla **daha verimli** olacak şekilde tasarlanmıştır.

---

+ Birden fazla *string*’i birleştirmemiz gerektiğinde, `+` operatörünün davranışı kullanışsız (hantal / zor yönetilir) hale gelir.
	- Yani, birden fazla *string*’i art arda birleştirmek istediğimizde, `+` operatörünü kullanmak karmaşık ve okunması zor bir hâl alır.

```rust
fn main() {
    let s1 = String::from("tic");
    let s2 = String::from("tac");
    let s3 = String::from("toe");

    let s = s1 + "-" + &s2 + "-" + &s3;
}
```

+ Bu noktada `s` değişkeni `tic-tac-toe` değerini içerecektir. Ancak bu kadar çok `+` ve `"-"` karakteri olduğu için, kodun ne yaptığını görmek zorlaşır. *String*’leri daha karmaşık şekillerde birleştirmek için bunun yerine `format!` makrosunu kullanabiliriz:
+ Bu kod da `s` değişkenini `tic-tac-toe` olarak ayarlar. `format!` makrosu `println!` makrosuna benzer şekilde çalışır; ancak çıktıyı ekrana yazdırmak yerine, içeriği bir `String` olan bir değer döndürür.
+ `format!` kullanan kod sürümü okunması çok daha kolaydır ve `format!` makrosu tarafından üretilen kod referanslar kullanır, böylece bu çağrı, parametrelerinden hiçbirinin sahipliğini almaz.


### 8.2.4. String’lere İndeksleme ile Erişim:

+ Birçok başka programlama dilinde, bir string içindeki tek tek karakterlere indeks numarasıyla erişmek geçerli ve yaygın bir işlemdir. Ancak Rust’ta bir `String`’in parçalarına indeksleme sözdizimini kullanarak erişmeye çalışırsanız, bir hata alırsınız. `Liste 8-19`’da geçersiz olan bir kod örneği gösterilmektedir.

**Bu kod derlenmez!**

```rust
fn main() {
    let s1 = String::from("hi");
    let h = s1[0];
}
```

> `Listing 8-19`: Bir String ile indeksleme sözdizimini kullanmaya çalışma

+ Bu kod çalıştırıldığında aşağıdaki hatayı üretir:

```rust
$ cargo run
   Compiling collections v0.1.0 (file:///projects/collections)
error[E0277]: the type `str` cannot be indexed by `{integer}`
 --> src/main.rs:3:16
  |
3 |     let h = s1[0];
  |                ^ string indices are ranges of `usize`
  |
  = note: you can use `.chars().nth()` or `.bytes().nth()`
          for more information, see chapter 8 in The Book: <https://doc.rust-lang.org/book/ch08-02-strings.html#indexing-into-strings>
  = help: the trait `SliceIndex<str>` is not implemented for `{integer}`
          but trait `SliceIndex<[_]>` is implemented for `usize`
  = help: for that trait implementation, expected `[_]`, found `str`
  = note: required for `String` to implement `Index<{integer}>`

For more information about this error, try `rustc --explain E0277`.
error: could not compile `collections` (bin "collections") due to 1 previous error
```

+ Bu hata mesajı durumu açıkça anlatır: **Rust string’ler indekslemeyi desteklemez.** Peki neden? Bu soruyu cevaplayabilmek için Rust’ın string’leri bellekte nasıl sakladığını konuşmamız gerekir.

#### 8.2.4.1. Dahili (İç) Gösterim:

+ Bir `String`, aslında `Vec<u8>` üzerine kurulmuş bir sarmalayıcıdır (wrapper).
+ `Liste 8-14`’teki düzgün şekilde `UTF-8` ile kodlanmış *string* örneklerimizden bazılarına bakalım. İlk olarak şu örneği ele alalım:

```rust
fn main() {
    let hello = String::from("السلام عليكم");
    let hello = String::from("Dobrý den");
    let hello = String::from("Hello");
    let hello = String::from("שלום");
    let hello = String::from("नमस्ते");
    let hello = String::from("こんにちは");
    let hello = String::from("안녕하세요");
    let hello = String::from("你好");
    let hello = String::from("Olá");
    let hello = String::from("Здравствуйте");
    let hello = String::from("Hola");  // <<===========
}
```

+ Bu durumda `len` değeri 4 olacaktır; bu da `"Hola"` *string*’ini saklayan vektörün 4 bayt uzunluğunda olduğu anlamına gelir. Bu harflerin her biri `UTF-8` ile kodlandığında 1 bayt yer kaplar. Ancak aşağıdaki satır sizi şaşırtabilir (bu *string*’in başındaki karakterin `3` rakamı değil, büyük Kiril harfi `Ze` olduğunu unutmayın):

```rust
fn main() {
    let hello = String::from("السلام عليكم");
    let hello = String::from("Dobrý den");
    let hello = String::from("Hello");
    let hello = String::from("שלום");
    let hello = String::from("नमस्ते");
    let hello = String::from("こんにちは");
    let hello = String::from("안녕하세요");
    let hello = String::from("你好");
    let hello = String::from("Olá");
    let hello = String::from("Здравствуйте");  // <<===========
    let hello = String::from("Hola");
}
```

+ Bu string’in uzunluğunun ne kadar olduğu sorulsa, muhtemelen 12 dersiniz. Oysa Rust’ın verdiği cevap 24’tür: Bunun nedeni, "Здравствуйте" kelimesini `UTF-8` ile kodlamak için 24 bayt gerekmesidir; çünkü bu *string* içindeki her *Unicode skaler değeri* 2 bayt yer kaplar.
+ Dolayısıyla string’in baytları üzerinden yapılan bir indeksleme, her zaman geçerli bir *Unicode skaler değerine* karşılık gelmez. Bunu göstermek için aşağıdaki geçersiz Rust kodunu düşünelim:


> [!NOTE]
> #### Unicode skaler değeri ne demektir?
> + **Unicode skaler değeri**, Unicode standardında tanımlanmış, **tek bir anlamlı karakter birimini** temsil eden sayısal bir değerdir.
> + Teknik olarak: **U+0000 ile U+D7FF** ve **U+E000 ile U+10FFFF** aralığındaki Unicode kod noktalarıdır(Unicode Code Point).
> + Yani **Unicode’un geçerli karakterleri** diyebiliriz.
> + Örnekler:
> 	- `A` → `U+0041`
> 	- `h` → `U+0068`
> 	- `З` → `U+0417`
> 	- `你` → `U+4F60`
> 
> Bunların her biri **bir Unicode skaler değeridir**.(Unicode scalar value = Geçerli bir Unicode karakteri)

**Bu kod derlenmez!**

```rust
let hello = "Здравствуйте";
let answer = &hello[0];
```

+ Artık `answer` değişkeninin, ilk harfi  **З** olmayacağını biliyorsunuz.  UTF-8 ile kodlandığında **З** harfinin ilk baytı 208, ikinci baytı ise 151’dir. Bu durumda `answer`’ın 208 olması gerektiği düşünülebilir; ancak 208 tek başına geçerli bir karakter değildir.
+ Bir kullanıcı bu *string*’in ilk harfini istediğinde, 208 değerinin döndürülmesi büyük olasılıkla istenen bir sonuç değildir. Üstelik string yalnızca Latin harfleri içerse bile kullanıcılar genellikle bayt değerini almak istemez: Eğer `&"hi"[0]` geçerli bir kod olsaydı, dönen değer `h` değil, 104 olurdu.
+ Sonuç olarak, beklenmeyen değerlerin döndürülmesini ve hemen fark edilmeyebilecek hataların oluşmasını engellemek için Rust bu kodu hiç derlemez ve geliştirme sürecinin erken aşamasında bu tür yanlış anlaşılmaları önler.

#### 8.2.4.2. Baytlar, Skaler Değerler ve Grafem Kümeleri:

+ UTF-8 ile ilgili bir diğer önemli nokta da, Rust’ın bakış açısından *string*’lere **aslında üç farklı şekilde** bakılabilmesidir: **baytlar**, **skaler değerler** ve **grafem kümeleri** (harf dediğimiz şeye en yakın kavram).

+ Devanagari alfabesiyle yazılmış Hintçe **"नमस्ते"** kelimesine bakarsak, bu kelime `u8` değerlerinden oluşan bir vektör olarak şu şekilde saklanır:

```rust
[224, 164, 168, 224, 164, 174, 224, 164, 184, 224, 165, 141, 224, 164, 164,
224, 165, 135]
```

+ Bu, toplam **18 bayt** eder ve bilgisayarların bu veriyi en nihayetinde saklama biçimi budur.
+ Bunu Unicode **skaler değerler** (Rust’taki `char` türünün temsil ettiği şey) olarak ele aldığımızda ise, bu baytlar şu şekilde görünür:

```rust
['न', 'म', 'स', '्', 'त', 'े']
```

+ Burada **altı adet `char` değeri** vardır; ancak dördüncü ve altıncı olanlar harf değildir. Bunlar tek başlarına anlam ifade etmeyen **işaretler (diacritics)** tir.


> [!TIP]
> #### Diacritics (Ayırt Edici İşaretler) Nedir?
> + **Diacritics**, tek başına **harf olmayan**, ancak bir harfin **okunuşunu, anlamını veya biçimini değiştiren** ek işaretlerdir.
> 	- `'न'`, `'म'`, `'स'`, `'त'` → harf
> 	- `'्'` ve `'े'` → **diacritics**
> + Özellik:
> 	- `'्'` (virama) → Harfin sesini bastırır.
> 	- `'े'` → Ünlü ses ekler
> #### Neden Rust bunu özellikle vurguluyor?
> + Çünkü;
> 	- `char` ≠ "insanın gördüğü harf"
> 	- Bir "harf" (grafem), **birden fazla `char`** içerebilir.
> 	- Diacritics bu farkın en net örneğidir.
> + Örneğin;
> ```text
> "स्" = 'स' + '्'
> ```
> + İnsan için: **tek harf**
> + Bilgisayar için: **iki Unicode skaler değeri**

+ Son olarak, bunlara **grafem kümeleri** olarak baktığımızda, bir insanın Hintçe kelimeyi oluşturan **dört harf** olarak algıladığı şeyleri elde ederiz:


> [!TIP]
> #### Grafem nedir?
> + **Grafem**, bir insanın **tek bir “harf” olarak algıladığı en küçük yazı birimidir**.
> + Grafem **bilgisayarın değil, insanın algısına** göredir.
> + Bir grafem:
> 	- 1 Unicode skaler değerden oluşabilir.
> 	- ya da **birden fazla Unicode skaler değerin birleşimi** olabilir.
> #### Grafem kümesi (grapheme cluster) nedir?
> + **Grafem kümesi,** bir grafemi oluşturan bir veya daha fazla Unicode skaler değerinin birleşimidir.
> + Unicode standardı, hangi skaler değerlerin birlikte **tek bir “görünen harf”** oluşturduğunu tanımlar. İşte bu birliktelik **grafem kümesi**dir.
> ##### Basit Latin Harfi:
> ```text
> "a"
> ```
> +  Unicode skaler değeri: `U+0061`
> + `char` sayısı: 1
> + grafem sayısı: 1
> ##### Aksanlı Harf:
> ```text
> "é"
> ```
> + İki farklı şekilde temsil edilebilir:
> 	- Tek skaler değer: `'é' → U+00E9`
> 	- Birleşik Biçim: `'e' (U+0065) + '́' (U+0301)`
> + İnsan için: **1 harf (1 grafem)**
> + Bilgisayar için: **2 char (2 skaler değer)**
> + Burada:
> 	- `'स्'` → **grafem kümesi**
> 	- `'ते'` → **grafem kümesi**


+ Rust, bilgisayarların depoladığı ham string verisini yorumlamanın farklı yollarını sağlar, böylece her program verinin hangi insan dilinde olduğuna bakılmaksızın ihtiyaç duyduğu yorumu seçebilir.
	- Bu cümle, Rust'ın string verilerini baytlar, Unicode scalar values veya grapheme clusters gibi farklı düzeylerde yorumlayabilme esnekliğini vurguluyor.
+ Rust’ın bir `String` üzerinde karakter elde etmek için indekslemeye izin vermemesinin son bir nedeni daha vardır: **indeksleme işlemlerinden her zaman sabit zamanlı (O(1)) olmaları beklenir**. Ancak `String` ile bunu garanti etmek mümkün değildir; çünkü Rust’ın, geçerli karakterlerin sayısını belirlemek için *string*’in başından başlayarak verilen indekse kadar içeriği adım adım dolaşması gerekir.


> [!NOTE]
> #### A. Sabit Zamanlı (O(1)) ne anlama geldir?
> + O(1) şu demektir:
> 	- Veri ne kadar büyük olursa olsun 
> 	- İstenen elemana erişim süresi değişmez.
> 	- Her zaman *tek adımda* erişilir
> + Örnek:
> 	- 10 elemanlı dizi
> 	- 10 milyon elemanlı dizi
> 
> Her ikisinde de:
> ```rust
> arr[5]
> ```
> işlemi aynı sürede gerçekleşir.
> #### B. O(1)’in temel şartı: Doğrudan adres hesaplama:
> + O(1) işlemler **asla arama yapmaz**.
> + Bunun yerine:
> 	1. Başlangıç adresi bilinir.
> 	2. Sabit bir matematiksel formülü hedef adres hesaplanır.
> 	3. Bellekten okunur.
> #### C. En net örnek: Dizi (array / Vec) indeksleme:
> ```rust
> let v = vec![10, 20, 30, 40];
> let x = v[2];
> ```
> ##### C.1. Bellekte olanlar
> Varsayalım:
> + `v` bellekte **0x1000** adresinde başlıyor
> + Her `i32` → **4 byte**
> ##### Rust/CPU şunu yapar:
> ```ini
> adres = 0x1000 + (2 * 4)
> ```
> + Bellekten oku → 30
> + **Ne Oldu?**
> 	- Döngü Yok
> 	- Karakter çözme yok
> 	- Veri sayısına bakılmadı.
> 
> ➡ **O(1)**
> #### O(1) neden her zaman mümkün değildir?
> Çünkü her veri yapısı sabit boyutlu değildir.
> ##### String Örneği:
> ```rust
> String = Vec<u8>
> ```
> + UTF-8 → karakterler **değişken uzunluklu**
> + 1 char = 1–4 byte
> + `s[i] → i.` karakter mi?
> 	- Bunu bulmak için baştan itibaren çözmek gerekir
> 
> ➡ **O(n)**

### 8.2.5. String'leri Dilimleme:

+ Bir string üzerinde indeksleme yapmak çoğu zaman **kötü bir fikirdir**, çünkü string indeksleme işleminin **hangi türde bir değer döndürmesi gerektiği açık değildir**:  bir **bayt değeri mi**, bir **karakter mi**, bir **grafem kümesi mi**, yoksa bir **string dilimi (&str)** mi?
+ Bu nedenle, indeksleri gerçekten kullanarak string dilimleri oluşturmanız gerekiyorsa, Rust sizden **daha açık ve net olmanızı ister**.
+ Tek bir sayı ile `[]` kullanarak indekslemek yerine, **bir aralık (range)** ile `[]` kullanarak belirli baytları içeren bir string dilimi oluşturabilirsiniz:

```rust
#![allow(unused)]
fn main() {
let hello = "Здравствуйте";

let s = &hello[0..4];
}
```

+ Burada `s`, string’in **ilk 4 baytını** içeren bir `&str` olacaktır. Daha önce de belirttiğimiz gibi, bu string’deki her karakter **2 bayt** uzunluğundadır; bu da `s` değişkeninin **“Зд”** içeriğine sahip olacağı anlamına gelir.

```rust
$ cargo run
   Compiling collections v0.1.0 (file:///projects/collections)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.43s
     Running `target/debug/collections`

thread 'main' panicked at src/main.rs:4:19:
byte index 1 is not a char boundary; it is inside 'З' (bytes 0..2) of `Здравствуйте`
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```


> [!caution]
> + Bu nedenle, aralıklar (range) kullanarak string dilimleri oluştururken **dikkatli olunmalıdır**, çünkü yanlış bir aralık seçimi **programınızın çökmesine (panic)** neden olabilir.

### 8.2.6. String’ler üzerinde iterasyon:

+ String’lerin parçaları üzerinde işlem yapmanın en iyi yolu, **karakterlerle mi yoksa baytlarla mı çalışmak istediğinizi açıkça belirtmektir**. Tek tek Unicode skaler değerleri için `chars` metodunu kullanın.
+ `"Зд"` üzerinde `chars` çağrıldığında, iki adet `char` türünde değer ayrıştırılır ve bunlar üzerinde yineleme (iterasyon) yaparak her bir elemana erişebilirsiniz:

```rust
#![allow(unused)]
fn main() {
	for c in "Зд".chars() {
	    println!("{c}");
	}
}
```

+ Bu kod aşağıdaki çıktıyı üretir:

```shell
З
д
```

+ Alternatif olarak, `bytes` metodu her bir ham baytı döndürür; bu da alanınıza (problem domain’inize) bağlı olarak uygun olabilir:

```rust
#![allow(unused)]
fn main() {
	for b in "Зд".bytes() {
	    println!("{b}");
	}
}
```

+ Bu kod, bu *string*’i oluşturan 4 baytı ekrana yazdırır:

```rust
208
151
208
180
```

+ Ancak **geçerli bir Unicode skaler değerin birden fazla bayttan oluşabileceğini unutmamak gerekir**.
+ Devanagari yazısı gibi durumlarda olduğu üzere, string’lerden **grafem kümeleri** elde etmek karmaşıktır; bu nedenle bu işlevsellik standart kütüphanede sunulmaz. Eğer buna ihtiyaç duyuyorsanız, **[crates.io](https://crates.io/)** üzerinde bu amaçla kullanılabilecek crate’ler mevcuttur.

### 8.2.7. String’lerin Karmaşıklıklarının Ele Alınması:

+ Özetlemek gerekirse, *string*’ler karmaşıktır.
+ Farklı programlama dilleri bu karmaşıklığı programcıya nasıl sunacakları konusunda farklı tercihler yapar. Rust ise String verisinin doğru şekilde ele alınmasını tüm Rust programları için varsayılan davranış haline getirmeyi seçmiştir.
	- Burada kastedilen **string’lerin (metinlerin) içsel olarak karmaşık olmasıdır**.
	- Bazı diller (örneğin *Python*, *JavaScript*): Bu karmaşıklığı **programcıdan gizler**, *String* indekslemeyi serbest bırakır, Hatalar genellikle **çalışma zamanında** ortaya çıkar. Yani Bu zor detayları sen düşünme, ben hallederim” yaklaşımı vardır.
	- Rust’un yaklaşımı farklıdır: Karmaşıklığı **saklamak yerine görünür kılar**, Potansiyel hatalara **derleme zamanında** engel olur, "Yanlış anlaşılabilecek" işlemleri (örneğin `s[0]`) **yasaklar**. Yani, Bu veriyi yanlış yorumlamanı istemiyorum. Ne yaptığını açıkça belirt.
+ Bu da programcıların UTF-8 verisini ele alırken en baştan daha fazla düşünmesini gerektirir. Bu tercih, *string*’lerin karmaşıklığını diğer programlama dillerine kıyasla daha görünür kılar; ancak geliştirme sürecinin ilerleyen aşamalarında ASCII olmayan karakterlerle ilgili hatalarla uğraşmak zorunda kalmanızı engeller.
+ İyi haber şu ki, standart kütüphane bu karmaşık durumları doğru şekilde ele alabilmenize yardımcı olmak için `String` ve `&str` türleri üzerine kurulmuş pek çok işlevsellik sunar.
+ Bir *string* içinde arama yapmak için `contains`, bir *string*’in belirli bölümlerini başka bir *string* ile değiştirmek için `replace` gibi faydalı metotların belgelerini mutlaka inceleyin.

+ Şimdi biraz daha az karmaşık bir konuya geçelim: hash map’ler!

## 8.3. Hash Map’lerde Anahtarlarla İlişkili Değerlerin Saklanması:

+ Yaygın koleksiyonlarımızdan sonuncusu hash map'tir.
+ `HashMap<K, V>` tipi, `K` tipindeki anahtarların `V` tipindeki değerlere eşleştirilmesini bir hashleme (*hashing*) fonksiyonu kullanarak saklar; bu fonksiyon, bu anahtarları ve değerleri belleğe nasıl yerleştireceğini belirler.
+ Birçok programlama dili bu tür bir veri yapısını destekler, ancak genellikle hash, map, object, hash table, dictionary veya associative array gibi farklı bir isim kullanırlar; bunlar sadece birkaç örnektir.

+ Hash map’ler, vektörlerde olduğu gibi bir **indeks** kullanarak değil, **herhangi bir türden olabilen bir anahtar** kullanarak veri aramak istediğinizde kullanışlıdır. Örneğin bir oyunda, her takımın skorunu bir hash map içinde tutabilirsiniz: burada her anahtar bir takımın adı olurken, değerler de o takımların skorlarıdır. Elinizde bir takım adı olduğunda, o takımın skorunu kolayca alabilirsiniz.

+ Bu bölümde hash map’lerin **temel API’sini** ele alacağız;
+ ancak standart kütüphanede `HashMap<K, V>` üzerinde tanımlı fonksiyonların içinde gizli daha pek çok kullanışlı özellik bulunmaktadır. Her zaman olduğu gibi, daha fazla bilgi için standart kütüphane dokümantasyonuna göz atın.

### 8.3.1. Yeni Bir Hash Map Oluşturma:

+ Boş bir hash map oluşturmanın bir yolu `new` kullanmak ve elemanları `insert` ile eklemektir. `Liste 8-20`’de, adları **Blue** ve **Yellow** olan iki takımın skorlarını takip ediyoruz. **Blue** takımı 10 puanla başlıyor, **Yellow** takımı ise 50 puanla başlıyor.

```rust
fn main() {
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);
}
```

> **Liste 8-20:** Yeni bir hash map oluşturma ve bazı anahtar–değer çiftlerini ekleme


> [!caution]
> + Standart kütüphanenin **collections** bölümünden `HashMap`’i önce `use` etmemiz gerektiğine dikkat edin!

+ Üç yaygın koleksiyonumuz arasında bu yapı en az kullanılanıdır; bu nedenle **prelude** tarafından otomatik olarak kapsama (scope) alınmaz.
+ Hash map’ler ayrıca standart kütüphaneden daha az destek alır; örneğin onları oluşturmak için yerleşik bir makro bulunmaz.

> [!important]
> + Vektörlerde olduğu gibi, hash map’ler de verilerini **heap** üzerinde saklar.
> + Bu `HashMap`’in anahtarları `String` türünde, değerleri ise `i32` türündedir.
> + Vektörlerde olduğu gibi hash map’ler de **homojendir**: tüm anahtarlar aynı türde olmalı ve tüm değerler de aynı türde olmalıdır.


### 8.3.2. Hash Map’te Değerlere Erişme:

+ Bir hash map’ten bir değeri almak için, **get** metoduna ilgili **anahtarı** veririz. Bu durum `Liste 8-21`’de gösterilmektedir.

```rust
fn main() {
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);

    let team_name = String::from("Blue");
    let score = scores.get(&team_name).copied().unwrap_or(0);
}
```

> **Liste 8-21:** Hash map’te saklanan Blue takımının skoruna erişme

+ Burada `score`, **Blue** takımıyla ilişkilendirilmiş değeri alır ve sonuç **10** olur.
+ `get` metodu `Option<&V>` döndürür; eğer hash map içinde bu anahtar için bir değer yoksa, `get` metodu `None` döner.
+ Bu programda `Option`, önce `copied` çağrılarak `Option<&i32>` yerine `Option<i32>` elde edilerek, ardından `unwrap_or` kullanılarak ele alınır.


> [!TIP]
> #### 1. `get` metodu neden `Option<&V>` döndürür?
> + `scores` bir `HashMap<String, i32>`
> + `get` metodu **değeri kopyalamaz**, yalnızca **içerideki değere bir referans** verir.
> + Bu yüzden dönüş tipi: `Option<&i32>`
> + Neden `Option`?
> 	- Çünkü verdiğin anahtar (`"Blue"`) hash map içinde **olabilir de olmayabilir de**
> 	- Rust, “kesin vardır” varsayımı yapmana izin vermez.
> + Durumlar:
> 	- Anahtar varsa → `Some(&10)`
> 	- Anahtar yoksa → `None`
> #### 2. Neden doğrudan `i32` değil de `&i32`?
> + Rust **varsayılan olarak sahipliği (ownership) vermez**.
> + Hash map hâlâ o değerin sahibidir.
> 	- `get` sadece “şuna bir bak” der
> 	- Bu nedenle sana **ödünç alınmış (borrowed)** bir değer verir: `&i32`
> 
> Bu, bellek güvenliği açısından çok kritiktir.

+ Böylece `scores` içinde bu anahtar için bir kayıt yoksa `score` değeri **sıfır (0)** olarak ayarlanır.
+ Bir hash map içindeki her **anahtar–değer** çiftini, vektörlerde yaptığımıza benzer şekilde, bir `for` döngüsü kullanarak dolaşabiliriz:

```rust
fn main() {
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);

    for (key, value) in &scores {
        println!("{key}: {value}");
    }
}
```

+ Bu kod, her anahtar–değer çiftini **rastgele (belirsiz) bir sırayla** yazdırır:

```rust
Yellow: 50
Blue: 10
```

### 8.3.3. Hash Map’lerde Sahipliğin (Ownership) Yönetilmesi:

+ `i32` gibi **Copy** trait’ini uygulayan türler için, değerler hash map içine **kopyalanır**. `String` gibi **sahipliği olan (owned)** türlerde ise değerler **taşınır (move edilir)** ve hash map bu değerlerin sahibi olur.
+ Bu durum Liste 8-22’de gösterilmektedir.

```rust
fn main() {
    use std::collections::HashMap;

    let field_name = String::from("Favorite color");
    let field_value = String::from("Blue");

    let mut map = HashMap::new();
    map.insert(field_name, field_value);
    // field_name ve field_value bu noktadan sonra geçersizdir;
    // kullanmayı denerseniz derleyicinin verdiği hatayı görebilirsiniz!
}
```

> **Liste 8-22:** Anahtarlar ve değerler eklendikten sonra hash map’in bunların sahibi olduğunu gösterme

+ `insert` çağrısıyla hash map içine taşındıktan sonra, `field_name` ve `field_value` değişkenlerini artık kullanamayız.


> [!warning]
> + Eğer *hash map* içine **değerlere ait referanslar** eklerseniz, değerler *hash map* içine taşınmaz.
> + Ancak bu referansların işaret ettiği değerler, en az *hash map* geçerli olduğu süre boyunca geçerli olmak zorundadır.
> + Bu konuları **10. Bölümdeki "[Ömürler (Lifetimes) ile Referansları Doğrulama](https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html#validating-references-with-lifetimes)"** kısmında daha ayrıntılı ele alacağız.
> ```rust
> use std::collections::HashMap;
>
> fn main() {
>    let field_name = String::from("Favorite color");
>    let field_value = String::from("Blue");
>
>    let mut map = HashMap::new();
>    map.insert(&field_name, &field_value); // <= Referanslar
>
>    println!("{field_name}");
>    println!("{}", field_value);
>}
> ```

### 8.3.4. Bir Hash Map’i Güncelleme:

+ Anahtar–değer çiftlerinin sayısı artırılabilir olsa da, **her benzersiz anahtar** aynı anda yalnızca **tek bir değerle** ilişkilendirilebilir (ancak bunun tersi geçerli değildir: örneğin **Blue** takımı ile **Yellow** takımı, `scores` *hash map*’i içinde her ikisi de **10** değerine sahip olabilir).
+ Bir *hash map* içindeki veriyi değiştirmek istediğinizde, bir anahtarın zaten bir değere sahip olduğu durumu **nasıl ele alacağınıza karar vermeniz gerekir**.
	- Eski değeri tamamen yok sayarak yeni değerle **değiştirebilirsiniz**.
	- Eski değeri koruyup yeni değeri yok sayabilir, yalnızca anahtarın zaten bir değeri yoksa yeni değeri ekleyebilirsiniz.(*Hash map* içinde **aynı anahtar zaten varsa** → **mevcut değere dokunma** veya *Hash map* içinde **bu anahtar yoksa** → **yeni değeri ekle**)
	- Ya da eski değer ile yeni değeri **birleştirebilirsiniz**.
+ Şimdi bunların her birinin nasıl yapılacağına bakalım!

#### 8.3.4.1. Bir Değerin Üzerine Yazma (Overwriting):

+ Bir hash map içine bir anahtar–değer çifti ekledikten sonra, **aynı anahtarı farklı bir değerle** tekrar eklerseniz, o anahtarla ilişkilendirilmiş olan değer **değiştirilir (üzerine yazılır)**.
+ `Liste 8-23`’teki  kod `insert`'i iki kez çağırsa da, *hash map* yalnızca bir anahtar-değer çifti içerecektir çünkü *Blue* takımın anahtarı için her iki seferde de değer ekliyoruz.

```rust
fn main() {
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Blue"), 25);

    println!("{scores:?}");
}
```

> **Liste 8-23:** Belirli bir anahtarla saklanan değerin değiştirilmesi

Bu kodun çıktısı:

```rust
{"Blue": 25}
```

+ olacaktır. Başlangıçta eklenen **10** değeri, **üzerine yazılarak** **25** ile değiştirilmiştir.


> [!NOTE]
> ```rust
> {scores:?}
> ```
> + `:?` → **Debug formatı** anlamına gelir.
> + Rust’ta bir tür `Debug` trait’ini implement ediyorsa, `:?` ile yazdırılabilir.
> + `HashMap` tipi **`Debug` trait’ini destekler**, bu yüzden bu kullanım geçerlidir.


> [!NOTE]
> + `HashMap` **`Display` trait’ini implement etmez.**
> + Bu nedenle şunu yazamazsın:
> ```rust
> println!("{}", scores); // ❌ derleme hatası
> ```
> + Ama şunu yazabilirsin:
> ```rust
> println!("{:?}", scores); // ✅
> ```

#### 8.3.4.2. Bir Anahtar Mevcut Değilse Yalnızca Anahtar ve Değer Ekleme:

+ Belirli bir anahtarın hash map içinde zaten bir değere sahip olup olmadığını kontrol etmek ve buna göre işlem yapmak oldukça yaygındır: Eğer anahtar hash map içinde **zaten varsa**, mevcut değer olduğu gibi **korunur**; eğer anahtar **yoksa**, anahtar ve ona karşılık gelen bir değer **eklenir**.
+ Hash map'lerin bunu yapmak için entry adında özel bir API'si vardır; bu API, kontrol etmek istediğiniz anahtarı parametre olarak alır.
+ `entry` metodunun dönüş değeri, bir değerin var olup olmadığını temsil eden **`Entry`** adlı bir *enum*’dur.
+ Örneğin **Yellow** takımı için bir değer atanmış mı diye kontrol etmek istediğimizi düşünelim. Eğer yoksa **50** değerini eklemek istiyoruz; **Blue** takımı için de aynı kontrolü yapıyoruz.
+ `entry` API’sini kullanarak kod, Liste 8-24’teki gibi görünür.

```rust
fn main() {
    use std::collections::HashMap;

    let mut scores = HashMap::new();
    scores.insert(String::from("Blue"), 10);

    scores.entry(String::from("Yellow")).or_insert(50);
    scores.entry(String::from("Blue")).or_insert(50);

    println!("{scores:?}");
}
```

> **Liste 8-24:** Anahtarın zaten bir değeri yoksa ekleme yapmak için `entry` metodunun kullanımı

+ `Entry` üzerinde tanımlı olan **`or_insert`** metodu,
	- eğer ilgili anahtar *hash map* içinde **mevcutsa**, o anahtara karşılık gelen değere **değiştirilebilir (mutable) bir referans** döndürür;
	- eğer anahtar mevcut değilse, parametre olarak verilen değeri bu anahtar için **yeni değer olarak ekler** ve eklenen bu değere ait **mutable bir referans** döndürür.
+ Bu teknik, kontrol mantığını kendimiz yazmaya kıyasla çok daha temizdir ve ayrıca **borrow checker** ile de daha uyumlu çalışır.

+ Liste 8-24’teki kod çalıştırıldığında aşağıdaki çıktı üretilir:

```rust
{"Yellow": 50, "Blue": 10}
```

+ İlk `entry` çağrısı, **Yellow** takımının henüz bir değeri olmadığı için anahtarı **50** değeriyle birlikte ekler.
+ İkinci `entry` çağrısı ise hash map’i değiştirmez; çünkü **Blue** takımı zaten **10** değerine sahiptir.


#### 8.3.4.3. Eski Değere Göre Bir Değeri Güncelleme:

+ Hash map’lerin yaygın kullanım senaryolarından biri, bir anahtarın değerini bulup **mevcut (eski) değere göre güncellemektir**.
+ Örneğin, Liste 8-25’teki kod, bir metin içinde her kelimenin kaç kez geçtiğini sayar. Burada anahtar olarak **kelimeleri**, değer olarak ise o kelimenin **kaç kez görüldüğünü** tutan bir *hash map* kullanılır. Eğer bir kelimeyle **ilk kez** karşılaşılıyorsa, önce **0** değeri eklenir.

```rust
fn main() {
    use std::collections::HashMap;

    let text = "hello world wonderful world";

    let mut map = HashMap::new();

    for word in text.split_whitespace() {
        let count = map.entry(word).or_insert(0);
        *count += 1;
    }

    println!("{map:?}");
}
```

> **Liste 8-25:** Kelimelerin kaç kez geçtiğini saymak için *hash map* kullanan örnek

+ Bu kodun çıktısı:

```rust
{"world": 2, "hello": 1, "wonderful": 1}
```

+ olacaktır. Anahtar–değer çiftlerinin farklı bir sırayla yazdırıldığını görebilirsiniz;
+ **"[8.3.2. Hash Map’te Değerlere Erişme](### 832-hash-mapte-değerlere-erişme:)"** bölümünde de belirtildiği gibi, *hash map* üzerinde dolaşma işlemi **rastgele (belirsiz) bir sırayla** gerçekleşir.
+ `split_whitespace` metodu, `text` içindeki değeri boşluklara göre ayırarak **alt dilimler (subslices)** üzerinde bir iterator döndürür.
+ `or_insert` metodu ise belirtilen anahtar için değerin **değiştirilebilir bir referansını (`&mut V`)** döndürür.
+ Burada bu mutable referansı `count` değişkeninde sakladığımız için, değere atama yapabilmek adına önce yıldız (`*`) operatörü ile `count`’u **dereference** etmemiz gerekir.
+ Bu mutable referans, `for` döngüsünün sonunda kapsam (scope) dışına çıkar; dolayısıyla yapılan tüm bu değişiklikler, **borrow kuralları** açısından güvenli ve izin verilen işlemlerdir.
	+ Yani, `count` **sadece for döngüsünün içindedir**. Döngünün **her turu (iteration)** ayrı bir scope gibidir. Tur bittiğinde `count` **yok edilir**

### 8.3.5. Hashleme Fonksiyonları

+ Varsayılan olarak `HashMap`, hash tablolarını hedef alan denial-of-service (DoS) saldırılarına karşı dayanıklılık sağlayabilen **SipHash** adlı bir hashleme fonksiyonu kullanır.
+ Bu, mevcut en hızlı hashleme algoritması değildir; ancak performanstaki düşüşe karşılık sağlanan **daha iyi güvenlik** bu ödün vermeye değerdir.
+ Eğer kodunuzun performansını analiz eder (profiling yapar) ve varsayılan hash fonksiyonunun sizin amaçlarınız için **çok yavaş** olduğunu fark ederseniz, **farklı bir hasher belirterek** başka bir fonksiyona geçebilirsiniz.
+ Bir _hasher_, `BuildHasher` trait’ini uygulayan bir türdür.


> [!tip]
> #### 1. BuildHasher Nedir?
> + **BuildHasher** = HashMap için hangi hashing algoritmasının kullanılacağını belirleyen bir trait
> #### 2. Tip Seviyesinde Seçim (Derleme Zamanı)
> + Rust'ta `HashMap` tanımına baktığında üç tane jenerik parametre görürsün: `HashMap<K, V, S>`
> + Buradaki **`S`** (State), `BuildHasher` trait'ini uygulayan yapıdır. Eğer siz bu `S` parametresini değiştirirseniz, `HashMap`'in kullanacağı algoritmayı da değiştirmiş olursunuz.
> #### 3. HashMap Tanımı (genel form)
> ```rust
> HashMap<K, V, S>
> ```
> + `K` → Key
> + `V` → Value
> + `S` → Hasher (varsayılan: `RandomState` → SipHash)


+ Trait’lerin ne olduğu ve nasıl uygulanacağı **Bölüm 10**’da ele alınacaktır. Kendi hasher’ınızı sıfırdan yazmanız gerekmez; **[crates.io](https://crates.io/)** üzerinde, Rust kullanıcıları tarafından paylaşılmış ve birçok yaygın hashleme algoritmasını uygulayan hasher’lar sunan kütüphaneler bulunmaktadır.

## 8.4. Özet:

+ Vektörler (`Vec`), string’ler (`String`) ve hash map’ler (`HashMap`), programlarda veriyi **saklamanız**, **erişmeniz** ve **değiştirmeniz** gerektiğinde ihtiyaç duyacağınız işlevselliğin büyük bir kısmını sağlar. İşte artık çözebilecek donanıma sahip olduğunuz bazı alıştırmalar:
	1. **Medyan ve Mod Hesaplama:** Bir tam sayı listesi verildiğinde, bir vektör kullanarak listenin **medyanını** (liste sıralandığında ortadaki değer) ve **modunu** (en sık tekrarlanan değer; burada bir hash map kullanmak faydalı olacaktır) döndürün.
	2. **Pig Latin Dönüştürücü:** Karakter dizilerini (stringleri) "Pig Latin"e dönüştürün. Her kelimenin ilk ünsüz harfi kelimenin sonuna taşınır ve "ay" eki eklenir; örneğin "first" kelimesi "irst-fay" olur. Ünlü harfle başlayan kelimelerin sonuna ise "hay" eklenir ("apple" kelimesinin "apple-hay" olması gibi). UTF-8 kodlamasıyla ilgili detayları aklınızda bulundurun
		+ Her kelimenin **ilk sessiz harfi** kelimenin sonuna taşınır ve **`ay`** eklenir ( `first` → `irst-fay`)
		+ **Sesli harfle başlayan** kelimelerin sonuna ise **`hay`** eklenir (`apple` → `apple-hay`)
	3. **Çalışan Yönetim Sistemi:** Hash map ve vektörleri kullanarak, bir kullanıcının bir şirketteki departmanlara çalışan isimleri eklemesine olanak tanıyan bir metin arayüzü oluşturun.
		+ Örneğin: "Sally'yi Mühendislik'e ekle" veya "Amir'i Satış'a ekle".
		+ Ardından, kullanıcının bir departmandaki tüm kişilerin listesini veya şirketteki tüm kişileri (departmanlara göre gruplanmış ve alfabetik olarak sıralanmış şekilde) görüntülemesini sağlayın.

+ Standart kütüphane (*standard library*) API dokümantasyonu; vektörlerin(`Vec`), karakter dizilerinin(`String`) ve hash map’lerin(`HashMap`) bu alıştırmalarda işinize yarayacak metotlarını detaylıca açıklamaktadır.
+ Artık işlemlerin başarısız olabileceği daha karmaşık programlara geçiyoruz; bu yüzden **hata yönetimi (error handling)** konusunu ele almak için mükemmel bir zaman. Bir sonraki bölümde bunu yapacağız!


# 9. Hata Yönetimi (Error Handling)

+ Yazılımda hatalar hayatın bir gerçeğidir; bu nedenle Rust, bir şeylerin ters gittiği durumları yönetmek için bir dizi özelliğe sahiptir. Pek çok durumda Rust, kodunuzun derlenmesi için bir hata olasılığını önceden kabul etmenizi ve buna karşı bir önlem almanızı zorunlu kılar. Bu gereklilik, hataları henüz canlı ortama (production) dağıtım yapmadan keşfetmenizi ve uygun şekilde yönetmenizi sağlayarak programınızı daha dayanıklı (robust) hale getirir.
+ Rust, hataları iki ana kategoriye ayırır: **kurtarılabilir (recoverable)** ve **kurtarılamaz (unrecoverable)** hatalar.
	- **Kurtarılabilir Hatalar:** "Dosya bulunamadı" gibi hatalardır. Bu durumda genellikle kullanıcıya sorunu raporlamak ve işlemi tekrar denemek isteriz.
	- **Kurtarılamaz Hatalar:** Bir dizinin sınırları dışındaki bir konuma erişmeye çalışmak gibi, her zaman birer "bug" (yazılım hatası) belirtisi olan durumlardır. Bu durumda programı derhal durdurmak isteriz.
+ Çoğu dil bu iki hata türü arasında bir ayrım yapmaz ve her ikisini de **istisnalar (exceptions)** gibi mekanizmalarla aynı şekilde yönetir. Rust'ta ise istisnalar yoktur.
+ Bunun yerine,
	- kurtarılabilir hatalar için `Result<T, E>` türünü,
	- program kurtarılamaz bir hatayla karşılaştığında ise çalışmayı durduran `panic!` makrosunu kullanır.
+ Bu bölüm, önce `panic!` makrosunun çağrılmasını ele alacak, ardından `Result<T, E>` değerlerinin döndürülmesinden bahsedecektir. Ayrıca, bir hatadan kurtulmaya çalışmak ile çalışmayı durdurmak arasında karar verirken neleri göz önünde bulundurmamız gerektiğini keşfedeceğiz.

## 9.1. `panic!` ile Kurtarılamaz Hatalar

+ Bazen kodunuzda kötü şeyler olur ve bu konuda yapabileceğiniz hiçbir şey yoktur. Bu durumlar için Rust, `panic!` makrosuna sahiptir.
+ Pratikte panik (panic) durumuna yol açmanın iki yolu vardır:
	1. Kodunuzun paniklemesine neden olacak bir eylemde bulunmak (bir dizinin sınırları dışındaki bir elemana erişmeye çalışmak gibi) veya
	2. `panic!` makrosunu doğrudan çağırmak.
+ Her iki durumda da programımızda bir panik durumu tetikleriz.
+ Varsayılan olarak bu panikler; bir hata mesajı yazdırır, yığını geri sarar (**unwind**), yığındaki verileri temizler ve programdan çıkar.
+ Bir ortam değişkeni (**environment variable**) aracılığıyla, paniğin kaynağını tespit etmeyi kolaylaştırmak adına Rust'ın panik anında çağrı yığınını (**call stack**) görüntülemesini de sağlayabilirsiniz.


> [!NOTE]
> #### Önemli Terimler Notu:
> + **Unwind (Geri sarma):** Panik anında Rust'ın bellek yığınını (stack) geriye doğru tarayarak her bir fonksiyondaki verileri temizlemesi işlemidir.
> + **Call Stack (Çağrı Yığını):** Programın o ana kadar hangi fonksiyonları hangi sırayla çağırdığını gösteren listedir.
> + **Explicitly (Doğrudan/Açıkça):** Kodun içinde sizin tarafınızdan bilerek yazılması.


> [!NOTE]
> + Varsayılan olarak, bir panik meydana geldiğinde program **yığını geri sarmaya (unwinding)** başlar. Bu, Rust'ın yığın (stack) boyunca geriye doğru ilerlemesi ve karşılaştığı her fonksiyondaki verileri temizlemesi anlamına gelir. Ancak, bu geriye doğru tarama ve temizlik işlemi oldukça zahmetli bir iştir. Bu nedenle Rust, alternatif olarak programı temizlik yapmadan anında sonlandıran **iptal etme (aborting)** seçeneğini seçmenize de olanak tanır.
> + İptal etme (aborting) durumunda, programın kullandığı belleğin işletim sistemi tarafından temizlenmesi gerekecektir. Eğer projenizde ortaya çıkan ikili dosya (binary) boyutunu mümkün olduğunca küçültmeniz gerekiyorsa, `Cargo.toml` dosyanızdaki ilgili `[profile]` bölümlerine `panic = 'abort'` satırını ekleyerek panik anında geri sarma yerine iptal etme yöntemine geçebilirsiniz.
> 	- Yani, Derleyici, programın içine "hata anında hangi veriler nasıl temizlenecek" bilgisini içeren **ekstra kodlar ve tablolar** eklemek zorundadır.(Stack unwinding aşamasında)
> 	- Bu ekstra kodlar, programın son boyutunun (binary) büyümesine neden olur.
> 	- Bu durumda, o "nazik temizlik" için gereken ekstra kodlara ihtiyaç kalmaz. Derleyici bu kodları dosyanın içine eklemediği için de **dosyanın boyutu küçülür.**
> + Örneğin, "release" modunda panik anında iptal etme yöntemini kullanmak istiyorsanız şunu ekleyin:
> ```rust
> [profile.release]
> panic = 'abort'
> ```

+ Gelin, basit bir programda `panic!` makrosunu çağırmayı deneyelim:

**Dosya adı:** `src/main.rs`

```rust
fn main() {
    panic!("crash and burn");
}
```

+ Programı çalıştırdığınızda şuna benzer bir çıktı göreceksiniz:

```rust
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.25s
     Running `target/debug/panic`

thread 'main' panicked at src/main.rs:2:5:
crash and burn
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

+ `panic!` çağrısı, son iki satırda yer alan hata mesajına neden olur.
+ İlk satır, bizim panik mesajımızı ve paniğin kaynak kodumuzda nerede oluştuğunu gösterir: `src/main.rs:2:5` ifadesi, hatanın `src/main.rs` dosyamızın **ikinci satırı, beşinci karakterinde** olduğunu belirtir.


> [!NOTE]
> #### Çıktıdaki Önemli Noktalar:
> + **`thread 'main' panicked`**: Hatanın ana iş parçacığında (main thread) gerçekleştiğini söyler.
> + **`crash and burn`**: Bizim `panic!` makrosu içine yazdığımız özel mesajdır.
> + **`src/main.rs:2:5`**: Hatanın tam koordinatıdır (Satır: 2, Sütun: 5).
> + **`RUST_BACKTRACE=1`**: Eğer hata daha karmaşık bir yerden geliyorsa, hataya giden tüm yol haritasını (backtrace) görmek için bu komutu nasıl kullanacağınızı hatırlatan bir nottur.


+ Bu durumda, belirtilen satır doğrudan kendi kodumuzun bir parçasıdır ve o satıra gittiğimizde `panic!` makrosu çağrısını görürüz. Ancak bazı durumlarda `panic!` çağrısı, kodumuzun çağırdığı başka bir kodun içinde olabilir. Bu gibi durumlarda hata mesajında bildirilen dosya adı ve satır numarası, en nihayetinde `panic!` çağrısına yol açan **bizim kodumuzun satırı değil**, `panic!` makrosunun çağrıldığı **başka birine ait (örneğin bir kütüphaneye ait) kodu** gösterir.
+ Paniğe neden olan kodumuzun hangi kısmı olduğunu bulmak için, `panic!` çağrısının geldiği fonksiyonların **backtrace** (geri izleme) dökümünü kullanabiliriz. Bir `panic!` geri izlemesinin nasıl kullanılacağını anlamak için başka bir örneğe bakalım: `panic!` çağrısının doğrudan makroyu çağırmamızdan değil de, kodumuzdaki bir hata (bug) nedeniyle bir kütüphaneden geldiği durumun nasıl olduğunu görelim. `Liste 9-1`, bir vektördeki geçerli indeks aralığının dışındaki bir indekse erişmeye çalışan bir kod içermektedir.

**Dosya adı:** `src/main.rs`

```rust
fn main() {
    let v = vec![1, 2, 3];

    v[99];
}
```

> **Liste 9-1**: Bir vektörün sonundaki elemandan sonrasına erişmeye çalışmak; bu durum `panic!` çağrısına neden olacaktır.

+ Burada, vektörümüzün 100. elemanına (indeksleme sıfırdan başladığı için 99. indekse) erişmeye çalışıyoruz, ancak vektörün sadece üç elemanı var. Bu durumda Rust panikleyecektir. `[]` (indeks operatörü) kullanımı bir eleman döndürmeyi amaçlar, ancak geçersiz bir indeks girdiğinizde Rust'ın burada döndürebileceği doğru bir eleman yoktur.
+ C dilinde, bir veri yapısının sınırlarının dışını okumaya çalışmak **tanımsız davranıştır (undefined behavior)**. Bellek o veri yapısına ait olmasa bile, veri yapısındaki o elemana karşılık gelecek bellek konumunda her ne varsa onu alabilirsiniz. Buna **tampon aşımı okuması (buffer overread)** denir; eğer bir saldırgan, veri yapısından sonra saklanan ve normalde izin verilmemesi gereken verileri okuyacak şekilde indeksi manipüle edebilirse, bu durum güvenlik açıklarına yol açabilir.


> [!NOTE]
> #### Önemli Teknik Kavramlar:
> + **Undefined Behavior (Tanımsız Davranış):** Programın nasıl davranacağının dilin standartları tarafından belirlenmediği, yani her türlü sonucun (çökme, yanlış veri, sessizce devam etme vb.) çıkabileceği durumdur.
> + **Buffer Overread (Tampon Aşımı Okuması):** Bir programın, kendisine ayrılan bellek sınırının ötesini okuması durumudur.


> [!TIP]
> #### Rust Neden Farklı?
>
> + C dili hızı önemsediği için her seferinde "Sınırın içinde miyiz?" diye kontrol etmez; bu da hata yapmaya açıktır. Rust ise her erişimde bu kontrolü yapar. 
> + Eğer sınır dışındaysanız, hatalı bir veri okuyup güvenlik açığı yaratmaktansa programı güvenli bir şekilde durdurmayı (`panic!`) tercih eder.

+ Programınızı bu tür güvenlik açıklarından korumak için Rust, mevcut olmayan bir indeksteki elemanı okumaya çalıştığınızda çalışmayı durdurur ve devam etmeyi reddeder. Hadi deneyip görelim:


```rust
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.27s
     Running `target/debug/panic`

thread 'main' panicked at src/main.rs:4:6:
index out of bounds: the len is 3 but the index is 99
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```









# 10. Jenerik Türler, Özellikler (Trait’ler) ve Yaşam Süreleri(Lifetimes)


## 10.3. Ömürler (Lifetimes) ile Referansları Doğrulama:



# 15. Referansı Takip Ederek Değere Ulaşma:
## Kaynak:

+ [READ THE BOOK!](https://doc.rust-lang.org/book/ch05-01-defining-structs.html)