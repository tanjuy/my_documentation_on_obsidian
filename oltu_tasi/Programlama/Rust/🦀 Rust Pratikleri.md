## Örnek 1: Binding and Mutability

+ Bir değişken yalnızca başlatılmışsa kullanılabilir.

```rust
// Aşağıdaki hatayı kodda en az değişiklik yaparak düzeltin.

fn main() {

    let x: i32; // başlatılmamış ancak kullanılmış, HATA!
    let y: i32; // başlatılmamış ama aynı zamanda kullanılmamış sadece bir Uyarı!

    assert_eq!(x, 5);
    println!("Success!");
```

```rust
   Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
warning: unused variable: `y`
  --> src/main.rs:11:9
   |
11 |     let y: i32; // başlatılmamış ama aynı zamanda kullanılmamış sadece bir Uyarı!
   |         ^ help: if this is intentional, prefix it with an underscore: `_y`
   |
   = note: `#[warn(unused_variables)]` on by default

error[E0381]: used binding `x` isn't initialized
  --> src/main.rs:13:5
   |
10 |     let x: i32; // başlatılmamış ancak kullanılmış, HATA!
   |         - binding declared here but left uninitialized
...
13 |     assert_eq!(x, 5);
   |     ^^^^^^^^^^^^^^^^ `x` used here but it isn't initialized
   |
   = note: this error originates in the macro `assert_eq` (in Nightly builds, run with -Z macro-backtrace for more info)
help: consider assigning a value
   |
10 |     let x: i32 = 42; // başlatılmamış ancak kullanılmış, HATA!
   |                ++++

For more information about this error, try `rustc --explain E0381`.
warning: `hello_world` (bin "hello_world") generated 1 warning
error: could not compile `hello_world` (bin "hello_world") due to 1 previous error; 1 warning emitted
FAIL
```


> [!NOTE]
> #### Kısa Hatırlatma:
> + Rust’taki **`assert_eq!`** makrosu, **iki değerin birbirine eşit olup olmadığını test etmek** için kullanılan bir **test ve hata ayıklama (debug)** aracıdır.
> + Eğer iki değer **eşit değilse**, program **panic (çökme)** ile durur ve hangi değerlerin farklı olduğunu gösterir.
> #### Temel Kullanım:
> ```rust
> fn main() {
>    let a = 5;
>    let b = 2 + 3;
>
>    assert_eq!(a, b);
> }
> ```
> + Bu örnek sorunsuz çalışır çünkü `a = 5` ve `b = 5` ve `assert_eq!(a, b)` doğru bir ifade (eşitler).
> #### Hata (Panic) Örneği:
> ```rust
> fn main() {
>    let a = 10;
>    let b = 20;
>
>    assert_eq!(a, b);
> }
> ```
> + **Çıktı:**
> ```text
>    Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
>    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.90s
>     Running `target/debug/hello_world`
>
>thread 'main' panicked at src/main.rs:5:5:
>assertion `left == right` failed
>  left: 10
> right: 20
>note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
>FAIL
> ```
> + Burada makro bize **hangi satırda hata oluştuğunu** ve **sol/sağ değerlerin ne olduğunu** açıkça gösterir.

### Çözüm:

```rust
let x: i32 = 5;
```

```rust
let _y: i32;
```

## Örnek 2: `mut` anahtar kelimesi

+ Derlenmesini sağlamak için koddaki boşlukları doldurun.

```rust
fn main() {
    let __ __ = 1;
    __ += 2;

    assert_eq!(x, 3);
    println!("Success!");
}
```

### Çözüm:

```rust
let mut x = 1;
x += 2;        // x = x + 2;

// x değeri 3 olur.
assert_eq!(x, 3);
println!("Success!");
```

## Örnek 3: Scope(Kapsam)

+ Kapsam(`scope`), öğenin(`variable`) geçerli olduğu program içindeki aralıktır.
+ Aşağıdaki hatayı en az değişiklikle düzeltin.

```rust
fn main() {
    // Fix the error below with least amount of modification
    // Outer scope
    let x: i32 = 10;

    {
        // Inner scope
        let y: i32 = 5;
        println!("The value of x is {} and value of y is {}",x, y);
    }

    println!("The value of x is {} and value of y is {}", x, y);
}
```

**Çıktı:**

```rust
   Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
error[E0425]: cannot find value `y` in this scope
 --> src/main.rs:9:62
  |
9 |     println!("The value of x is {} and value of y is {}", x, y);
  |                                                              ^ help: a local variable with a similar name exists: `x`

For more information about this error, try `rustc --explain E0425`.
error: could not compile `hello_world` (bin "hello_world") due to 1 previous error
FAIL
```
### Çözüm 3: Scope

+ `y` değişkenini `main` scope da tanımlayarak sorunu çözüyoruz. 
+ `main scope` bir diğer adı en dış scope veya global scope olarak adlandırılır.

```rust
fn main() {
    // Fix the error below with least amount of modification
    // Outer scope
    let x: i32 = 10;
    let y: i32 = 5;

    {
        // Inner scope
        // let y: i32 = 5;
        println!("The value of x is {} and value of y is {}",x, y);
    }

    println!("The value of x is {} and value of y is {}", x, y);
} // x ve y değişkenleri burada sonlanır.
```

**Çıktı:**

```shell
   Compiling hello_world v0.1.0 (/home/ottoman/rustDersleri/hello_world)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 1.11s
     Running `target/debug/hello_world`
The value of x is 10 and value of y is 5
The value of x is 10 and value of y is 5
```

## Örnek 4: 

```rust
// `define_x` kullanımındaki hatayı düzeltin.
fn main() {
    println!("{}, world", x);
}

