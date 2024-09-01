#linux_commands
### curl
```bash
$ curl -I http://192.168.1.125/assets/images/clients/c3.png
```
> **Explanation:**

### update-alternative
```shell
$ sudo update-alternative --config python
```
> **Explanation:**  ==ubuntu==, ==rocky linux==
> python versiyon arasında geçiş yapmamıza izin veriyor.

### openssl
```shell
$ openssl rand -base64 10
```

### shutdown
###### Örnek 1: +dakika
```shell
$ shutdown +10 "10 dakika sonra makine kapanacak"
```
> **Explanation:**
> Makineye uzaktan veya yerel(local) olarak bağlı olan terminal ekranlarına mesaj gönderiyoruz ve +10 anlamı, mesaj da söylendiği gibi 10 dakika sonra kapanacağıdır.

###### Örnek 2: -k parametresi (UYARI)
```shell
$ shutdown -k +5
```
> **Explanation:**
> `-k` parametresi makinenin kapatılmayacağı veya yeniden başlatılmayacağı ama bulunduğu zamandan 5 dakika sonra kapanacağını söylemektedir. Bir UYARI
> Uyarı mesaj tüm terminallere ulaşır.

```shell
$ shutdown -k 22:30:25
```
> **Explanation:**
> Yukarıdaki komut gibi çalışır ama burada belirlen zaman verilmiştir. Uyarı mesajı tüm terminaller 22:30:24 sadece kapanacağı uyarısı verir.

