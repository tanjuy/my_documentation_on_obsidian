#programlama #rust #database  #postgreSQL 

## Database Bağlanma:

```rust
use postgres::{Client, NoTls, Error};

fn main() -> Result<(), Error> {
    // Veritabanına bağlan
    let mut client = Client::connect(
        "host=localhost port=5432 user=postgres password=sifre dbname=postgres",
        NoTls,
    )?;

    // Sorguyu çalıştır
    let row = client.query_one("SELECT version()", &[])?;
    
    // Sonucu yazdır
    let version: &str = row.get(0);
    println!("{}", version);

    // Rust'ta bağlantı otomatik olarak kapanır (RAII)
    // client.close() gibi bir metoda gerek yok
    
    Ok(())
}
```

```toml
[dependencies]
postgres = "0.19"
```


## Database Listeleme:

```rust

```