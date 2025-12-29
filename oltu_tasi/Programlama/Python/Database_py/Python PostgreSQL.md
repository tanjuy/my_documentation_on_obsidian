# Psycopg2
## 1. Sanal Ortam Kurulumu:

```shell
python3 -m venv .venv
```

```shell
source .venv/bin/activate  
```

## 2. Kurulumu:

```shell
(.venv) pip install psycopg2
```

```shell
(.venv) pip list
```
## 3. Bağlantının Kurulması:

### 3.1. Temel Bağlantı Yöntemi:

**Dosya Adı:** `connect_postgres.py` 

```python
import psycopg2

conn = psycopg2.connect(
        dbname = "postgres",
        user= "postgres",
        password = "sifre",
        host = "localhost",
        port = "5432"
        )
```

## 4. Veritabanlarını Listeleme:

+ PostgreSQL’de veritabanlarını listelemek için **herhangi bir veritabanına** (genellikle `postgres`) bağlanmanız gerekir.
+ PostgreSQL veritabanları `pg_database` sistem tablosunda tutulur.

**Dizin Yapısı:**

```shell
pyPostgres
├── connect_postgres.py
├── main.py
├── main.py.back
└── __pycache__
    └── connect_postgres.cpython-310.pyc

1 directory, 4 files
```

**Dosya Adı:** `main.py`

```python
from connect_postgres import connect

cursor = connect.cursor()

cursor.execute("""
               SELECT datname FROM pg_database;
               """)

databases = cursor.fetchall()

for db in databases:
    print(db[0])

cursor.close()
connect.close()
```

> + `pg_database` → PostgreSQL sistem kataloğu
> + `fetchall()` → Tüm sonuçları alır

> [!NOTE]
> + `template0` ve `template1` hariç tutmak için aşağıdaki SQL komutunu kullanabilirsiniz:
> ```sql
> SELECT datname FROM pg_database
> 	WHERE datistemplate = false;
> ```


## 5. Veritabanı Oluşturma:

### 5.1. Temel Kullanımı:

```python
from connect_postgres import connect 


connect.autocommit = True
cursor = connect.cursor()

cursor.execute("""
               CREATE DATABASE test_db_2;
               """)

cursor.close()
connect.close()
```

### 5.2. Güvenli Oluşturma:

```python
from connect_postgres import connect
from psycopg2 import sql

connect.autocommit = True
cursor = connect.cursor()

db_name = "test_db_3"

cursor.execute(
        sql.SQL("CREATE DATABASE {}").format(
            sql.Identifier(db_name)
            )
        )

cursor.close()
connect.close()
```


# Psycopg - Doc

**Psycopg'un Temel Özellikleri:**

