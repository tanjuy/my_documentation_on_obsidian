# Komut Modu

## Tuş Kombinasyonları
##### Silme:
1. `d^` : İmlecin bulunduğu noktadan en başına kadar siler.
2. `d$`: İmlecin bulunduğu noktadan en sonuna kadar siler.
3. `dd`: İmlecin bulunduğu tüm satırı siler.

##### Kopyalama:
1. `yy` : 

### HTML için Tuş Kombinasyonları:

#### 1. `dit` tuş kombinasyonu:

+ **d**: delete (sil)
+ **i**: inner (içindeki)
+ **t**: tag (HTML/XML etiketi)
+ Yani `"dit"` kombinasyonu, imlecin bulunduğu yerdeki **HTML veya XML etiketinin içeriğini siler**, ancak etiketin kendisini silmez.

```html
<p>Merhaba dünya!</p>
```

> **Explanation:**
> + Diyelim ki elinde şu satır var ve imleç `<p>` etiketi içindeyken:

```html
<p></p>
```

> **Explanation:**
> + Yani `<p>` ve `</p>` yerinde durur, sadece içeriği silinir.

#### 2. `dat` tuş kombinasyonu:

#### 3. `zfat` veya `zfit` tuş kombinasyonu:

+ İki etiket arasını kapatır 
+ `za`: iki etiketi acar.

## set komutu:

### set paste
###### Örnek 1: clipboard'dan vim'e kopyalama
```vim
:set paste 
```
> **Explanation:**
> 1. yapıştırma modu (paste mode) özelliğini etkinleştirir.
> 2. Bu mod, dışarıdan (örneğin, başka bir metin belgesinden veya web tarayıcısından) Vim'e içerik yapıştırırken, Vim'in otomatik biçimlendirme ve girinti (indentation) gibi işlemlerini devre dışı bırakır.
> 3. **Devre dışı bırakma:**   `set nopaste`
> 4. **Neden Kullanılır:**
> 	- Normalde Vim, yazarken otomatik olarak girintileri ve biçimlendirme kurallarını uygular.
> 	- Ancak dışarıdan bir şey yapıştırırken bu otomatik girintiler ve formatlama bozulmalara yol açabilir.
> 	- `:set paste` komutunu kullanarak, bu otomatik işlemleri devre dışı bırakarak, yapıştırdığınız metnin orijinal biçimini korumasını sağlayabilirsiniz.


### set cursorline:

```vim
:set cursorline
```
> **Explanation:**
> + 

### set laststatus

+ Vim'de ekranın alt kısmında bir **durum satırı (status line)** vardır.
+ Bu satırda genellikle açık olan dosyanın adı, değişiklik durumu, satır/kolon bilgisi gibi bilgiler yer alır.

```vim
:set laststatus
```


> [!NOTE]
> Bu ayar:
> - `0`: Hiçbir zaman gösterme
> - `1`: Eğer birden fazla pencere (window) varsa göster
> - `2`: Her zaman göster





### set mouse

+ Vim’de **mouse** (fare) desteğini aktif etmek oldukça kolaydır ve hem normal modda hem de visual, insert, command modlarda **tıklama**, **seçme**, **scroll** gibi işlemleri yapmanı sağlar.

#### Tüm Modlar için:

```vim
:set mouse=a
```

# fold ve unfold:

+ Fold, belirli bir satır aralığını **gizlenebilir bir blok** haline getirir. Bu bloklar daraltılabilir (fold) veya genişletilebilir (unfold).

## Tuş Kombinasyonu ile

| Komut | Açıklama                                   |
| ----- | ------------------------------------------ |
| `zc`  | Fold'u kapat (collapse)                    |
| `zo`  | Fold'u aç (open)                           |
| `za`  | Açık ise kapatır, kapalı ise açar (toggle) |
| `zM`  | Tüm fold’ları kapat                        |
| `zR`  | Tüm fold’ları aç                           |
| `zd`  | Fold’u sil (disable)                       |
| `zE`  | Tüm fold’ları sil                          |
## Komut ile

### Örnek 1: Marker yöntemi

+ Dosyaya şöyle bir şey yazınız:

```python
# {{{ Başlangıç
def foo():
    pass
# }}}
```


```vim
:set foldmethod=marker
```

> **Tuş kombinasyonu:**
> + `zf` veya `zc` :  `# {{{` ile başlayan ve `# }}}` ile sonlana ara ifadeleri kapatacaktır.
> + `zo` : `# {{{` ile başlayan ve `# }}}` ile sonlana ara ifadeleri açacaktır.


# 2. Tabpage:
+ Vim, aynı anda birden fazla dosyayla çalışmanı sağlar. Bunu yapmanın birkaç farklı yolu vardır:
	-  **Buffer**: Arka planda açık olan dosyalar.
	- **Window**: Ekranı yatay veya dikey böler.
	- **Tab Page (Sekme)**: Tam ekran bölünmesini ayrı ayrı düzenleyebileceğin farklı sayfalar.


> [!TIP]
> + Vim'in yardım sayfasında ulaşmak için;
> ```vim
> :help tagpage
> ```

## 2.1. Komut:

### Örnek 1:

+ Yeni boş sekme (tab) açar.

```vim
:tabnew
```

### Örnek 2:

+ Eğer `python.py` dosyası var ise dosyayı açar aksi taktirde `python.py` dosyası oluşturur.

```vim
:tabnew python.py
```

### Örnek 3: sekme kapatma

+ Aktif sekmeyi kapatır.

```vim
:tabclose
```

## 2.2. Tuş Kombinasyonu:

+ Tab'lar arasında gezinmek için `gt` veya `gt` tuşlarına sırası ile basılır.
+ `g` tuş anlamı `go` ve `t` tuş anlamı `tab` 


| Tuş Kombinasyonu |       Açıklama        |
| :--------------: | :-------------------: |
|       `gt`       | Bir sonraki tab'a geç |
|       `gT`       | Bir önceki tab'a geç  |
|      `2gt`       | 2. sıradaki tab'a geç |
|                  |                       |


# 3. Windows:

## 3.1. vsplit:

## 3.2. split:

# Metinde Düzenleme:

## A. substitute:

### A.1. Yardım Sayfası:

+ Vim'de **substitutions** konusu, resmi dokümantasyonda **":substitute"** komutu altında geçer ve **komut modunda (command-line mode)** kullanılan bir metin düzenleme komutu olarak adlandırılır.


> [!NOTE]
> + Vim terminolojisinde **substitution** işlemi:
> 	- **"Ex command"** (ya da **Ex mode command**) olarak geçer.
> 	- Tam adıyla **`:substitute` komutu** olarak tanımlanır.
> + Komut satırında `:s` kısa adıyla kullanılır. Bu, `:substitute`'ün kısaltmasıdır.


```vim
:help :substitute
```

# change.txt:

## 4. Complex changes

### 4.1. Substitute

#### Syntax:

```vim
:[range]s[ubstitute]/{pattern}/{string}/[flags] [count]
```

> + `:` → Komut moduna geç.
> + `[range]` → Hangi satırlar üzerinde işlem yapılacağı.
> + 