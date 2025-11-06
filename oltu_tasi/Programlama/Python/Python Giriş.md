#programlama #python


# Python Kullanım Alanları:

1. **Web Geliştirme:** Python, Django ve Flask gibi popüler web framework'leri ile web siteleri geliştimek için kullanılabilir.
2. **Otomansyon ve Betik Yazımı:** Python, tekrar eden görevleri otomatikleştirmek ve sistem üzerinde komut dosyalarını çalıştırmak için idealdir. Örneğin; dosya işlemleri, veri kazıma(`web scraping`), e-posta gönderimi gibi işlevler otomatikleştirilir.
3. **Matematiksel Hesaplamalar:** Pandas, Numpy, Matplotlib gibi kütüphaneler sayesinde veri setleri üzerinde kolayca analiz yapılabilir.
4. **Veri tabanı İşlemleri:** Python ile veritabanlarına(MySQL, PostgreSQL, SQLite gibi) bağlanabilir ve veri çekme, ekleme, güncelleme gibi işlemleri yapılabilir.
5. **API ile Entegrasyon:** Python, REST API'ler ile iletişim kurmak, veri çekmek ve veri göndermek için kullanılabilir.
6. **Görsel ve Grafikİşlemleri:** OpenCV, PIL(Pillow) gibi kütüphanelerle görsel işlemler yapılabilir. Görüntü analizleri, filtreleme ve grafiksel düzenlemeler mümkündür.
7. **Oyun Geliştirme:** Pygame gibi kütüphanelerle basit oyunlar geliştirebilirsiz.
8. **Yapay Zeka:** Doğal dil işleme, görüntü işleme, derin öğrenme gibi yapay zeka alanlarında python çok güçlüdür. Keras, PyTorch gibi kütüphaneler bu alanda sıkça kullanılır. 

# Giriş:


> [!CAUTION]
> +  Python kodları Linux ortamında yazılıp test edilmektedir. 


## İlk Kod:

```python
#!/usr/bin/python3

print("Python is so easy!");
```
> **Explanation:**
> + 

# Değişkenler:





# Yorum Satırları:
## Tek Satır Yorum(`#`):


# Koşul Durumları:



# Fonksiyonlar
### print fonksiyonu:
```python
#!/usr/bin/python3

print("Merhaba Dünya")
```
> `print` built-in bir fonksiyondur.

#### A. sep parametresi:
```python
#!/usr/bin/python3
print("Linux","Mac", "Windows", sep="-")
```

#### B. end parametresi:

```python
#!/usr/bin/python3
print("Python", end="")
print("Javascript", end="")
print("Java", end="")
```

### Type Fonksiyonu:

## Sınıflar:
### str:
+ Python'da `str` sınıfı, string (dize) veri tipini temsil eden bir sınıftır ve Python'da metinleri işlemek için kullanılır.
+ Bu sınıf, stringlerin nasıl saklanacağını ve bu stringlerle nasıl işlem yapılacağını belirler.
#### 1.Değiştirilemezlik (Immutable):
+ `str` sınıfının bir örneği(instance) oluşturulduktan sonra değiştirilemez.
+ Yani bir stringin içindeki karakterler doğrudan değiştirilemez. Yeni bir string elde etmek için, bir dönüşüm yapılması gerektiğinde yeni bir string yaratılır.
###### Örnek 1:
```python
lang = "Python"
lang[0] = "C"
```
> + Eğer `lang` değişkenindeki `P` harfini yani 0.indeksi `C` harfi ile değiştirmeye istersek hata verecektir. Çünkü string veri türleri bir kez belleğe yazıldıktan sonra değiştirilemez.

