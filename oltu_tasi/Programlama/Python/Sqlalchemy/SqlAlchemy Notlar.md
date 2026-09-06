
# 1. SqlAlchemy'e Giriş

**SQLAlchemy**, Python programlama dili için geliştirilmiş, ilişkisel veritabanları (PostgreSQL, MySQL, SQLite, Oracle vb.) ile çalışmayı son derece kolaylaştıran popüler ve açık kaynaklı bir kütüphanedir.

Temel olarak, Python kodlarınız ile veritabanınız arasında bir "çevirmen" görevi görür. Veritabanı işlemlerini uzun ve karmaşık SQL sorguları yazmak yerine, Python'un kendi nesne yönelimli (object-oriented) yapısını kullanarak yapmanızı sağlar.

SQLAlchemy, Python için yazılmış bir **SQL toolkit ve ORM (Object-Relational Mapping)** kütüphanesidir.

**Temel olarak iki katmandan oluşur:**

1. **Core (SQL Toolkit)** — Ham SQL'e çok yakın bir seviyede çalışmanı sağlar. SQL sorgularını Python nesneleri üzerinden, veritabanı motorundan bağımsız şekilde yazmana olanak tanır.
2. **ORM (Object-Relational Mapping)** — Veritabanı tablolarını Python sınıflarına, satırları da bu sınıfların örneklerine (instance) eşler. Yani SQL yazmak yerine Python nesneleriyle çalışırsın:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True)

