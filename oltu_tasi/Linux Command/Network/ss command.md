```
$ ss -ltuns
```
> **Explanation:**
> parametreler
> + -l, --listening  : Yanlızca dinlen soketleri göster
> + -t, --tcp : TCP soketlerini göster
> + -u, --udp: UDP soketlerini göster
> + -n, --numeric: servis adlarını çözümlemeye çalışma
> + -s, --summary: Özet istatistiği ekrana bas.

### ss:

###### -t parametresi:
```shell
$ ss -t
```
> **Explanation:**
> + `-t` parametresi  sadece TCP bağlantılarını listeler.

###### -l parametresi:
```shell
$ ss -t -l
```
> **Explanation:**
> + Hem TCP bağlantılarını(`-t`) hem de dinlenen portları(`-l`) ekrana yazar. Yani `-l` parametresi dinlenen portları verir. 
> + `-l` parametresini yalnız da kullanabilirsiniz.