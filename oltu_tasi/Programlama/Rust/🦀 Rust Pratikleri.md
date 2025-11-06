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

+ Aşağıdaki hatayı en az değişiklikle düzeltin.

```rust

```