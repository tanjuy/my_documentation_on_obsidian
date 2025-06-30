#programlama


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






