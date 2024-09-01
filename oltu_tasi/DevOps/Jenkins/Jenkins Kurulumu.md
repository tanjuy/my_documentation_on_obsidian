### İşletim Sistemi Üzerine Kurulum:

[Jenkins Official Installation Site](https://www.jenkins.io/doc/book/installing/linux/)

>[!INFO] Bilgi
> Kurulum Ubuntu 22.04.4 LTS (Jammy Jellyfish) üzerinde yapılıyor.

```bash
$ apt search openjdk
```
> **Explanation:**
> Ubuntu üzerindeki tüm java versionlarını ekran basacaktır.

```bash
$ sudo apt install openjdk-11-jdk
```
> **Explanation:**
> java 11 versionun kurulumu.

```
$ java --version
```

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
```

```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

```bash
sudo apt-get update
sudo apt-get install jenkins
```

```bash
$ sudo systemctl status jenkins.service
```
> **Explanation:**
> jenkins'ın çalışma durumunu kontrol ediyoruz. Ayrıca çıktıda göreceğiniz gibi ==8080== port'u üzerinde yayın yapmaktadır.

>[!INFO] Bilgi
> `$ ip -c a` veya `ipconfig` komutları ile ip adresini alıp, http://192.168.1.134:8080 ile tarayıcı ile giriş yapabilirisiniz

> [!TIP]
> Giriş ekranında açıkladığı gibi `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` ile Administrator password şifresini alabiliriz.

### Docker Üzerine Kurulum:

[TechWorld with Nana](https://www.youtube.com/watch?v=pMO26j2OUME&list=PLy7NrYWoggjw_LIiDK1LXdNN82uYuuuiC)

