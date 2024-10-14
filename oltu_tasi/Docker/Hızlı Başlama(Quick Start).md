#docker 

#### 1. Contianer oluşturma:

```
$ docker run hello-world
```
> **Explanation:**
> + `hello-world` imajından bir container oluşturur.
> + container'a isim vermek isterseniz `run --name containerName` komutunu kullanabilirsiniz.

> [!CAUTION]
> Docker  da container içersindeki süreç(process) kapandığında veya durduğunda container'da sonlarınır veya kapanır.
> Container'ların ömrü, container'ınların içerisinde çalışan süreç(process) kadardır.

#### 2. Container'ları Listeleme:

```shell
$ docker ps 
```
> **Explanation:**
> + Makine Üzerinde yani host üzerinde çalışan container'ları ekrana basar.

```shell
$ docker ps -a
```
> **Explanation:**
> + Hem çalışan hem de durdurulan container'ları listeler.

#### 3. Container Kaldırma:

```shell
$ docker rm hello-world
```
> **Explanation:**
> + `hello-world` adındaki container'ı kaldırıyoruz.
> + **UYARI:** `hello-world` container'ın durdurulmuş olması gerekir.

#### 4. Çalışan Container Üzerinde İşlem(`docker exec`) :
###### 1. Komut çalıştırma
```sh
$ docker exec web-server date
```
> **Explanation:**
> + `nginx` imajından oluşturulan `web-server` adındaki container  docker'ın `exec` komut ile `date` komut çalıştırılmıştır. 
> + `docker exec` komutu host üzerinde çalışan container'ların içerisinde mevcut olan komutları yürütülmesine imkan verir.
> + `docker exec` komut `docker run` komutuna benzer ama `exec` sadece çalışan container'larda etkisini gösterir. 

###### 2. Shell Açma:
```sh
$ docker exec -i -t web-server bash
```
> **Explanation:**
> + `web-server` container çalıştığı için `docker exec` kullanıyoruz. 
> + Container içerisinde bir `bash shell` açmak için `ektileşimli tty` ihtiyaç var etkileşim için `-i` parametresi ve `tty` içinde `-t` parametresi kullanıyoruz.
> + container(`web-server`) sonra hangi kabuğu kullanacaksak onu yazıyoruz.