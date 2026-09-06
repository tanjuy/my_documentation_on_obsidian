# Sqlite nedir?

+ **SQLite**, gömülü (embedded) bir **veritabanı yönetim sistemidir (DBMS)**.
+ Genellikle küçük ve orta ölçekli uygulamalarda tercih edilir çünkü kurulumu, konfigürasyonu ve sunucuya ihtiyacı yoktur.
+ Dosya tabanlı çalışır ve tüm veritabanı tek bir `.sqlite` veya `.db` dosyasında saklanır.

### Temel Özellikeri:

|Özellik|Açıklama|
|---|---|
|**Sunucusuz**|MySQL veya PostgreSQL gibi bir sunucuya ihtiyaç duymaz.|
|**Tek dosyada saklama**|Tüm veriler bir `.db` dosyasında tutulur.|
|**Küçük boyut**|Kütüphane boyutu çok küçüktür (yaklaşık 1 MB civarında).|
|**Taşınabilirlik**|Veritabanı dosyasını başka sistemlere doğrudan kopyalayabilirsin.|
|**ANSI SQL desteği**|Standart SQL komutlarının büyük çoğunluğunu destekler.|
|**Yaygın kullanım**|Android, iOS, tarayıcılar (Firefox), gömülü sistemler gibi yerlerde kullanılır.|

# Sqlite Yükleme:

## Debian/Ubuntu:

```shell
sudo apt-get install sqlite3
```


# A. Yardım:

```shell
.help
```

# B. Database İşlemeleri:

## B.1. Database Listeleme:

Bağlı olduğunuz SQLite oturumundaki veritabanlarını listeleme

```SQL
.databases
```

**Çıktı:**

```
sqlite> .database
main: /home/admin/Flask_Dersleri/users.db r/w
```
## B.2. Database Oluşturma:

SQLite'ta veritabanı oluşturmak için özel bir `CREATE DATABASE` komutu yoktur. SQLite dosya tabanlı bir veritabanı olduğu için, veritabanı ismiyle istemciyi başlatmak veya bir dosyaya bağlanmak veritabanını otomatik olarak oluşturur.

### B.2.1. Komut Satırı (CLI) ile:

Terminal veya komut satırına dosya adını yazarak veritabanını oluşturabilirsiniz:

```bash
sqlite3 veritabani_adi.db
```

_Dosya henüz yoksa SQLite yeni bir veritabanı dosyası oluşturur ve SQLite komut istemcisini açar._
### B.2.2. SQLite İstemcisi İçindeyken:

`sqlite3` başlatıldıktan sonra başka bir veritabanına bağlanmak veya yenisini oluşturmak için:

```sql
.open veritabani_adi.db
```

# C. Tabloları İşlemleri

## C.1. Tabloları Listeleme:

```sql
.tables
```

## C.2 Tablo Oluşturma:

### C.2.1 Syntax:

```sql
CREATE TABLE table_name (
	column1 type1,
	column2 type2,
	...
);
```

### C.2.2. Örnek 1:

```sql
CREATE TABLE employee (
	id INTERGER PRIMARY KEY,
	name TEXT NOT NULL,
	email TEXT NOT NULL,
	department TEXT NOT NULL,
	age INTEGER
)
```

> +  `INTEGER` : 

## C.3. Tablo Şeması Bakma

Belirli bir tablonun oluşturulma SQL'ini gösterir. 

```SQL
.schema users
```

Örneğin `users` tablosu şu şekilde oluşturulmuş olsun:

```SQL
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT NOT NULL,
    email TEXT UNIQUE,
    age INTEGER
);
```

`.schema users` çıktısı:

```SQL
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT NOT NULL,
    email TEXT UNIQUE,
    age INTEGER
);
```

Bu yöntem tabloyu oluştururken kullanılan SQL ifadesini gösterdiği için oldukça kullanışlıdır.


# Programlama Dilleri:

## A. 🐍Python:

### A.1. sqlite3 Modülünü Dahil Etme

```python
import sqlite3
```

Bu satır Python'un standart kütüphanesinde bulunan **sqlite3** modülünü programa dahil eder.
- `sqlite3`, SQLite veritabanlarıyla çalışmayı sağlayan bir modüldür.
- Python'un içerisinde hazır gelir, ayrıca yüklemenize (`pip install`) gerek yoktur.

### A.2. Veritabanına Bağlanma

```python
import sqlite3

conn = sqlite3.connect('users.db')
```

Bu satır iki işlem yapar.

**a) `sqlite3.connect()`**

`connect()` fonksiyonu belirtilen SQLite veritabanına bağlanır.

```python
sqlite3.connect('users.db')
```

Python, `users.db` isimli dosyayı arar.
- Dosya varsa → ona bağlanır.
- Dosya yoksa → otomatik olarak oluşturur.

Örneğin dizininiz şöyle olsun:

```
proje/
│
├── app.py
```

Program çalışınca:

```
proje/
│
├── app.py
├── users.db
```

şeklinde yeni bir veritabanı dosyası oluşur.