# SQL yazmadan sorgu:
user = User.query.filter_by(username="tanju").first()
```

## 1.1. Neden SQLAlchemy Kullanmalısınız?

+ **Veritabanı Bağımsızlığı (Agnostic):** Projenize küçük ve yerel bir veritabanı olan SQLite ile başlayıp, proje büyüdüğünde kodunuzda neredeyse hiçbir değişiklik yapmadan PostgreSQL veya MySQL'e geçebilirsiniz. SQLAlchemy aradaki farklılıkları (diyalektleri) sizin için yönetir.
+ **Güvenlik:** Kullanıcıdan alınan verileri otomatik olarak temizleyerek, web uygulamalarındaki en yaygın güvenlik açıklarından biri olan **SQL Injection** saldırılarına karşı koruma sağlar.
+ **Daha Az Tekrar, Daha Temiz Kod:** Veritabanı işlemlerini Python nesneleri üzerinden yapmak, kodun okunabilirliğini ve bakımını ciddi şekilde kolaylaştırır.
+ **Karmaşık İlişkiler:** Tablolar arasındaki "Bire-Çok" (One-to-Many) veya "Çoka-Çok" (Many-to-Many) gibi karmaşık ilişkileri (JOIN işlemleri) nesneler üzerinden çok rahat bir şekilde kurgulamanızı sağlar.

Özetle SQLAlchemy; veri odaklı Python uygulamaları (özellikle Flask ve FastAPI gibi web framework'leri ile geliştirilen projeler) için endüstri standardı haline gelmiş, esnek ve güçlü bir köprüdür.

# 2. SQLAlchemy Kurulumu

SQLAlchemy, Python'un standart paket yöneticisi olan `pip` kullanılarak saniyeler içinde kurulabilir. Ancak kuruluma geçmeden önce, projelerinizin bağımlılıklarının birbirine karışmaması için bir **sanal ortam (virtual environment)** kullanmanız her zaman en iyi uygulamadır.
## 2.1. Sanal Ortam Oluşturma(Önerilen)

Projenizin ana dizininde terminali açın ve aşağıdaki komutları sırasıyla çalıştırarak sanal ortamınızı oluşturup aktif hale getirin:

**Windows için:**

```powershell
python -m venv venv
```

**macOS ve Linux için:**

```bash
python3 -m venv venv
source venv/bin/activate
```

## 2.2. SQLAlchemy'yi Yükleme

Sanal ortamınız aktifken (terminalde satırın başında `(venv)` ibaresini göreceksiniz), aşağıdaki komut ile SQLAlchemy'nin en güncel sürümünü indirebilirsiniz:

```bash
pip install SQLAlchemy
```

**Terminal Çıktısı:**

```bash
Package           Version
----------------- -------
greenlet          3.5.4
pip               23.3.2
SQLAlchemy        2.0.51
typing_extensions 4.16.0
```
## 2.3. Kurulumu Doğrulama

Kurulumun başarıyla tamamlandığını ve hangi sürümün yüklendiğini kontrol etmek için terminalde Python kabuğuna (shell) girip şu küçük testi yapabilirsiniz:

```python
import sqlalchemy
print(sqlalchemy.__version__)
```

**Terminal Çıktısı:**

```python
'2.0.51'
```

Eğer ekranda sürüm numarasını (örneğin `2.0.30` gibi) görüyorsanız, SQLAlchemy başarıyla kurulmuş demektir.

> [!info]
> #### Veritabanı Sürücüleri (DBAPI)
> SQLAlchemy, veritabanları ile iletişim kurmak için bir köprü görevi görse de, arka planda o veritabanına özel bir sürücüye (driver) ihtiyaç duyar.
> + **SQLite:** Python'un standart kütüphanesinde gömülü olarak bulunduğu için ekstra bir sürücü yüklemenize gerek yoktur. Geliştirme ve test aşamaları için anında kullanmaya başlayabilirsiniz.
> + **PostgreSQL:** Eğer projenizde PostgreSQL kullanacaksanız, SQLAlchemy'nin yanı sıra `psycopg2` sürücüsünü de kurmalısınız: `pip install psycopg2-binary`
> + **MySQL:** MySQL için genellikle `pymysql` veya `mysqlclient` tercih edilir: `pip install pymysql`
# 3. Veritabanına Bağlanmak - Engine (Motor) Oluşturma

SQLAlchemy'de veritabanı ile uygulamanız arasındaki ana iletişim noktası **Engine** (Motor) olarak adlandırılır. Engine; veritabanı bağlantılarını, bağlantı havuzunu (connection pool) ve arka planda çalışacak SQL lehçesini (dialect) yöneten merkezdir.

Uygulamanızın veritabanına göndereceği tüm SQL komutları bu motor üzerinden geçer.
## 3.1. Sqlite ile Engine Oluşturma

### 3.1.1. Veritabanı URL Yapısı (Connection String)

Genel formatı şöyle:

```
dialect+driver://username:password@host:port/database_name
```

- **dialect:** Veritabanının türü (sqlite, postgresql, mysql vb.)
- **driver:** Kullanılan Python sürücüsü (psycopg2, pymysql vb.)
- **username / password:** Veritabanı kimlik bilgileri (SQLite için gerekmez)
- **host / port:** Veritabanının çalıştığı sunucu ve port (Örn: localhost:5432)
- **database_name:** Bağlanılacak veritabanının adı

| Veritabanı          | Örnek                                          |
| ------------------- | ---------------------------------------------- |
| SQLite              | `sqlite:///dosya_adi.db` (dosya yolu göreceli) |
| SQLite (mutlak yol) | `sqlite:////home/tanju/proje/veritabani.db`    |
| SQLite (bellekte)   | `sqlite:///:memory:`                           |

> [!TIP]
> SQLite'ta üç eğik çizgi (`///`) göreceli yol, dört eğik çizgi (`////`) mutlak yol anlamına gelir — bu detay çoğu kişinin kafasını karıştırır.

#### 3.1.1.1. Dialect nedir?

Her veritabanı sistemi (PostgreSQL, MySQL, SQLite, Oracle, MS SQL Server vb.) SQL standardını biraz farklı yorumlar — kendine özgü söz dizimi (syntax), veri tipleri ve özellikleri vardır. SQLAlchemy'de bu farklılıkları yöneten bileşene **dialect** denir.

Yani `dialect` kısmı, bağlantı dizesinde **hangi veritabanına** bağlanacağını söyler:

|Dialect|Veritabanı|
|---|---|
|`sqlite`|SQLite|
|`postgresql`|PostgreSQL|
|`mysql`|MySQL / MariaDB|
|`oracle`|Oracle|
|`mssql`|Microsoft SQL Server|
#### 3.1.1.2. Driver(sürücü) ile farkı ne?

`dialect` "hangi veritabanı" sorusuna cevap verirken, `+driver` kısmı "bu veritabanına **Python'dan hangi kütüphane ile** bağlanacağım" sorusuna cevap verir.

