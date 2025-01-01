#### ssh Config Dosyası


## ssh Komutları:
### 1.ssh-copy-id:
```shell
$ ssh-copy-id -i /home/$USER/.ssh/id_rsa.pub user@IP_address 
```
> **Expalanation:**
> + ssh-copy-id, public SSH anahtarınızı uzak makinenin `authorized_keys` dosyasına kopyalayan bir scripttir. Yani şifresiz SSH girişini mümkün kılar.
> + `ssh-copy-id` komutu, yerel bilgisayarınızdaki genel SSH anahtarınızı (genellikle `~/.ssh/id_rsa.pub` veya `~/.ssh/id_ed25519.pub`) uzak sunucunun `~/.ssh/authorized_keys` dosyasına ekler.
> + `-i` parametresi: Eğer varsayılan `id_rsa.pub` dışında bir anahtar kullanıyorsanız, `-i` seçeneği ile belirtebilirsiniz:


> [!CAUTION]
> + `ssh-copy-id` komut *linux* ve *mac* işletim sistemlerinde mevcuttur. 
> + *Windows* işletim sistemlerinde yoktur.

### 2.ssh-keygen:
#### `-R` parametresi:

+ `ssh-keygen -R` komutu, **`known_hosts`** dosyasından bir ana bilgisayar (`host`) kaydını kaldırmak için kullanılır.
+ Bu, genellikle bir uzak sunucunun (`host`) anahtar bilgileri değiştiğinde veya bir bağlantı problemi yaşandığında kullanılır.
+ Aşağıdaki gibi mesaj alıyorsanız.
```shell
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
```

```shell
ssh-keygen -R 192.168.1.120
```

+ **`known_hosts` Dosyası Nedir?**
+ SSH istemcisi, her bağlantı kurduğu ana bilgisayarın (`host`) `public key`'ini **`~/.ssh/known_hosts`** dosyasına kaydeder.
+ Anahtar(`key`), bağlantının güvenilir olduğundan emin olmak için kullanılır. Eğer anahtar değişirse, SSH bir uyarı verir ve bağlantıyı engeller.


> [!WARNING]
> + Eğer bir ana bilgisayar özel bir port üzerinden bağlanıyorsa, port numarasını belirtmek gerekir:
> + Örneğin; `ssh-keygen -R [192.168.1.10]:2222` 
> + Burada, `192.168.1.10` adresindeki ve `2222` portundaki kayıt kaldırılır.

#### Manual Kullanımı:
+ `ssh-keygen -R` işlemini manuel olarak da yapabilirsiniz.

```shell
vim ~/.ssh/known_hosts
```

+ Hedef ana bilgisayarın (host) satırını bulun ve silin.
+ Kaydedin ve çıkın.
