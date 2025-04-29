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
## Panes

## Commands:


> [!NOTE]
> + tmux de komut moduna geçmemiz içine veya komut modunu aktif edebilmemiz için `Ctrl + B` ardından `:` tuşlarına basmamız gerekmektedir.

### set ve setw komutları:
#### synchronize-panes:
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

#### set ile setw arasındaki fark:

1. **Set:**
	+ 
2. **Setw:**
### Kaynaklar
+ [tmuxcheatsheet](https://tmuxcheatsheet.com/)
+ 