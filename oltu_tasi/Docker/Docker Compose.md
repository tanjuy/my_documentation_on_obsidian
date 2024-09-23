#docker 
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