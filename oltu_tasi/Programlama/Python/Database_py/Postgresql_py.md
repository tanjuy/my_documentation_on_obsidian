
# Psycopg
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

```python
import psycopg2

conn = psycopg2.connect(
        dbname = "postgres",
        user= "postgres",
        password = "sifre",
        host = "localhost",
        port = "5432"
        )

cur = conn.cursor()

cur.execute("SELECT version();")
print(cur.fetchone())

cur.close()
conn.close()
```

**Çıktı:**

```shell
('PostgreSQL 14.20 (Ubuntu 14.20-0ubuntu0.22.04.1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 11.4.0-1ubuntu1~22.04.2) 11.4.0, 64-bit',)
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

## KAYNAK:

1. [psycopg.org](https://www.psycopg.org/docs/index.html)
