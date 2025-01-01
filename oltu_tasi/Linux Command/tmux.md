## Sessions
```shell
$ tmux
```
> **Explanation:**
> Terminal ekranına sadece `tmux` yazarsak varsayılan değerler ile açılacaktır.

```shell
$ 
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