#linux_commands 


### 1. sudo parametreleri:

###### 1.1. `-l` parametresi:
```shell
$ sudo -l
```
> **Explanation:**
> + Linux ve Unix tabanlı sistemlerde bir kullanıcının hangi **sudo** yetkilerine sahip olduğunu ve hangi komutları yönetici (root) yetkisiyle çalıştırabileceğini listelemek için kullanılır.
> + 

###### 1.2. `-k` parametresi:
```shell
$ sudo -k
```
> **Explanation:**
> +  Eğer sudo ile komut çalıştırıp ve terminale her hangi bir girdi yapmazsak, 5 dakikalık süre boyunca `sudo` şifre istemez.
> + `-k` parametresi ile 5 dakikalık süreyi sıfırlayabiliriz ve `sudo` ile komut çalıştırdığımızda şifre ister.
### 2. visudo Komutu:

+ 
### 3. `/etc/sudoers` Dosyası:

##### 3.1.`ALL=(ALL:ALL) ALL`

```shell
[user] [host] = ([run_as_user]:[run_as_group]) [commands]
```

```
root ALL=(ALL:ALL) ALL
```
> **Explanation:**
> 1. root : kuralın hangi kullanıcı veya grup için geçerli olduğunu belirtir. Bu durumda, kural `root` kullanıcısı içindir.
> 2. ALL : kuralın hangi makinelerde (hosts) geçerli olduğunu gösterir. `ALL` yazdığı için, bu kural tüm makinelerde geçerlidir.
> 3. (ALL : ALL): 
> 	+ Parantez içindeki ilk `ALL`, komutun hangi kullanıcı adına çalıştırılabileceğini belirtir (yani herhangi bir kullanıcı).
> 	+ İkinci `ALL`, komutun hangi grup adına çalıştırılabileceğini belirtir (yani herhangi bir grup).
> 4. hangi komutların çalıştırılabileceğini gösterir. `ALL`, kullanıcının herhangi bir komutu çalıştırabileceği anlamına gelir.

#### 3.2. `/etc/sudoers.d` Klasörü
+ `/etc/sudoers.d` dizini, Linux sistemlerinde `sudo` yetkilendirmelerini daha yönetilebilir ve esnek hale getirmek için kullanılan önemli bir yapıdır.
+ `/etc/sudoers.d` dizini, `sudo` yetkilendirme kurallarını ana `sudoers` dosyasından ayrı tutarak yönetmenizi sağlayan bir yapıdır.
+ Ana `sudoers` dosyası `/etc/sudoers` konumunda bulunur ve genellikle tüm sistem üzerinde geçerli olan genel `sudo` kurallarını içerir.
+ Ancak, bu dosyayı doğrudan düzenlemek yerine, `/etc/sudoers.d` dizininde ayrı dosyalar oluşturarak belirli kullanıcılar veya gruplar için özel kurallar tanımlayabilirsiniz.
---
##### 1. Kullanıcı Oluşturma:

```shell
$ sudo adduser tanju
```
>  **Explanation:**
> + `tanju` adında kullanıcı oluşturuyoruz. `ubuntu OS` da bu işlem yapılıyor.
> + `adduser` script'i kullanıcı oluşturmak için gereken tüm işlemleri yapıyor.

---
##### 2. Kullanıcı dosyası oluşturma:
```shell
$ sudo visudo -f /etc/sudoers.d/tanju
```
>  **Explanation:**
>  + Yetki kısıtlaması yapmak istediğimiz kullanıcın(tanju) `/etc/sudoers.d` dizini altında `tanju` dosyasını oluşturuyoruz.

###### 2.1 Kullanıcı Bazında Yetkilendirme:
```sudoers
tanju ALL=(ALL) /usr/bin/ls, /usr/bin/pwd
tanju ALL=(ALL) /usr/bin/systemctl status nginx
```
>  **Explanation:**
>  + `tanju` adlı kullanıcı  yalnızca  sudo komut ile `ls` ve `pwd` komutlarını kullanabilecektir. 
>  + `/usr/bin/ls` ve `/usr/bin/pwd` komutları yerine `ALL` yazsaydık tüm komutlar üzerinde yetkisi olacaktır.
>  + `sudo -l` komut ile ne kadar yetki verdiğinizi listeleyebilirsiniz.

###### 2.2 Grup Bazında Yetkilendirme:
```sudoers
%web ALL=(ALL) /usr/bin/systemctl restart nginx, /usr/bin/systemctl stop nginx
```
>  **Explanation:**
> + `web` grubundaki kullanıcılara sadece `nginx` servislerini yönetme izni verebilirsiniz.
> + Bu, `web` grubundaki kullanıcıların sadece `systemctl restart nginx` ve `systemctl stop nginx` komutlarını `sudo` ile çalıştırmasına izin verir.
> + **Dikkat:** Kullanıcıdan farklı olarak `%` ile başladığına dikkat ediniz. Bu da bunun grup olduğunu gösterir.