fn define_x() {
    let x = "hello";
}
```

### Çözüm 4.1:

```rust
fn main() {
    define_x();
}

fn define_x() {
    let x = "hello";
    println!("{}, world", x);
}
```

**Kod Çıktısı:**

```bash
hello, world
```

## Örnek 5:

+ Önceki bir değişkenle aynı ada sahip yeni bir değişken tanımlayabilirsiniz, burada ilkinin ikincisi tarafından gölgelendiğini (shadowed) söyleyebiliriz.

```rust
// `println!` işlevinin çalışması için `assert_eq!` ifadesini değiştirmeniz yeterlidir (terminalde `42` yazdırın).

fn main() {
    let x: i32 = 5;
    {
        let x = 12;
        assert_eq!(x, 5);
    }

    assert_eq!(x, 12);

    let x = 42;
    println!("{}", x); // Prints "42".
}
```

### Çözüm 5.1:

```rust
fn main() {
    let x: i32 = 5;
    {
        let x = 12;
        assert_eq!(x, 12);
    }

    assert_eq!(x, 5);

    let x = 42;
    println!("{}", x); // Prints "42".
}
```

**Kod Çıktısı:**

```bash
42
```

## Örnek 6:

```rust

```

# String Alıştırmaları:

## Problem 1: + operatörü

Verilen kelimeyi belirli bir sayıda ekran yazdırınız.
Aşağıdaki çıktıyı üreten `repeat` fonksiyonunu **`+` operatörünü kullanarak** yazınız:

Çıktı:

```
Enter a world:
Rust
Enter repeat number:
3
Rust Rust Rust
```

Kullanım:

```rust
use std::io::stdin;

fn main() {
    let mut world = String::new();

    println!("Enter a world:");
    stdin().read_line(&mut world).expect("Failed to read line! 1");
    let world = world.trim();

    println!("Enter repeat number:");
    let mut times = String::new();
    stdin().read_line(&mut times).expect("Failed to read line! 2");
    let times: u32 = times.trim().parse().expect("Invalid number");

    let result = repeat(world, times);
    println!("{}", result);
}

fn repeat(text: &str, times: u32) -> String {
	// Code... 
}
```

Kurallar:
- Fonksiyon imzası değiştirilmemelidir:

```rust
fn repeat(text: &str, times: u32) -> String
```

### Çözüm 1: `+` operatörü ile

**Dosya adı:** `src/main.rs`

```rust
use std::io::stdin;

fn main() {
    let mut world = String::new();

    println!("Enter a world:");
    stdin().read_line(&mut world).expect("Failed to read line! 1");
    let world = world.trim();

    println!("Enter repeat number:");
    let mut times = String::new();
    stdin().read_line(&mut times).expect("Failed to read line! 2");
    let times: u32 = times.trim().parse().expect("Invalid number");

    let result = repeat(world, times);
    println!("{}", result);
}


fn repeat(text: &str, times: u32) -> String {
    let mut result = String::new();
    for _ in 0..times {
        result = result + text + " ";
    }
    result
}

```

- `+` operatörü kullanılarak `String` ve `&str` değerleri birleştirilmektedir.
- `+` operatörü sadece şu şekilde çalışır:

```rust
String + &str
```

- Bu yüzden `result` değişkeni `String` olmak zorundadır ve `text` ise `&str` olarak eklenebilir.

> [!CAUTION]
> `+` operatörü **sol taraftaki String’in ownership’ini alır**
> Bu yüzden şu olur:
> ```rust
> let s1 = String::from("Hello");
> let s2 = "World";
> 
> let s3 = s1 + s2;
> ```
> - `s1` → `+`’ın sol tarafı → **taşınır (move)**
> - `s2` → sağ taraf → borrow edilir (`&str`)
> 
> Bu yüzden şunu yapamazsın:
> ```rust
> println!("{}", s1); // ❌ artık kullanılamaz
> ```

###  Çözüm 2: `push_str` ve push  string metotları

```rust
use std::io::stdin;

fn main() {
    let mut world = String::new();

    println!("Enter a world:");
    stdin().read_line(&mut world).expect("Failed to read line! 1");
    let world = world.trim();

    println!("Enter repeat number:");
    let mut times = String::new();
    stdin().read_line(&mut times).expect("Failed to read line! 2");
    let times: u32 = times.trim().parse().expect("Invalid number");

    let result = repeat(world, times);
    println!("{}", result);
}

fn repeat(text:&str, times: u32) -> String {
    let mut result = String::new();
    for _ in 0..times {
        result.push_str(text);
        result.push(' ');
    }
    result
}
```

+ `push_str` → mevcut buffer’ı kullanır, yeni `String` oluşturmaz ve çok daha **performanslı ve idiomatic Rust**
###  Çözüm 3:  map metotu ile

```rust
use std::io::stdin;

fn main() {
    let mut world = String::new();

    println!("Enter a world:");
    stdin().read_line(&mut world).expect("Failed to read line! 1");
    let world = world.trim();

    println!("Enter repeat number:");
    let mut times = String::new();
    stdin().read_line(&mut times).expect("Failed to read line! 2");
    let times: u32 = times.trim().parse().expect("Invalid number");

    let result = repeat(world, times);
    println!("{}", result);
}

fn repeat(text:&str, times: u32) -> String {
	let result: Vec<&str> = (0..times).map(|_| text).collect();
	result.join(" ");
}
```

# Kaynak:

1.  [Learn Rust Programming - Complete Course 🦀](https://www.youtube.com/watch?v=BpPEoZW5IiY)
2. 