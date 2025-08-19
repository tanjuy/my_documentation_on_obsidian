## Sessions
### Tmux Dışında:

```shell
$ tmux
```
> **Explanation:**
> Terminal ekranına sadece `tmux` yazarsak varsayılan değerler ile açılacaktır.


```shell
$ tmux new -s nginx -c /etc/nginx
```

### Tmux İçerisinde:

- `tmux` içerisinde iken `Ctrl + b` tuş kombinasyonuna basın ve ardından `:` (iki nokta üst üste) tuşuna basarak komut satırı moduna geçin.

```tmux
: new -s nginx -c /etc/nginx
```

> **Explanation:**
> + `-s nginx` : nginx adında yeni bir session açar.
> + `-c /etc/nginx` : nginx session'ın varsayılan dizini `/etc/nginx` olacaktır.

#### Session Adını Değiştirme:

+ `Ctrl` + `b`  daha sonrasında `$`  tuş kombinasyonu

veya

+ `Ctrl` + `b`  daha sonrasında `:`

```tmux
: rename-session [-t current-name] [new-name]
```

## Windows

## Pencere Taşıma:

+ Tmux'ta pencereleri (windows) taşımak için aşağıdaki yöntemleri kullanabilirsiniz:

## Panes

# Commands:


> [!NOTE]
> + tmux de komut moduna geçmemiz içine veya komut modunu aktif edebilmemiz için `Ctrl + B` ardından `:` tuşlarına basmamız gerekmektedir.




## A. Window Komutları:
### A.1. new-window Komutu:

+ `tmux`'ta `new-window` komutu, yeni bir pencere (window) oluşturmak için kullanılır.
+ `new-window`, tmux oturumu içinde yeni bir pencere açar.
+ Her pencere kendi içinde bir terminal gibi çalışır ve içinde bir veya daha fazla "pane" olabilir.

#### 🧪 Örnek 1: Temel Kullanım

```shell
tmux new-window
```

> +  Bu komut, geçerli tmux oturumuna yeni bir pencere ekler.

#### 🧪 Örnek 2: Pencereye isim verme(`-n`)

```shell
tmux new-window -n myWindow
```

> + `-n mywin`: Pencereye özel bir isim verir. Boş bir terminal ekrana gelir.

#### 🧪 Örnek 3: Pencereyi program ile açma

```shell
tmux new-window -n myWindow 'htop'
```

> + `-n mywin`: Pencereye özel bir isim verir.
> + `'htop'`: Yeni pencerede otomatik olarak `htop` komutu çalıştırılır.

#### 🧪 Örnek 4: Pencereyi belirli dizine açma

```shell
tmux new-window -c /var/www/html
```

> + `-c /path/to/dir`: Yeni pencereyi belirtilen dizinde başlatır.


> [!NOTE]
> + Tmux içinde çalışırken şu kısayolla yeni pencere açabilirsin:
> ```css
> Ctrl + b, ardından c
> ```
> + (c, create window anlamında)

### A.2. list-windows Komutu:

#### 🧪 Örnek 1:

```shell
tmux list-windows
```

**Çıktı:**

```shell
0: zsh (1 panes) [156x48] [layout e795,156x48,0,0,45] @25
1: zsh- (1 panes) [156x48] [layout e796,156x48,0,0,46] @26
2: myWindow* (1 panes) [156x48] [layout 6791,156x48,0,0,50] @30 (active)
```

### A.3. select-window Komutu:


### A.4. rename-window Komutu:


## B. Session Komutları:
### B.1. new-session Komutu:

## C. Send-keys Komtu:

### 🧪 Örnek 3:

```shell
tmux send-keys -t mySession:0.1 'htop' C-m
```

> + Buradaki `:0.1` kısmı, tmux içinde **hedef pencere(window) ve panel (pane)** konumunu ifade eder.
> + `C-m` : klavyedeki `Enter` tuşuna karşılık gelir.

> [!NOTE]
> **`tmux -t` parametresi:**
> - `-t` = "target" yani hedef oturum/pencere/panel belirtilir.
> ```less
> [session]:[window].[pane]
> ```


> [!NOTE]
> **Örnek:**
> ```shell
> mySession:0.1
> ```
> + `mySession` :  Oturumun (session) adı
> + `0` : Pencere numarası — burada ilk pencere (0. pencere)
> + `1` : Panel (pane) numarası — burada pencerenin ikinci paneli
> +  Yani bu ifade: `mySession` adlı oturumda, **0. penceredeki 1. paneli** hedef alır.




## D. Set-option Komutu:

+ `set-option`, tmux içinde **ayarları değiştirmek** için kullanılır.
+ Bu ayar; durum çubuğunun rengi, pencere isimlendirme şekli, tuş atamaları gibi birçok özelliği kapsar.

### Syntax: 

```shell
set-option [-g] <seçenek> <değer>
```

