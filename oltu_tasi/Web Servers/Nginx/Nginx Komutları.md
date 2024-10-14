#nginx 
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
