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


```shell
$ docker node ls
```
> **Explanation:**
> Docker swarm'ın hem *worker* hem de *manager* düğümlerini listeler

```shell
$ docker node ps 
```
> **Explanation:** Manager makine
> Bir yada birden çok çalışan düğüm üzerinde task'ları lister, varsayılan olarak mevcut düğüm üzerindekini listeler. `docker node ps self` veya `docker node ps portainer` yukarıdaki ile aynı anlama gelir.

```shell
$ docker node ps nfsserver
```
> **Explanation:** Worker makine
> nfsserver makinesindeki task'ları listeler

```shell
$ docker node inspect nfsserver
```
> **Explanation:** Manager makine
> 1. Bu komut *manager makine* üzerinden yapılıyor ve nfsserver node bir *worker makine*
> 2. Bu komut bize nfsserver içerisine girmeden durumu ve IP adresini alabiliriz.
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
        constraints: [node.role == manager]         # 2
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
      update_config:                                   # 1 
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
      placement:                                       # stack line
        constraints: [node.role == manager]            # 2
  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8083:8080"
    stop_grace_period: 1m30s
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]            # 2
networks:
  frontend:
  backend:

volumes:
  db-data:
```

> **Explanation:**
> 1.  [[Docker Compose#update_config|update_config]] bakınız. (Docker compose ile aynı)
> 2. `[node.role == hostname]` hostname alanına ne yazarsak o servis o hostname üzerinde çalışacak. 


```shell
$ docker stack deploy --compose-file docker_stack.yml voteapplication
```
> **Explanation:**

```
$ docker stack ls
```
> **Explanation:**
> swarm'daki stack'leri listeler

```shell
$ docker stack ps voteapplication 
```
> **Explanation:**
> voteapplication bir stack'dir. Bu komut voteapplication'ın da mevcut olan task'ları listeyecektir.

```shell
$ docker stack services ls
```
> **Explanation:**
> stack ile oluşturulmuş servisleri listeler.

## Docker Swarm Secret

> [!TIP] Ipucu
> docker'ın swarm orkestrasyonuda:
> 1. docker stack de yaml dosyasında 
>  ```
> placement:
 >   constraints: [node.role == worker]
>  ```
>  2. Yada `docker --constraint=node.role==worker` 
>  Eğer worker yazarsak herhangi bir worker da çalışır veya manager yazarsak her hangi bir manager da çalışır o container ama direk makinenin(hostname) yazarsak belirlediğimiz hostname de çalışır.

###### Örnek 1:  having problems
```shell
$ openssl rand -base64 10 | docker secret create db_root_password -
```
> **Explanation:**
> [[Linux komutları#openssl|openssl]] için bakınız.
> openssl rastgele oluşturulan değeri docker secret'e yönlendiriyoruz ve db_root_password adında oluşturuyoruz.

```shell
$ openssl rand -base64 10 | docker secret create db_dba_password -
```
> **Explanation:**
> [[Linux komutları#openssl|openssl]] için bakınız.

```bash
$ docker secret ls
```
> **Explanation:**
> secret'leri listeler

```bash
$ docker secret rm db_root_password
```
> **Explanation:**
> Eğer secret'leri silmek isterseniz; secret(db_root_password) adını veya secret ID vererek silme işlemini gerçekleştirebilirsiniz. Yukarıda secret adı verilmiş. Eğer secret adını veya secret ID görmek için `docker secret ls` kulanız.

```bash
$ docker secret inspect db_root_password
```
> **Explanation:**
> Oluşturmuş olduğumuz secret için detaylı bilgi almak için kullanabiliriz


```yaml
version: "3.3"

services:
  db:
    image: mysql
    secrets:
      - db_root_password                        # 2 
      - db_dba_password                         # 2
    deploy:
      replicas: 1
      placement:
        constraints: [node.role == worker]
      resources:
        reservations:
          memory: 128M
        limits:
          memory: 256M
    ports:
      - 3306:3306
    environment:
      MYSQL_USER: dba
      MYSQL_DATABASE: mydb
      MYSQL_ROOT_PASSWORD_FILE: /run/secrets/db_root_password
      MYSQL_PASSWORD_FILE: /run/secrets/db_dba_password
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - type: bind
        source: /opt/docker/volumes/mysql
        target: /var/lib/mysql
  adminer:
    image: adminer
    ports:
      - 8080:8080

secrets:
  db_root_password:                    # 1
    external: true
  db_dba_password:                     # 1
    external: true
```

> **Explanation:**
> 1. `external: true`, Compose dosyasının bu secret'ları doğrudan oluşturmayacağını, bunun yerine Docker Swarm içinde zaten var olan secret'ları kullanacağını belirtir. Yani, bu secret'lar daha önce `docker secret create` komutu ile oluşturulmuş olmalıdır. Zaten yukarıda oluşturduk.
> 2. Bir Docker Compose dosyasında bir hizmete secret eklemek için, secret'ı servis tanımı altında `secrets` anahtarına eklemeniz gerekir:
> Kaynak: BTK akademi


> [!WARNING] Uyarı:
> Mysql de mydb adında veritabanı oluşturulamadı!

---
###### Örnek 2: Wordpress ve mariadb

```shell
$ echo "write your password" | docker secret create root_db_password -
```
> **Explanation:**
> *write your password* şifremiz oluşturulmuş olan `root_db_password` içerisine yazılacaktır. İsterseniz yukarıdaki [[Docker Swarm#Örnek 1 having problems|örnek 1]] de olduğu gibi openssl kullanılarak rastgele şifrede oluşturulabilir.
> Bu secret mariadb için oluşturuluyor.

```shell
$ echo "write your password" | docker secret create wp_db_password -
```
> **Explanation:**
> Yukarıdaki işlemi *wordpress* için yapıyoruz.

```shell
$ docker secret ls
```
> **Explanation:**
> Oluşturulan secret'leri listeleyebilirsiniz.

```shell
$ docker network create -d overlay wp
```
> **Explanation:**
>Makineler(Host) arasındaki haberleşmeyi sağlamak için *overlay* ağ kuruyoruz.
>-d veya --driver parametresi, ağı yönetmek için sürücü seçiyoruz.
>*overlay* ağın isimi de wp oluyor.

```shell
$ docker service create \
	--name mariadb \
	--replicas 1 \
	--constraint=node.role==manager \
	--network wp \
	--secret source=root_db_password,target=root_db_password \
	--secret source=wp_db_password,target=wp_db_password \
	-e MYSQL_ROOT_PASSWORD_FILE=/run/secrets/root_db_password \
	-e MYSQL_PASSWORD_FILE=/run/secrets/wp_db_password \
	-e MYSQL_USER=wp \
	-e MYSQL_DATABASE=wp \
	mariadb:10.1
```
> **Explanation:**
> Kaynak: BTK akademi

```shell
$ docker service create \
	--name wordpress \
	--replicas 1 \
	--constraint=node.role==worker \
	--network wp \
	--publish 80:80 \
	--secret source=wp_db_password,target=wp_db_password,mode=0400 \
	-e WORDPRESS_DB_USER=wp \
	-e WORDPRESS_DB_PASSWORD_FILE=/run/secrets/wp_db_password \
	-e WORDPRESS_DB_HOST=mariadb \
	-e WORDPRESS_DB_NAME=wp \
	wordpress:4.7
```

> **Explanation:**
> Kaynak: BTK akademi