> + `-g`: (Global) Tüm oturumlar için geçerlidir. Yazılmazsa sadece aktif oturuma uygulanır.
> + `<seçenek>`: Değiştirmek istediğin ayarın adıdır. (örnek: `status`, `mouse`, `status-position`, `prefix`...)
> + `<değer>`: Ayara atamak istediğin değerdir. (örnek: `on`, `top`, `C-a`...)

### 🧪 Örnek 1: Durum Çubuğunu Konumu

```shell
tmux set-option -g status-position top
```

> + `set-option`: tmux yapılandırmasında bir ayarı değiştirmek için kullanılır.
> + `-g`: "global" yani **tüm oturumlar (sessions)** için geçerli olduğunu belirtir.
> + `status-position`: Bu, tmux durum çubuğunun ekranın **üstünde mi yoksa altında mı** gösterileceğini belirleyen bir ayardır.
> + `top`: Durum çubuğu ekranın **üst kısmında** yer alacak şekilde ayarlanır.


> [!TIP]
> + Varsayılan olarak `tmux` durum çubuğunu **altta** (`bottom`) gösterir.
> + Eğer bu satır `.tmux.conf` dosyanıza eklerseniz, tmux açıldığında çubuğu yukarıda görürsünüz.
> ```conf
> set-option -g status-position top
> ```
> + Sonra tmux'u yeniden başlatarak veya aşağıdaki komutla yapılandırmayı yeniden yükleyerek aktif hale getirebilirsin:
> ```conf
> tmux source-file ~/.tmux .conf
> ```


> [!TIP]
> + İstersen aynı ayarı geçici olarak (sadece o tmux oturumu için) aşağıdaki komutla da verebilirsin:
> ```shell
> tmux set-option status-position top
> ```
> + Yani, `-g` yerine yazılmazsa sadece aktif oturuma uygulanır.



> [!NOTE]
> + Eğer durum çubuğunu aşağı almak isterseniz:
> ```shell
> set-option -g status-position bottom
> ```
> + Varsayılan olarak durum çubuğu aşağıdadır. Eğer yukarıdaki komutu çalıştırmazsanız da durmu çubuğu aşağıda olacaktır.  




### 🧪 Örnek 2: Vi Modunu Aktif Etmek

```shell
tmux set-option -g mode-keys vi
```

### `repeat-time`

+ `tmux` oturumlarında `prefix` tuş kombinasyonu (varsayılan olarak `Ctrl + b`) sonrasında bir komut girene kadar geçen süreyi değiştirmek için `repeat-time` ayarını kullanabilirsiniz.
+ Bu süre, `prefix` tuşuna bastıktan sonra tmux'un bir sonraki tuş girişini bekleme süresini belirler.


> [!NOTE]
> + Eğer `prefix` (örneğin `Ctrl + b`) sonrasında daha uzun süre beklemek istiyorsanız, bu değeri artırabilirsiniz.
> + Ancak çok yüksek değerler kullanıcı deneyimini yavaşlatabilir.


> [!CAUTION]
> + Bu ayar, `prefix` tuş kombinasyonu sonrasındaki bekleme süresini etkiler, ancak `tmux` içindeki diğer tuş kombinasyonlarının tepkime süresini değiştirmez.

#### Syntax:

+ **Geçici olarak değiştirmek** (mevcut oturumda geçerli):

```tmux
tmux set-option -g repeat-time <süre_ms>
```

> + `repeat-time`: Varsayılan değer genellikle `500` ms'dir (0.5 saniye).
> + `<süre_ms>`: Milisaniye cinsinden süre (örneğin, `1000` = 1 saniye).
> + `-g`: Bu ayarı tüm tmux oturumlarında global olarak uygular.

#### 🧪Örnek 1: 

```tmux
tmux set-option -g repeat-time 1000
```

> + 1000 ms (1 saniye) yapmak için:


> [!TIP]
> + **Kalıcı olarak değiştirmek** (`~/.tmux.conf` dosyasına ekleyin):
> ```tmux
>  set-option -g repeat-time 1000
> ```
> + Değişikliği uygulamak için:
> ```shell
> tmux source-file ~/.tmux.conf
> ```



## E. set ve setw komutları:
### synchronize-panes:
+ Tmux'ta bir pencerede yazdığınızın diğer pencerelere de yansımasını sağlamak için **synchronize-panes (panelleri senkronize etme)** özelliğini kullanabilirsiniz.
+ Bu özellik, bir window içindeki tüm panellerin aynı komutları almasını sağlar.

```tmux
set synchronize-panes on
```

> **Explanation:**
> 1. Bir pencerede birkaç panel oluşturmak için; `Ctrl-b %`: Dikey bölme ve `Ctrl-b "`: Yatay bölme oluşturunuz.
> 2. Panelleri senkronize etmek için; *Komut Modunu Aç*: `Ctrl-b :` ve yukarıdaki komutu giriniz.

```tmux
set synchronize-panes off
```

> **Explanation:**
> + Komut moduna girmek için `Ctrl-b :` ve daha sonrasında bu komutu girebilirsiniz.

