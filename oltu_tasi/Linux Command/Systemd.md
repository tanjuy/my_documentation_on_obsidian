#linux_commands 

> [!INFO] Bilgi:
> `systemd`'de bir **unit** (birim), sistemdeki çeşitli kaynakları ve hizmetleri yönetmek için kullanılan yapı taşıdır.
> Türleride mevcuttur. Örneğin; Unit dosyaları genellikle `/etc/systemd/system/`, `/usr/lib/systemd/system/` veya `/run/systemd/system/` dizinlerinde bulunur ve `.service`, `.socket`, `.device`, `.mount`, `.automount`, `.swap`, `.target`, `.path`, `.timer`, `.slice`, ve `.scope` gibi uzantılara sahiptir.

```
$ systemctl list-units
```

## daemon-reload:
+ `systemctl daemon-reload`, Linux'ta systemd yönetim sistemi(systemd systemd manager) kullanıldığında daemon’lara ait yapılandırma(configuration) dosyalarının yeniden yüklenmesini sağlar.
+ Bu, tüm üreteçleri(generator) yeniden çalıştıracak (systemd.generator(7)'ye bakın), tüm birim(unit) dosyalarını yeniden yükleyecek ve tüm bağımlılık ağacını yeniden oluşturacaktır.aemon yeniden yüklenirken, systemd'nin kullanıcı yapılandırması adına dinlediği tüm soketler erişilebilir kalacaktır. (man systemctl)

#### status:
```
$ sudo systemctl status
```
> **Explanation:**
> + Tüm çalışan veya durdurulmuş hizmetler hakkında genel bilgi verir.

## systemd-analyze:

+ `systemd-analyze`, **systemd**'nin bir parçası olan ve sistem başlangıç sürecini analiz etmeye yarayan bir araçtır.
+  Sisteminizin açılış performansını inceleyebilir, servislerin başlangıç sürelerini görebilir ve olası sorunları tespit edebilirsiniz.

### Örnek 1: Temel Kullanım

```shell
systemd-analyze
```

```shell
Startup finished in 6.855s (kernel) + 18.126s (userspace) = 24.982s
graphical.target reached after 16.095s in userspace
```

> **Explanation:**


# 3. Systemctl Komutları

## 3.1. list-unit-files parametresi

`systemctl list-unit-files` komutu, sistemde yüklü olan tüm **unit dosyalarını** ve bunların **durumlarını (state)** listeler. Aktif olsun olmasın, sistemde tanınan tüm unit'leri gösterir.

```bash
sudo systemctl list-unit-files
```

Çıktı şu şekilde iki sütun halinde gelir:

```bash
UNIT FILE                                                                 STATE           PRESET
proc-sys-fs-binfmt_misc.automount                                         static          -
-.mount                                                                   generated       -
boot-efi.mount                                                            generated       -
boot.mount                                                                generated       -
dev-hugepages.mount                                                       static          -
dev-mqueue.mount                                                          static          -
proc-sys-fs-binfmt_misc.mount                                             disabled        disabled
sys-fs-fuse-connections.mount                                             static          -
...
```

**STATE Sütunundaki Olası Değerler**

- **enabled** – Sistem açılışında otomatik başlayacak şekilde ayarlanmış
- **disabled** – Yüklü ama açılışta otomatik başlamıyor
- **static** – Doğrudan etkinleştirilemez, başka bir unit tarafından tetiklenir (kendi `[Install]` bölümü yok)
- **masked** – Tamamen devre dışı bırakılmış, elle bile başlatılamaz (`/dev/null`'a bağlanmış)
- **generated** – Bir generator tarafından otomatik oluşturulmuş
- **transient** – Çalışma anında (runtime) oluşturulmuş, kalıcı değil
- **indirect** – Başka bir unit üzerinden dolaylı olarak etkinleştirilir

**Yararlı Filtreleme Seçenekleri**

```bash
# Sadece servisleri listele
systemctl list-unit-files --type=service

# Sadece "enabled" olanları göster
systemctl list-unit-files --state=enabled

# Sadece "disabled" olanları göster
systemctl list-unit-files --state=disabled

# İsimde arama yaparak filtrele (örn. network ile ilgili olanlar)
systemctl list-unit-files | grep network
```


> [!TIP]
> #### `systemctl list-units` ile Farkı
> Bu noktada karıştırılan bir başka komut var, ondan da bahsedeyim:
> + **`list-unit-files`** → Diskte yüklü olan _tüm_ unit dosyalarını gösterir (çalışıyor olsun olmasın)
> + **`list-units`** → Şu an **belleğe yüklenmiş ve aktif/etkin** olan unit'leri gösterir (yani sistemin şu anki çalışma durumunu yansıtır)



### 3.1.1. `--type=service` argümanı