```
postgresql+psycopg2://...
   ↑           ↑
dialect      driver
```

- **dialect** = PostgreSQL'in SQL lehçesini ve davranışını SQLAlchemy'ye tanıtan katman
- **driver** = Python ile veritabanı arasında ham bağlantıyı kuran alt kütüphane (DBAPI)

**Driver belirtmezsen**, SQLAlchemy o dialect için varsayılan sürücüyü kullanır. Örneğin:

```python
# Driver belirtilmemiş -> varsayılan sürücü kullanılır (psycopg2)
engine = create_engine("postgresql://user:pass@localhost/dbname")

# Driver açıkça belirtilmiş -> psycopg2 kullanılır (aynı sonuç)
engine = create_engine("postgresql+psycopg2://user:pass@localhost/dbname")

# Farklı bir driver seçilmiş -> asyncpg kullanılır (asenkron çalışma için)
engine = create_engine("postgresql+asyncpg://user:pass@localhost/dbname")
```

> [!TIP]
> SQLite'ta genelde driver belirtmeye gerek yoktur çünkü Python'un standart kütüphanesindeki `sqlite3` modülü varsayılan olarak kullanılır — bu yüzden örneklerde sadece `sqlite:///...` gördün, `sqlite+sqlite3` yazmadık.

### 3.1.2. Engine Oluşturma

Engine oluşturmak için SQLAlchemy kütüphanesinden `create_engine` fonksiyonunu içe aktarıyoruz. Kitabımız boyunca başlangıç için kurulumu en kolay olan **SQLite** üzerinden ilerleyeceğiz.

```python
from sqlalchemy import create_engine

# SQLite kullanarak proje dizininde 'kutuphane.db' adında bir veritabanı oluşturalım
veritabani_url = "sqlite:///kutuphane.db"

# Engine nesnesini oluşturuyoruz
engine = create_engine(veritabani_url, echo=True)
```


> [!TIP]
> #### `echo=True` Parametresi Nedir?
> `create_engine` içine `echo=True` argümanını eklemek, SQLAlchemy'nin arka planda ürettiği ve veritabanına gönderdiği tüm ham SQL kodlarını terminalinize (veya konsolunuza) yazdırmasını sağlar. 
> 
> Bu özellik, SQLAlchemy'nin nasıl çalıştığını öğrenmek ve hata ayıklamak (debugging) için mükemmel bir araçtır. Projenizi canlıya (production) alırken bu değeri `False` yapmanız önerilir.

### 3.1.3. Bağlantıyı Test Etme

Motorumuzu oluşturduk, peki gerçekten veritabanına bağlanabiliyor muyuz? Bunu test etmek için motor üzerinden bir bağlantı (connection) açabiliriz:

```python
from sqlalchemy import create_engine, text

# Engine oluştur
engine = create_engine("sqlite:///kutuphane.db", echo=False)

# Bağlantı aç ve basit bir sorgu gönder
with engine.connect() as connection:
    # Veritabanına 'Merhaba Dünya' dedirtelim
    result = connection.execute(text("SELECT 'Bağlantı Başarılı!'"))
    print(result.all())
```

Eğer bu kodu çalıştırdığınızda konsolda `[('Bağlantı Başarılı!',)]` çıktısını görüyorsanız ve proje klasörünüzde `kutuphane.db` adında boş bir dosya belirdiyse, tebrikler! SQLAlchemy ile veritabanınıza başarıyla bağlandınız.
## 3.2. PostgreSQL ile Engine Oluşturma

```python
from sqlalchemy import create_engine

# PostgreSQL için (psycopg2 sürücüsü gerekir: pip install psycopg2-binary)
engine = create_engine("postgresql://kullanici:sifre@localhost:5432/veritabani_adi")
```


> [!CAUTION]
> `create_engine()` çağrıldığında **henüz bağlantı kurulmaz**, sadece gelecekteki bağlantılar için bir "şablon" oluşturulur. Bağlantı, ilk sorgu çalıştırıldığında (lazy/tembel şekilde) kurulur.

| Veritabanı | Örnek                                          |
| ---------- | ---------------------------------------------- |
| PostgreSQL | `postgresql://user:pass@localhost/dbname`      |

# 4. Modelleri Tanımlamak ve Tablo Oluşturmak (ORM)

