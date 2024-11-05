#docker 


> [!NOTE]
> + `Dockerfile` da yorum karakteri `#` ile yapılır.

### Dockerfile Örnekleri:
##### Örnek 1:
```shell
$ mkdir web_docker; cd web_docker
```

```shell
$ ls -ltr
total 8
-rw-rw-r-- 1 ottoman ottoman 211 Nov  4 14:47 index.html
-rw-rw-r-- 1 ottoman ottoman  90 Nov  4 14:47 Dockerfile
```
> **Explanation:**
> + `web_docker` adında dizin yani klasör oluşturduk ve içerisinde de `index.html` ve `Dockerfile` adında dosyalar oluşturduk.

**Dockerfile**
```Dockerfile
FROM nginx:latest                         # 1
COPY index.html /usr/share/nginx/html     # 2
CMD ["nginx", "-g", "daemon off;"]        # 3
```
> **Explanation:**
> 1. `FROM` komutu ile base imajımızın `nginx` olduğunu söylüyoruz
> 2.  *Build context* de mevcut bulunan `index.html` dosyasını `COPY` komut ile build container'a kopyalıyoruz.
> 3. Container çalıştırıldığında varsayılan olarak çalıştırılacak program veya uygulama veya process ve burada çalışacak olan process ise nginx olmaktadır.

