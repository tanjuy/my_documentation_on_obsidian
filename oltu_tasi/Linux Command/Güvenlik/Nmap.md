## SERVICE AND VERSION DETECTION:
### `-sV` parametresi:
```shell
nmap -p 80,443 -sV 192.168.1.132
```

**Çıktı:**
```shell
Starting Nmap 7.80 ( https://nmap.org ) at 2024-12-28 14:29 +03
Nmap scan report for 192.168.1.132
Host is up (0.0017s latency).

PORT    STATE  SERVICE VERSION
80/tcp  open   http    nginx
443/tcp closed https

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.46 seconds
```

> **Explanation:**
> + **`-p`** seçeneği, belirli portları taramak için kullanılır.
> + Burada port **80** ve **443** taranıyor
> + `-sV` seçeneği, bir portta çalışan hizmetin **versiyon bilgilerini** tespit etmeye çalışır.
> + Yani, yalnızca portun açık olup olmadığını öğrenmekle kalmaz, o portta çalışan yazılımın türünü ve sürümünü de öğrenmeye çalışır.
> + Bu(`192.168.1.132`), taranacak hedefin adresidir. Bu bir alan adı (örneğin, bir web sitesi) veya bir IP adresi olabilir.
> + `192.168.1.132` adresinde kendim oluşturduğum `nginx server`'e belirli portlar üzerinden versiyon taraması yapıyoruz.
> + Eğer `-p` parametresini kullanmazsak tüm portları tarar.