```tmux
show-options -w
```

> **Explanation:**
> + Senkronizasyonun açık olup olmadığını anlamak için girilecek komut
> + `Ctrl-b :` ardından bu komut yazıyoruz.

### set ile setw arasındaki fark:

1. **Set:**
	+ 
2. **Setw:**

# Otomatik Oturum Başlatma:

## 🧪 Örnek 1:

```sh
#!/usr/bin/env bash

SESSION='PHP1'

# Eğer oturum(session) zaten varsa, ona bağlan
tmux has-session -t $SESSION 2>/dev/null
if [ $? -eq 0 ]; then
        tmux attach -t $SESSION
        exit 0
fi

# Yeni bir tmux oturumu başlat(arka planda)
tmux new-session -d -s $SESSION -c \
        '/var/www/html/connectPostgreSQL' -n 'PDO'

# 1. pencere: vim aç
tmux send-keys -t $SESSION:0 \
        'sudo vim -p connect_postgres1.php  prepare.php' C-m

# Aynı pencere dikey böl
tmux split-window -h -t $SESSION


# Yeni pencere: basicPHP
tmux new-window -t $SESSION -c \
        '/home/ottoman/phpDerleri' -n basicPHP

# 2. pencere: vim aç
tmux send-keys -t $SESSION:1 'vim callByValueReference.php' C-m

# 2. pencereyi horzantal olarak ikiye böl
tmux split-window -h -t $SESSION:1 -c '/home/ottoman/phpDerleri'

# Mouse etkileşimini aktif etmek
tmux set mouse on

# Yukarıdaki kodlar ile oluşturulan PHP session'a bağlnıyoruz:
tmux attach -t $SESSION
```


# Tmux Config:


> [!NOTE]
> Tmux başlatıldığında **sadece aşağıdaki yolları** kontrol eder:
> 1. **Kullanıcı yapılandırması:**
> 	+ `~/.tmux.conf` ✅
> 	+ Bu kullanıcıya özel ayar dosyasıdır. Varsa bu dosya yüklenir.
> 2. **Sistem genelindeki ayar:**
> 	+ `/etc/tmux.conf`
> 	+ Tüm kullanıcılar için geçerli sistem yapılandırmasıdır.



> [!TIP]
> + apılandırma dosyasını kaydettikten sonra tmux’u yeniden başlatmak yerine şu komutu çalıştırarak ayarları yeniden yükleyebilirsin:
> ```shell
> tmux source-file ~/.tmux.conf
> ```


```tmux
set-option -g status-position top
set -g mouse on
```
# Tmux Eklentileri(Plug-in):

## TPM (Tmux Plugin Manager):

+ Tmux’ta plugin eklemenin **en yaygın ve kolay yolu**, [TPM (Tmux Plugin Manager)](https://github.com/tmux-plugins/tpm)'i kullanmaktır.

### 1. TPM'yi Kur:

+ TPM, tmux için bir plugin yöneticisidir. Plugin’leri kurmak, güncellemek ve silmek için kullanılır.

```shell
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### 2. 🧰 `.tmux.conf` Dosyasını Ayarla:

+ Ev dizininde (genellikle `~/.tmux.conf`) şu satırları ekle:

```tmux
# TPM'yi yükle
set -g @plugin 'tmux-plugins/tpm'

# Örnek olarak bazı plugin’ler:
set -g @plugin 'tmux-plugins/tmux-sensible'     # Kullanışlı varsayılan ayarlar
set -g @plugin 'tmux-plugins/tmux-resurrect'    # Oturumları kaydet ve geri yükle

# TPM'yi çalıştır (her zaman en sonda olmalı)
run '~/.tmux/plugins/tpm/tpm'
```

### 🔄  3. Tmux’u Yeniden Başlat veya Yapılandırmayı Yeniden Yükle:

+ Tmux'u baştan başlat ya da config'i yeniden yükle:

```shell
tmux source-file ~/.tmux.conf
```

veya

+ Ctrl+b` tuşlayıp ardından `:` yaz, sonra şu komutu gir:

```shell
:source-file ~/.tmux.conf
```

### ⬇️ 4. Plugin’i Kur:

+ Tmux içinde şu tuş kombinasyonunu kullan:
+ **Ctrl + b  ardından  I  (büyük i)**
+ Bu, `.tmux.conf` dosyasındaki tüm `@plugin` satırlarını okur ve gerekli dosyaları indirir.



> [!NOTE]
> **Plugin Başarıyla Yüklendi mi?**
> + Örneğin `tmux-resurrect` yüklediysen şu komutları deneyebilirsin:
> 	- Oturumu kaydet: `Ctrl + b` ardından `Ctrl + s`
> 	- Oturumu geri yükle: `Ctrl + b` ardından `Ctrl + r`


### Kaynaklar
+ [tmuxcheatsheet](https://tmuxcheatsheet.com/)
+ 