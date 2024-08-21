#docker
## Docker Swarm Kurulumu
```
$ docker  info | grep -i 'swarm'
```
> **Explanation:**
> Docker swarm aktiflik durumunu kontrol ediyoruz.

```
$ docker swarm init
```
> **Explanation:**


## Docker Swarm Araçları
#### Docker Swarm Visualizer 
[Official Site](https://github.com/dockersamples/docker-swarm-visualizer)
```
$ docker service create \
  --name=viz \
  --publish=8080:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer
```

> [!INFI] Bilgi
> http://192.168.1.134:8082/ gibi kendi ip'iniz üzerinden tarayıcıdan ulaşabilirsiniz.

#### Portainer.io
[Resmi Sitesi](https://docs.portainer.io/start/install-ce/server/swarm/linux)

## Docker Swarm Yönetimi
> [!CAUTION] Dikkat
> Bu komutlar sadece Docker Swarm Manager Düğümünde çalışır.

> [!IMPORTANT] Önemli
> Bu tanım swarm'daki servisler için geçerlidir.
> Node(düğüm): Çalışan makineleri kast eder yani worker makineleri
> Task(Görev): Node'lar içerisinde çalışan container'ları kast eder.


```
$ docker node ls
```
> **Explanation:**
> Docker swarm'ın hem *worker* hem de *manager* düğümlerini listeler

```
$ docker node ps 
```
> **Explanation:** Manager makine
> Bir yada birden çok çalışan düğüm üzerinde task'ları lister, varsayılan olarak mevcut düğüm üzerindekini listeler. `docker node ps self` veya `docker node ps portainer` yukarıdaki ile aynı anlama gelir.

```
$ docker node ps nfsserver
```
> **Explanation:** Worker makine
> nfsserver makinesindeki task'ları listeler
## Docker Swarm Service
>[!INFO] Bilgi
> + microservis => servis => app (container)
> + task => replica (Her bir kopya)

#### Servis Oluşturma - create
```
$ docker service create --name WebService --publish 8080:80 --replicas 4 nginx
```
> **Explanation:**
> Adı WebService olan 8080 portundan yayın yapan 4 kopyası olan bir nginx servisi oluşturuyoruz

```
$ docker service create --name sabit_hostname \ 
--constraint "node.hostname==gopostgresql" --replicas 3 nginx
```
> **Explanation:**
> <span style=color:blue>--constraint "node.hostname==gopostgresql"</span> anlamı oluşturulacak 3 nginx replicas'ların gopostgresql makinesinde oluşması istenmektedir.

```
$ docker service create --name harici_hostname \
--constraint "node.hostname!=nfsserver" --replicas 3 nginx
```
> **Explanation:**
> <span style=color:red>--constraint "node.hostname!=nfsserver"</span> anlamı oluşturulacak 3 nginx kopyaların nfsserver makinesinde oluşturulmamasını ve diğer makinelerde oluşturulması istenmektedir.

#### Servislerin Silinmesi - rm

> [!INFO] Bilgi
> Usage:  docker service rm SERVICE [SERVICE...]

```
$ docker service ls
```
> **Explanation:**
> Servisleri listeler

```
$ docker service ps WebService
```
> **Explanation:**
> Bir yada birden çok servislerin görevlerini listeler

---
#### Servis Öleçeklendirme - scale
> [!INFO] Bilgi
> Usage:  docker service scale SERVICE=REPLICAS [SERVICE=REPLICAS...]

```
$ docker service scale WebService=2
```
> **Explanation:**
> WebService adındaki servisin task'larını 4'den 2'ye ölçeklendiriyoruz.

---
```
$ docker service update --replicas 5 WebService
```
> **Explanation:**
>  Bir önceki komut ile aynı işlemi yapar yani WebService'ın tasklarını 2'den 5'e çıkarır.

#### Docker stack
>[!CAUTION] Dikkat
>`docker stack` da kullanılan yaml formatı `docker compose` formatının aynısı ama çok az ek özelikleri mevcuttur.


```yaml
version: "3"
services:
  redis:
    image: redis:alpine
    networks:
      - frontend
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure
  db:
    image: postgres:9.4
    environment:
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "postgres"
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - backend
    deploy:
      placement:
        constraints: [node.role == manager]
  vote:
    image: dockersamples/examplevotingapp_vote:before
    ports:
      - 5000:80
    networks:
      - frontend
    depends_on:
      - redis
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
      restart_policy:
        condition: on-failure
  result:
    image: dockersamples/examplevotingapp_result:before
    ports:
      - 5001:80
    networks:
      - backend
    depends_on:
      - db
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
      restart_policy:
        condition: on-failure
  worker:
    image: dockersamples/examplevotingapp_worker
    networks:
      - frontend
      - backend
    depends_on:
      - db
      - redis
    deploy:
      mode: replicated
      replicas: 1
      labels: [APP=VOTING]
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
      placement:
        constraints: [node.role == manager]
  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8083:8080"
    stop_grace_period: 1m30s
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]
networks:
  frontend:
  backend:

volumes:
  db-data:
```

> **Explanation:**
> +  [[Docker Compose#update_config|update_config]] bakınız. (Docker compose ile aynı)


```
$ docker stack deploy --compose-file docker_stack.yml voteapplication
```
> **Explanation:**

```
$ docker stack ls
```
> **Explanation:**
> swarm'daki stack'leri listeler

```
$ docker stack ps voteapplication 
```
> **Explanation:**
> voteapplication bir stack'dir. Bu komut voteapplication'ın da mevcut olan task'ları listeyecektir.

```
$ docker stack services ls
```
> **Explanation:**
> stack ile oluşturulmuş servisleri listeler.