+ Build context ve build container ne olduğu ile ilgi bilgi almak için [[Dockerfile#COPY#Kaynak|COPY]] baskınız.

**index.html**
```html
<html>
<body style="background-color:gray;">
<center><h1 style="color:red;">Congrats!!!</p></h1></center>
<br>
<center><h1 style="color:red;">You have built your first image.</p></h1></center>
</body>
</html>
```
> **Explanation:**
> + `index.html`  *Build context*(`.`)  içerisinde mevcut olmalıdır. Yani Aşağıdaki `docker image build` komut index.html dosyasın bulunduğu dizine çalıştırılmalıdır. 

**imaj oluşturma**
```shell
$ docker image build -t tanjuu/webserver:latest -f Dockerfile .
```
> **Explanation:**
> + `-t` parametresi imajımızı isimlendiriyoruz ve etiketliyoruz(`tanjuu/webserver:latest`).
> + `-f` parametresi Dockerfile dosyasını adını veya yolu göstermektedir.
> + **Dikkat:** Bu komutu `web_docker` klasöründe çalıştırıyoruz.

```shell
$ docker run -d --name web -p 8080:80 tanjuu/webserver 
```
> **Explanation:**
> + Oluşturduğumuz imajımızı web adındaki container dönüştürüp çalıştırıyoruz.
> + `-p` parametresi ile container içerisindeki 80 portunu dışarıya 8080 ile yayınladık.
> + `-d` parametresi ile container'ın arka planda çalışmasını sağladık.
> + `curl -X GET 192.168.1.134:8080` veya tarayıcı ile GET isteği atarak sonucu görebilirsiniz.
> + **Dikkat:** Eğer `Dockerfile` dosyasını incelerseniz `EXPOSE` komutunun olamadığı halede `-p` parametresini kullanıldığını görebilirsiniz.

```shell
$ docker exec web cat /usr/share/nginx/html/index.html
```
> **Explanation:**
> + Bu komut ile `index.html` dosyasını içerisine bakarak teyit edebilirsiniz.

##### Örnek 2:
```shell
$ mkdir node_app; cd node_app                       # 1
```

```shell
$ touch Dockerfile package.json server.js           # 2
```
> **Explanation:**
> 1. `node_app` adında dosya oluşturuyoruz ve `node_app` klasör içerisine giriş yapıyoruz.
> 2. `touch` komut ile `Dockerfile`, `package.json` ve `server.js` adında dosyalar oluşturuyoruz. Çünkü bu dosyalar aşağıdaki değerler ile doldurulacaktır. 

**Dockerfile**
```Dockerfile
# source: https://nodejs.org/en/docs/guides/nodejs-docker-webapp/
FROM node:12                          

# Create app directory
WORKDIR /usr/src/app

# Copy source files
COPY package.json .
COPY server.js .

# Install app dependencies
RUN npm install

# Exposing the port 8080
EXPOSE 8080

CMD [ "node", "server.js" ]
```
> **Explanation:**
> + `FROM` komut ile `node` imajının 12 versiyononu temel alınıyor.
> + `WORKDIR` komutu ile çalışma dizinimizi(`/usr/src/app`) belirliyoruz.
> + `COPY` komut ile `build context` içerisinde bulunan `package.json` ve `server.js` dosyalarını `build container`'a gönderiyoruz. Kısacası, `docker image build` komutun çalıştırıldığı dizindeki dosyaları oluşturulan imajın içerisine atıyoruz.
> + `RUN` komutu ile imaj içerinde çalışmasını sağlamaktadır. `npm install`, package.json içerisinde belirtilen bağımlıkları yükler.
> + `EXPOSE` komut ile 8080 port'un imaj içerisinden dinlediğini belgelendiriyoruz.
> + `CMD` komutu ile imajdan container oluşturup varsayılan olarak çalıştırdığımızda çalışacak komutdur.(`node server.js`)

**package.json**
```json
{
    "name": "docker_web_app",
    "version": "1.0.0",
    "description": "Node.js on Docker",
    "author": "First Last <first.last@example.com>",
    "main": "server.js",
    "scripts": {
      "start": "node server.js"
    },
    "dependencies": {
      "express": "^4.16.1"
    }
  }
```
> **Explanation:**

**server.js**
```js
'use strict';

const express = require('express');

// Constants
const PORT = 8080;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```
> **Explanation:**

**imaj oluşturma**
```shell
$ docker image build -t node_server .
```
> **Explanation:**
> + Bu komut `node_app` içerisinde çalıştırdığımız için ve oluşturduğumuz dosya adı `Dockerfile` olduğu için `-f` parametresi kullanımı yapmadık.
> + Nokta (`.`), çalıştırdığımız dizini göstermektedir yani `node_app` klasörünü işaret etmektedir.
> + `docker image ls` komut ile oluşturduğumuz imajı teyit edebiliriz.

**Container oluşturma:**
```shell
$ docker run --name -d -p 8080:8080 node_server:latest
```
> **Explanation:**
> + 
> + `curl -X GET 192.168.1.134:8080` veya tarayıcı ile GET isteği atarak sonucu görebilirsiniz.
> + GET isteğinin sonucu `Hello World` olacaktır.
### FROM:
+ **Amaç:** `FROM` komutu, bir Dockerfile'ın en temel ve ilk komutudur. İmaj oluşturma işlemi sırasında hangi taban (base) imajın kullanılacağını belirtir.

###### Syntax:
```Dockerfile
FROM [--platform=<platform>] <image> [AS <name>]
```
veya
```Dockerfile
FROM [--platform=<platform>] <image>[:<tag>] [AS <name>]
```
+ `<image>` : Kullanılacak taban imajın adı. Örneğin, `ubuntu`, `alpine`, veya `node` gibi popüler taban imajlar kullanılabilir.
+ **`<tag>`**: Taban imajın sürümünü veya versiyonunu belirtir. Eğer `tag` belirtilmezse, varsayılan olarak `latest` etiketi kullanılır
###### Çoklu `FROM` Kullanımı (Multi-Stage Build):
+ Aynı Dockerfile içerisinde birden fazla `FROM` komutu kullanılabilir. Bu yöntem, özellikle multi-stage build denilen yapılar için faydalıdır.
+ Farklı aşamalarda farklı taban imajlar kullanarak daha küçük ve optimize edilmiş imajlar oluşturabilirsiniz.

```Dockerfile
# Derleme aşaması
FROM golang:1.16 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# Çalışma aşaması (sonuç imaj)
FROM alpine:latest
COPY --from=builder /app/myapp /myapp
CMD ["/myapp"]
```
> **Explanation:**
> + Bu örnekte, Go dilinde bir uygulama ilk `FROM` komutuyla `golang` imajında derlenir; sonrasında ise `alpine` imajı üzerine sadece derlenmiş uygulama dosyası kopyalanır.

---
### COPY:
 + **Amaç:** Dockerfile'da `COPY` komutu, yerel dosyaları veya dizinleri Docker imajının içine kopyalamak için kullanılır. Bu komut, belirttiğiniz kaynak dosya veya dizinleri imajdaki belirli bir hedef dizine taşır.
###### Syntax:
```Dockerfile
COPY [OPTIONS] <src> ... <dest>
COPY [OPTIONS] ["<src>", ... "<dest>"]
```
+ `<src>` : Kopyalanacak dosya veya dizin. Bu, Dockerfile'ın bulunduğu dizine göre bağıl bir yol olmalıdır.
+ `<dest>` : Dosya veya dizinin kopyalanacağı imaj içindeki hedef yol. Bu yol, mutlak bir yol veya önceden tanımlanmış bir `WORKDIR` olabilir.
###### Örnek 1:
```Dockerfile
FROM alpine:latest
COPY file /app/myapp
```
> **Explanation:**
> + - Bu komut, yerel `myapp` dosyasını Docker imajındaki `/app/myapp` konumuna kopyalar.

#### Kaynak:
+ COPY ile birden fazla kaynak dosyası veya dizini belirtebilirsiniz. Son argüman her zaman hedef noktası olmalıdır.
+ Örneğin; iki dosyayı(`file1.txt` ve `file2.txt`), *build context*'den *build container* içerisinde `/usr/src/things` kopyalar;

```Dockerfile
COPY file1.txt file2.txt /usr/src/things/
```

+ Birden fazla kaynak dosyası belirtirseniz(ya direk olarak veya wildcard kullanarak) o zaman hedef bir dizin olmalı(üstelik `/` ile de bitmelidir).

> [!IMPORTANT]
> + **Build Context (Yapı Bağlamı)**:
> + Docker'da bir imaj oluştururken, Dockerfile'ın bulunduğu dizin ve bu dizindeki dosyalar "build context" olarak adlandırılır.
> + Yani, Docker build komutunu çalıştırdığınızda, Docker tüm bu dizini "bağlam" olarak kabul eder ve yalnızca bu dizindeki dosyalar Dockerfile ile kopyalanabilir veya kullanılabilir.
> + Örneğin, `docker build .` komutu ile "." (mevcut dizin) build context olarak belirlenir.
> + **Türkçesi**: Yapı Bağlamı veya Derleme Bağlamı.


> [!IMPORTANT]
> + **Build Container (Yapı Konteyneri)**:
> + Docker, bir Dockerfile'ı çalıştırarak imaj oluştururken geçici bir yapı konteyneri (build container) oluşturur.
> + Bu konteyner, Dockerfile’daki adımları sırayla çalıştırır ve son adımda imaj haline gelir.
> + "COPY" gibi komutlarla bu geçici konteyner içinde dosyalar belirli dizinlere kopyalanabilir.
> + **Türkçesi**: Yapı Konteyneri veya Derleme Konteyneri.

+ **Özetle**, "build context" Dockerfile ile erişilebilecek tüm dosyaların bulunduğu dizini, "build container" ise Dockerfile komutlarının yürütüldüğü geçici konteyneri ifade eder.
#### Hedef:


+ Kaynak: [COPY](https://docs.docker.com/reference/dockerfile/#copy)
---

### HEALTHCHECK:
+ **Amaç:** Dockerfile'da `HEALTHCHECK` komutu, bir konteynerin sağlığını kontrol etmek için kullanılır. Bu komut, belirli aralıklarla bir komut çalıştırarak konteynerin sağlıklı (healthy) ya da sağlıksız (unhealthy) olup olmadığını belirler.
+ `HEALTHCHECK`, özellikle kritik uygulamaların çalıştığı konteynerlerde durum takibi yapmaya ve gerektiğinde otomatik müdahale için Docker’ın gerekli bilgileri sağlamasına olanak tanır.

##### 1.Düzenli Kontrol Yapma:
###### Syntax:


---
### RUN:
+ **Amaç:** Dockerfile'da `RUN` komutu, bir Docker imajı oluşturulurken belirli komutları çalıştırmak için kullanılır.
+ **Çalışma Yapısı:** Bu komut, imaja yeni katmanlar (layers) ekleyerek yazılımların kurulması, yapılandırmaların yapılması veya dosyaların düzenlenmesi gibi işlemleri gerçekleştirir.
+ `RUN` komutu sayesinde imaj içine komutlar eklenir ve bu işlemlerin çıktısı imajda kalıcı hale getirilir.

###### Syntax:
```Dockerfile
# Shell form:
RUN [OPTIONS] <command> ...
# Exec form:
RUN [OPTIONS] [ "<command>", ... ]
```
##### Kullanımı:
###### 1.Shell Formu:
+ Komutu, shell (örn. `/bin/sh -c`) üzerinden çalıştırır.

```Dockerfile
# Shell form:
RUN [OPTIONS] <command> ...
```

###### 2.Exec Formu:
+ Komutu doğrudan çalıştırır, shell kullanılmaz (daha güvenlidir).

```Dockerfile
RUN ["<komut>", "<arg1>", "<arg2>"]
```

---
### CMD(Command):
+ **Amaç**: Konteyner çalıştırıldığında varsayılan olarak çalıştırılacak komutu tanımlar.
+ **Esneklik**: `docker run` komutu ile konteyner çalıştırılırken CMD ile belirtilen komut, kullanıcı tarafından geçersiz kılınabilir.
+ **Kullanım Senaryosu**: Genellikle konteynerin temel işlevini tanımlamak için kullanılır ve esnekliği sayesinde farklı komutlar çalıştırmak istendiğinde idealdir.

```Dockerfile
FROM ubuntu:latest
CMD ["echo", "Merhaba Dünya"]
```

+ Bu Dockerfile ile oluşturulan imaj, konteyner çalıştırıldığında `echo "Merhaba Dünya"` komutunu varsayılan olarak çalıştırır. Ancak, kullanıcı `docker run` ile farklı bir komut belirtebilir:


> [!CAUTION]
> + Bir Dockerfile'da yalnızca bir CMD talimatı olabilir. Birden fazla CMD listelerseniz yalnızca son CMD geçerli olur.


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
### EXPOSE:
+ **Amaçı:** Dockerfile'da `EXPOSE` komutu, konteynerin hangi ağ portlarını dinleyeceğini belirtir.
+ Bu komut, bir uygulamanın çalıştığı portu diğer konteynerlere veya host sisteme bildirmek için kullanılır.

> [!CAUTION]
> + EXPOSE komutu aslında portu yayınlamaz. imajı oluşturan kişi ile konteyneri çalıştıran kişi arasında hangi portların yayınlanmasının amaçlandığı konusunda bir tür dokümantasyon işlevi görür. (Resmi Site)
> + Konteyneri çalıştırırken portu yayınlamak için, docker run sırasında `-p` bayrağını kullanarak bir veya daha fazla portu yayınlayıp eşleyin veya `-P` bayrağını kullanarak tüm açık portları yayınlayıp bunları yüksek sıralı portlara eşleyin. (Resmi Site)
> + `EXPOSE` komutunun tek başına bir portu dış dünyaya açmadığını belirtmek önemlidir; sadece imajın hangi portlarda çalışabileceğine dair bilgi sağlar. (ChatGPT)
> + Gerçek anlamda bir portu dışa açmak için konteyneri başlatırken `-p` veya `--publish` seçeneği kullanılır. (ChatGPT)


###### 1.Tek Port Tanımlama:
```Dockerfile
FROM node:14
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]
```
> **Explanation:**
> + Bu Dockerfile, Node.js tabanlı bir uygulama için `3000` portunu açar.
> + `EXPOSE 3000` komutu, bu uygulamanın `3000` portunu dinlediğini belirtir.

###### 2.Birden Fazla Port Tanımlama:
```Dockerfile
FROM nginx:latest
EXPOSE 80 443
```
> **Explanation:**
> + Bu örnekte, `80` ve `443` portları belirtilmiştir. Bu, bir web sunucusunun hem HTTP (80) hem de HTTPS (443) üzerinden erişilebilir olduğunu belirtir.

###### 3.`EXPOSE` ve Port Yönlendirme:
+ `EXPOSE` komutu, yalnızca bilgilendirme ve belge sağlamak amacıyla kullanılır.
+ Bir portu dış dünyaya açmak için konteyneri başlatırken `-p` veya `--publish` seçeneği ile host portunu konteyner portuna bağlamalısınız:
```shell
$ docker run -p 8080:3000 myapp
```

---
### WORKDIR:
+ **Amaçı:** Dockerfile'da `WORKDIR`, bir Docker konteynerinde varsayılan çalışma dizinini ayarlamak için kullanılır. Yani, WORKDIR komutu, Dockerfile'da onu takip eden tüm RUN, CMD, ENTRYPOINT, COPY ve ADD komutları için çalışma dizinini ayarlar.
+ **Kolaylık**: Her komutta dizin belirtmek zorunda kalmadan, çalışma dizinini bir kez ayarlayarak işlemleri daha kolay yönetebilirsiniz.
+ Bash kabuğundaki `cd` komutuna karşılık gelemektedir.
###### Syntax:
```Dockerfile
WORKDIR /path/to/directory
```

###### Örnek 1:
```Dockerfile
FROM alpine:latest
WORKDIR /app
RUN mkdir uygulama
```
> **Explanation:**
> + Bu komut, konteynerin çalışma dizinini `/app` olarak ayarlar.
> + Böylece, Dockerfile içindeki sonraki komutlar (örneğin `RUN`, `CMD`, `COPY` gibi) `/app` dizininde çalışacaktır.

###### Örnek 2:
```Dockerfile
FROM ubuntu:latest
WORKDIR /app
RUN echo "Hello" > hello.txt
WORKDIR /app/subdir
RUN echo "World" > world.txt
```
> **Explanation:**
> + İlk `WORKDIR /app` komutu, `/app` dizinini çalışma dizini olarak ayarlar.
> + `RUN echo "Hello" > hello.txt` komutu, `/app` dizininde bir `hello.txt` dosyası oluşturur.
> + İkinci `WORKDIR /app/subdir` komutu, çalışma dizinini `/app/subdir` olarak değiştirir.
> + `RUN echo "World" > world.txt` komutu, `/app/subdir` dizininde bir `world.txt` dosyası oluşturur.

---
### Apps ile Dockerfile:
###### Örnek: 1
Yapılcak çalışma ama ingilizce [link](https://www.youtube.com/watch?v=0eMU23VyzR8)
###### Örnek: 2
