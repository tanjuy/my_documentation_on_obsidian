#programlama

# Giriş:

## print fonksiyonu:
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

# String Veri Tipi:
+ String veri tipi ilkel bir tiptir ancak Python’da sınıf olarak tanımlandığı için metotlara sahiptir.

## String Dilimleme:
### Syntax:
```python
variable[index start: end of index: step]
```
> **Explanation:**
> + `index start`:  Dilimleme işleminin nereden başlayacağını gösterir.
> + `end of index`: Dilimleme işleminin nerede sonlanacağını gösterir.
> + `step`: Her adımda ne kadar ilerleyeceği

### 1.Tek index ile:
```python
#!/usr/bin/python3
message = "Linux is AWESOME"
print("1.index:", message[0])
print("2.index:", message[1])
```


## Tip Dönüşümü:
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

### title metodu:
```python
#!/usr/bin/python3
message = 'Linux is AWESOME'
titleMessage = message.title()
print("İlk mesaj:", message)
print("Yeni mesaj:", titleMessage)
```






