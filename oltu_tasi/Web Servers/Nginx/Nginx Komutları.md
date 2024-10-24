#nginx 

#### Nginx Yardım:
```shell
$ sudo nginx -h
```

**Çıktı:**
```shell
nginx version: nginx/1.27.2
Usage: nginx [-?hvVtTq] [-s signal] [-p prefix]
             [-e filename] [-c filename] [-g directives]

Options:
  -?,-h         : this help
  -v            : show version and exit
  -V            : show version and configure options then exit
  -t            : test configuration and exit
  -T            : test configuration, dump it and exit
  -q            : suppress non-error messages during configuration testing
  -s signal     : send signal to a master process: stop, quit, reopen, reload
  -p prefix     : set prefix path (default: /usr/local/nginx/)
  -e filename   : set error log file (default: /var/log/nginx/error.log)
  -c filename   : set configuration file (default: /etc/nginx/nginx.conf)
  -g directives : set global directives out of configuration file
```


##### `nginx.conf` syntax kontrol:
```bash
$ sudo nginx -t 
```
> **Explanation:**


```bash
$ sudo nginx -s reload
```
> **Explanation:**
> + nginx servisini yeniden başlatıyoruz. `nginx.conf` dosyası düzenlendiğinde gerek duyulan komutur.

```
$ sudo systemctl restart nginx.service
```
> **Explanation:**
> + Yukarıdaki komut ile aynı işi yapar.


> [!WARNING]
> + `nginx -s reload` komut nginx SSL sertifikaları yeniledikten sonra bu komut düzgün çalışmamaktır.
> + Eğer SSL sertifikası yenilemesi yaptıktan sonra SSL sertifikların tekrardan yüklenmesi için nginx servisini başlatmak için `systemctl restart nginx.service` komutunu kullanınız.