SQLAlchemy ORM (Object Relational Mapper) kullanmanın en büyük avantajı, veritabanı tablolarını SQL kodu yazmak yerine Python sınıfları (class) olarak tanımlayabilmemizdir. Bu sınıflara SQLAlchemy terminolojisinde **Model** denir.

İster SQLite ister PostgreSQL kullanın, tanımladığınız Python sınıfı SQLAlchemy tarafından otomatik olarak ilgili veritabanının anlayacağı SQL diline çevrilir.

## 4.1. Base (Temel) Sınıf Oluşturma

Modellerimizi oluşturmaya başlamadan önce, tüm modellerimizin miras alacağı bir ana (Base) sınıf tanımlamamız gerekir. Bu Base sınıf, SQLAlchemy'nin hangi sınıfların veritabanı tablosu olduğunu takip etmesini sağlar.


> [!caution]
> Bu kitapta güncel **SQLAlchemy 2.0** standartlarını kullanıyoruz.

```python
from sqlalchemy.orm import DeclarativeBase

class Base(DeclarativeBase):
    pass
```

## 4.2. Modelimizi Tanımlayalım (Kullanıcı Tablosu)

Şimdi `Base` sınıfından miras alan bir `Kullanici` modeli oluşturalım. SQLAlchemy 2.0'da sütunları tanımlarken Python'un tip belirteçlerini (Type Hints - `Mapped`) kullanırız. Bu, kod yazarken editörümüzün (VSCode, PyCharm vb.) bize otomatik tamamlama sunmasını ve hataları önceden yakalamasını sağlar.

```python
from sqlalchemy.orm import Mapped, mapped_column
from sqlalchemy import String
from datetime import datetime

class Kullanici(Base):
    __tablename__ = "kullanicilar" # Veritabanındaki tablonun tam adı

    # Sütun Tanımlamaları
    id: Mapped[int] = mapped_column(primary_key=True)
    isim: Mapped[str] = mapped_column(String(50), nullable=False)
    eposta: Mapped[str] = mapped_column(String(100), unique=True, nullable=False)
    
    def __repr__(self) -> str:
        return f"<Kullanici(isim='{self.isim}', eposta='{self.eposta}')>"
```

**Koddaki Kavramlar:**

- `__tablename__`: Sınıf adımız `Kullanici` olsa da, veritabanında tablonun adının ne olacağını belirtir.
- `Mapped[tip]`: Bu alanın SQLAlchemy tarafından yönetilen bir sütun olduğunu belirtir.
- `mapped_column()`: Sütunun özelliklerini (Birincil anahtar mı? Boş bırakılabilir mi? Benzersiz mi?) belirler.
- `String(50)`: Metin uzunluğunu kısıtlar.
- `__repr__`: Nesneyi ekrana yazdırdığımızda okunabilir ve anlaşılır bir çıktı görmemizi sağlar.

## 4.3. Tabloları Veritabanında Oluşturma (SQLite ve PostgreSQL)

Modelimizi Python tarafında tasarladık. Şimdi bu tasarımı fiziksel olarak veritabanına aktarmamız (tabloları oluşturmamız) gerekiyor.

İşte SQLAlchemy'nin "Veritabanı Bağımsızlığı" tam burada parlıyor! Aynı Python modelini, sadece **Engine (Motor)** değiştirerek hem SQLite'a hem de PostgreSQL'e uygulayabiliriz.

Aşağıdaki kodda, `Base.metadata.create_all(engine)` komutu veritabanına bakar; eğer `kullanicilar` tablosu yoksa, kullandığımız veritabanına uygun SQL (`CREATE TABLE...`) sorgusunu üreterek tabloyu oluşturur.

### 4.3.1.  Senaryo A: SQLite İçin Tablo Oluşturma

Genellikle geliştirme aşamasında kullanılır.

```python
from sqlalchemy import create_engine

# SQLite Motoru
sqlite_engine = create_engine("sqlite:///kutuphane.db", echo=True)

# Base sınıfına bağlı tüm tabloları veritabanında oluşturur
Base.metadata.create_all(sqlite_engine)
```
### 4.3.2. Senaryo B: PostgreSQL İçin Tablo Oluşturma

Genellikle canlı (production) ortamlarda kullanılır.

