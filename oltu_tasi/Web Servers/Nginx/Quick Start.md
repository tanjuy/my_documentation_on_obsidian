#nginx 

##### 1. Nginx Kurulumu:

> [!CAUTION]
> + *Nginx kurulum* ve *Config dosya ayarları* **Ubuntu 22.04** üzerinde gerçekleştirilmektedir.


```shell
$ sudo apt install nginx
```
> **Explanation:**
> + `apt` paket yöneticisi kullanılarak nginx kurulumu yapılıyoruz.
> + Alternatif kurulum için [[Nginx Config File#Nginx Kurulumu|Nginx Kuruluma]] bakınız.


> [!NOTE]
> + Nginx'in config dosyası `/etc/nginx` dizinde mevcuttur. 
> + Nginx'in log dosyları da `/var/log/nginx` dizininde mevcuttur.

##### 2. Durum Kontrolü
```shell
$ sudo systemctl status nginx.service
```
Veya

```shell
$ ps aux | grep nginx
```
> **Explanation:**
> + Nginx'in kurulup kurulmadığını ve düzgün çalışıp çalışmadığını kontrol edebilirsiniz.

##### 3. İstek Atma:
```shell
$ curl -i http://192.168.1.129/
```
> **Explanation:**
> + Kurmuş olduğumuz nginx sunucuya `curl`  ile `GET` isteği yapıyoruz.
> + Bu işlemi tarayıcının bar'ına yazılarak da yapılabilir.

##### 4. Log Dosyasından İzleme:
```shell
$ tail -f /var/log/nginx/*
```
> **Explanation:**
> + `tail` komut ve `-f` parametresi ile nginx'in log dosyalarını canlı bir şekilde izleyebiliyoruz.
> + `/var/log/nginx/` dizini altında `access.log` ve `error.log` adında iki dosya mevcuttur.
> + Yukarıda yaptığımız `GET` istekleri buradaki `access.log` dosyasına yazılacaktır.

**Tail Komut Çıktısı:**
```shell
==> /var/log/nginx/error.log <==
2024/10/06 19:27:09 [notice] 19962#19962: signal process started

==> /var/log/nginx/access.log <==
192.168.1.106 - - [06/Oct/2024:19:27:16 +0000] "GET / HTTP/1.1" 200 396 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:131.0) Gecko/20100101 Firefox/131.0"
192.168.1.106 - - [06/Oct/2024:19:27:44 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:131.0) Gecko/20100101 Firefox/131.0"
```

+ **error.log:** nginx servisini yeniden başlatıldığını söylemektedir. (`sudo nginx -s reload`)
+ **access.log:**  nginx servisine 2 `GET` isteğin yapıldığını *ilk olarak* nginx, 200 response code aldığını görünüyor. Çünkü ilk istek olduğu için. 
	+ *İkinci istekte* ise nginx, 304 response code alındığı görünmektedir. 
	+ Çünkü tarayıcı, nginx'in statik içerğini önbelleğe alındığını nginx bildirmiştir(**If-Modified-Since**) ve 
	+ nginx, statik içerikte değişiklik olup olmadığına bakmıştır(**Last-Modified**) sonuç olarak; istek de bir değişiklik olmadığıdır.(Kısa açıklama)