###### 2.3 Komut Alias'ları Kullanma:
```sudoers
Cmd_Alias BACKUP_CMDS = /usr/bin/rsync, /usr/bin/tar
backup ALL=(ALL) BACKUP_CMDS
```
>  **Explanation:**
>  + `backup` kullanıcısına sadece yedekleme komutlarını çalıştırma izni verebilirsiniz.
>  + Bu, `backup` kullanıcısının sadece `rsync` ve `tar` komutlarını `sudo` ile çalıştırmasına izin verir.
>  + `Cmd_Alias` komut ile `/usr/bin/rsync` ve `/usr/bin/tar` değerlerini `BACKUP_CMDS` değişkenine atıyoruz.


> [!CAUTION]
> + **Dosya İzinleri:**
> + `/etc/sudoers.d` dizinindeki dosyaların doğru izinlere sahip olması çok önemlidir. Genellikle, dosyaların sahibi `root` ve izinleri `440` (sadece okunabilir) olmalıdır.
> ```
>  $ sudo chmod 440 /etc/sudoers.d/tanju
>  $ sudo chown root:root /etc/sudoers.d/tanju  
> ```


> [!TIP]
> + **Syntax Hatalarından Kaçınma:**
> + Sudoers dosyalarında syntax hataları sistemde `sudo` kullanımını tamamen engelleyebilir.
> + Dosyaları düzenlerken mutlaka `visudo` komutunu kullanın.
> + Ancak, `visudo` genellikle sadece ana `sudoers` dosyasını düzenlemek için kullanılır. `/etc/sudoers.d` dizinindeki dosyaları düzenlerken dikkatli olun ve syntax doğrulaması yapın.
> ```
>  $ sudo visudo -cf /etc/sudoers.d/tanju
> ```
> + `-c` parametresi:  `tanju` adlı dosyasını sözdizimi(systax) hatalarını kontrol eder.
> + `-f` parametresi: varsayılan dizinden farklı bir yol belirmek için kullanılır.

---
##### 3. Sudo Yetkilerini Görüntüleme:

```shell
$ sudo -l -U tanju
```

**Çıktı:**
```shell
Matching Defaults entries for learn on portainer:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User learn may run the following commands on portainer:
    (ALL) /usr/bin/systemctl, /usr/bin/journalctl, /usr/bin/vim
```
>  **Explanation:**
>  + Bu komut, `tanju` kullanıcısının hangi `sudo` komutlarını çalıştırabileceğini listeler.
>  + `-l` Belirtilen kullanıcı(`-U`) için izin verilmiş ve yasaklanmış komutları listeler. Burada dikkat edilmesi gereken iki şekilde kullanıcı belirtilebiliyor olması; `-U` ve `-u` 
>  + `man sudo` sayfasında da belirtildiği üzere eğer `-l` parametresini kullanıldığında kullanıcı(`user`) belirtmek istendiğinde `-U` kullanılması söylenmektedir.

##### 4. sudoers Zafiyetleri:
+ `sudo visudo /etc/sudoers.d/tanju` dosyası üzerinde işlem yapılıyor.

###### Senaryo 1:
```sudoers
tanju ALL=(ALL)    /bin/bash                  
```
> **Explanation:**
> + Eğer `sudo` yetkisine `bash` kabuğunu verirsek `bash` ile dolaylı yoldan birden komuta erişim hakkı kazanacaktır. 

###### Senaryo 2:
```sudoers
tanju ALL=(ALL)    /home/tanju/tell_me.sh                # 1 
tanju ALL=(ALL)    /usr/bin/more /etc/ssh/ssh_config     # 2
```

**1. tell_me.sh**
```bash
#!/usr/bin/bash

echo "Merhaba Linux"
sudo -i
```
> **Explanation:**
> + Eğer vermiş olduğmuz kısıtlı bash script de `sudo -i` eklerse ve `sudo ./tell_me.sh` ile komutu çalıştırsa `root` kullanıcısına giriş yapacaktır.

**2. more komutu:**
```shell
$ sudo more /etc/ssh/ssh_config
```
> **Explanation:**
> + `more` komut ile açtığımızda önce `!` işaretine sonra `bash` yazıp `enter` bastığımızda `root` kullanıcısına giriş yapmış olacağız. 


### 4. Nasıl sudo Yetekileri Kazanılır?

###### 4.1. sudo grubuna dahil etme:
```shell
sudo usermod -aG <username>
```
> **Explanation:**

###### 4.2. sudoers ile:
```shell
$ EDITOR=vim sudo visudo /etc/sudoers.d/<username>
```

```sudoers
<username> ALL=(ALL)    ALL
```
> **Explanation:**

### Kaynak:
1. [Btk Akademi - siber guvenlikte linux isletim sistemleri]()