```python
# PostgreSQL Motoru (Kullanıcı adı, şifre ve db adını kendi bilgilerinize göre değiştirin)
pg_url = "postgresql+psycopg2://postgres:sifre123@localhost:5432/kutuphane_db"
pg_engine = create_engine(pg_url, echo=True)

# AYNI Base sınıfını kullanarak bu kez PostgreSQL'de tablo oluşturur
Base.metadata.create_all(pg_engine)
```


> [!warning]
> #### SQLite ve PostgreSQL Arasındaki Temel Farklar
> SQLAlchemy çoğu farkı sizin için örtbas etse de, tablo tasarlarken bazı detaylara dikkat etmek gerekir:
> 1. **String Uzunlukları:** SQLite, `String(50)` gibi uzunluk kısıtlamalarını (VARCHAR kısıtlaması) arka planda genellikle görmezden gelir ve istediğiniz kadar metin girmenize izin verir. Ancak aynı kodu PostgreSQL'de çalıştırdığınızda, 51 karakterlik bir metin eklerseniz PostgreSQL hata fırlatır (Strict typing). Bu yüzden modellerinizi her zaman PostgreSQL gibi katı kuralları olan veritabanlarına göre tasarlamak en güvenli yoldur.
> 2. **Özel Veri Tipleri:** PostgreSQL'in `JSONB`, `UUID` veya `ARRAY` gibi çok güçlü kendine has veri tipleri vardır. SQLAlchemy bunları destekler, ancak modelinizde bu tipleri kullanırsanız uygulamanız SQLite'da çalışmayabilir. İki veritabanını da destekleyecek projelerde standart veri tiplerinde kalınmalıdır.

# 5. Veritabanı ile Etkileşim - Session (Oturum) ve Veri Ekleme (INSERT)


> [!info]
> Bu bölüm, SQLAlchemy'nin "Veritabanı Bağımsızlığı" felsefesinin en net görüldüğü yerdir. 
> Çünkü **bundan sonra yazacağımız tüm kodlar, arka planda SQLite veya PostgreSQL kullanmanızdan bağımsız olarak tamamen aynı olacaktır.**

SQLAlchemy'de `Engine` (Motor) veritabanına olan fiziksel bağlantımızı sağlarken, **`Session` (Oturum)** bu bağlantı üzerinde işlemler yaptığımız, verileri geçici olarak tuttuğumuz ve değişiklikleri yönettiğimiz "çalışma alanımızdır".

Bir benzetme yapmak gerekirse; `Engine` veritabanına giden otoyoldur, `Session` ise o otoyolda taşıdığımız kargoları yönettiğimiz aracımızdır.
## 5.1. Session Nasıl Çalışyor? (Staging Area Kavramı)

Bir Python nesnesi (Model) oluşturup bunu `Session`'a eklediğimizde, veri hemen veritabanına yazılmaz. Bunun yerine **"Beklemede" (Pending)** durumuna geçer. Değişikliklerin veritabanına kalıcı olarak yazılması için süreci onaylamamız, yani **Commit** etmemiz gerekir. Bu yapı, bir hata durumunda işlemi geri alabilmemizi (Rollback) sağlar.
## 5.2. Tek Bir Kayıt Ekleme(INSERT)

Yeni bir kullanıcı oluşturmak ve veritabanına eklemek için SQLAlchemy 2.0'ın önerilen yapısı olan `with` bloğunu (Context Manager) kullanacağız. Bu yapı, işlem bittiğinde oturumun (Session) otomatik olarak kapatılmasını garanti eder ve kaynak sızıntılarını önler.

```python
from sqlalchemy.orm import Session

# Not: 'engine' nesnesini önceki bölümde oluşturduğumuz
# SQLite veya PostgreSQL motoru olarak düşünebilirsiniz.

# Session başlatıyoruz
with Session(engine) as session:
    # 1. Adım: Python nesnemizi (Kullanici) oluşturuyoruz
    yeni_kullanici = Kullanici(isim="Ahmet Yılmaz", eposta="ahmet@ornek.com")
    
    # 2. Adım: Nesneyi Session'a ekliyoruz (Şu an 'Pending' durumunda)
    session.add(yeni_kullanici)
    
    # 3. Adım: Değişiklikleri veritabanına kaydediyoruz
    session.commit()
    
    print(f"Kullanıcı başarıyla eklendi! Atanan ID: {yeni_kullanici.id}")
```


