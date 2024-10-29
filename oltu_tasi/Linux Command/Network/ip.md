#linux_commands 

### Syntax:
+ **Usage:** `ip [ OPTIONS ] OBJECT { COMMAND | help }`

## Objects:
### link:
```shell
$ ip -color link
```
> **Explanation:**
> + Linux'ta `ip link` komutu, ağ arayüzlerini yönetmek ve incelemek için kullanılan bir komuttur.
> + Bu komut ile mevcut ağ arayüzlerinin durumlarını görebilir, arayüzleri etkinleştirebilir (up) veya devre dışı bırakabilir (down), MAC adreslerini değiştirebilir, MTU değerlerini (Maksimum İletim Birimi) ayarlayabilirsiniz.

#### link show:
```shell
$ ip -color link show
```
> **Explanation:**
> + Sistemdeki(host) tüm ağ arayüzlerini(interface) ve onların durumlarını gösterir.
> + **Tüm ağ arayüzlerini listelemek için kullanılır**

#### link set:
##### link set dev
```shell
$ ip link set dev eth0 up
```
> **Explanation:**
> - **Bir ağ ara yüzünü etkinleştirme için kullanılır.**
> - `eth0` adlı ağ arayüzünü(interface) etkinleştirir.

```shell
$ ip link set dev eth0 down
```
> **Explanation:**
> - **Bir ağ arayüzünü devre dışı bırakma için kullanılır**
> - `eth0` adlı ağ arayüzünü(interface) devre dışı bırakır.