1. **En popüler adaptör**: Python'da PostgreSQL ile çalışmak için en çok tercih edilen kütüphane
2. **Python [DB API 2.0](https://peps.python.org/pep-0249/) uyumlu**: Python'un standart veritabanı arayüzüne tam uyumlu
3. **Thread-safe (İş parçacığı güvenli)**: Birden fazla thread (iş parçacığı) aynı anda aynı bağlantıyı güvenle kullanabilir.
4. **Yüksek performanslı**: Özellikle şu durumlarda çok etkilidir:
	- Çok sayıda cursor açıp kapatan uygulamalarda
	- Aynı anda binlerce `INSERT` veya `UPDATE` yapan sistemlerde
	- Web servisleri, API'ler gibi çok kullanıcılı uygulamalarda

Bu özellikler sayesinde psycopg2, büyük ölçekli ve yoğun trafikli uygulamalar için ideal bir tercihtir.

**Psycopg 2'nin Teknik Özellikleri:**

1. **C dilinde yazılmış:**
	+ Python yerine C dilinde kodlanmış (daha hızlı çalışır)
	+ [`libpq`](https://www.postgresql.org/docs/current/libpq.html) (PostgreSQL'in resmi C kütüphanesi) üzerine inşa edilmiş
	+ Bu sayede hem **performanslı** hem de **güvenli**
2. **Cursor türleri:**
	+ **Client-side (İstemci tarafı) cursor**: Veriler Python uygulamasının belleğinde tutulur.
	+ **Server-side (Sunucu tarafı) cursor**: Büyük veri setleri için, veriler veritabanı sunucusunda kalır.
3. **Asenkron özellikler**:
	+ Asenkron sorgu çalıştırma (programı bloklamadan)
	+ PostgreSQL bildirimlerini (NOTIFY/LISTEN) dinleyebilme
4. **COPY desteği**:
	+ Büyük veri kümelerini çok hızlı şekilde içe/dışa aktarma
5. **Otomatik tip dönüşümü**:

```python
# Python tipleri otomatik PostgreSQL tiplerine dönüşür
   cursor.execute("INSERT INTO tablo (sayi, metin, tarih) VALUES (%s, %s, %s)",
                  (42, "merhaba", datetime.now()))
   # int → INTEGER, str → TEXT, datetime → TIMESTAMP
```

6. **Özelleştirilebilir**: Kendi veri tipleriniz için özel dönüştürücüler yazabilirsiniz.

+ Psycopg 2, hem Unicode uyumludur hem de Python 3 ile uyumludur.

## 1. Yükleme:

+ Psycopg, Python programlama dili için bir PostgreSQL bağdaştırıcısıdır (adapter). PostgreSQL’in resmi istemci kütüphanesi olan libpq için bir sarmalayıcıdır (wrapper).


> [!NOTE]
> #### Sarmalayıcı(Wrapper) nedir?
> + Psycopg, PostgreSQL ile doğrudan kendisi konuşan bir kütüphane değildir; bunun yerine PostgreSQL’in resmi istemci kütüphanesi olan `libpq`’nin fonksiyonlarını Python’dan kullanılabilir hâle getiren bir katmandır.
> + Biraz daha açarsak:
> 	- **libq** : PostgreSQL’in C diliyle yazılmış, düşük seviyeli (low-level) resmi istemci kütüphanesidir.
> 	- **Wrapper (sarmalayıcı)** : Bu düşük seviyeli C kütüphanesini “sarar” ve onun karmaşık ayrıntılarını gizleyerek, Python geliştiricisinin rahatça kullanabileceği bir API sunar.
> 	- **Psycopg’nin yaptığı iş**
> 		1. `libpq` fonksiyonlarını çağırır
> 		2.  Bellek yönetimi, veri türü dönüşümleri (ör. PostgreSQL → Python), hata yönetimi gibi işleri üstlenir.
> 		3. Python’a özgü, okunabilir ve güvenli bir arayüz sağlar.
> + **Özet:** Psycopg, PostgreSQL ile doğrudan konuşmak yerine, PostgreSQL’in resmi C kütüphanesini kullanır ve onu Python dünyasına uygun hâle getirir.

+ Çoğu işletim sistemi için Psycopg’yi kurmanın en hızlı yolu, [PyPI](https://pypi.org/project/psycopg2-binary/) üzerinde bulunan wheel paketini kullanmaktır.

```shell
$ pip install psycopg2-binary
```

+ Bu işlem, aşağıda açıklanan derleme (build) veya çalışma zamanı (runtime) ön koşullarına ihtiyaç duymayan, önceden derlenmiş ikili (binary) bir modül sürümünü kuracaktır. Güncel bir pip sürümü kullandığınızdan emin olun (örneğin `pip install -U pip` komutuyla güncelleyebilirsiniz).
+ Bunun ardından `psycopg2` paketini her zamanki şekilde import edebilirsiniz.

```python
import psycopg2

# Connect to your postgres DB
conn = psycopg2.connect("dbname=test user=postgres")

# Open a cursor to perform database operations
cur = conn.cursor()

# Execute a query
cur.execute("SELECT * FROM my_data")

# Retrieve query results
records = cur.fetchall()
```

### 1.1. psycopg ile psycopg-binary arasındaki farklar:



## KAYNAK:

1. [psycopg.org](https://www.psycopg.org/docs/index.html)