> [!CAUTION]
> `yeni_kullanici` nesnesini oluştururken `id` değeri vermedik. Veritabanında (hem SQLite hem de PostgreSQL) `id` sütununu `primary_key=True` olarak ayarladığımız için, `commit()` işlemi gerçekleştiğinde veritabanı otomatik olarak bir ID atayacak ve SQLAlchemy bu yeni ID'yi anında Python nesnemizin içine çekecektir.

## 5.3. Birden Fazla Kayıt Ekleme (Bulk Insert)

Eğer aynı anda birden fazla veri eklemek istiyorsak, her biri için tek tek `session.add()` yazmak yerine `session.add_all()` metodunu kullanarak bir liste gönderebiliriz.

```python
with Session(engine) as session:
    # Birden fazla kullanıcı nesnesi oluşturuyoruz
    kullanici1 = Kullanici(isim="Ayşe Demir", eposta="ayse@ornek.com")
    kullanici2 = Kullanici(isim="Mehmet Çelik", eposta="mehmet@ornek.com")
    kullanici3 = Kullanici(isim="Zeynep Kaya", eposta="zeynep@ornek.com")
    
    # Tüm kullanıcıları tek seferde Session'a ekliyoruz
    session.add_all([kullanici1, kullanici2, kullanici3])
    
    # Tek bir commit ile hepsini veritabanına yazıyoruz
    session.commit()
    
    print("Toplu ekleme işlemi başarılı!")
```

## 5.4. Hata Yönetimi ve İşlemi Geri Alma(Rollback)

Veritabanı işlemlerinde bazen işler ters gidebilir. Örneğin, e-posta adresini `unique=True` (benzersiz) olarak ayarlamıştık. Eğer veritabanında zaten var olan bir e-posta adresiyle yeni bir kayıt eklemeye çalışırsak, veritabanı hata fırlatır (IntegrityError).

Bu gibi durumlarda `Session`, yarım kalan veya hatalı işlemleri iptal etmek için `rollback()` metodunu sunar.

```python
from sqlalchemy.exc import IntegrityError

with Session(engine) as session:
    try:
        # Daha önce eklediğimiz e-postayı tekrar eklemeyi deneyelim
        hatali_kullanici = Kullanici(isim="Ahmet İkiz", eposta="ahmet@ornek.com")
        session.add(hatali_kullanici)
        session.commit()
        
    except IntegrityError:
        # Hata yakalanırsa, Session'ı temizle ve işlemi geri al
        session.rollback()
        print("Hata: Bu e-posta adresi zaten kullanılıyor! İşlem iptal edildi.")
```


> [!TIP]
> #### İşlem (Transaction) Bütünlüğü
> Bir `Session` açıp `commit()` yapana kadar geçen süreç bir "Transaction" (İşlem) olarak adlandırılır. 
> 
> Eğer `add_all()` ile 100 kişi ekleyip commit ederseniz ve 99. kişide bir hata çıkarsa, hiçbir kayıt veritabanına eklenmez (hepsi geri alınır). Bu, veritabanınızın tutarlılığını (consistency) koruyan hayati bir özelliktir.

# 6. Verileri Sorgulama ve Filtreleme (SELECT İşlemleri)

Önceki bölümlerde veritabanımıza bağlantı kurduk ve yeni kayıtlar ekledik. Şimdi bu verileri nasıl okuyacağımızı öğreneceğiz.

> [!CAUTION]
> Burada SQLAlchemy ORM'in en büyük gücüyle karşılaşıyoruz: **Yazacağımız sorgulama kodları; alt yapıda SQLite, PostgreSQL veya MySQL kullanmanızdan bağımsız olarak tamamen aynı olacaktır.**

> [!info]
> SQLAlchemy 2.0 sürümü ile birlikte sorgulama işlemleri için `select()` fonksiyonu kullanılır. Bu fonksiyon, SQL'deki `SELECT` komutunun Pythonik karşılığıdır.

## 6.1. Tüm Kayıtları Çekme(SELECT *)

[Kaldığım nokta](https://gemini.google.com/app/32a3aaa2050d94e1)