```python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

---

#### 2. Veri Türü Dönüştirme:
+ Diğer veri tiplerini string veri tipine dönüştürmek için kullanılır.

#### 3. String Metotları:
+ 


## Temel Veri Türleri:

### Değişken Tanımlama:


### İlker Veri Tipleri
#### 1.String Veri Tipi:

```python
#!/usr/bin/python3
isim = "Linux is Awesome"
print("String Değer:", isim)
```
> **Explanation:**
> + String türkçe karakter dizisi olarak geçmektedir.

#### 2.Sayı Veri Tipi:
##### 2.1. Integer:
```python
#!/usr/bin/python3
date = 1453
print("İstanbul'un fethi:", date)
```

##### 2.2. Float:
```python
#!/usr/bin/python3
PI = 3.14
print("Matematik PI sayısı:", PI)
```

#### 3. None:
```python
#!/usr/bin/python3
amount = None
print("Kalan Bakiye:", amount)
```

#### 4. Boolean:
```python
#!/usr/bin/python3
married = True
print("Evli mi:", married)
```

## İlker Veri Tipi Olmayanlar:
### Liste Veri Tipi:
```python
#!/usr/bin/python3
personal_data = ["Mehmet", 35, 1.70, False]
```

### Tuple Veri Tipi:
```python
#!/usr/bin/python3
student_data = ("Ayşe", 83, 45.3, True)
```

### Dictionary Veri Tipi:
```python
#!/usr/bin/python3
tr_en = {
		 "Programming": "Programlama",
		 "Language": "Dil",
		 "Data" : "Veri"
}
```

### Set Veri Tipi:
```python
#!/usr/bin/python3
fruitBasket = {'elma', 'armut', 'kiraz', 'çilek'}
```


# Fonksiyon Tanımlama:


# String Veri Tipi:
+ Python'da _string_ (dize) verisi, bir metni veya karakterler dizisini temsil eder ve genellikle metinsel veri depolamak için kullanılır.
+ Stringler, tırnak işaretleri (tek `'...'` veya çift `"... "`) içinde tanımlanır.
+ Python’da stringler değiştirilemez (immutable) veri tiplerindendir; yani, bir kez oluşturulduktan sonra içindeki karakterler değiştirilemez.

#### 1.İndeksleme:

```python
#!/usr/bin/python3
message = "Linux is AWESOME"
print("1.index:", message[0])         # Çıktı: 'L'
print("2.index:", message[1])         # Çıktı: 'i'
```

#### 2.String Dilimleme:
##### Syntax:
```python
variable[index start: end of index: step]
```
> **Explanation:**
> + `index start`:  Dilimleme işleminin nereden başlayacağını gösterir.
> + `end of index`: Dilimleme işleminin nerede sonlanacağını gösterir.
> + `step`: Her adımda ne kadar ilerleyeceği
##### Temel Kullanım:
```python
#!/usr/bin/python3
message = "Linux is AWESOME"
print("index 0 ile 5 arasındaki:", message[0:5])
```
> **Explanation:**
> + 

#### 3.Tip Dönüşümü:
+ Bazı verileri string veri tipine dönüştürme işlemi yapabiliriz.

```python
#!/usr/bin/python3
date = 1453
print('Değişken:', date,' - ','Veri Tipi:', type(date))
strDate = str(date)
print('String Değişken:', strDate,' - ' ,'Veri Tipi:', type(strDate))
print('Son Karakter:', strDate[-1])
```


## String Metodlerı:
+ String veri tipi ilkel bir tiptir ancak Python’da sınıf olarak tanımlandığı için metotlara sahiptir.

### title metodu:
```python
#!/usr/bin/python3
message = 'Linux is AWESOME'
titleMessage = message.title()
print("İlk mesaj:", message)
print("Yeni mesaj:", titleMessage)
```








# `with ... as ...` Kullanımı:

+ Python’daki `with ... as ...` yapısı aslında **context manager** (bağlam yöneticisi) kullanımına dayanır.

## 📌 Amaç:

+ `with ... as ...` ifadesi, bir kaynağı (dosya, bağlantı, kilit, vb.) **açıp kapatma** işlemlerini otomatikleştirmek için kullanılır.
+ Normalde manuel olarak `open()` ile dosya açıp sonra `close()` çağırmanız gerekir. `with` ise bu işi otomatik yapar.

## Syntax:

```python
with expression as variable:
    # bu blok içinde variable kullanılabilir
    # blok bitince kaynak otomatik kapanır
```

## Örnek 1: Dosya

**with_as_key.py**

```python
with open("deneme.txt", 'w') as f:
	f.write("Merhaba Python!\n")
```

> + `open("deneme.txt", "w")` → bir dosya açar.
> + `as f` → açılan dosya nesnesini `f` isimli değişkene atar.
> + `with` → blok bittiğinde (`:` ile başlayan bölüm), dosyayı **otomatik olarak kapatır** (`f.close()` çağrılır).


> [!NOTE]
> 1. Kaynağın **otomatik kapatılmasını** sağlar.
> 2. Daha **temiz ve güvenli kod** yazılır.
> 3. Hata olsa bile (örneğin yazarken exception oluşsa bile), `with` bloğundan çıkınca dosya kapanır.

## Örnek 2: email

+ `with ... as ...` yapısı **`smtplib.SMTP()`** ile de sık kullanılır çünkü **bağlantıyı açıp kapatma işini** otomatik hale getirir.

```python
import smtplib

sender = "kullanici@gmail.com"
reciever = "alici@gmail.com"
message = "Merhaba Python!"

server = smtplib.SMTP("smtp.gmail.com", 587)
server.starttls()
server.login(sender, "App passwords şifresi")
server.sendmail(sender, reciever, message)
server.quit()  # 🔴 önemli, yoksa bağlantı açık kalır
```

> + Burada `server.quit()` çağırmazsan, SMTP oturumu açık kalır. Hata veya istisna olursa `quit()` hiç çalışmayabilir.

---

```python
import smtplib

