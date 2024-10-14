#### ssh Config Dosyası


#### ssh-copy-id:
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



