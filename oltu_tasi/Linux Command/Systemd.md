#linux_commands 
> [!INFO] Bilgi:
> `systemd`'de bir **unit** (birim), sistemdeki çeşitli kaynakları ve hizmetleri yönetmek için kullanılan yapı taşıdır.
> Türleride mevcuttur. Örneğin; Unit dosyaları genellikle `/etc/systemd/system/`, `/usr/lib/systemd/system/` veya `/run/systemd/system/` dizinlerinde bulunur ve `.service`, `.socket`, `.device`, `.mount`, `.automount`, `.swap`, `.target`, `.path`, `.timer`, `.slice`, ve `.scope` gibi uzantılara sahiptir.

```
$ systemctl list-units
```

