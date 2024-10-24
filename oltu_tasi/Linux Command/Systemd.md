#linux_commands 
> [!INFO] Bilgi:
> `systemd`'de bir **unit** (birim), sistemdeki çeşitli kaynakları ve hizmetleri yönetmek için kullanılan yapı taşıdır.
> Türleride mevcuttur. Örneğin; Unit dosyaları genellikle `/etc/systemd/system/`, `/usr/lib/systemd/system/` veya `/run/systemd/system/` dizinlerinde bulunur ve `.service`, `.socket`, `.device`, `.mount`, `.automount`, `.swap`, `.target`, `.path`, `.timer`, `.slice`, ve `.scope` gibi uzantılara sahiptir.

```
$ systemctl list-units
```

#### daemon-reload:
+ `systemctl daemon-reload`, Linux'ta systemd yönetim sistemi(systemd systemd manager) kullanıldığında daemon’lara ait yapılandırma(configuration) dosyalarının yeniden yüklenmesini sağlar.
+ Bu, tüm üreteçleri(generator) yeniden çalıştıracak (systemd.generator(7)'ye bakın), tüm birim(unit) dosyalarını yeniden yükleyecek ve tüm bağımlılık ağacını yeniden oluşturacaktır.aemon yeniden yüklenirken, systemd'nin kullanıcı yapılandırması adına dinlediği tüm soketler erişilebilir kalacaktır. (man systemctl)
+ 