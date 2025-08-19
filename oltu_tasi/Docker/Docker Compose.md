#docker 


## docker-compose.yml


> [!NOTE]
> + `docker-compose.yml` dosyası üç ana bölümden oluşabilir:
> ##### 1. version:
> + Compose dosyasının biçim sürümü (`3.8`, `3.9`, vb.)
> ##### 2. services:
> + Burada tek veya birden fazla container tanımı yapılır.
> ```yaml
> services:
>   web:
>     image: nginx
>   db:
>     image: postgres
> ```
> + Bu durumda `web` ve `db` adında **iki farklı container** çalışır.
> ##### 3. volumes:/networks:/configs:
> + İsteğe bağlı altyapı tanımları. 

### 1. version:

### 2. services:

+ **services:** başlığı altında, çalıştırmak istediğin her bir `container` (yani servis) tanımlanır.
+ Her servis için hangi imajın kullanılacağı, hangi portların açılacağı, hangi volume’lerin bağlanacağı, hangi ortam değişkenlerinin verileceği gibi ayarlar yapılır.

### 3. volumes:/networks:/configs:




## Compose Deploy Specification:

##### environment:

##### deploy:
###### placement:

###### replicas:
> Servis `replicated`(varsayılandır) edilecekse, `replicas` belirli bir zamanda çalıştırılacak `container` sayısını belirler. (Çeviri: [replicas ing](https://docs.docker.com/reference/compose-file/deploy/#replicas) )
> Yani, Eğer `mode: replicated` yazmasak varsayılan olarak bu şekilde çalışacaktır. Aşağıda da görüldüğü gibi `replica: 6` demişiz. Bu da 6 tane kopya *container(example/webapp)* ayağa kaldıracaktır. (Kendi bilgim)

```yaml
services:
  frontend:
    image: example/webapp
    deploy:
      mode: replicated
      replicas: 6
```
###### restart_policy:

###### resources:

###### update_config:
Servislerin nasıl güncelleneceğini yapılandırır. rolling update yapılandırılması için kullanışlı.
1. `parallelism`: Aynı anda günçellencek container sayısı
	+ Aynı anda 2 container güncellenir (`parallelism: 2`).
2. `delay`: Bir container gurubun güncellenmesi arasında beklenen süre.
	+ Her iki container güncellendikten sonra 10 saniye beklenir (`delay: 10s`).


##### ports:


Kaynak: [Compose Deploy Specification](https://docs.docker.com/compose/compose-file/deploy/)