sender = "kullanici@gmail.com"
reciever = "alici@gmail.com"
message = "Merhaba Python!"

with smtplib.SMTP("smtp.gmail.com", 587) as server:
    server.starttls()
    server.login(sender, "App passwords şifresi")
    server.sendmail(sender, reciever, message)
# ✅ Burada blok bitince server.quit() otomatik çağrılır
```

## Örnek 3: with ve hata




> [!NOTE]
> + **⚙️Arka Planı:** Eğer `with...as...` kullanımın arka mekanizmasını nasıl çalıştığını merak ediyorsanız, `__enter__` ve `__exit__` dunder metotları bakınız. 
> + Konu `Dunder Metoları` bağlığı altında `2. __enter__` ve `__exit__` metotları alt başlığı da anlatılmıştır. 


# Dunder Metodları:

## 1. `__setitem__` metodu:


## 2. `__enter__` ve `__exit__` metotları:

+ Python’daki `__enter__` ve `__exit__` dunder (veya magic) metotları **context manager** denilen yapının temel taşlarıdır.
+ Yani `with` ifadesini kullandığımızda aslında arka planda bu iki metot çalışır.
+ **`__enter__`**: `with` bloğuna girerken çalışan metottur. Genellikle bir kaynak (dosya, veritabanı bağlantısı, socket vs.) açma/başlatma işlemi yapar.
+ **`__exit__`**: `with` bloğundan çıkarken çalışan metottur. Kaynağı güvenli bir şekilde kapatma/temizleme işlemi yapar.

### Örnek 1:

**dunder_methods.py**

```python
class Deneme:
    def __enter__(self):
        print("Block başlıyor...")
        return "Merhaba"
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Block bitiyor...")


with Deneme() as mesaj:
    print(mesaj)
```

```shell
python3 dunder_methods.py
```

**Çıktı:**

```python
Block başlıyor...
Merhaba
Block bitiyor...
```

### Örnek 2:

```python

```

# env oluşturma:

+ Python’da **env** (environment → sanal ortam) oluşturmak, projeni diğer projelerden izole etmek için kullanılır.
+ Böylece her proje kendi bağımlılıklarına sahip olur ve karışıklık çıkmaz.
+ Bunu yapmak için en sık kullanılan yöntem `venv` modülüdür.

## venv:

### 1. Sanal Ortam (env) Oluşturma:

+ Terminal veya PowerShell’den proje klasörüne girip şu komutu çalıştırabilirsin:

> [!CAUTION]
> + Ubuntu işletim sisteminde `venv` modülü kullanabilmek için;
> ```shell
> sudo apt install python3.12-venv
> ```
> + komut kullanarak `python3.13-venv` paketini yükleyniz.

**Linux Bash:**

```shell
python3 -m venv .venv
```

**Powershell:**

```powershell
py.exe -m venv .venv
```

> + `python` veya  `py.exe` → kullandığın Python sürümünü çağırır.
> + `-m venv` → `.venv` modülü ile sanal ortam oluşturur.
> + `.venv` → oluşturulacak klasörün adı (istediğin ismi verebilirsin, genelde `env` veya `venv` denir).
> + Bu komut çalışınca proje dizininde `venv/` adında bir klasör oluşur.
### 2. Ortamı Aktifleştirme:

+ **Windows (PowerShell)**:

```powershell
.\.venv\Scripts\Activate.ps1
```

+ **Windows (CMD)**:

```cmd
.venv\Scripts\activate.bat
```

+ **Linux / macOS**:

```shell
source .venv/bin/activate
```

> Aktifleştirildiğinde terminalde `(venv)` gibi bir ibare görürsün. Bu, sanal ortamda olduğun anlamına gelir.

### 3. Ortamı Pasifleştirme:

+ `venv` ortamından çıkış yapmak için;

```shell
deactivate
```

### 4. Paket Kurma:

+ Sanal ortam aktifken kurduğun paketler sadece bu ortama kurulur:

```shell
pip install requests flask
```

### 5. requirements.txt

+ Projendeki mevcut paketleri kaydetmek için:

```shell
pip freeze > requirements.txt
```

+ Dosyanın içeriği şöyle görünür (örnek):

```shell
Flask==3.0.0
requests==2.31.0
```

### 6. Başka yerde aynı ortamı kur:

Başka bir bilgisayara geçtiğinde veya ortamı sildiğinde, tekrar oluşturabilirsin:
1. Yeni sanal ortam oluştur:
	
```shell
python3 -m venv venv
```
	
2. Ortamı aktif et.

```shell
source .venv/bin/activate
```

3. Tüm paketleri yükle:

```shell
pip install -r requirements.txt
```

> + ✅ Bu şekilde her proje izole olur ve bağımlılıklar karışmaz.
