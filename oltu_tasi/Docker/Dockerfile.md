#docker 


### CMD(Command):
+ **Amaç**: Konteyner çalıştırıldığında varsayılan olarak çalıştırılacak komutu tanımlar.
+ **Esneklik**: `docker run` komutu ile konteyner çalıştırılırken CMD ile belirtilen komut, kullanıcı tarafından geçersiz kılınabilir.
+ **Kullanım Senaryosu**: Genellikle konteynerin temel işlevini tanımlamak için kullanılır ve esnekliği sayesinde farklı komutlar çalıştırmak istendiğinde idealdir.

```Dockerfile
FROM ubuntu:latest
CMD ["echo", "Merhaba Dünya"]
```

+ Bu Dockerfile ile oluşturulan imaj, konteyner çalıştırıldığında `echo "Merhaba Dünya"` komutunu varsayılan olarak çalıştırır. Ancak, kullanıcı `docker run` ile farklı bir komut belirtebilir:

```sh
$ docker run ubuntu_echo ls -la
```
> **Explanation:**
> + `ls -la` komutu `CMD ["echo", "Merhaba Dünya"]` komutunu ezer(overide).

```sh
$ docker ps -a
```
> **Explanation:**
> + Bu komut çıktısında  `COMMAND` sütüne bakarsanız orada container hangi komut ile çalıştırıldığını göreceksiniz.
> + `docker run --name sade_hali ubuntu_echo`  COMMAND Çıktı: `echo Merhaba Dünya`
> + `docker run --name ls_hali ubuntu_echo` COMMAND Çıkıt: `ls -la`

---
### ENTRYPOINT:

+ **Amaç**: Konteyner çalıştırıldığında asıl çalıştırılacak komutu tanımlar ve bu komut genellikle değiştirilemez.
+ **Sabitlik**: `docker run` komutu ile ek argümanlar verilebilir, ancak ENTRYPOINT tarafından tanımlanan komut değiştirilemez.
+ **Kullanım Senaryosu**: Konteynerin belirli bir uygulamayı veya işlemi gerçekleştirmesini kesinleştirmek istediğiniz durumlarda kullanılır.

```Dockerfile
FROM ubuntu:latest
ENTRYPOINT ["echo"]
```

+ Bu Dockerfile ile oluşturulan imaj, konteyner çalıştırıldığında `echo` komutunu çalıştırır. Kullanıcı ek argümanlar sağlayabilir:

```sh
$ docker run ubuntu_echo2 "Merhaba Dünya"
```
> **Explanation:**
> + Bu durumda, `echo "Merhaba Dünya"` komutu çalıştırılır.
> + `ENTRYPOINT` üzerine yazılamadığı(no overide) için sadece `echo` komutlarında uygun parametreler vermek zorundayız. 

```sh
$ docker ps -a
```
> **Explanation:**
> + Bu komut çıktısında  `COMMAND` sütüne bakarsanız orada container hangi komut ile çalıştırıldığını göreceksiniz.
> + `docker run --name echo_komut  ubuntu_echo2 "Merhaba Dünya"` COMMAND Çıktı: `echo Merhaba Dünya`  


##### ENTRYPOINT ve CMD Birlikte Kullanımı:
+ Hem `ENTRYPOINT` hem de `CMD` talimatlarını birlikte kullanarak esneklik ve belirli bir temel komut sağlamanın avantajlarından faydalanabilirsiniz.

```Dockerfile
FROM ubuntu:latest
ENTRYPOINT ["echo"]
CMD ["Linux is Awesome"]
```
> **Explanation:**
> + Eğer kullanıcı sadece `docker run --name komutsuz ubuntu_echo3` komutunu çalıştırırsa, `echo "Varsayılan Mesaj"` çalıştırılır.
> + Eğer kullanıcı `docker run --name komutlu ubuntu_echo3 "Windows is not Awesome"` derse, `echo "Windows is not Awesome"` çalıştırılır.

###### Özetle:
+ **CMD**: Konteynerin varsayılan komutunu belirtir ve kullanıcı tarafından değiştirilebilir.
+ **ENTRYPOINT**: Konteynerin çalıştıracağı temel komutu belirtir ve genellikle değiştirilmez, ancak argüman eklenebilir.
+ **Birlikte Kullanım**: ENTRYPOINT ile temel komut belirlenirken, CMD ile varsayılan argümanlar sağlanabilir.

---
### Apps ile Dockerfile:
###### Örnek: 1
Yıpılcak çalışma ama ingilizce [link](https://www.youtube.com/watch?v=0eMU23VyzR8)
###### Örnek: 2
