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


## set komutu:
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

