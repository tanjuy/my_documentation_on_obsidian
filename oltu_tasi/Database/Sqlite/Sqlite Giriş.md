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


# Yardım:

```shell
.help
```

# Tabloları İşlemleri

## A. Tabloları Listeleme:

```sql
.tables
```

## B. Tablo Oluşturma:

### B.1. Syntax:

```sql
CREATE TABLE table_name (
	column1 type1,
	column2 type2,
	...
);
```

### B.2. Örnek 1:

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


# Programlama Dilleri:

## A. 🐍Python:


