# PostgreSQL nedir?

+ **PostgreSQL**, açık kaynak kodlu, nesne-ilişkisel bir veritabanı yönetim sistemidir (RDBMS).
+ Verilerin saklanması, düzenlenmesi ve sorgulanması için güçlü ve esnek bir platform sağlar.

> [!NOTE]
> + **PostgreSQL**, veri tutarlılığına, güvenilirliğe ve standartlara (örneğin SQL) yüksek oranda bağlı, güçlü bir veritabanı sistemidir.

| Özellik                   | Açıklama                                                                                       |
| ------------------------- | ---------------------------------------------------------------------------------------------- |
| ✅ Açık kaynak             | Ücretsizdir ve herkes tarafından geliştirilebilir.                                             |
| ✅ SQL standart uyumu      | ANSI SQL standardının büyük bir kısmını destekler.                                             |
| ✅ ACID uyumluluğu         | Veritabanı işlemleri **Atomicity, Consistency, Isolation, Durability** ilkesine uygun çalışır. |
| ✅ Geniş veri tipi desteği | JSON, XML, ARRAY, UUID, IP adresi, coğrafi konum gibi özel veri tiplerini destekler.           |
| ✅ Uzantı desteği          | `PostGIS` (coğrafi veri), `pg_trgm`, `uuid-ossp` gibi güçlü eklentilerle geliştirilebilir.     |
| ✅ Çoklu eşzamanlılık      | Aynı anda birçok kullanıcının çakışmadan veri okuma/yazma yapabilmesini sağlar (MVCC sistemi). |
| ✅ Güçlü güvenlik          | Yetkilendirme, rol yönetimi, SSL ile bağlantı gibi güvenlik katmanlarına sahiptir.             |


> [!NOTE]
> **Ne için kullanılır?**
> + Web uygulamalarında (örneğin Django, Ruby on Rails, Laravel projelerinde)
> + Mobil uygulamaların arka plan servislerinde
> + Veri analitiği ve raporlama sistemlerinde
> + Coğrafi bilgi sistemlerinde (PostGIS ile)
> + Büyük veri ve veri ambarlarında

# PostgreSQL Yükleme:

## Linux OS:

### Paket Yöneticisi ile

#### Debian Temeli OS:

```shell
sudo apt-get install postgresql  # Debain Temeli
```

#### Red Hat Temeli OS:

```shell
sudo yum install postgresql # RHEL Temeli
```

[Resmi Sitesi](https://www.postgresql.org/download/linux/redhat/)
## PIP ile Yükleme:

```shell
mkdir postgreSQL
```

```shell
python3 -m venv .venv
```

```shell
 source .venv/bin/activate
```


```shell
deactivate
```
# Yükleme Sonrası:

## 1. PostgreSQL Servisinin Durumunu Kontrol Et:

```shell
sudo systemctl status postgresql
```

**Çıktı:**

```shell
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
     Active: active (exited) since Sat 2025-05-03 16:53:36 +03; 3h 31min ago
    Process: 30327 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 30327 (code=exited, status=0/SUCCESS)
        CPU: 11ms

May 03 16:53:36 nginx-tutorial3 systemd[1]: Starting PostgreSQL RDBMS...
May 03 16:53:36 nginx-tutorial3 systemd[1]: Finished PostgreSQL RDBMS.
```

+ Eğer yukarıdaki çıktıda aktif değil ise;

```shell
sudo systemctl start postgresql.service
```

+ Eğer yukarıdaki çıktıda `enable` yerine `disable` yani işletim sistemi her yeniden başlatıldığında akif olmasını istiyorsanız;

```shell
sudo systemctl enable postgresql.service
```

+ Her iki komutun bileşeni hem postgresql aktif eder hem de yeniden başlatıldığında aktif olur;

```shell
sudo systemctl enable --now postgresql.service
```

## 2. `postgres` Kullanıcısına Geçiş Yap:

+ PostgreSQL kurulduğunda otomatik olarak `postgres` adında bir sistem kullanıcısı oluşturulur. 
+ Veritabanı işlemleri genellikle bu kullanıcı üzerinden yapılır:

```shell
sudo -i -u postgres
```

## 3. psql Konsoluna Gir:

+ PostgreSQL dünyasında, komut satırı aracı olan **`psql`**, bir veritabanı yöneticisinin en yakın yol arkadaşıdır.
+ Bu araç sayesinde kullanıcılar, veritabanlarıyla doğrudan iletişim kurabilir; verileri sorgulayabilir, güncelleyebilir, hatta sistemin yapısını değiştirebilirler.
+ PostgreSQL'in etkileşimli terminaline (`psql`) geçmek için:

```shell
psql
```


> [!NOTE]
> + `psql` ile `psql -U postgres -d postgres` aynıdır. Çünkü, postgreSQL'ın varsayılan kullanıcısı `postgres`' ve varsayılan veritabanı(database) `postgres`'dir.
> + `psql -U username -d database` komutu ile başka kullanıcılara ve ilgili veritabanlarına(databes) geçiş yapabilirsiniz.

+ Girdikten sonra şöyle bir ekran görürsün:
+ Artık SQL komutlarını çalıştırabiliriz.

```shell
psql (14.17 (Ubuntu 14.17-0ubuntu0.22.04.1))
Type "help" for help.

postgres=#
```

+ SQL komut satırından çıkmak için:

```shell
psql (14.17 (Ubuntu 14.17-0ubuntu0.22.04.1))
Type "help" for help.

postgres=# \q
```


## 4. Yardım Sayfaları:

### psql dışından:

#### options:

```shell
postgres@nginx-tutorial3:~$ psql --help  # veya psql -?
```


#### commands:

+ Bu komutu yazdığınızda, **`psql` arayüzünde kullanabileceğiniz özel komutların bir listesini** görürsünüz.
+ Bunlar, klasik SQL komutlarından farklıdır; genellikle ters bölü (`\`) işaretiyle başlarlar ve veritabanı yönetimini kolaylaştıran pratik araçlardır.

```shell
postgres@nginx-tutorial3:~$ psql --help=commands
```


> [!NOTE]
> + Eğer `psql` içerisine girdiyseniz, orada da aynı bilgileri şu komutla alabilirsiniz:
> ```shell
> postgres=# \?
> ```


> [!NOTE]
> + `psql` içindeki bu komutlar, veritabanı ile "hızlı konuşma yolları" gibidir. 
> + Uzun uzun SQL yazmadan bir bakışta tablo listesine ulaşmak, mevcut veritabanlarını görmek gibi işleri kolaylaştırır.

#### variables:

+ Veritabanı yönetiminde bazen yalnızca komutlar yeterli olmaz; sistemin davranışını belirleyen, ince ayarlar sunan bazı **değişkenlere** ihtiyaç duyarız.
+ İşte PostgreSQL’in komut satırı aracı olan `psql`, bu ihtiyacı karşılamak için bize “değişkenler” sunar.
+ Bu değişkenler, `psql`’in nasıl davrandığını kontrol eder.


> [!NOTE]
> Örneğin;
> + Komutların sonuçları renkli mi olsun?
> + Satır sonlarında hangi karakter görünsün?
> + Giriş satırlarında hangi istemi (prompt) gösterelim?
> + SQL çıktısı tablo şeklinde mi yoksa düz metin mi olsun?

##### Temel Kullanımı:

```shell
postgres@nginx-tutorial3:~$  psql -d postgres -U postgres --set=AUTOCOMMIT off
```


```psql
\echo :AUTOCOMMIT -- Çıktı: off
```

### psql içerinden:

#### options:


#### commands:


#### variables:

##### Temel Kullanımı:

```psql
postgres=# \set AUTOCOMMIT off 
```


```psql
postgres=# \echo :AUTOCOMMIT  -- Çıktı: off 
```



# SQL istemcileri:

## psql istemcisi:

### Örnek 1: `psql --html` 

+ `psql` komut satırı aracında `-H` veya `--html` parametresi, sorgu sonuçlarını HTML formatında çıktı almaya yarar.


> [!CAUTION]
> + `-H` parametresi tek başına tam bir HTML belgesi oluşturmaz, sadece `<table>` etiketi ve içeriğini üretir.
> + Tam bir HTML sayfası oluşturmak için ek işlem gerekebilir.
> + Çıktıyı doğrudan tarayıcıda görüntülemek için dosya uzantısının `.html` olması gerekir


```shell
tanju@nginx-tutorial3:~$ psql -c "\du"
```

**Çıkıt:**

```sql
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 linus     | Superuser, Create role, Create DB                          | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 selcuk    | Create DB, Cannot login                                    | {}
 tanju     | Superuser, Create DB                                       | {}
 tanjuu    | Create DB                                                  | {}
```

+ `-H` veya `--html` parametresi sayesinde html formatında çıktı üretik:

```shell
tanju@nginx-tutorial3:~$ psql -c "\du" -H
```


> [!NOTE]
> + Oluşturulan html çıktısını bir dosyaya kayıt etmek için;
> + Yönlendirme operatör(`>`) ile
> ```shell
> tanju@nginx-tutorial3:~$ psql -c "\du" -H > output.html
> ```
> + `-o` parametresi ile
> ```shell
> tanju@nginx-tutorial3:~$ psql -c "\du" -H -o output.html
> ```


**Çıkıt:**

```html
<table border="1">
  <caption>List of roles</caption>
  <tr>
    <th align="center">Role name</th>
    <th align="center">Attributes</th>
    <th align="center">Member of</th>
  </tr>
  <tr valign="top">
    <td align="left">linus</td>
    <td align="left">Superuser, Create role, Create DB</td>
    <td align="left">{}</td>
  </tr>
  <tr valign="top">
    <td align="left">postgres</td>
    <td align="left">Superuser, Create role, Create DB, Replication, Bypass RLS</td>
    <td align="left">{}</td>
  </tr>
  <tr valign="top">
    <td align="left">selcuk</td>
    <td align="left">Create DB, Cannot login</td>
    <td align="left">{}</td>
  </tr>
  <tr valign="top">
    <td align="left">tanju</td>
    <td align="left">Superuser, Create DB</td>
    <td align="left">{}</td>
  </tr>
  <tr valign="top">
    <td align="left">tanjuu</td>
    <td align="left">Create DB</td>
    <td align="left">{}</td>
  </tr>
</table>
```

### Örnek 1: `\dt` Komutu:

+ PostgreSQL'de `\dt` komutu, *psql (PostgreSQL terminal arayüzü)* içinde kullanılan **bir meta-komuttur**.
+ Bu komut, veritabanındaki **mevcut tabloları listelemek** için kullanılır.


> [!NOTE]
> + `\dt`, "display tables" anlamına gelir.
> + Sadece **tabloları** listeler (view, index, sequence gibi diğer nesneleri göstermez).
> + Varsayılan olarak, **kullanıcının erişebildiği tabloları** listeler.

```psql
\dt
```

**Meta-komut Çıktı:**

```shell
            List of relations
 Schema |      Name       | Type  | Owner
--------+-----------------+-------+-------
 public | employee_data   | table | tanju
 public | employee_data_1 | table | tanju
(2 rows)

```

#### `\dt` Komutun SQL Karşılığı:

```sql

```
## pgcli istemcisi:

+ `pgcli`, PostgreSQL için geliştirilmiş, **renkli, otomatik tamamlamalı ve daha kullanıcı dostu bir komut satırı arayüzüdür**.


> [!NOTE]
> - ✅ Otomatik tamamlama (tablolar, kolonlar, SQL sözcükleri)
> - ✅ Renkli sözdizimi (syntax highlighting)
> - ✅ Komut geçmişi
> - ✅ Daha rahat yazım deneyimi
> - ✅ `psql` komutlarının çoğu çalışır


### pgcli Kurulumu:
 
+ Resmi web sitesi kurulum aşamaları:  [pgcli yükleme](https://www.pgcli.com/install)
#### Paket Yöneticisi ile

```shell
sudo apt-get update
```

```shell
sudo apt-get pgcli
```

#### PIP ile yükleme:

```shell
sudo apt update
```

```shell
sudo apt insall python3-pip
```

```shell
python3 -m venv .venv
```

```shell
source .venv/bin/activate
```

```shell
pip3 insall pgcli
```

### PostgresSQL bağlanma:

```shell
pgcli -h localhost -U postgres -d postgres
```

> **Explanation:**
> + `-h` parametresi: veritabanın makinesin(host) adresini belirler. 
> + `-U` parametresi: veritabanına bağlanacak kullanıcıyı belirler.
> + `-d` parametresi: hangi veritabanına bağlanılacağını belirler.

**pg_hba.conf:**

```conf
# Database administrative login by Unix domain socket
local   all             postgres                                peer

# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     peer
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256
```

> **Explanation:**
> 

```shell
pgcli -U postgres -d postgres
```

**pg_hba.conf:**

```conf
# Database administrative login by Unix domain socket
local   all             postgres                                md5

# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     peer
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256
```


> [!CAUTION]
> + `pg_hba.conf` dosyasında bir değişiklik yaptıktan sonra aktif olabilmesi için;
> ```shell
>  sudo systemctl restart postgresql.service
> ```




## pgAdmin4:

+ [Yükleme Sayfası:](https://www.pgadmin.org/download/pgadmin-4-apt/)

# Log(Günlük):
## Log Ayarları:

```shell
sudo vim /etc/postgresql/14/main/postgresql.conf
```

+ Log ayarlarını değiştirmek için `postgresql.conf` dosyasında şu parametreleri ayarlayabilirsiniz.
+ `postpgresql.conf` dosyasında sadece log ile ilgili bölümler alınmıştır;

```python
#------------------------------------------------------------------------------
# REPORTING AND LOGGING
#------------------------------------------------------------------------------

# - Where to Log -

#log_destination = 'stderr'             # Valid values are combinations of
                                        # stderr, csvlog, syslog, and eventlog,
                                        # depending on platform.  csvlog
                                        # requires logging_collector to be on.

# This is used when logging to stderr:
#logging_collector = off                # Enable capturing of stderr and csvlog
                                        # into log files. Required to be on for
                                        # csvlogs.
                                        # (change requires restart)

# These are only used if logging_collector is on:
#log_directory = 'log'                  # directory where log files are written,
                                        # can be absolute or relative to PGDATA
#log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'        # log file name pattern,
                                        # can include strftime() escapes
#log_file_mode = 0600                   # creation mode for log files,
                                        # begin with 0 to use octal notation
#log_rotation_age = 1d                  # Automatic rotation of logfiles will
                                        # happen after that time.  0 disables.
#log_rotation_size = 10MB               # Automatic rotation of logfiles will
                                        # happen after that much log output.
                                        # 0 disables.
#log_truncate_on_rotation = off         # If on, an existing log file with the
                                        # same name as the new log file will be
                                        # truncated rather than appended to.
                                        # But such truncation only occurs on
                                        # time-driven rotation, not on restarts
                                        # or size-driven rotation.  Default is
                                        # off, meaning append to existing files
                                        # in all cases.
# These are relevant when logging to syslog:
#syslog_facility = 'LOCAL0'
#syslog_ident = 'postgres'
#syslog_sequence_numbers = on
#syslog_split_messages = on

# This is only relevant when logging to eventlog (Windows):
# (change requires restart)
#event_source = 'PostgreSQL'

# - When to Log -

#log_min_messages = warning             # values in order of decreasing detail:
                                        #   debug5
                                        #   debug4
                                        #   debug3
                                        #   debug2
                                        #   debug1
                                        #   info
                                        #   notice
                                        #   warning
                                        #   error
                                        #   log
                                        #   fatal
                                        #   panic

#log_min_error_statement = error        # values in order of decreasing detail:
                                        #   debug5
                                        #   debug4
                                        #   debug3
                                        #   debug2
                                        #   debug1
                                        #   info
                                        #   notice
                                        #   warning
                                        #   error
                                        #   log
                                        #   fatal
                                        #   panic (effectively off)

#log_min_duration_statement = -1        # -1 is disabled, 0 logs all statements
                                        # and their durations, > 0 logs only
                                        # statements running at least this number
                                        # of milliseconds

#log_min_duration_sample = -1           # -1 is disabled, 0 logs a sample of statements
                                        # and their durations, > 0 logs only a sample of
                                        # statements running at least this number
                                        # of milliseconds;
                                        # sample fraction is determined by log_statement_sample_rate

#log_statement_sample_rate = 1.0        # fraction of logged statements exceeding
                                        # log_min_duration_sample to be logged;
                                        # 1.0 logs all such statements, 0.0 never logs


#log_transaction_sample_rate = 0.0      # fraction of transactions whose statements
                                        # are logged regardless of their duration; 1.0 logs all
                                        # statements from all transactions, 0.0 never logs

# - What to Log -

#debug_print_parse = off
#debug_print_rewritten = off
#debug_print_plan = off
#debug_pretty_print = on
#log_autovacuum_min_duration = -1       # log autovacuum activity;
                                        # -1 disables, 0 logs all actions and
                                        # their durations, > 0 logs only
                                        # actions running at least this number
                                        # of milliseconds.
#log_checkpoints = off
#log_connections = off
#log_disconnections = off
#log_duration = off
#log_error_verbosity = default          # terse, default, or verbose messages
#log_hostname = off
log_line_prefix = '%m [%p] %q%u@%d '            # special values:
                                        #   %a = application name
                                        #   %u = user name
                                        #   %d = database name
                                        #   %r = remote host and port
                                        #   %h = remote host
                                        #   %b = backend type
                                        #   %p = process ID
                                        #   %P = process ID of parallel group leader
                                        #   %t = timestamp without milliseconds
                                        #   %m = timestamp with milliseconds
                                        #   %n = timestamp with milliseconds (as a Unix epoch)
                                        #   %Q = query ID (0 if none or not computed)
                                        #   %i = command tag
                                        #   %e = SQL state
                                        #   %c = session ID
                                        #   %l = session line number
                                        #   %s = session start timestamp
                                        #   %v = virtual transaction ID
                                        #   %x = transaction ID (0 if none)
                                        #   %q = stop here in non-session
                                        #        processes
                                        #   %% = '%'
                                        # e.g. '<%u%%%d> '
#log_lock_waits = off                   # log lock waits >= deadlock_timeout
#log_recovery_conflict_waits = off      # log standby recovery conflict waits
                                        # >= deadlock_timeout
#log_parameter_max_length = -1          # when logging statements, limit logged
                                        # bind-parameter values to N bytes;
                                        # -1 means print in full, 0 disables
#log_parameter_max_length_on_error = 0  # when logging an error, limit logged
                                        # bind-parameter values to N bytes;
                                        # -1 means print in full, 0 disables
#log_statement = 'none'                 # none, ddl, mod, all
#log_replication_commands = off
#log_temp_files = -1                    # log temporary files equal or larger
                                        # than the specified size in kilobytes;
                                        # -1 disables, 0 logs all temp files
log_timezone = 'Europe/Istanbul'

```

+ SQL komut satırı içerisinde iken `postgresql.conf` dosyasındaki ayarları durumunu görebiliriz:

```sql
SHOW log_directory;
```

**Çıktı:**

```sql
 log_directory
---------------
 log
(1 row)
```


> [!CAUTION]
> + Değişikliklerin etkili olması için PostgreSQL'i yeniden başlatmanız gerekebilir:
> ```shell
> sudo systemctl restart postgresql.service
> ```

## Log'ları İzleme:

```shell
tail -f /var/log/postgresql/postgresql-14-main.log
```

# `reload` ve `restart` işlemleri:

```sql
SELECT pg_reload_conf();
```


```shell
sudo systemctl reload postgresql.service
```

# PostgreSQL'e Bağlanma:

## Örnek 1: Yerelden Bağlanma - peer

+ PostgreSQL’de `psql` komut satırı aracı, PostgreSQL veritabanı kullanıcılarıyla eşleşen bir Linux kullanıcısıyla daha kolay çalışır.
+ Örneğin, varsayılan olarak `psql` komutunu yazdığınızda sistem, aktif Linux kullanıcınızla aynı isme sahip bir PostgreSQL kullanıcısıyla bağlantı kurmaya çalışır (peer authentication yöntemi).
+ Kendi Linux kullanıcınızı oluşturup bu kullanıcıyla `psql` kullanmak için şu adımları izleyebilirsiniz:

### 1. Linux Kullanıcısı Oluşturma:

+ Bu komut, `tanju` adında yeni bir kullanıcı oluşturur. Parola vb. bilgileri girmeniz istenebilir.
+ Eğer işletim sisteminiz ubuntu ise *interaktif* bir betik çalışacaktır.

```shell
sudo adduser tanju
```

### 2. PostgreSQL içinde aynı isimde bir kullanıcı oluşturun:

+ PostgreSQL sistemine `postgres` kullanıcısı üzerinden girip linux kullanıcısı(`tanju`) ile eşleşen veritabanı kullanıcısını(`tanju`) oluşturmanız gerekir:

```shell
sudo -u postgres psql
```

+ Sonrasında PostgreSQL kabuğunda(shell):

```sql
CREATE ROLE tanju WITH LOGIN CREATEDB;
```

> + İsterseniz `CREATEDB`, `CREATEROLE`, `SUPERUSER` gibi yetkiler de verebilirsiniz.
> + Şayet sadece `psql` bağlantısı için bir kullanıcı oluşturuyorsanız, `WITH LOGIN` yeterlidir.
> + Aynı İşlevde komut: `CREATE USER tanju WITH CREATEDB;`

```sql
CREATE DATABASE tanju;
```
### 3. Oluşturulan Kullanıcıya Geçiş:

+ Yeni kullanıcıya geçiş yapınız:

```shell
sudo -i -u tanju
```

> **Explanation:**
> + `sudo` şifresi ile `tanju` adlı kullanıcıya geçiş yapıyoruz


> [!TIP]
> + Eğer `tanju` kullanıcısın kendi şifresi ile kullanıcı geçişi yapmak istiyorsanız:
> + Önce `tanju` adlı kullanıcıya şifresini veriyoruz
> ```shell
>passwd tanju
> ```
> + Daha sonra `su` komutu ile `tanju` adlı kullanıcıya geçiş yapıyoruz.
> ```shell
> su -l tanju
> ```

### 4. `pg_hba.conf` Dosyası:

+ PostgreSQL, istemcilerin (örneğin `psql`) veritabanına bağlanmasına izin vermek için **kimlik doğrulama kurallarını** `/etc/postgresql/<version>/main/pg_hba.conf` dosyasından okur.

```shell
sudo vim /etc/postgresql/14/main/pg_hba.conf 
```

+ `local` makinelerin tüm kullanıcılar tüm veritabanı üzerindeki işlemleri `peer` olarak gerçekleştir.
+ **Kısa açıklaması(`peer`)**: Linux kullanıcı, PostgreSQL kullanıcısı ve PostgreSQL database ile eşleşirse şifresiz direk olarak bağlanır. 

```ini
# "local" is for Unix domain socket connections only
local   all             all                                     peer
```

#### `peer` Authentication Nedir?

+ `peer`, **Linux işletim sistemi kullanıcısına** göre kimlik doğrulaması yapar. Yani PostgreSQL şunu der:
+ "Bu işlemi çalıştıran Linux kullanıcısı kim? Eğer aynı isimde bir PostgreSQL rolü varsa, girişe izin veririm."


> [!NOTE]
> **Örnek:**
> - Sistemde bir **Linux kullanıcısı**: `tanju`
> - PostgreSQL içinde bir **rol (user)**: `tanju`

### 4. İstemci Tarafı:


> [!CAUTION]
> + İstemci(client) tarafı PostgreSQL sunucusu ile aynıdır. Yani istemci işlemlerini PostgreSQL sunucusu içerisinde yapılmaktadır.
> + İstemci ile Sunucu aynı makinedir.

+ Sonra `psql` komutunu doğrudan çalıştırabilirsiniz:

```shell
tanju@nginx-tutorial3:~$ psql
```
 
+ → Bu durumda PostgreSQL, "`tanju` adlı Linux kullanıcısı bağlanmaya çalışıyor, `tanju` adlı bir veritabanı kullanıcısı da var → girişe izin veriyorum" der. 

+ Bu durumda PostgreSQL `peer` yöntemi ile Linux kullanıcı adı ve PostgreSQL kullanıcı adı eşleştiği için şifre sormadan bağlanır.


> [!CAUTION]
> + Eğer `tanju` adında veritabanı yok ise hata verir. Database'leri listelemek için `\l` komutunu kullanabilirsiniz.
> ```shell
> tanju@nginx-tutorial3:~$ psql -d linus_d
> ```
> + Mevcuttaki `linus_d` adındaki veritabanına bağlanılabilir. 

## Örnek 2: Uzaktan Bağlanma - MD5

### PostgreSQL Sunucu Tarafı:

#### `postgresql.conf` Dosyası:

```shell
vim /etc/postgresql/14/main/postgresql.conf
```

**Çıktı:**

```ini
#------------------------------------------------------------------------------
# CONNECTIONS AND AUTHENTICATION
#------------------------------------------------------------------------------

# - Connection Settings -

listen_addresses = '192.168.1.132'
#listen_addresses = 'localhost'         # what IP address(es) to listen on;
                                        # comma-separated list of addresses;
                                        # defaults to 'localhost'; use '*' for all
                                        # (change requires restart)
port = 5432                             # (change requires restart)
max_connections = 100                   # (change requires restart)
#superuser_reserved_connections = 3     # (change requires restart)
unix_socket_directories = '/var/run/postgresql' # comma-separated list of directories
                                        # (change requires restart)
#unix_socket_group = ''                 # (change requires restart)
#unix_socket_permissions = 0777         # begin with 0 to use octal notation
                                        # (change requires restart)
#bonjour = off                          # advertise server via Bonjour
                                        # (change requires restart)
#bonjour_name = ''                      # defaults to the computer name
                                        # (change requires restart)

# - TCP settings -
# see "man tcp" for details

#tcp_keepalives_idle = 0                # TCP_KEEPIDLE, in seconds;
                                        # 0 selects the system default
#tcp_keepalives_interval = 0            # TCP_KEEPINTVL, in seconds;
                                        # 0 selects the system default
#tcp_keepalives_count = 0               # TCP_KEEPCNT;
                                        # 0 selects the system default
#tcp_user_timeout = 0                   # TCP_USER_TIMEOUT, in milliseconds;
                                        # 0 selects the system default

#client_connection_check_interval = 0   # time between checks for client
                                        # disconnection while running queries;
                                        # 0 for never

# - Authentication -

#authentication_timeout = 1min          # 1s-600s
#password_encryption = scram-sha-256    # scram-sha-256 or md5
#db_user_namespace = off

# GSSAPI using Kerberos
#krb_server_keyfile = 'FILE:${sysconfdir}/krb5.keytab'
#krb_caseins_users = off

# - SSL -

ssl = on
#ssl_ca_file = ''
ssl_cert_file = '/etc/ssl/certs/ssl-cert-snakeoil.pem'
#ssl_crl_file = ''
#ssl_crl_dir = ''
ssl_key_file = '/etc/ssl/private/ssl-cert-snakeoil.key'
#ssl_ciphers = 'HIGH:MEDIUM:+3DES:!aNULL' # allowed SSL ciphers
#ssl_prefer_server_ciphers = on
#ssl_ecdh_curve = 'prime256v1'
#ssl_min_protocol_version = 'TLSv1.2'
#ssl_max_protocol_version = ''
#ssl_dh_params_file = ''
#ssl_passphrase_command = ''
#ssl_passphrase_command_supports_reload = off

```

> **Explanation:**
> + `listen_addresses: 192.168.1.132` : PostgreSQL sunucusunun `192.168.1.132` ağ adreslerinden gelen bağlantıları dinleyeceğini belirler.
> + **listen_addresses**: PostgreSQL sunucusunun hangi IP adreslerinde bağlantıları kabul edeceğini belirtir.
> + Varsayılan değer genellikle `localhost` veya `127.0.0.1`'dir, yani sadece yerel bağlantılara izin verir.
> + Sunucunun uzaktan bağlantıları kabul etmesi için bu parametrenin değiştirilmesi gerekir.


> [!NOTE]
> + `listen_addresses = 'localhost'` - Sadece yerel bağlantılar (varsayılan)
> + `listen_addresses = '*'` - Tüm ağ arabirimlerinden gelen bağlantıları kabul et
> + `listen_addresses = '192.168.1.100, 10.0.0.5'` - Belirli IP adreslerini dinle


> [!WARNING]
> 1. Bu parametreyi değiştirdikten sonra PostgreSQL'i yeniden başlatmanız gerekir.
> 2. Uzaktan erişime izin vermek için `pg_hba.conf` dosyasında da ilgili ayarların yapılması gerekir.
> 3. Güvenlik nedeniyle, üretim(Production) ortamlarında sadece gerekli IP adreslerinin belirtilmesi önerilir.

#### `pg_hba.conf` Dosyası:


> [!NOTE]
> 


```python
# PostgreSQL Client Authentication Configuration File
# ===================================================
#
# Refer to the "Client Authentication" section in the PostgreSQL
# documentation for a complete description of this file.  A short
# synopsis follows.
#
# This file controls: which hosts are allowed to connect, how clients
# are authenticated, which PostgreSQL user names they can use, which
# databases they can access.  Records take one of these forms:
#
# local         DATABASE  USER  METHOD  [OPTIONS]
# host          DATABASE  USER  ADDRESS  METHOD  [OPTIONS]
# hostssl       DATABASE  USER  ADDRESS  METHOD  [OPTIONS]
# hostnossl     DATABASE  USER  ADDRESS  METHOD  [OPTIONS]
# hostgssenc    DATABASE  USER  ADDRESS  METHOD  [OPTIONS]
# hostnogssenc  DATABASE  USER  ADDRESS  METHOD  [OPTIONS]
#
# (The uppercase items must be replaced by actual values.)
#
# The first field is the connection type:
# - "local" is a Unix-domain socket
# - "host" is a TCP/IP socket (encrypted or not)
# - "hostssl" is a TCP/IP socket that is SSL-encrypted
# - "hostnossl" is a TCP/IP socket that is not SSL-encrypted
# - "hostgssenc" is a TCP/IP socket that is GSSAPI-encrypted
# - "hostnogssenc" is a TCP/IP socket that is not GSSAPI-encrypted
#
# DATABASE can be "all", "sameuser", "samerole", "replication", a
# database name, or a comma-separated list thereof. The "all"
# keyword does not match "replication". Access to replication
# must be enabled in a separate record (see example below).
#
# USER can be "all", a user name, a group name prefixed with "+", or a
# comma-separated list thereof.  In both the DATABASE and USER fields
# you can also write a file name prefixed with "@" to include names
# from a separate file.
#
# ADDRESS specifies the set of hosts the record matches.  It can be a
# host name, or it is made up of an IP address and a CIDR mask that is
# an integer (between 0 and 32 (IPv4) or 128 (IPv6) inclusive) that
# specifies the number of significant bits in the mask.  A host name
# that starts with a dot (.) matches a suffix of the actual host name.
# Alternatively, you can write an IP address and netmask in separate
# columns to specify the set of hosts.  Instead of a CIDR-address, you
# can write "samehost" to match any of the server's own IP addresses,
# or "samenet" to match any address in any subnet that the server is
# directly connected to.
#
# METHOD can be "trust", "reject", "md5", "password", "scram-sha-256",
# "gss", "sspi", "ident", "peer", "pam", "ldap", "radius" or "cert".
# Note that "password" sends passwords in clear text; "md5" or
# "scram-sha-256" are preferred since they send encrypted passwords.
#
# OPTIONS are a set of options for the authentication in the format
# NAME=VALUE.  The available options depend on the different
# authentication methods -- refer to the "Client Authentication"
# section in the documentation for a list of which options are
# available for which authentication methods.
#
# Database and user names containing spaces, commas, quotes and other
# special characters must be quoted.  Quoting one of the keywords
# "all", "sameuser", "samerole" or "replication" makes the name lose
# its special character, and just match a database or username with
# that name.
#
# This file is read on server startup and when the server receives a
# SIGHUP signal.  If you edit the file on a running system, you have to
# SIGHUP the server for the changes to take effect, run "pg_ctl reload",
# or execute "SELECT pg_reload_conf()".
#
# Put your actual configuration here
# ----------------------------------
#
# If you want to allow non-local connections, you need to add more
# "host" records.  In that case you will also need to make PostgreSQL
# listen on a non-local interface via the listen_addresses
# configuration parameter, or via the -i or -h command line switches.




# DO NOT DISABLE!
# If you change this first entry you will need to make sure that the
# database superuser can access the database using some other method.
# Noninteractive access to all databases is required during automatic
# maintenance (custom daily cronjobs, replication, and similar tasks).
#
# Database administrative login by Unix domain socket
local   all             postgres                                md5

# TYPE  DATABASE        USER            ADDRESS                 METHOD
host    all             all             192.168.1.0/24          md5

# "local" is for Unix domain socket connections only
local   all             all                                     peer
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256

```

> **Explanation:**
> + PostgreSQL'in `pg_hba.conf` (Host-Based Authentication) dosyasında `md5`, bir kimlik doğrulama yöntemidir ve şifrelerin MD5 hash algoritmasıyla korunarak iletilmesini sağlar.

> [!NOTE]
> + **md5**: Kullanıcının şifresini MD5 hash'ine dönüştürerek sunucuya gönderir.
> + Şifre veritabanında şifrelenmiş (hashlenmiş) olarak saklanır.
> + Ham şifre asla ağ üzerinden gönderilmez, sadece hash değeri iletilir.



> [!NOTE]
> + `md5` ve `scram-sha-256` nasıl bir çıktı ürettiğini görmek için;
> + `md5` için;
> ```shell
> echo -n "sifre" | md5sum
> ```
> + `sha256` için; 
> ```shell
> echo -n "sifre" | sha256sum
> ```


```python
# TYPE  DATABASE        USER            ADDRESS                 METHOD
host    all             all             192.168.1.0/24          md5
```

> **Explanation:**
> + Bu örnekte, 192.168.1.0/24 ağındaki tüm istemciler, herhangi bir veritabanına bağlanırken MD5 yöntemiyle kimlik doğrulaması yapacaktır.


> [!TIP]
> + Eğer sadece bir  IP belirtmek isterseniz; `192.168.1.132/32`
> ```python
> # TYPE  DATABASE        USER            ADDRESS                 METHOD
> host    all             all             192.168.1.106/32        md5
> ```
> + Bu postgreSQL sunucusuna uzaktan sadece `192.168.1.106` nolu IP adresi bağlanabilir


> [!TIP]
> + Eğer sadece bir kullanıcı belirtmek isterseniz; tanju
> ```python
> # TYPE  DATABASE        USER            ADDRESS                 METHOD
> host    all             tanju           192.168.1.100/32        md5
> ```
> + Bu postgreSQL sunucusuna uzaktan bağlanılabimesi için kullanıcısı `tanju` ve IP adresi `192.168.1.132` olması gerekmetedir.


> [!TIP]
> + Eğer sadece belirli bir database bağlanılması istenirse; `market_store`
> ```python
> # TYPE  DATABASE            USER            ADDRESS                 METHOD
> host    market_store        tanju           192.168.1.100/32        md5
> ```
> + Bu postgreSQL sunucusuna `192.168.1.132` adresi ile bağlanan `tanju` adındaki kullanıcı `market_store` veri tabanına bağlanabilir. 


> [!NOTE]
> **Özelikleri ve Avantajları:**
> 1. **Ağ Güvenliği**: Ham şifre yerine hash gönderildiği için ağ üzerinden şifre ele geçirilemez.
> 2. **Uyumluluk**: Eski PostgreSQL sürümleriyle uyumludur.
> 3. **Kolay Yapılandırma**: Basit bir şekilde ayarlanabilir

#### PostgreSQL'i Yeniden Başlatma:

```shell
sudo systemctl restart postgresql.service
```

### İstemci Tarafı:
#### psql istemcisi:

##### Syntax 1: Parametre ile

```shell
psql -h <server_IP> -p <port> -U <postgreSQL_user> -d <database>
```

##### Örnek 1: Parametre ile

```shell
psql -h 192.168.1.132 -p 5432 -U postgres -d postgres
```

##### Syntax 2: URI ile

```shell
psql postgresql://tanju@192.168.1.132/postgres?sslmode=require
```


> [!CAUTION]
> + Bazı terminal shell'leri hata verirse: örneğin `zsh` gibi
> ```shell
> psql "postgresql://tanju@192.168.1.132/postgres?sslmode=require"
> ```
> + Çift veya tek tırnak içerisinde yazınız!

##### Syntax 3: conninfo string ile


##### Örnek 3: conninfo string ile

```shell
psql "host=192.168.1.132 port=5432 dbname=postgres user=postgres sslmode=require connect_timeout=10" 
```


> [!TIP]
> + Hem URI'yı hem de conninfo string'i beraber kullanabiliriz;
> ```shell
> psql -h 192.168.1.132 -p 5432 -d postgres -U postgres -c "sslmode=require" -c "connect-timeout=10"
> ```

#### pgcli istemcisi:

##### Syntax 1: Parametre ile

```shell
pgcli -h <sunucu_ip> -p <port> -U <kullanıcı_adı> -d <veritabanı_adı>
```

##### Örnek 1: Parametreler ile

```shell
pgcli -h 192.168.1.132 -p 5432 -U tanju -d postgres
```


##### Syntax 2: URI ile

```shell
postgresql://[user[:password]@][netloc[:port]][/veritabanı][?param1=değer1&param2=değer2...]
```

> **Explanation:**
> + Protokol belirteci (alternatif olarak `postgres://` de kullanılabilir)
> + `user` : postgreSQL sunucusunda mevcut kullanıcı;
> 	- Kullanıcıları listeleme için: `\l` veya `\list` komutu
> 	- Kullanıcı oluşturmak için: `CREATE USER linus WITH PASSWORD 'sifre';`
> + `password` : postgreSQL kullanıcı şifresi. Eğer burada belirtmez iseniz `Enter` tuşuna bastığınızda istenecektir.
> + 

##### Örnek 2: URI ile

```shell
pgcli postgresql://tanju@192.168.1.132/postgres?sslmode=require
```

> **Explanation:**
> + `user` : tanju
> + `password` : şifre belirtilmemiş bundan dolayı enter bastığınızda istenecektir.
> + `netloc` : PostgreSQL sunucusun IP adresi `192.168.1.132`
> + `port` :  port belirtilmediğinde varsayılan olarak `5432` portu kullanılır. Eğer sunucu tarafında farklı bir port tanıtılmışsa burada kesinlikle yazılmak zorundadır.
> + `database`:  Bağlanılacak veritabanı adı`postgres`'dir.
> + `param1=value1` :  SSL bağlantı parametresi `sslmode=require`

**Çıktı:**

```shell
Using local time zone Europe/Istanbul (server uses Europe/Istanbul)
Use `set time zone <TZ>` to override, or set `use_local_timezone = False` in the config
Server: PostgreSQL 14.17 (Ubuntu 14.17-0ubuntu0.22.04.1)
Version: 4.3.0
Home: http://pgcli.com
tanju@192.168.1.132:postgres>
```

## Örnek 3: Uzaktan Bağlanma - scram-sha-256

+ **Yukarıdaki `Örnek 2: Uzaktan Bağlanma - md5` ile birebir aynı şekilde yapılandırılır. Fakat;**
+ SCRAM-SHA-256 (Salted Challenge Response Authentication Mechanism with SHA-256), PostgreSQL'de kullanılan modern bir şifre doğrulama protokolüdür. İşte teknik detayları:


> [!NOTE]
> 1. **MD5 Zayıflığı**: MD5 artık kriptografik açıdan zayıf kabul edilir.
> 2. **Daha İyi Alternatifler**: PostgreSQL 10'dan itibaren `scram-sha-256` daha güvenli bir alternatiftir 

+ Yeni sistemlerde daha güvenli olan `scram-sha-256` yönteminin kullanılması önerilir:

```ini
host    all             all             192.168.1.0/24          scram-sha-256
```

+ `md5` yöntemi, eski uygulamalarla uyumluluk gerektiğinde veya güvenlik gereksinimlerinin düşük olduğu ortamlarda kullanılabilir.

### SCRAM-SHA-256 vs MD5 Karşılaştırması:

| Özellik            | SCRAM-SHA-256        | MD5          |
| ------------------ | -------------------- | ------------ |
| Şifre İletimi      | Kanıt tabanlı        | Hash tabanlı |
| Tuzlama(salting)   | Evet                 | Hayır        |
| İterasyon          | Çoklu (configurable) | Tek hash     |
| Sunucu Doğrulaması | Evet                 | Hayır        |
| MITM Direnci       | Yüksek               | Düşük        |
| Şifre Sniffing     | İmkansız             | Mümkün       |


# Kod ile Bağlanma:

## PHP:

## Python:
# Kullanıcılar:

## A. Kullanıcıları Listeleme:

### psql içerisinden:

```shell
postgres=# \du
```

```shell
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

```


```sql
SELECT * FROM pg_user;
```

```shell
 usename  | usesysid | usecreatedb | usesuper | userepl | usebypassrls |  passwd  | valuntil | useconfig
----------+----------+-------------+----------+---------+--------------+----------+----------+-----------
 postgres |       10 | t           | t        | t       | t            | ******** |          |
```

## B. Yeni Kullanıcı Oluşturma:

### psql içinden:

#### Syntax: `CREATE USER`

```sql
CREATE USER user_name WITH PASSWORD 'password';
```
> **Explanation:**
> + 

#### Örnek 1: Temel Kullanımı

```sql
CREATE USER tanju WITH PASSWORD 'Linux';
```

**Çıktı:**

```sql
ALTER ROLE
```

##### Kontrol

+ Oluşturmuş olduğumuz kullanıcıları kontrol edelim;

```sql
\du
```

```shell
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 selcuk    | Superuser                                                  | {}
 tanju     | Superuser                                                  | {}
```

```sql
SELECT * FROM pg_user;
```

```shell
 usename  | usesysid | usecreatedb | usesuper | userepl | usebypassrls |  passwd  | valuntil | useconfig
----------+----------+-------------+----------+---------+--------------+----------+----------+-----------
 postgres |       10 | t           | t        | t       | t            | ******** |          |
 tanju    |    16384 | f           | t        | f       | f            | ******** |          |
 selcuk   |    16385 | f           | t        | f       | f            | ******** |          |
(3 rows)
```

```sql
SELECT usename, usesuper, passwd FROM pg_user;
```

```shell
 usename  | usesuper |  passwd
----------+----------+----------
 postgres | t        | ********
 tanju    | t        | ********
 selcuk   | t        | ********
(3 rows)
```

#### Örnek 2: Belirli Yetikler ile Oluşturma

```sql
CREATE USER 'Linus' WITH PASSWORD 'Linux' 
	CREATEDB
	CREATEROLE
	LOGIN;
```

#### Syntax: `CREATE ROLE`

```sql
CREATE ROLE user_name WITH PASSWORD 'password';
```


#### `CREATE USER` vs `CREATE ROLE`:

+ PostgreSQL'de `CREATE USER` ile `CREATE ROLE` arasındaki fark, **temelde yoktur** — sadece **sözdizimi (syntax)** farkı vardır.
+ İşlevsel olarak ikisi de aynı şeyi yapabilir.


> [!TIP]
> + `CREATE USER` → `CREATE ROLE` + `LOGIN` anlamına gelir.
> + `CREATE ROLE` → daha genel bir komuttur, login olamayan roller de oluşturabilir.

##### Kıyaslama Tablosu:

|Özellik|`CREATE USER`|`CREATE ROLE`|
|---|---|---|
|Varsayılan olarak login yetkisi verir mi?|✅ Evet (`LOGIN`)|❌ Hayır (açıkça `LOGIN` denmeli)|
|Sözdizimi sade mi?|✅ Evet|✅ Evet|
|Daha esnek mi?|❌ Hayır|✅ Evet|
|Kullanıcı oluşturmak için kullanılır mı?|✅ Evet|✅ Evet|
|Grup gibi davranan roller oluşturmak için uygun mu?|❌ Genelde hayır|✅ Evet|

##### Örneklerle Açıklama:

`CREATE USER`:

```sql
CREATE USER ali WITH PASSWORD 'sifre';
```

+ Bu aslında şuna denktir:

```sql
CREATE ROLE ali WITH LOGIN PASSWORD 'sifre';
```

`CREATE ROLE`(Login olmayan bir rol):

```sql
CREATE ROLE readonly;
```

+ Bu rol login olamaz, yani doğrudan `psql -U readonly` gibi bağlantı kuramaz. Ancak bir **grup rol** gibi kullanılabilir:

```sql
GRANT readonly TO ali;
```


> [!TIP]
> **Ne Zaman Hangisi Kullanılmalı?**
> + Bir veritabanı **kullanıcısı** oluşturuyorsan:
> 	- → `CREATE USER` (veya `CREATE ROLE ... WITH LOGIN`) kullan.
> + Bir **grup rol** (yetki seti) oluşturuyorsan:
> 	- → `CREATE ROLE` kullan.


> [!NOTE]
> + PostgreSQL resmi dokümantasyonunda şöyle belirtilir:
> + "CREATE USER is now an alias for CREATE ROLE. The only difference is that when the command is spelled CREATE USER, LOGIN is assumed by default, whereas NOLOGIN is assumed when the command is spelled CREATE ROLE."

### createuser Komutu:

#### Syntax:

```shell
createuser [connection-option...] [option...] [username]
```
#### Örnek 1: Etkileşimli

```shell
sudo -u postgres createuser --interactive
```

**Kontrol:**

```sql
\du
```

```shell
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 linus     | Superuser, Create role, Create DB                          | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 tanju     | Superuser                                                  | {}
```

#### Örnek 2: 
## C. Kullanıcıları Silme:

### C.1. psql içinden:

#### Syntax:

```sql
DROP USER user_name;
```

#### Örnek C.1: Temel Kullanım

```sql
\du
```

```shell
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 selcuk    | Superuser                                                  | {}
 tanju     | Superuser                                                  | {}
```

```sql
DROP USER selcuk;
```

**Çıktı:**
```sql
DROP ROLE
```

**Kontrol:**

```sql
\du
```

```shell
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 tanju     | Superuser                                                  | {}
```


## D. Kullanıcıları Düzenleme:

### D.1. psql içerisinden:

#### Syntax:

```sql
ALTER USER user_name WITH [OPTION]
```

#### Örnek D.1: Superuser Yetkisi Verme


> [!NOTE]
> **Superuser nedir?**
> + PostgreSQL'de **superuser** (süper kullanıcı), veritabanı sisteminde tüm yetkilere sahip özel bir kullanıcı rolüdür.
> + Varsayılan olarak PostgreSQL kurulumuyla birlikte gelen `postgres` kullanıcısı bir superuser'dır.


> [!NOTE]
> **Superuser Yetkileri ve Özellikleri**
> 1. Veritabanı Yönetimi:
> 	- **Tüm veritabanlarını** görüntüleme, oluşturma, değiştirme ve silme
> 	- Diğer kullanıcıların veritabanlarına erişim sağlama
> 	- Veritabanı bağlantı limitlerini aşma
> 2. Kullanıcı ve Rol Yönetimi:
> 	- Yeni kullanıcı/rol oluşturma ve silme

+ **Senaryo:** `linus` adlı kullanıcıyı `superuser` yapmak yani, `superuser` kullanıcı yetkilerini atamak isteniyor.

```sql
SELECT * FROM pg_user;
```

> **Explanation:**
> + `linus` adlı kullanıcıyı hangi yetkileri mevcut diye kontrol ediyoruz.

**Çıktı:**

```shell
 usename  | usesysid | usecreatedb | usesuper | userepl | usebypassrls |  passwd  | valuntil | useconfig
----------+----------+-------------+----------+---------+--------------+----------+----------+-----------
 postgres |       10 | t           | t        | t       | t            | ******** |          |
 tanju    |    16384 | f           | t        | f       | f            | ******** |          |
 linus    |    16387 | t           | f        | f       | f            | ******** |          |
(3 rows)
```

> **Explanation:**
> + `linus` kullanıcısın `usesuper` kolonuna baktığımızda `f` değerini yani `false` değerini görünmektedir.
> + Bunun anlamı `linus` kullanıcısın `superuser` yetkisi yok!

```sql
\du
```

**Çıktı:**

```shell
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 linus     | Create role, Create DB                                     | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 tanju     | Superuser                                                  | {}
```

> **Explanation:**
> + `du` komutunu kullanarak da `linus` adlı kullanıcın `superuser` yetkisi olup olmadığını teyit edebiliriz.
> + Eğer dikkat ederseniz, `tanju` ve `postgres` kullanıcıların `superuser` yetkisi olduğunu görebilirsiniz ama `linus` kullanıcısın `superuser` yetkisin olmadığı da görünmektedir. 

```sql
ALTER USER linus WITH SUPERUSER;
```

**Çıktı:**

```sql
ALTER ROLE
```

**Kontrol:**

```sql
\du
```

```shell
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 linus     | Superuser, Create role, Create DB                          | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 tanju     | Superuser                                                  | {}
```

> **Explanation:**
> + Kullanıcıları listelediğimizde `linus` adlı kullanıcında `superuser` yetkisin olduğu görünmektedir.

#### Örnek 2: Superuser Yetkisi Alma


#### Örnek 3: `createdb` Yetkisi Verme:

+ **Senaryo:** `tanju` adlı kullanıcıyı database(veritabanı) oluşturma yetkisi verilmesi istenmektedir.

**Başlangıçtaki Durum:**

```sql
\du
```

```shell
                             List of roles
 Role name |                         Attributes
-----------+------------------------------------------------------------
 linus     | Superuser, Create role, Create DB
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS
 tanju     | Superuser
```

```sql
ALTER USER tanju WITH createdb;
```


```sql
\du
```

```shell
                             List of roles
 Role name |                         Attributes
-----------+------------------------------------------------------------
 linus     | Superuser, Create role, Create DB
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS
 tanju     | Superuser, Create DB
```


#### Örnek 4: Kullanıcıya Şifre Verme:

```sql
ALTER USER tanju WITH PASSWORD 'sifre';
```



#### Örnek 5: Kullanıcı Şifresini Kaldırma:

```sql
SELECT * FROM pg_authid;
```


> [!TIP]
> + `SELECT * FROM pg_authid`  
> 	- sql komutu çok uzun bir çıktı vermektedir
> + `SELECT rolname, rolpassword FROM pg_authid`
> 	- Bu sql komutu ise sadece kullanıcı adını ve ona karşılık olarak `sha256` algoritması ile gizlenmiş şifreyi ekrana verir.
> 	- Eğer `rolpassword` kolunu boş ise kullanıcın şifresi atanmamıştır.

+ PostgresSQL kullanıcısı olan `tanju` kullanıcın şifresini kaldırıyoruz:

```sql
ALTER USER tanju WITH PASSWORD NULL;
```

+ Tekrardan  `SELECT rolname, rolpassword FROM pg_authid;` komutu ile kontrol etiğimizde `tanju` adlı kullanıcın `rolpassword` kolunun boş olduğunu göreceğiz. 

#### Örnek: Role Membership


# Database:

## a. Database Listeleme:

```sql
\l      -- \list
```

## b. Database Oluşturma:

### A. createdb Komutu:

+ `createdb`, PostgreSQL'de yeni veritabanları oluşturmak için kullanılan bir **komut satırı aracıdır**.
+ Bu araç, SQL'in `CREATE DATABASE` komutunu kullanıcı dostu bir şekilde sunar.
+ Perl programlama dili ile yazılmıştır.

#### Syntax:

```shell
createdb [connection-option...] [option...] [dbname [description]]
```

#### Örnek 1: Temel Kullanım - peer


> [!CAUTION]
> +  Bu işlemleri yapmadan önce  [[PostgreSQL Giriş#PostgreSQL'e Bağlanma#Örnek 1: Yerelden Bağlanma - peer]]  başlılığını okumanızı şiddetle önriyorum!

+ `sudo` komut ile `tanju` adlı kullanıcıya geçiş yapıyoruz. `tanju` adlı kullanıcıya şifre atanmamış. eğer `tanju` adlı kullanıcın şifre  atanmış ise `su -l tanju` kullanabilirsiniz.

```shell
ottoman@nginx-tutorial3:~$ sudo -u tanju -i
```


> [!TIP]
> + `Örnek 1: Yerelden Bağlanma - peer` başlığında olduğu gibi, linux kullanıcısı ile aynı isim ile postgresql kullanıcısı oluşturmanız gerekmektedir;
> ```sql
> CREATE ROLE tanju WITH LOGIN PASSWORD 'sifre';
> ```

```shell
tanju@nginx-tutorial3:~$ createdb test_database 
```

+ `pg_hba.conf` dosyasında şu ayar mutlaka olmalı çünkü `createdb` komutunda `-h` parametresi kullanılmadığında varsyılan olarak `unix domain socket` bağlantısı kullanılır.

```ini
# "local" is for Unix domain socket connections only
local   all             all                                     peer
```
#### Örnek 2: sudo komutu - peer

+ **Senaryo:** Başka bir linux kullanıcı(`ottoman`) üzerinden başka bir postgresql kullanıcısı(`tanju`)  ile işlem yapmak istenirse:
+ Diğer deyiş ile `Unix domain socket` kullanılacak ve `local` için ise `peer` olarak ayarlanmıştır.

```shell
ottoman@nginx-tutorial3:~$ sudo -u tanju createdb test_db_local 
```

> **Explanation:**
> + `ottoman@nginx-tutorial3:~$`
> 	- Linux prompt  incelerseniz, linux kullanıcısın `ottoman` olduğu görülmektedir.
> + `sudo -u tanju`
> 	- `sudo` komutuna `-u` parametresi ile `tanju` kullanıcısı verilmiştir.

```shell
ottoman@nginx-tutorial3:~$ sudo -u postgres createdb -O tanju test_db_local
```

> **Explanation:**
> + **Linux kullanıcısı :** `postgres`
> + **Postgresql kullanıcsı :** `tanju` ayrıca `test_db_local` veritabanın sahibi de `tanju` olacaktır.


> [!TIP]
> + **SQL Komut Karşılığı :**  `CREATE DATABASE test_db_local OWNER tanju;`
#### Örnek 3: scram-sha-256

```shell
createdb -h 192.168.1.132 -p 5432 -U tanju test_db_remote
```

+ `pg_hba.conf` dosyasında şu ayar mutlaka olmalı çünkü

```ini
# TYPE  DATABASE        USER            ADDRESS                 METHOD
host    linus_d         tanju           192.168.1.106/32        scram-sha-256
```

#### Örnek 4: md5


### B. SQL Komutları ile:



## c. Database Silme:

### c.1. SQL Komutları ile Silme:
#### Syntax:

```sql
DROP DATABASE database_name;
```

#### Örnek 1: 

```sql
SELECT * FROM pg_database;
```

```sql
SELECT oid, datname, datacl FROM pg_database;
```

```sql
  oid  |  datname  |               datacl
-------+-----------+-------------------------------------
 13761 | postgres  |
 16390 | linus_d   |
     1 | template1 | {=c/postgres,postgres=CTc/postgres}
 13760 | template0 | {=c/postgres,postgres=CTc/postgres}
 16394 | tanjuTest |
 16395 | test      |
 16396 | selcuk    |
 16397 | selcuk2   |
 16414 | tanju     |
(9 rows)
```

```sql
DROP DATABASE 
```

### c.2. dropdb Komutu ile Silme:

#### Syntax:

```shell
dropdb [connection-option...] [option...] dbname
```

#### Örnek 1: local - `peer`

+ Öncelikle `tanju` adında PostgreSQL kullanıcısı var mı diye kontrol edelim:

```shell
sudo -u postgres psql -c "\du"
```

+ Evet, aşağıdaki çıktıdan da görüleceği üzeri `tanju` adında PostgreSQL kullanıcısı mevcuttur.

```shell
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 linus     | Superuser, Create role, Create DB                          | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 selcuk    | Create DB, Cannot login                                    | {}
 tanju     | Superuser, Create DB                                       | {}
 tanjuu    | Create DB                                                  | {}

```

+ Daha sonra `tanju` adında linux kullanıcı var mı diye kontrol edelim: 

```shell
cat /etc/passwd | grep -i 'tanju'
```

+ Evet, çıktıdan anlaşılacağı üzeri  `tanju` adında linux kullanıcısı var:

```
tanju:x:1003:1003:postgreSQL user:/home/tanju:/bin/bash
```

+ Linux kullanıcısı `tanju` adlı kullanıcıya geçiş yapıyoruz:

```shell
sudo -u tanju -i
```

+ PostgrSQL sunucusunda hangi veritabanaları var ekrana yazdırıyoruz.

```shell
ottoman@nginx-tutorial3:~$ psql -l
```

+ Görüleceği üzeri bir database aşağıdaki listede görünmektedir.

```shell
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
-----------+----------+----------+-------------+-------------+-----------------------
 linus_d   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 selcuk    | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 selcuk2   | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 tanjuTest | tanjuu   | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 test      | tanjuu   | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 uzak      | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
(9 rows)
```

+ Yerel makine üzerinden işlem yapacağız. Yani Postgresql sunucu üzerinde işlemler olacak: 
+ `/etc/postgresql/14/main` dizini altındaki `pg_hba.conf` dosyasında aşağıdaki gibi ayarlandığında emin olunuz!

```ini
# "local" is for Unix domain socket connections only
local   all             all                                     peer
```

+ Yukarıdaki çıktı listesinden `uzak` adlı veritabanını kaldıralım.
+ `dropdb`'e `-h` parametresi ile IP verilmediği için varsayılan olarak `unix domain socket`'i kullanacaktır.


> [!NOTE]
> + `peer` ifadesi, eğer linux kullanıcısı ile postgreSQL rolü eşleşir ise işlemler için şifre istemez.
> + Yani aşağıdaki komut işlemi için herhangi bir şifre istenmeyecektir.

```shell
ottoman@nginx-tutorial3:~$ dropdb uzak
```

+ Tekrardan veritabanını ekran bastığımızda `uzak` adlı veritabanı silindiğini göreceksiniz:

```shell
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
-----------+----------+----------+-------------+-------------+-----------------------
 linus_d   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 selcuk    | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 selcuk2   | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 tanjuTest | tanjuu   | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 test      | tanjuu   | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
(8 rows)
```

#### Örnek 2: remote - `scram-sha-256`

##### Sunucu(Server) Tarafı:

+ `psql` komutunda `-h` parametresini kullanabilmek için `pg_hba.conf` dosyasında bu ayar mutlaka bulunmalı:
+ `pg_hba.conf` dosyasın bulunduğu dizin: `/etc/postgresql/14/main`

**pg_hba.conf:**

```shell
# TYPE  DATABASE        USER            ADDRESS                 METHOD
host    tanju           tanju           192.168.1.106/32        scram-sha-256
```

> + `host` :  bir TCP/IP soketidir. (şifrelenmiş veya şifresiz olabilir.)
> + `tanju` : postgresql sunucusunda bir veritabanı
> + `tanju`: postgresql sunucusunda bir kullanıcı
> + `192.168.1.132/32` : Postgresql sunucusuna erişebilecek makine veya makinelerin IP adresi
> + `scram-sha-256` : istemcin şifresini(password) bu algoritmaya göre hash'le
> + **Özet :** `tanju` adlı kullanıcı ve IP'si `192.168.1.132` olarak TCP/IP üzerinden `tanju` adlı veritabanına ulaşma hakkı vardır ve `tanju` adlı kullanıcın şifresi ağ üzerinde kullanılırken `scram-sha-256` göre hash'le  

##### İstemci(Client) Tarafı:

+ Öncelikle, hangi postgresql kullanıcıların olduğunu bir kontrol edelim. 
+ Ağ trafiğin güvenli olması için `ssl` şifrelemeyi kullanıyoruz.

**psql parametre ile:**

```shell
psql -h 192.168.1.132 -p 5432 -U tanju -d tanju --set=sslmode=require -c "\du"
```

> + `-h` : uzak sunucun IP adresi (`192.168.1.132`)
> + `-p`: uzak sunucun Port numarası (`5432`)
> + `-U` : PostgreSQL'ın kullanıcısı(`tanju`)
> + `-d` : PostgreSQL'in veritabanı(`tanju`)
> + `--set` : **değişken atamak** için kullanılır.(`sslmode=require`)
> + `-c` : psql aracına **doğrudan bir SQL komutu veya psql meta komutu çalıştırmasını** söyleyen bir seçenektir. (`"\du"`)


**psql URI ile:**

```shell
psql "postgresql://tanju@192.168.1.132:5432/tanju?sslmode=require" -c "\du"
```

> + Bu postgresql URI da ise `tanju` veritabanı belirtilmiştir.

veya

```shell
psql "postgresql://tanju@192.168.1.132:5432?sslmode=require" -c "\du"
```

> + `tanju` veritabanı adını belirtmezseniz aynı sonucu verecektir.

**Çıktı:**

+ Aşağıdaki çıktı da görüleceği üzeri tüm PostgreSQL kullanıcıları ekrana basılmıştır.
+ Bağlantıyı `tanju` adlı PostgreSQL kullanıcı ile sağlandı.

```shell
                             List of roles
 Role name |                         Attributes
-----------+------------------------------------------------------------
 linus     | Superuser, Create role, Create DB
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS
 selcuk    | Create DB, Cannot login
 tanju     | Superuser, Create DB
 tanjuu    | Create DB
```

+ PostgreSQL sunucusun da mevcut veritabanlarını listeleyelim:

```shell
psql "postgresql://tanju@192.168.1.132:5432/tanju?sslmode=require" -l
```

**Çıktı:**

```sql
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
-----------+----------+----------+-------------+-------------+-----------------------
 linus_d   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 selcuk    | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 selcuk2   | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 tanju     | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 tanjuTest | tanjuu   | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 test      | tanjuu   | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
(9 rows)
```


```shell
dropdb -h 192.168.1.132 -p 5432 -U tanju test
```

```sql
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
-----------+----------+----------+-------------+-------------+-----------------------
 linus_d   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 selcuk    | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 selcuk2   | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 tanju     | tanju    | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 tanjuTest | tanjuu   | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
(8 row
```

# Veri Tipleri:



# Tablolar:

## a. Tablo Oluşturma:


### Temel Syntax:

```sql
CREATE TABLE [IF NOT EXISTS] tablo_adi (
    sutun1 veri_tipi [kisitlamalar],
    sutun2 veri_tipi [kisitlamalar],
    ...
    [tablo_kisitlamaları]
);
```

### Örnek 1:  Temel Kullanımı

```shell
ottoman@nginx-tutorial3:~$ sudo -u tanju -i
```

```shell
tanju@nginx-tutorial3:~$ psql -l
```


```shell
tanju@nginx-tutorial3:~$ psql 
```

**SQL: Tablo Oluşturma**

```sql
-- 1. Yöntem: Sütun tanımıyla birlikte
CREATE TABLE students (
	student_id SERIAL PRIMARY KEY,
	name VARCHAR(50),
	surname VARCHAR(50)
);
```

> + Bu SQL komutunda kullanılan anahtar kelimeleri `nedir?` başlığı altında inceleyelim.
####  PRIMARY KEY nedir?

+ PostgreSQL'de (ve genel olarak ilişkisel veritabanı sistemlerinde) **PRIMARY KEY (birincil anahtar)**, bir tablodaki her satırı **benzersiz şekilde tanımlayan** bir veya birden fazla sütundur.

> [!NOTE]
> **Özellikleri:**
> 1.  **Benzersiz (UNIQUE)** olmalıdır: Aynı değerden birden fazla olamaz.
> 2. **NULL olamaz (NOT NULL)**: Boş değer içeremez.
> 3. **Her tabloda yalnızca bir tane** PRIMARY KEY olabilir.
> 4. **İlişkilerin temelini** oluşturur (FOREIGN KEY'ler buraya referans verir)
> 5. Genellikle tablonun kimliğini (ID’sini) temsil eder.

+ 2. Yöntem: Ayrı constraint olarak yazılmıştır. Sözdizimi(Syntax) olarak 1. yöntem ile kıyaslayınız.

```sql
-- 2. Yöntem: Ayrı constraint olarak
CREATE TABLE students (
	student_id SERIAL,
	name VARCHAR(50),
	surname VARCHAR(50),
	PRIMARY KEY (student_id)
);
```

##### PRIMARY KEY vs UNIQUE

| Özellik      | PRIMARY KEY     | UNIQUE Constraint     |
| ------------ | --------------- | --------------------- |
| NULL değeri  | Kabul etmez     | Kabul edebilir        |
| Her tabloda  | 1 tane olabilir | Birden fazla olabilir |
| Benzersizlik | Sağlar          | Sağlar                |

#### SERIAL veri tipi nedir?

+ SERIAL, PostgreSQL'de **otomatik artan (auto-increment) sayısal değerler** oluşturmak için kullanılan özel bir veri türüdür.
+ *Genellikle PRIMARY KEY alanlarında kullanılır.*

> [!NOTE]
> **Temel Özellikleri:**
> 1. **Otomatik Artırma**: Yeni her kayıtta değer otomatik olarak artar.
> 2. **Integer Tabanlı**: Arka planda INTEGER (veya BIGINT) veri türünü kullanır.
> 3. **Sequence (Dizi) Tabanlı**: Bir sequence (sıra) nesnesiyle çalışır.
> 4. **Benzersiz Değerler** üretir.

##### SERIAL Çeşitleri:
| Tür         | Arka Plandaki Veri Tipi | Aralık                         | Kullanım Senaryosu  |
| ----------- | ----------------------- | ------------------------------ | ------------------- |
| SERIAL      | INTEGER                 | 1 to 2,147,483,647             | Çoğu genel kullanım |
| BIGSERIAL   | BIGINT                  | 1 to 9,223,372,036,854,775,807 | Çok büyük tablolar  |
| SMALLSERIAL | SMALLINT                | 1 to 32,767                    | Küçük tablolar      |

+ `student` tablosun `PRIMARY KEY`'ni `INTEGER` veri tipi ile tanımlayalım, `teacher` tablosun `PRIMARY KEY`'ni `SERIAL` veri tipi ile tanılayıp kıyaslayalım: 

**SERIAL veri tipi ile:**

```sql
CREATE TABLE students (
	student_id SERIAL,
	name VARCHAR(50),
	surname VARCHAR(50),
	PRIMARY KEY (student_id)
);
```

**INTEGER veri tipi ile:**

```sql
CREATE TABLE teachers (
	teacher_id INTEGER,
	name VARCHAR(50),
	surname VARCHAR(50),
	PRIMARY KEY (teacher_id)
);
```


> [!NOTE]
> + `students` tablosuna veri girişi:
> ```sql
> INSERT INTO students (name, surname) VALUES ('linus', 'ubuntu');
> ```
> + `teacher` tablosuna veri girişi:
> ```sql
>  INSERT INTO teachers (teacher_id, name, surname) VALUES (1, 'tanju', 'yucal');
> ```
> + Eğer dikkat ederseniz `student` tablosuna 2 kolon veri girilirken, `teacher` tablosuna 3 veri girildiğine dikkat ediniz! 


> [!NOTE]
> + `students` tablosuna girilen verileri listeleme:
> ```sql
> SELECT * FROM public.students;
> ```
> + `teacher` tablosuna girilen verileri listeleme:
> ```sql
> SELECT * FROM public.teachers;
> ```


+ PostgreSQL'de bir tablonun `PRIMARY KEY` sütununun `SERIAL` (veya `GENERATED`) olarak tanımlanıp tanımlanmadığını doğrudan görebilmek için birkaç farklı yöntem vardır.

1. `\d` veya `\ds` komutu (psql terminalinde):

```sql
\d 
```

**Çıktı:**

```sql
                  List of relations
 Schema |          Name           |   Type   | Owner
--------+-------------------------+----------+-------
 public | students                | table    | tanju
 public | students_student_id_seq | sequence | tanju
 public | teachers                | table    | tanju
(3 rows)
```

> + `students_student_id_seq` veri tipi `sequence` olduğuna dikkat ediniz. 
> + Buradan `students` tablosunun `student_id`'si `SERIAL` olduğu görünmektedir.
> + Fakat `teachers` tablosun `sequence` türünde veri tipi olduğu görünmemektedir.

2. `pg_get_serial_sequence` Fonksiyonu ile:

**Student Tablosu:**

```sql
SELECT pg_get_serial_sequence('students', 'student_id');
```

**Çıktı:**

```sql
     pg_get_serial_sequence
--------------------------------
 public.students_student_id_seq
(1 row)
```

> + `students` tablosunda `student_id`'sinde `SERIAL` veri tipi kullanılmıştır.
> + Bundan dolayı `pg_get_serial_sequence` fonksiyonu `public.students_student_id_seq` değeri geri dönmektedir.

**Tecacher Tablosu:**

```sql
SELECT pg_get_serial_sequence('teachers', 'teacher_id');
```

**Çıktı:**

```sql
 pg_get_serial_sequence
------------------------

(1 row)
```

> + `teacher` tablosunda `teacher_id`'sinde `SERIAL` veri tipi değil de `INTGER` veri tipi kullanmıştık.
> + Bundan dolayı `pg_get_serial_sequence` fonksiyonu her hangi bir değer dönmedir.

#### `VARCHAR(...)` veri tipi nedir?

+ VARCHAR, PostgreSQL'de ve diğer birçok ilişkisel veritabanında kullanılan bir **string (karakter dizisi) veri türüdür**.
+ "Variable Character" (Değişken Karakter) ifadesinin kısaltmasıdır.

##### VARCHAR vs TEXT vs CHAR:

| Özellik          | VARCHAR(n)                      | TEXT                 | CHAR(n)                   |
| ---------------- | ------------------------------- | -------------------- | ------------------------- |
| Maksimum uzunluk | Belirtilen (n)                  | Sınırsız             | Sabit (n)                 |
| Depolama         | Gerçek uzunluk kadar            | Gerçek uzunluk kadar | Her zaman n karakter      |
| Performans       | Orta                            | TEXT ile benzer      | Küçük fark                |
| Kullanım         | Uzunluk sınırı önemli olduğunda | Uzun metinlerde      | Sabit uzunluklu verilerde |


> [!NOTE]
> 1. **VARCHAR(255)** geleneksel olarak yaygın kullanılır, ancak PostgreSQL'de performans açısından TEXT'ten farkı yoktur.
> 2. PostgreSQL'de VARCHAR sınırı olmadan kullanılırsa (sadece VARCHAR yazılırsa) TEXT ile aynı davranır.
> 3. UTF-8 karakterlerde, bir karakter birden fazla byte kaplayabilir (özel karakterler, emojiler gibi).
> 4. VARCHAR için belirtilen uzunluk, karakter sayısını ifade eder (byte değil).

### Örnek 2: PRIMARY KEY ve CONSTRAINT 

+ Manual olarak `PRIMARY KEY`'in `CONSTRAINT` değerini ayarlayabiliriz.
+ Eğer `PRIMARY KEY`'in `CONSTRAINT` değerini manuel olarak *ayarlamaz iseniz*, PostgreSQL otomatik olarak bir isim üretir. 

```sql
CREATE TABLE schools (
	school_id SERIAL,
	school_name VARCHAR(50),
	schoo_location VARCHAR(50),
	CONSTRAINT schools_pkey_u PRIMARY KEY (school_id)
);
```

## b. Tablo Listeleme:

### Örnek 1: Tüm tabloları listeleme

+ PostgreSQL'de `\d` komutu, **`psql` adlı komut satırı arayüzü** içinde kullanılan bir **meta-komuttur**.
+ Bu komut bir tablo, görünüm (view), dizin (index) veya başka bir nesne hakkında özet bilgi verir.

> [!CAUTION]
> + Sadece `psql` içinden çalışır, normal SQL sorgusu değildir.


```sql
\d
```

> + `\d` : Tabloları(`tables`), `views` ve `sequences` listeler
> + `\dt` :  Komutu ise sadece tabloları(`tables`) listeler.

**Çıktı:**

```sql
                  List of relations
 Schema |          Name           |   Type   | Owner
--------+-------------------------+----------+-------
 public | students                | table    | tanju
 public | students_student_id_seq | sequence | tanju
 public | teacher                 | table    | tanju
(3 rows)
```

### Örnek 2: Belirli bir tabloyu incelemek

> [!NOTE]
> **Syntax:**
> + `\d[S+]` NAME
> + NAME değeri tablo(`table`), `views` ve `sequences` olabilir! 


**students tablosu:**

```psql
\d students
```

> + NAME  değeri `students` adında bir tablo(`table`)

**students Çıktı:**

```sql
                       Table "public.teacher"
   Column   |         Type          | Collation | Nullable | Default
------------+-----------------------+-----------+----------+---------
 teacher_id | integer               |           | not null |
 name       | character varying(50) |           |          |
 surname    | character varying(50) |           |          |
Indexes:
    "teacher_pkey" PRIMARY KEY, btree (teacher_id)

```

> + `students` tablosu oluşturulurken `teacher_id` veri tipi olarak `integer` olarak verilmiştir. Bu yüzden `Default` kolonunda `nextval` değeri yok!
> + `PRIMARY KEY`'in `CONSTRAINT` değeri `teacher_pkey` postgreSQL tarafından varsayılan olarak verilmiştir.

**teachers tablosu:**

```psql
\d teachers
```

**teachers Çıktısı:**

```sql
                                         Table "public.students"
   Column   |         Type          | Collation | Nullable |                   Default
------------+-----------------------+-----------+----------+----------------------------------------------
 student_id | integer               |           | not null | nextval('students_student_id_seq'::regclass)
 name       | character varying(50) |           |          |
 surname    | character varying(50) |           |          |
Indexes:
    "students_pkey" PRIMARY KEY, btree (student_id)

```

### Örnek 3: `Sequence` veri tipini inceleme:

```sql
\d students_student_id_seq
```

**students_student_id_seq Çıktısı:**

```sql
              Sequence "public.students_student_id_seq"
  Type   | Start | Minimum |  Maximum   | Increment | Cycles? | Cache
---------+-------+---------+------------+-----------+---------+-------
 integer |     1 |       1 | 2147483647 |         1 | no      |     1
Owned by: public.students.student_id

```
## c. Tablo Silme:

### c.1. DELETE Komutu:

```sql
DROP TABLE table_name;
```

### c.2. TRUNCATE Komutu:

+ PostgreSQL'de `TRUNCATE` komutu, bir tablodaki **tüm verileri hızlıca ve kalıcı olarak silmek** için kullanılır.
+ `DELETE` komutuna benzer ama çok daha hızlı çalışır, çünkü verileri satır satır silmez, tüm tabloyu bir kerede boşaltır.

> [!NOTE]
> + Bir tablodaki **tüm satırları siler**.
> + **Rollback yapılabilir** (eğer bir transaction içinde kullanılırsa).
> + Varsayılan olarak **otomatik olarak COMMIT eder** (eğer transaction içinde değilse).
> + `DELETE`'ten farklı olarak **trigger’ları çalıştırmaz** (önemli fark).

#### TRUNCATE vs DELETE

| Özellik           | `TRUNCATE`          | `DELETE`                 |
| ----------------- | ------------------- | ------------------------ |
| Hız               | Çok hızlı           | Daha yavaş (satır satır) |
| WHERE kullanımı   | ❌ Desteklemez       | ✅ Destekler              |
| Trigger çalışması | ❌ Çalışmaz          | ✅ Çalışır                |
| Rollback desteği  | ✅ Evet (tx içinde)  | ✅ Evet                   |
| Otomatik Commit   | ✅ Evet (tx dışında) | ❌ Hayır                  |
#### Syntax:

```sql
TRUNCATE TABLE tablo_adi;
```


> [!CAUTION]
> + `TRUNCATE`, verileri **geri alınamaz şekilde** siler (eğer bir transaction içinde değilse).


> [!TIP]
> + **İlişkili tablolar varsa** (foreign key ile bağlı), doğrudan `TRUNCATE` çalışmaz. Bunun yerine `CASCADE` kullanılır:
> ```sql
> TRUNCATE TABLE orders CASCADE;
> ```
>  + Bu, `orders` tablosuna bağlı diğer tabloların verilerini de siler.

#### Örnek 1:


# Tek Tırnak vs Çıft Tırnak:


# Fonksiyonlar:

## 1. pg_get_userbyid Fonksiyonu:

+ `pg_get_userbyid`, PostgreSQL'in sistem kataloğunda bulunan bir fonksiyondur ve bir kullanıcı veya rolün OID (Object Identifier) numarasını alarak karşılık gelen kullanıcı/rol adını döndürür.


> [!NOTE]
> **Sistem tablolarındaki "owner" alanları** için kullanılır:
> - `pg_database.datdba` (veritabanı sahibi)
> - `pg_class.relowner` (tablo/schema sahibi)
> - `pg_proc.proowner` (fonksiyon sahibi)

### Syntax:

```sql
pg_get_userbyid ( role oid ) → name
```

+ **`oid`**: PostgreSQL içindeki kullanıcıların (rollerin) sistemdeki **benzersiz nesne kimliğidir (Object ID)**.
+ Fonksiyon, bu `oid`'ye karşılık gelen kullanıcı/rol adını bir `text` olarak döndürür.
### Örnek 1: `pg_database.datdba`


```sql
SELECT oid, datname, datdba, datacl FROM pg_database; 
```

> [!TIP]
> + `pg_database` tablosun tüm kolonlarını görmek için;
> ```sql
> SELECT * FROM pg_database;
> ```

**Çıktı:**

```sql
  oid  |  datname  | datdba |               datacl
-------+-----------+--------+-------------------------------------
 13761 | postgres  |     10 |
 16390 | linus_d   |     10 |
     1 | template1 |     10 | {=c/postgres,postgres=CTc/postgres}
 13760 | template0 |     10 | {=c/postgres,postgres=CTc/postgres}
 16394 | tanjuTest |  16392 |
 16395 | test      |  16392 |
 16396 | selcuk    |  16384 |
 16397 | selcuk2   |  16384 |
 16414 | tanju     |  16384 |
(9 rows)
```

+ `datdba` kolonundan verileri `pg_get_userbyid` fonksiyonuna gönderiyoruz. 

```sql
SELECT oid, datname, pg_get_userbyid(datdba), datacl FROM pg_database;
```

**Çıktı:**

+ `pg_get_userbyid` fonksiyonu `oid` değerlerine göre veritabanın(`datname`) kime ait olduğunu yazıyor.

```sql
  oid  |  datname  | pg_get_userbyid |               datacl
-------+-----------+-----------------+-------------------------------------
 13761 | postgres  | postgres        |
 16390 | linus_d   | postgres        |
     1 | template1 | postgres        | {=c/postgres,postgres=CTc/postgres}
 13760 | template0 | postgres        | {=c/postgres,postgres=CTc/postgres}
 16394 | tanjuTest | tanjuu          |
 16395 | test      | tanjuu          |
 16396 | selcuk    | tanju           |
 16397 | selcuk2   | tanju           |
 16414 | tanju     | tanju           |
(9 rows)
```

### Örnek 2: `pg_class.relowner`

```sql
SELECT oid, relname, relowner FROM pg_class;
```

```sql
  oid  |                    relname                    | relowner
-------+-----------------------------------------------+----------
  2619 | pg_statistic                                  |       10
  1247 | pg_type                                       |       10
  2836 | pg_toast_1255                                 |       10
  2837 | pg_toast_1255_index                           |       10
  4171 | pg_toast_1247                                 |       10
  4172 | pg_toast_1247_index                           |       10
  2830 | pg_toast_2604                                 |       10
  2831 | pg_toast_2604_index                           |       10
  2832 | pg_toast_2606                                 |       10
  2833 | pg_toast_2606_index                           |       10
  4157 | pg_toast_2612                                 |       10
  4158 | pg_toast_2612_index                           |       10
```

```sql
SELECT oid, relname, pg_get_userbyid(relowner) FROM pg_class;
```
### Örnek 3: `pg_proc.proowner`




# Veri Girişi:

## INSERT INTO:

```sql
INSERT INTO employee (
	"name", description
) 
VALUES (
	'Web Development', 'Web Development Description'
)
```


# Backup(Yedek Alma):

## A. pg_dump Komutu:

+ `pg_dump`, PostgreSQL veritabanını yedeklemek için kullanılan resmi komut satırı aracıdır.
+ Bir veritabanının tamamını veya belirli tabloları dışa aktarmanı (export) sağlar.
+ Genellikle bir veritabanını daha sonra geri yüklemek (restore etmek) için kullanılır.


> [!NOTE]
> **Fonksiyonu:**
> + Veritabanının **yedeklemesini** alır.
> + Yedeği dosya olarak kaydeder (metin veya özel formatta).
> + Bu yedek, başka bir veritabanına ya da aynı veritabanına ileride **geri yüklenebilir**.


### A.1. Yerel(local) - peer auth

**Sistem Bilgileri:**

```shell
cat /etc/os-release
```

**Çıktı:**

```shell
PRETTY_NAME="Ubuntu 22.04.5 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.5 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```

#### Linux Kullanıcısı Oluşturma:

+ PostgreSQL'ün `peer authentication` için linux kullanıcısı oluşturmaz gerekmektedir:

```shell
sudo adduser backup_sql
```

> + `adduser` komutu çalıştırdığımızda kullanıcı oluşturmak için bir script çalışacaktır.

veya

```shell
sudo useradd -m -d /home/backup_sql -s /sbin/bash -c "postgreSQL user" backup_sql
```

> + `useradd`: Bu, Linux'ta **yeni bir kullanıcı hesabı oluşturmak** için kullanılan ana komuttur.
> + `-m`: Bu seçenek, yeni kullanıcının **ana dizininin (home directory) oluşturulmasını** sağlar. Eğer bu seçenek kullanılmazsa, `/home/backup_sql` dizini otomatik olarak oluşturulmaz ve manuel olarak oluşturmanız gerekebilir.
> + `-d /home/backup_sql`: Bu seçenek, oluşturulan kullanıcının **ana dizininin nerede olacağını** belirtir. Burada, `backup_sql` kullanıcısının ana dizini `/home/backup_sql` olarak ayarlanmıştır.
> + `-s /sbin/bash`: Bu seçenek, kullanıcının **varsayılan kabuğunu (shell)** belirler. `/sbin/bash`, Bourne-Again Shell'in (Bash) yoludur ve Linux sistemlerinde en yaygın kullanılan kabuklardan biridir. Bu, kullanıcının sisteme giriş yaptığında hangi komut yorumlayıcısını kullanacağını belirtir.
> + `-c "postgreSQL user"`: Bu seçenek, kullanıcı için bir **yorum (comment)** veya açıklama ekler. Bu yorum, genellikle kullanıcının tam adını veya hesabın amacını belirtmek için kullanılır. Burada, kullanıcının amacının "postgreSQL user" olduğu belirtilmiştir. Bu bilgi, `/etc/passwd` dosyasında kullanıcı bilgileriyle birlikte saklanır ve sadece bilgilendirme amaçlıdır.
> + `backup_sql`: Bu, **oluşturulacak yeni kullanıcının adıdır**. Yani, bu komutla `backup_sql` adında yeni bir kullanıcı oluşturulur.

#### Client Auth Ayarlama:

```shell
sudo vim /etc/postgresql/14/main/pg_hba.conf
```

**Çıktı:**

```python
# "local" is for Unix domain socket connections only
local   all             all                                     peer
```

veya

```python
# "local" is for Unix domain socket connections only
local   all             backup_sql                              peer
```

> + `pg_hba.conf` dosyasında yukarıdaki gibi ayarlandığından emin olunuz.
> + `all` ile tüm kullanıcılar izin verebilirsiniz veya  sadece`backup_sql` kullanıcısına izin verebilirsiniz. 

#### Kullanıcıya Geçiş:

```shell
sudo -u backup_sql -i
```


> [!TIP]
> + `sudo` ile kullanıcı değiştirmek yerine `passwd` komutu ile kullanıcıya şifre ataması yapılabilir:
> ```shell
> passwd backup_sql
> ```


#### PostgreSQL Role Oluşturma:


> [!CAUTION]
> + Eğer PostgreSQL role veya kullanıcı oluşturmadan `psql` komutu çalıştırsanız:
> ```shell
>  backup_sql@nginx-tutorial3:~$ psql
> ```
> + Hata:
> ```shell
> psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  role "backup_sql" does not exist
> ```

+ Öncelikle `backup_sql` kullanıcısından çıkış yapıp  postgreSQL ile varsayılan gelen linux kullanıcısı `postgres` geçiş yapalım:

```shell
sudo -u postgres -i
```

+ `backup_sql` linux kullanıcısı için postgreSQL role(`backup_sql`) ve veritabanı(`backup_sql`) oluşturmak için `psql` komutunu çalıştırıyoruz:

```shell
postgres@nginx-tutorial3:~$ psql
```


> [!TIP]
> + Sadece `psql` komutunu çalıştırdığımızda
> ```shell
>  psql -h /var/run/postgresql -U postgres -d postgres
> ```
> + `-U` ve `-d` parametre değerlerini linux kullanıcısından alır.

+ `backup_sql` adında postgreSQL kullanıcısı oluşturuyoruz.

```sql
CREATE ROLE backup_sql WITH LOGIN CREATEDB;
```


> [!TIP]
> + `CREATE ROLE` alternatif olarak;
> ```sql
> CREATE USER backup_sql WITH NOPASSWORD CREATEDB;
> ```

+ `backup_sql` adında veritabanı oluşturuyoruz:

```sql
CREATE DATABASE backup_sql;
```


> [!CAUTION]
> + Eğer veritabanı oluşturmasaydık:
> ```shell
> backup_sql@nginx-tutorial3:~$ psql
> ```
> Hata:
> ```shell
> psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  database "backup_sql" does not exist
> ```


```shell
ottoman@nginx-tutorial3:~$ sudo -u backup_sql -i
```

#### Örnek 1.1: plain format

```shell
backup_sql@nginx-tutorial3:~$ pg_dump > default_backup.sql
```

> + `backup_sql` veritabanını `default_backup.sql` dosyasına yedekliyoruz.

> [!TIP]
> + Her hangi bir parametre verilmeden çalıştırıldığında;
> ```shell
> pg_dump -h /var/run/postgresql -U backup_sql -d backup_sql -F p > default_backup.sql
> ```
> + Socket yolunu öğrenmek için sql içerisinde 
> ```sql
> SHOW unix_socket_directories;
> ```

```shell
backup_sql@nginx-tutorial3:~$ cat default_backup.sql
```


> [!CAUTION]
> + `default_backup.sql` dosyasının uzantısı `.sql` olsa da ama bu text dosyasıdır.
> ```shell
> file default_backup.sql    # Çıkıt: backup_text.sql: ASCII text
> ```

**Çıktı:**

```text
--
-- PostgreSQL database dump
--

-- Dumped from database version 14.17 (Ubuntu 14.17-0ubuntu0.22.04.1)
-- Dumped by pg_dump version 14.17 (Ubuntu 14.17-0ubuntu0.22.04.1)

SET statement_timeout = 0;
SET lock_timeout = 0;
SET idle_in_transaction_session_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;

--
-- PostgreSQL database dump complete
--
```

**psql ile geri yükleme:**

+ `default_restored` adında bir veritabanı oluşturuyoruz.

```shell
backup_sql@nginx-tutorial3:~$ createdb default_restored
```


> [!TIP]
> + Her hangi bir parametre girilmediğinde varsayılan olarak şöyledir;
> ```shell
> createdb -h /var/run/postgresql -U backup_sql default_restored
> ```
> + `-U` parametresi yazılmadığında linux kullanıcısından alacaktır.


```shell
backup_sql@nginx-tutorial3:~$ psql -d default_restored < default_backup.sql
```


> [!CAUTION]
> + `psql` parametrelerini değiştirerek başka kullanıcıya veya sunucuya geri yükleme(`restore`) yapabilirsiniz:
> ```shell
>  psql -h /var/run/postgresql -U backup_sql -d backup_sql < default_backup.sql
> ```

#### Örnek 1.2: custom format:

```shell
backup_sql@nginx-tutorial3:~$ pg_dump -F c -f default_backup.dmp
```

> `-f` : Hedef dosya adı
> `-F`: Format: `p` = plain (sql), `c` = custom, `t` = tar

##### `.dmp` (Custom Format) - Format Nedir?

+ **`.dmp` dosyası:** `pg_dump` ile `-F c` (veya `--format=custom`) seçeneği kullanılarak oluşturulmuş bir **özel yedekleme formatıdır**.
+ Bu format:
	- Sıkıştırılmıştır.
	- Bölümler halinde içeriğe sahiptir (tablo, veri, index, trigger vb.).

> [!CAUTION]
> - **Sadece `pg_restore` aracıyla geri yüklenebilir.**


> [!TIP]
>  **`.dmp` uzantısı zorunlu mu?**
> + Hayır. Uzantı tamamen kullanıcı tercihine bağlıdır. `.dmp`, `.backup`, `.pgdump` veya `.custom` da kullanılabilir.
> + Önemli olan **dosyanın içeriğinin hangi formatta olduğudur**, adı değil.
> + En doğru sonucu `file` komutu verir:
> ```shell
> file default_backup.dmp 
> ```
> + Sonuc:
> ```shell
> default_backup.dmp: PostgreSQL custom database dump - v1.14-0
> ```

#### Örnek 1.3: tar format

```shell
backup_sql@nginx-tutorial3:~$ pg_dump -F t -f backup.tar backup_sql
```

> `-f` : Hedef dosya adı
> `-F`: Format: `p` = plain (sql), `c` = custom, `t` = tar

> [!CAUTION]
> - **Sadece `pg_restore` aracıyla geri yüklenebilir.**

## B. pg_restore Komutu:

+ `pg_restore`, PostgreSQL veritabanı sisteminde kullanılan bir komut satırı aracıdır.
+ Bu araç, `pg_dump` komutuyla **özel formatta** (`-Fc` gibi) yedeklenmiş veritabanı dosyalarını geri yüklemek (restore etmek) için kullanılır.
+ `pg_restore`, `pg_dump` tarafından oluşturulan bir arşiv dosyasından bir PostgreSQL veritabanını geri yükler.

> [!NOTE]
> + `pg_dump` → Veritabanını yedekler.
> + `pg_restore` → Bu yedeği tekrar bir veritabanına geri yükler.

### Syntax:

```shell
pg_restore [connection-option...] [option...] [filename]
```

### B.1. Yerel(local) - peer auth


+ `tar_backup` adında veritabanı oluşturalım:

```shell
backup_sql@nginx-tutorial3:~$ createdb tar_backup
```

+ Aşağıdaki komut oluşturulan veritabanlarını listeler. Eğer `tar_backup` liste içerisinde ise işlem başarılıdır:

```shell
backup_sql@nginx-tutorial3:~$ psql -l
```

#### B.1.1. `pg_restore -l` komutu:

+ `pg_restore -l` komutu, PostgreSQL veritabanı yedeklerini (dump dosyalarını) listelemek için kullanılan bir komuttur.
+ Bu komut, bir PostgreSQL yedek dosyasının(`dvdrental.tar`) içeriğini analiz eder ve dosyada bulunan tüm veritabanı nesnelerinin bir listesini gösterir.


> [!NOTE]
> **Ne İşe Yarar?**
> + Yedek dosyasının içeriğini görüntüler (tablolar, indeksler, fonksiyonlar, vs.)
> + Yedek dosyasının yapısını anlamanızı sağlar.
> + Geri yükleme işlemi öncesinde inceleme yapmanıza olanak tanır.
> + Hangi nesnelerin geri yükleneceğini kontrol etmenizi sağlar.

```shell
backup_sql@nginx-tutorial3:~$ pg_restore -l dvdrental.tar
```

**Çıktı:**

```shell
;
; Archive created at 2019-05-12 10:36:37 +03
;     dbname: dvdrental
;     TOC Entries: 144
;     Compression: 0
;     Dump Version: 1.13-0
;     Format: TAR
;     Integer: 4 bytes
;     Offset: 8 bytes
;     Dumped from database version: 11.3
;     Dumped by pg_dump version: 11.2
;
;
; Selected TOC Entries:
;
632; 1247 16723 TYPE public mpaa_rating postgres
635; 1247 16734 DOMAIN public year postgres
231; 1255 16736 FUNCTION public _group_concat(text, text) postgres
232; 1255 16737 FUNCTION public film_in_stock(integer, integer) postgres
233; 1255 16738 FUNCTION public film_not_in_stock(integer, integer) postgres
248; 1255 16739 FUNCTION public get_customer_balance(integer, timestamp without time zone) postgres
249; 1255 16740 FUNCTION public inventory_held_by_customer(integer) postgres
250; 1255 16741 FUNCTION public inventory_in_stock(integer) postgres
234; 1255 16742 FUNCTION public last_day(timestamp without time zone) postgres
235; 1255 16743 FUNCTION public last_updated() postgres
196; 1259 16744 SEQUENCE public customer_customer_id_seq postgres
197; 1259 16746 TABLE public customer postgres
251; 1255 16753 FUNCTION public rewards_report(integer, numeric) postgres
721; 1255 16754 AGGREGATE public group_concat(text) postgres
198; 1259 16755 SEQUENCE public actor_actor_id_seq postgres
199; 1259 16757 TABLE public actor postgres
200; 1259 16762 SEQUENCE public category_category_id_seq postgres
201; 1259 16764 TABLE public category postgres
202; 1259 16769 SEQUENCE public film_film_id_seq postgres
203; 1259 16771 TABLE public film postgres
204; 1259 16783 TABLE public film_actor postgres
205; 1259 16787 TABLE public film_category postgres
206; 1259 16791 VIEW public actor_info postgres
207; 1259 16796 SEQUENCE public address_address_id_seq postgres
208; 1259 16798 TABLE public address postgres
209; 1259 16803 SEQUENCE public city_city_id_seq postgres
210; 1259 16805 TABLE public city postgres
211; 1259 16810 SEQUENCE public country_country_id_seq postgres
212; 1259 16812 TABLE public country postgres
...
```

#### B.1.2. Dump Dosyasındaki TOC(Table of Contents):

```shell
632; 1247 16723 TYPE public mpaa_rating postgres
```

> 1. **632**: Bu, dump dosyası içindeki nesnenin sıra numarasıdır (entry ID).
> 2. **1247**: Nesnenin "catalog ID"si. PostgreSQL'in sistem kataloğundaki `pg_class` tablosunda bu nesneye karşılık gelen OID (Object ID).
> 3. **16723**: Nesnenin "catalog ID"si. Bu durumda, `pg_type` sistem tablosundaki OID.
> 4. **TYPE**: Nesne türü. Burada bir veri tipi (user-defined type) olduğunu gösteriyor.
> 5. **public**: Nesnenin ait olduğu şema (schema) adı.
> 6. **mpaa_rating**: Nesnenin (tipin) adı.
> 7. **postgres**: Nesneyi oluşturan kullanıcı (owner).

#### Örnek B.1:

```shell
backup_sql@nginx-tutorial3:~$ pg_restore --no-owner -v -d tar_backup dvdrental.tar
```

> [dvdrental.tar](https://neon.tech/postgresql/postgresql-getting-started/postgresql-sample-database) dosyasını bu bağlantıdan indirebilirsiniz.


> [!TIP]
> + Her hangi bir parametre girilmediğinde varsayılan olarak alınan parametreler;
> ```shell
> backup_sql@nginx-tutorial3:~$ pg_restore -h /var/run/postgresql -p 5432 -U backup_sql --no-owner -v -d tar_backup dvdrental.tar
> ```
> + `pg_hba.conf` dosyasında `peer auth` dolayı `-h`, `-p`, `-d` ve `-U` parametre değerlerini linux(`backup_sql`) kullanıcısından alacaktır.  Ama dikkat ederseniz `-d` parametresi varsayılan değil de `tar_backup` veritabanı yazılmıştır.



> [!CAUTION]
> + Yukarıda `ps_restore -l dvdrental.tar` komutu ile `dvdrental.tar` dosyasın içerisine baktığımızda veritabanın `postgres` kullanıcısına ait olduğu görülmektedir.
> + `--no-owner` parametresi kullanılmaz ise aşağıdaki hatayı verir.
> ```
> ERROR: must be member of role "postgres"
> ```
> + Bu parametre(`--no-owner`) ile yedeği geri yüklerken nesnelerin `OWNER TO ...` kısımlarını **atlayarak**, tüm nesnelerin sahibi olarak **geri yüklemeyi yapan kullanıcıyı** (yani `backup_sql`) atar.




# Monitor(İzleme):

+ PostgreSQL'de bağlı olan client'ları (istemcileri) görüntülemek için birkaç farklı yöntem bulunmaktadır:

## 1. `pg_stat_activity` View'ını Kullanma:

+ En yaygın yöntem, PostgreSQL'in sistem view'ı olan `pg_stat_activity`'i sorgulamaktır:

```sql
SELECT * FROM pg_catalog.pg_stat_activity;
```

+ Sadece belirli kolonları izlemsi yapabiliriz ve `\watch` komutu ile her 10 saniye de yenileyebiliriz.

```sql
SELECT pid, usename, application_name, client_addr, backend_start, state FROM pg_stat_activity;
\watch 10;
```

**Çıkıt:**

```sql
                                   19.05.2025 16:34:42 (every 10s)

 pid  | usename  |     application_name     |  client_addr  |         backend_start         | state
------+----------+--------------------------+---------------+-------------------------------+--------
  791 | postgres |                          |               | 2025-05-19 14:32:47.850275+03 |
  789 |          |                          |               | 2025-05-19 14:32:47.850608+03 |
 1725 | tanju    | psql                     | 192.168.1.131 | 2025-05-19 15:14:12.810436+03 | idle
 1816 | tanju    | psql                     | 192.168.1.106 | 2025-05-19 15:30:41.719104+03 | active
 2085 | tanju    | pgAdmin 4 - DB:tanju     | 192.168.1.106 | 2025-05-19 15:55:47.867567+03 | idle
 2115 | tanju    | pgAdmin 4 - CONN:4634385 | 192.168.1.106 | 2025-05-19 16:02:01.044917+03 | idle
  787 |          |                          |               | 2025-05-19 14:32:47.856069+03 |
  786 |          |                          |               | 2025-05-19 14:32:47.855332+03 |
  788 |          |                          |               | 2025-05-19 14:32:47.852791+03 |
(9 rows)
```

### `\watch` Komutu nedir?

+ `\watch` komutu, PostgreSQL'in komut satırı aracı olan `psql` içinde kullanılan çok kullanışlı bir meta-komuttur (backslash komutu).

#### Syntax:

```sql
\watch [saniye]
```

+ Bu komut, bir önceki SQL sorgusunun sonuçlarını belirtilen aralıklarla (varsayılan 2 saniye) otomatik olarak yeniler.
+ `5` parametresi verdiğinizde, sorgu sonuçlarını her 5 saniyede bir yenileyecektir.

#### Örnek 1: Temel Kullanımı

1. 1. Önce bir sorgu çalıştırın:

```sql
SELECT pid, usename, datname, state, query FROM pg_catalog.pg_stat_activity;
```

2. 2. Sonra bu sorgunun sonuçlarını izlemek için:

```sql
\watch 7;
```


> [!CAUTION]
> + 1. **Çıkış**: `Ctrl+C` ile izlemeyi durdurabilirsiniz.

# Veri Güncelleme(UPDATE):

+ PostgreSQL'de `UPDATE` komutu, bir tabloda **mevcut verileri güncellemek** (değiştirmek) için kullanılır.
+ Bu komutla bir veya birden fazla satırın belirli sütunlarındaki değerleri değiştirebilirsin.
## Syntax:

```sql
UPDATE tablo_adi
SET sütun1 = yeni_değer1,
    sütun2 = yeni_değer2,
    ...
WHERE koşul;
```

> + `tablo_adi`: Güncelleme yapmak istediğin tablonun adı.
> + `SET`: Güncellemek istediğin sütun ve yeni değeri.
> + `WHERE`: Hangi satır ya da satırların güncelleneceğini belirten koşul (çok önemlidir!).


> [!CAUTION]
> + `WHERE` ifadesi koymazsan **bütün satırlar** güncellenir.
> + `RETURNING` ile hangi verilerin değiştiğini görebilirsin.
> + Karmaşık güncellemelerde alt sorgular (subquery) da kullanılabilir.



> [!NOTE]
> + Aşağıdaki örneklerde kullanacağımız tablo:
> ```sql
> CREATE TABLE employee_data (
>	emp_id SERIAL PRIMARY KEY,
>	emp_name VARCHAR(100),
>	emp_place VARCHAR(255),
>	emp_age INTEGER,
>	emp_dob VARCHAR(255)
> );
> ```


> [!NOTE]
> **Ve onun verileri:**
> 1. Veri 
> ```sql
> INSERT INTO employee_data (
>	emp_name, emp_place, emp_age, emp_dob
> ) 
> VALUES (
>	'Ahmet', 'california', 25, '25/09/2000'
> );
> ```
> 2. Veri
> ```sql
> INSERT INTO employee_data (
>	emp_name, emp_place, emp_age, emp_dob) 
> VALUES (
>	'Melih', 'New York', 36, '25/09/1989'
> );
> ```
> 3. Veri
> ```sql
> INSERT INTO employee_data (
>	emp_name, emp_place, emp_age, emp_dob
> ) 
> VALUES (
>	'Oğuzhan', 'Utak', 20, '25/09/2003'
> );
> ```

## Örnek 1:

**Senaryo:** `employee_data` tablosundaki `Utak` kelimesini `Utah` olarak çevirmek isteniyor.

```sql
SELECT * FROM public.employee_data;
```

**SELECT Çıktısı:**

```sql
 emp_id |  emp_name  | emp_place  | emp_age |  emp_dob
--------+------------+------------+---------+------------
      1 | linus      | california |      25 | 25/09/2000
      2 | Arch Linux | New York   |      36 | 25/09/1989
      3 | Ubuntu     | Utak       |      20 | 25/09/2003
(3 rows)
```

**Veri Güncelleme:**

```sql
UPDATE employee_data SET emp_place = 'Utah' WHERE emp_id = 3;
```

**UPDATE Çıktısı:**

```sql
 emp_id |  emp_name  | emp_place  | emp_age |  emp_dob
--------+------------+------------+---------+------------
      1 | linus      | california |      25 | 25/09/2000
      2 | Arch Linux | New York   |      36 | 25/09/1989
      3 | Ubuntu     | Utah       |      20 | 25/09/2003
(3 rows)

```

## Örnek 2: `RETURNING *`

+ PostgreSQL'de `UPDATE` komutuyla birlikte `RETURNING` ifadesi kullanmak, yapılan güncellemenin sonucunu **hemen görmek** için çok faydalıdır.
+ Bu özellik, özellikle veritabanında neyin değiştiğini anında kontrol etmek istediğinde kullanılır.

```sql
SELECT * FROM public.employee_data;
```

**SELECT Çıktısı:**

```sql
 emp_id |  emp_name  | emp_place  | emp_age |  emp_dob
--------+------------+------------+---------+------------
      1 | linus      | california |      25 | 25/09/2000
      2 | Arch Linux | New York   |      36 | 25/09/1989
      3 | Ubuntu     | Utah       |      20 | 25/09/2003
(3 rows)

```

**Veri Güncelleme: RETURNING**

```sql
 UPDATE employee_data SET emp_place = 'California' WHERE emp_id = 1 RETURNING *;
```

**UPDATE Çıktısı:**

```sql
 emp_id | emp_name | emp_place  | emp_age |  emp_dob
--------+----------+------------+---------+------------
      1 | linus    | California |      25 | 25/09/2000
(1 row)


UPDATE 1
```

## Örnek 3: BETWEEN ve UPDATE

```sql

```

## Örnek 4: `UPDATE ... FROM (VALUES ...)`

**Amaç:** Aynı tabloda **birden fazla satırı**, **farklı değerlerle**, **tek bir sorguda** güncellemek.

**Öncesi:**

```sql
SELECT * FROM public.employee_data
```

**SQL Çıktısı:**

```shell
 emp_id | emp_name | emp_place  | emp_age |  emp_dob
--------+----------+------------+---------+------------
      1 | Ahmet    | california |      25 | 25/09/2000
      2 | Melih    | New York   |      36 | 25/09/1989
      3 | Oğuzhan  | Utak       |      20 | 25/09/2003
      4 | Mert Can | Tunceli    |      24 | 12/05/2001
      5 | Eyüphan  | New York   |      19 | 26/06/2006
      6 | Atilla   | California |      38 | 15/02/1987
      7 | Çetin    |            |      50 | 26/01/1975
      8 | Ali Riza |            |      48 | 07/07/1977
      9 | Umut     |            |      18 | 17/09/2006
(9 rows)

```

**UPDATE komutu:**

```sql
    UPDATE employee_data AS e_d
    SET
        emp_place = v.emp_place
    FROM (
        VALUES
            (7, 'Çorum'),
            (8, 'Sivas'),
            (9, 'Şanlıurfa')
    ) AS v(emp_id, emp_place)
    WHERE e_d.emp_id = v.emp_id
```


> [!NOTE]
> `VALUES (...)`  Bu satırlar aslında **küçük bir geçici tablo** gibi çalışıyor:
> ```text
> emp_id | emp_place
> -------+--------
>     7  | 'Çorum'
>     8  | 'Sivas'
>     9  | 'Şanlıurfa'
> ```


> [!NOTE]
> - `AS v(id, salary)` : Bu tabloya isim veriyoruz (`v`) ve sütun isimlerini tanımlıyoruz
> 	+ `emp_id` : eşleştirme için
> 	+ `emp_salary` : yeni değer
> - `UPDATE employees_data SET emp_place = v.emp_place`
> 	+ Gerçek tablodaki `emp_place` değerini, `v` tablosundaki yeni maaşla değiştiriyoruz.
> - `WHERE e_d.emp_id = v.emp_id`: eşleşmeyi `emp_id` değerine göre yapıyoruz. Yani:
> 	- `e_d.emp_id = 6` → `v.emp_place = 'Çorum'`
> 	-  `e_d.emp_id = 7` → `v.emp_place = 'Sivas'`
> 	- `e_d.emp_id = 8` → `v.emp_place = 'Şanlıurfa`



**Sonrası:**

```sql
SELECT * FROM public.employee_data
```

**SQL Çıktısı:**

```shell
 emp_id | emp_name | emp_place  | emp_age |  emp_dob
--------+----------+------------+---------+------------
      1 | Ahmet    | california |      25 | 25/09/2000
      2 | Melih    | New York   |      36 | 25/09/1989
      3 | Oğuzhan  | Utak       |      20 | 25/09/2003
      4 | Mert Can | Tunceli    |      24 | 12/05/2001
      5 | Eyüphan  | New York   |      19 | 26/06/2006
      6 | Atilla   | California |      38 | 15/02/1987
      7 | Çetin    | Çorum      |      50 | 26/01/1975
      8 | Ali Riza | Sivas      |      48 | 07/07/1977
      9 | Umut     | Şanlıurfa  |      18 | 17/09/2006
(9 rows)
```

