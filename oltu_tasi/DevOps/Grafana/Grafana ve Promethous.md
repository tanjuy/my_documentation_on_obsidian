
# Kurulum 1: Bare Metal

+ **Makinde Adı:** 22.04.5 LTS (Jammy Jellyfish)
+ **Kurulacak Programlar:** Prometheus, Node Exporter, Pushgateway ve Grafana


> [!TIP]
> + Ubuntu versiyon hakkında bilgi almak için aşağıdaki komutu kullanabilirisiniz:
> ```shell
> cat /etc/os-release
> ```
> + Komut Çıktıs:
> ```shell
> PRETTY_NAME="Ubuntu 22.04.5 LTS"
> NAME="Ubuntu"
> VERSION_ID="22.04"
> VERSION="22.04.5 LTS (Jammy Jellyfish)"
> VERSION_CODENAME=jammy
> ID=ubuntu
> ID_LIKE=debian
> HOME_URL="https://www.ubuntu.com/"
> SUPPORT_URL="https://help.ubuntu.com/"
> BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
> PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
> UBUNTU_CODENAME=jammy
> ```

## 1. Adım:

### Promethous Kurulumu:

```shell
sudo useradd \
	--system \
	--no-create-home \
	--shell /bin/false prometheus
```

> + `--system` : Bir sistem hesabı oluşturur.
> + `--no-create-home`: Bir ev dizin yani klasörü oluşturmayacaktır. Kısa parametresi: `-M`
> + `--shell /bin/false` : Prometheus kullanıcısına girişi engeleyecektir.
> + **Sonuç:** Bu komut *Prometheus Kullanıcısı ve Prometheus Grup* oluşturacaktır.
> 	- `less /etc/passwd` ve `less /etc/group` komutları ile bu durumu teyit edebilirsiniz.


> [!TIP]
>+ Her servisin kendine ait kullanıcıya sahip olması iki amaca hizmet eder:  
> 	1. Hizmette bir sorun olması durumunda etkiyi azaltmak için bir güvenlik önlemidir. 
> 	2. Hangi kaynakların hangi hizmete ait olduğunu takip etmeyi kolaylaştırdığı için yönetimi basitleştirir.

---

```shell
wget https://github.com/prometheus/prometheus/releases/download/v2.53.5/prometheus-2.53.5.linux-amd64.tar.gz
```

> + Resmi indirme Sayfası: [Prometheus Download](https://prometheus.io/download/)
> + Eğer `wget` komut yok ise `sudo apt install wget` komut ile yükleme yapabilirsiniz.

---

```shell
tar -xvf prometheus-2.53.5.linux-amd64.tar.gz
```

> + Arşivden tüm prometheus dosyalarını çıkarıyoruz.

---

```shell
sudo mkdir -p /data /etc/prometheus
```

> + `/data` klasörünü bir diske bağlayabiliriz.
> + `/etc/prometheus` klasörü `prometheus configuration` dosyalarını muhafaza edecektir.

---

```shell
cd prometheus-2.53.5.linux-amd64
```

---

```shell
sudo cp -v prometheus promtool /usr/local/bin/
```

> + promtool yapılandırma dosyalarını ve Prometheus kurallarını kontrol etmek için kullanılır.

---

```shell
sudo cp -vr consoles/ console_libraries/ /etc/prometheus/
```

> + `console` kütüphanelerini `prometheus configuration` dizinine taşıyabiliriz.

---

```shell
sudo cp -v prometheus.yml /etc/prometheus/prometheus.yml
```

> + Temel prometheus konfigürasyon(`configuration`) dosya örneğini `/etc/prometheus/` dizinine taşıyoruz.

---

```shell
sudo chown -R prometheus:prometheus /etc/prometheus /data
```

> + İzin sorunlarından kaçınmak için `/etc/prometheus/` ve data dizini için doğru sahipliği ayarlamanız gerekir.

---

```shell
prometheus --version
```

> + Yukarıdaki komutu çalıştırarak Prometheus ikili dosyasını(`binary`) çalıştırabildiğinizi doğrulayın.

**Çıktı:**

```shell
prometheus, version 2.53.5 (branch: HEAD, revision: d344ea7bf4cc9e9e131a0318d10025982e9c4cc1)
  build user:       root@31e33add4c49
  build date:       20250630-10:18:05
  go version:       go1.23.10
  platform:         linux/amd64
  tags:             netgo,builtinassets,stringlabels
```

---

```shell
prometheus --help
```

> + Daha fazla bilgi ve konfigürasyon seçenekleri için Prometheus yardımını çalıştırın.
> + Bu seçeneklerden bazılarını servis tanımında(`prometheus.service`) kullanacağız.

**Çıkıt:**

```shell
usage: prometheus [<flags>]

The Prometheus monitoring server


Flags:
  -h, --[no-]help                Show context-sensitive help (also try --help-long and --help-man).
      --[no-]version             Show application version.
      --config.file="prometheus.yml"
                                 Prometheus configuration file path.
      --web.listen-address="0.0.0.0:9090"
                                 Address to listen on for UI, API, and telemetry.
      --auto-gomemlimit.ratio=0.9
                                 The ratio of reserved GOMEMLIMIT memory to the detected maximum
                                 container or system memory
      --web.config.file=""       [EXPERIMENTAL] Path to configuration file that can enable TLS or
                                 authentication.
      --web.read-timeout=5m      Maximum duration before timing out read of the request, and closing
                                 idle connections.
      --web.max-connections=512  Maximum number of simultaneous connections.
      --web.external-url=<URL>   The URL under which Prometheus is externally reachable (for example,
                                 if Prometheus is served via a reverse proxy). Used for generating
                                 relative and absolute links back to Prometheus itself. If the URL has
                                 a path portion, it will be used to prefix all HTTP endpoints served
                                 by Prometheus. If omitted, relevant URL components will be derived
                                 automatically.
      --web.route-prefix=<path>  Prefix for the internal routes of web endpoints. Defaults to path of
                                 --web.external-url.
      --web.user-assets=<path>   Path to static asset directory, available at /user.
      --[no-]web.enable-lifecycle
                                 Enable shutdown and reload via HTTP request.
      --[no-]web.enable-admin-api
                                 Enable API endpoints for admin control actions.
      --[no-]web.enable-remote-write-receiver
                                 Enable API endpoint accepting remote write requests.
      --web.console.templates="consoles"
                                 Path to the console template directory, available at /consoles.
      --web.console.libraries="console_libraries"
                                 Path to the console library directory.
      --web.page-title="Prometheus Time Series Collection and Processing Server"
                                 Document title of Prometheus instance.
      --web.cors.origin=".*"     Regex for CORS origin. It is fully anchored. Example:
                                 'https?://(domain1|domain2)\.com'
      --storage.tsdb.path="data/"
                                 Base path for metrics storage. Use with server mode only.
      --storage.tsdb.retention=STORAGE.TSDB.RETENTION
                                 [DEPRECATED] How long to retain samples in storage. This flag has been
                                 deprecated, use "storage.tsdb.retention.time" instead. Use with server
                                 mode only.
      --storage.tsdb.retention.time=STORAGE.TSDB.RETENTION.TIME
                                 How long to retain samples in storage. When this flag is set
                                 it overrides "storage.tsdb.retention". If neither this flag nor
                                 "storage.tsdb.retention" nor "storage.tsdb.retention.size" is set,
                                 the retention time defaults to 15d. Units Supported: y, w, d, h, m, s,
                                 ms. Use with server mode only.
      --storage.tsdb.retention.size=STORAGE.TSDB.RETENTION.SIZE
                                 Maximum number of bytes that can be stored for blocks. A unit is
                                 required, supported units: B, KB, MB, GB, TB, PB, EB. Ex: "512MB".
                                 Based on powers-of-2, so 1KB is 1024B. Use with server mode only.
      --[no-]storage.tsdb.no-lockfile
                                 Do not create lockfile in data directory. Use with server mode only.
      --storage.tsdb.head-chunks-write-queue-size=0
                                 Size of the queue through which head chunks are written to the disk to
                                 be m-mapped, 0 disables the queue completely. Experimental. Use with
                                 server mode only.
      --storage.agent.path="data-agent/"
                                 Base path for metrics storage. Use with agent mode only.
      --[no-]storage.agent.wal-compression
                                 Compress the agent WAL. Use with agent mode only.
      --storage.agent.retention.min-time=STORAGE.AGENT.RETENTION.MIN-TIME
                                 Minimum age samples may be before being considered for deletion when
                                 the WAL is truncated Use with agent mode only.
      --storage.agent.retention.max-time=STORAGE.AGENT.RETENTION.MAX-TIME
                                 Maximum age samples may be before being forcibly deleted when the WAL
                                 is truncated Use with agent mode only.
      --[no-]storage.agent.no-lockfile
                                 Do not create lockfile in data directory. Use with agent mode only.
      --storage.remote.flush-deadline=<duration>
                                 How long to wait flushing sample on shutdown or config reload.
      --storage.remote.read-sample-limit=5e7
                                 Maximum overall number of samples to return via the remote read
                                 interface, in a single query. 0 means no limit. This limit is ignored
                                 for streamed response types. Use with server mode only.
      --storage.remote.read-concurrent-limit=10
                                 Maximum number of concurrent remote read calls. 0 means no limit.
                                 Use with server mode only.
      --storage.remote.read-max-bytes-in-frame=1048576
                                 Maximum number of bytes in a single frame for streaming remote read
                                 response types before marshalling. Note that client might have limit
                                 on frame size as well. 1MB as recommended by protobuf by default.
                                 Use with server mode only.
      --rules.alert.for-outage-tolerance=1h
                                 Max time to tolerate prometheus outage for restoring "for" state of
                                 alert. Use with server mode only.
      --rules.alert.for-grace-period=10m
                                 Minimum duration between alert and restored "for" state. This is
                                 maintained only for alerts with configured "for" time greater than
                                 grace period. Use with server mode only.
      --rules.alert.resend-delay=1m
                                 Minimum amount of time to wait before resending an alert to
                                 Alertmanager. Use with server mode only.
      --rules.max-concurrent-evals=4
                                 Global concurrency limit for independent rules that can run
                                 concurrently. When set, "query.max-concurrency" may need to be adjusted
                                 accordingly. Use with server mode only.
      --alertmanager.notification-queue-capacity=10000
                                 The capacity of the queue for pending Alertmanager notifications.
                                 Use with server mode only.
      --query.lookback-delta=5m  The maximum lookback duration for retrieving metrics during expression
                                 evaluations and federation. Use with server mode only.
      --query.timeout=2m         Maximum time a query may take before being aborted. Use with server
                                 mode only.
      --query.max-concurrency=20
                                 Maximum number of queries executed concurrently. Use with server mode
                                 only.
      --query.max-samples=50000000
                                 Maximum number of samples a single query can load into memory. Note
                                 that queries will fail if they try to load more samples than this into
                                 memory, so this also limits the number of samples a query can return.
                                 Use with server mode only.
      --enable-feature= ...      Comma separated feature names to enable. Valid options: agent,
                                 auto-gomemlimit, exemplar-storage, expand-external-labels,
                                 memory-snapshot-on-shutdown, promql-per-step-stats,
                                 promql-experimental-functions, remote-write-receiver (DEPRECATED),
                                 extra-scrape-metrics, new-service-discovery-manager, auto-gomaxprocs,
                                 no-default-scrape-port, native-histograms, otlp-write-receiver,
                                 created-timestamp-zero-ingestion, concurrent-rule-eval. See
                                 https://prometheus.io/docs/prometheus/latest/feature_flags/ for more
                                 details.
      --log.level=info           Only log messages with the given severity or above. One of: [debug,
                                 info, warn, error]
      --log.format=logfmt        Output format of log messages. One of: [logfmt, json]
```

---

```shell
sudo vim /etc/systemd/system/prometheus.service
```

> + Linux işletim sistemleri için bir sistem ve servis yöneticisi olan systemd'yi kullanacağız.


**prometheus.service:**

```systemd
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=prometheus
Group=prometheus
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/prometheus \
	--config.file=/etc/prometheus/prometheus.yml \
	--storage.tsdb.path=/data \
	--web.console.templates=/etc/prometheus/consoles \
	--web.console.libraries=/etc/prometheus/console_libraries \
	--web.listen-address=0.0.0.0:9090 \
	--web.enable-lifecycle

[Install]
WantedBy=multi-user.target
```

> [!NOTE]
> 1. `Restart` :  
> 	+ Hizmet süreci sonlandırıldığında, sonlandırıldığında veya zaman aşımına ulaşıldığında hizmetin yeniden başlatılıp başlatılmayacağını yapılandırır.
> 2. `Restart=on-failure` :
> 	+ Servis **sadece başarısız olduğunda** (yani sıfır olmayan bir çıkış kodu ile kapandığında) otomatik olarak yeniden başlatılacaktır.
> 	+ Servis normal şekilde sonlandırıldığında (örneğin `systemctl stop` komutu ile veya başarılı çıkış kodu ile) yeniden başlatılmayacaktır.
> 3. systemd'de `Restart` direktifinin diğer olası değerleri:
> 	+ `no`: Servis asla yeniden başlatılmaz (varsayılan)
> 	+ `always`: Servis her durumda yeniden başlatılır
> 	+ `on-success`: Sadece başarılı çıkış durumunda yeniden başlatılır
> 	+ `on-abnormal`: Anormal sonlanmalarda (sinyal ile öldürme, zaman aşımı vb.) yeniden başlatılır
> 	+ `on-watchdog`: Watchdog zaman aşımında yeniden başlatılır.
> 	+ `on-abort`: Sadece anormal sonlanma sinyali alındığında yeniden başlatılır


> [!NOTE]
> 1. `RestartSec=5` : 
> 	+ 5 saniye bekledikten sonra yeniden başlatılır. Yani `Restart=` komutu çalıştırılır.


> [!NOTE]
> 1. `User` ve `Group`, 
> 	+ systemd servis dosyalarında bir servisin hangi kullanıcı ve grup altında çalışacağını belirten temel direktiflerdir.
> 2. `User` Direktifi:
> 	+ **Tanım**: Servisin çalışacağı işletim sistemi kullanıcısını belirtir
> 	+ **Kullanım Amacı**: Servisleri root olmayan kullanıcılarla çalıştırarak güvenliği artırmak
> 3. `Group` Direktifi:
> 	+ **Tanım**: Servisin çalışacağı işletim sistemi grubunu belirtir.
> 	+ **Kullanım Amacı**: Ek grup izinleri vermek veya servis erişimini sınırlamak
> 4. **Varsayılan Değer**: Belirtilmezse servis root kullanıcısı olarak çalışır


> [!NOTE]
> 1. `-config.file=/etc/prometheus/prometheus.yml`
> 	+ **Açıklama**: Prometheus'un ana yapılandırma dosyasının yolunu belirtir.
> 	+ **Detaylar**:
> 		- Hedefleri (scrape targets), scrape aralıkları ve kurallar bu dosyada tanımlanır.
> 		- Varsayılan olarak `prometheus.yml` aranır, ancak bu parametre ile özel bir yol belirtilebilir.
> 2.  `--storage.tsdb.path=/data`
> 	+ **Açıklama**: Zaman serisi verilerinin (TSDB) depolanacağı dizini belirtir.
> 	+ **Detaylar**:
> 		- Prometheus verilerini bu dizinde saklar.
> 		- Disk alanı tükenirse Prometheus çalışmayı durdurabilir.
> 		- SSD kullanımı performansı önemli ölçüde artırır.
> 3. `--web.console.templates=/etc/prometheus/consoles`
> 	+  **Açıklama**: Konsol şablonlarının bulunduğu dizin
> 	+ **Detaylar**:
> 		- Prometheus web arayüzündeki konsol şablonlarını içerir.
> 		- HTML ve JavaScript dosyalarından oluşur.
> 		- Özel paneller oluşturmak için kullanılabilir
> 4.  `--web.console.libraries=/etc/prometheus/console_libraries`
> 	+ **Açıklama**: Konsol şablonları tarafından kullanılan JavaScript kütüphanelerinin dizini
> 	+ **Detaylar**:
> 		- Konsol şablonlarının kullandığı ortak JS fonksiyonlarını içerir.
> 		- Genellikle `console_templates` ile birlikte kullanılır
> 5. `--web.listen-address=0.0.0.0:9090`
> 	+ **Açıklama**: Prometheus web arayüzünün dinleyeceği adres ve port
> 	+ **Detaylar**:
> 		-  `0.0.0.0` tüm ağ arabirimlerinde dinleme yapacağını belirtir.
> 		- `9090` varsayılan port numarasıdır
> 		- Güvenlik için belirli bir IP ile sınırlandırılabilir (örn. `127.0.0.1:9090`)
> 		- İstekleri Prometheus'a yönlendirmek için nginx gibi bir proxy'niz olabilir.
> 6. `--web.enable-lifecycle`
> 	+ **Açıklama**: HTTP API üzerinden yapılandırmanın yeniden yüklenmesine ve Prometheus'un yeniden başlatılmasına izin verir
> 	+ **Detaylar**:
> 		- `POST /-/reload` endpoint'ini aktif eder.
> 		- Yapılandırma değişikliklerini yeniden başlatmadan uygulamayı sağlar.
> 		- **Güvenlik Notu**: Bu özellik dikkatle kullanılmalıdır, çünkü API'ye erişimi olan herkes Prometheus'u yeniden yükleyebilir.
> 7. `--storage.tsdb.retention.time`
> 	+ Veri saklama süresini belirtir (örn. `15d` = 15 gün)


```shell
sudo systemctl enable prometheus.service
```

> + Makine her yeniden başlatıldığında prometheus programın tekrar başlaması için `systemctl enable` komutunu kullanıyoruz.

```shell
sudo systemctl start prometheus.service
```

> + Prometheus programın arka tarafta başlaması için `systemctl start` komutunu çalıştırıyoruz.

> [!TIP]
> + `enable` ve `start` komutlarını aynı anda yapmak için;
> ```shell
> sudo systemctl enable --now prometheus.service
> ```


```shell
sudo systemctl status prometheus.service
```

> + `prometheus` programını düzgün çalışıp çalışmadığını teyit ediyoruz.

---

```shell
journalctl -u prometheus -f --no-pager
```

> + Bu komut, systemd journal (sistem günlükleri) içinde Prometheus servisine ait logları görüntülemek için kullanılır.


> [!NOTE]
> 1. `journalctl` : - systemd'nin günlük yönetim aracı ve sistem ve servis loglarını görüntüler.
> 2. `-u prometheus`
> 	+ `--unit=prometheus` kısaltması
> 	+ Sadece "prometheus.service" birimine ait logları gösterir.
> 	+ Servis adını belirtir (örneğin: `prometheus`, `nginx`, `postgresql`)
> 3. `-f`
> 	+ `--follow` kısaltması
> 	+ Logları gerçek zamanlı olarak takip etmeyi sağlar (tail -f benzeri)
> 	+ Yeni oluşan log mesajlarını anında gösterir.
> 4. `--no-pager`
> 	+ Çıktıyı sayfalandırıcı (less/more) olmadan doğrudan terminale yazdırır.
> 	+ Scriptlerde veya pipe işlemlerinde kullanışlıdır

**Tarayıcıda:**

![Prometheus Tarayıcı](./Pictures/prometheus.png)

> + Tarayıcı da `http://192.168.1.129:9090` adresine gidiyoruz.
> + Ubuntu sunucusun IP adresini kullanıyoruz.


![prometheus_target](./Pictures/prometheus_target.png)

> + Eğer targets'ı tıklarsak sadece bir tane target(`Prometheus target`) görünecektir.
> + Varsayılan olarak her 15 saniyede kendisinden veri toplayacaktır.


> [!NOTE]
>  **Prometheus Tanımı:**
> + **Scrape**, Prometheus’un belirli aralıklarla hedef sistemlerin (target'ların) `/metrics` endpoint’lerine HTTP isteği göndererek **metrik verilerini çekmesi** işlemidir.

## 2. Adım:

+ CPU yükü ve disk I/O gibi Linux sistem metriklerini toplamak için Node Exporter'ı kurup yapılandıracağız.
+ Node Exporter bunları Prometheus tarzı metrikler olarak çıktılar üretecektir.

### Node Exporter Kurulumu:

```shell
sudo useradd \
	--system \
	--no-create-home \
	--shell /bin/false node_exporter
```

> + 1. Adımda Prometheus ile benzer şekilde kullanıcı oluşturduk.

---

```shell
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.1/node_exporter-1.9.1.linux-amd64.tar.gz
```

> + Resmi indirme Sayfası: [Node_Exporter Download](https://prometheus.io/download/)
> + Eğer `wget` komut yok ise `sudo apt install wget` komut ile yükleme yapabilirsiniz.

---

```shell
tar -xvf node_exporter-1.9.1.linux-amd64.tar.gz
```

---

```shell
sudo mv -v node_exporter-1.9.1.linux-amd64/node_exporter \
	/usr/local/bin/
```

---

```shell
node_exporter --help
```

> + `node_exporter` ikili dosyanın düzgün yüklenip yüklenmediğini teyit ediyoruz.

**Çıktısı:**

```shell
usage: node_exporter [<flags>]

Flags:
  -h, --[no-]help                Show context-sensitive help (also try --help-long and --help-man).
      --collector.arp.device-include=COLLECTOR.ARP.DEVICE-INCLUDE
                                 Regexp of arp devices to include (mutually exclusive to
                                 device-exclude).
      --collector.arp.device-exclude=COLLECTOR.ARP.DEVICE-EXCLUDE
                                 Regexp of arp devices to exclude (mutually exclusive to
                                 device-include).
      --[no-]collector.arp.netlink
                                 Use netlink to gather stats instead of /proc/net/arp.
      --[no-]collector.bcache.priorityStats
                                 Expose expensive priority stats.
      --[no-]collector.cpu.guest
                                 Enables metric node_cpu_guest_seconds_total
      --[no-]collector.cpu.info  Enables metric cpu_info
      --collector.cpu.info.flags-include=COLLECTOR.CPU.INFO.FLAGS-INCLUDE
                                 Filter the `flags` field in cpuInfo with a value that must be a regular
                                 expression
      --collector.cpu.info.bugs-include=COLLECTOR.CPU.INFO.BUGS-INCLUDE
                                 Filter the `bugs` field in cpuInfo with a value that must be a regular
                                 expression
      --collector.diskstats.device-exclude="^(z?ram|loop|fd|(h|s|v|xv)d[a-z]|nvme\\d+n\\d+p)\\d+$"
                                 Regexp of diskstats devices to exclude (mutually exclusive to
                                 device-include).
      --collector.diskstats.device-include=COLLECTOR.DISKSTATS.DEVICE-INCLUDE
                                 Regexp of diskstats devices to include (mutually exclusive to
                                 device-exclude).
      --collector.ethtool.device-include=COLLECTOR.ETHTOOL.DEVICE-INCLUDE
                                 Regexp of ethtool devices to include (mutually exclusive to
                                 device-exclude).
      --collector.ethtool.device-exclude=COLLECTOR.ETHTOOL.DEVICE-EXCLUDE
                                 Regexp of ethtool devices to exclude (mutually exclusive to
                                 device-include).
      --collector.ethtool.metrics-include=".*"
                                 Regexp of ethtool stats to include.
      --collector.filesystem.mount-points-exclude="^/(dev|proc|run/credentials/.+|sys|var/lib/docker/.+|var/lib/containers/storage/.+)($|/)"
                                 Regexp of mount points to exclude for filesystem collector. (mutually
                                 exclusive to mount-points-include)
      --collector.filesystem.mount-points-include=COLLECTOR.FILESYSTEM.MOUNT-POINTS-INCLUDE
                                 Regexp of mount points to include for filesystem collector. (mutually
                                 exclusive to mount-points-exclude)
      --collector.filesystem.fs-types-exclude="^(autofs|binfmt_misc|bpf|cgroup2?|configfs|debugfs|devpts|devtmpfs|fusectl|hugetlbfs|iso9660|mqueue|nsfs|overlay|proc|procfs|pstore|rpc_pipefs|securityfs|selinuxfs|squashfs|sysfs|tracefs)$"
                                 Regexp of filesystem types to exclude for filesystem collector.
                                 (mutually exclusive to fs-types-include)
      --collector.filesystem.fs-types-include=COLLECTOR.FILESYSTEM.FS-TYPES-INCLUDE
                                 Regexp of filesystem types to exclude for filesystem collector.
                                 (mutually exclusive to fs-types-exclude)
      --collector.hwmon.chip-include=COLLECTOR.HWMON.CHIP-INCLUDE
                                 Regexp of hwmon chip to include (mutually exclusive to device-exclude).
      --collector.hwmon.chip-exclude=COLLECTOR.HWMON.CHIP-EXCLUDE
                                 Regexp of hwmon chip to exclude (mutually exclusive to device-include).
      --collector.hwmon.sensor-include=COLLECTOR.HWMON.SENSOR-INCLUDE
                                 Regexp of hwmon sensor to include (mutually exclusive to
                                 sensor-exclude).
      --collector.hwmon.sensor-exclude=COLLECTOR.HWMON.SENSOR-EXCLUDE
                                 Regexp of hwmon sensor to exclude (mutually exclusive to
                                 sensor-include).
      --collector.interrupts.name-include=COLLECTOR.INTERRUPTS.NAME-INCLUDE
                                 Regexp of interrupts name to include (mutually exclusive to
                                 --collector.interrupts.name-exclude).
      --collector.interrupts.name-exclude=COLLECTOR.INTERRUPTS.NAME-EXCLUDE
                                 Regexp of interrupts name to exclude (mutually exclusive to
                                 --collector.interrupts.name-include).
      --[no-]collector.interrupts.include-zeros
                                 Include interrupts that have a zero value
      --collector.ipvs.backend-labels="local_address,local_port,remote_address,remote_port,proto,local_mark"
                                 Comma separated list for IPVS backend stats labels.
      --collector.netclass.ignored-devices="^$"
                                 Regexp of net devices to ignore for netclass collector.
      --[no-]collector.netclass.ignore-invalid-speed
                                 Ignore devices where the speed is invalid. This will be the default
                                 behavior in 2.x.
      --[no-]collector.netclass.netlink
                                 Use netlink to gather stats instead of /proc/net/dev.
      --[no-]collector.netclass_rtnl.with-stats
                                 Expose the statistics for each network device, replacing netdev
                                 collector.
      --collector.netdev.device-include=COLLECTOR.NETDEV.DEVICE-INCLUDE
                                 Regexp of net devices to include (mutually exclusive to
                                 device-exclude).
      --collector.netdev.device-exclude=COLLECTOR.NETDEV.DEVICE-EXCLUDE
                                 Regexp of net devices to exclude (mutually exclusive to
                                 device-include).
      --[no-]collector.netdev.address-info
                                 Collect address-info for every device
      --[no-]collector.netdev.enable-detailed-metrics
                                 Use (incompatible) metric names that provide more detailed stats on
                                 Linux
      --[no-]collector.netdev.netlink
                                 Use netlink to gather stats instead of /proc/net/dev.
      --[no-]collector.netdev.label-ifalias
                                 Add ifAlias label
      --collector.netstat.fields="^(.*_(InErrors|InErrs)|Ip_Forwarding|Ip(6|Ext)_(InOctets|OutOctets)|Icmp6?_(InMsgs|OutMsgs)|TcpExt_(Listen.*|Syncookies.*|TCPSynRetrans|TCPTimeouts|TCPOFOQueue|TCPRcvQDrop)|Tcp_(ActiveOpens|InSegs|OutSegs|OutRsts|PassiveOpens|RetransSegs|CurrEstab)|Udp6?_(InDatagrams|OutDatagrams|NoPorts|RcvbufErrors|SndbufErrors))$"
                                 Regexp of fields to return for netstat collector.
      --collector.ntp.server="127.0.0.1"
                                 NTP server to use for ntp collector
      --collector.ntp.server-port=123
                                 UDP port number to connect to on NTP server
      --collector.ntp.protocol-version=4
                                 NTP protocol version
      --[no-]collector.ntp.server-is-local
                                 Certify that collector.ntp.server address is not a public ntp server
      --collector.ntp.ip-ttl=1   IP TTL to use while sending NTP query
      --collector.ntp.max-distance=3.46608s
                                 Max accumulated distance to the root
      --collector.ntp.local-offset-tolerance=1ms
                                 Offset between local clock and local ntpd time to tolerate
      --path.procfs="/proc"      procfs mountpoint.
      --path.sysfs="/sys"        sysfs mountpoint.
      --path.rootfs="/"          rootfs mountpoint.
      --path.udev.data="/run/udev/data"
                                 udev data path.
      --collector.perf.cpus=""   List of CPUs from which perf metrics should be collected
      --collector.perf.tracepoint=COLLECTOR.PERF.TRACEPOINT ...
                                 perf tracepoint that should be collected
      --[no-]collector.perf.disable-hardware-profilers
                                 disable perf hardware profilers
      --collector.perf.hardware-profilers=COLLECTOR.PERF.HARDWARE-PROFILERS ...
                                 perf hardware profilers that should be collected
      --[no-]collector.perf.disable-software-profilers
                                 disable perf software profilers
      --collector.perf.software-profilers=COLLECTOR.PERF.SOFTWARE-PROFILERS ...
                                 perf software profilers that should be collected
      --[no-]collector.perf.disable-cache-profilers
                                 disable perf cache profilers
      --collector.perf.cache-profilers=COLLECTOR.PERF.CACHE-PROFILERS ...
                                 perf cache profilers that should be collected
      --collector.powersupply.ignored-supplies="^$"
                                 Regexp of power supplies to ignore for powersupplyclass collector.
      --collector.qdisc.fixtures=""
                                 test fixtures to use for qdisc collector end-to-end testing
      --collector.qdisc.device-include=COLLECTOR.QDISC.DEVICE-INCLUDE
                                 Regexp of qdisc devices to include (mutually exclusive to
                                 device-exclude).
      --collector.qdisc.device-exclude=COLLECTOR.QDISC.DEVICE-EXCLUDE
                                 Regexp of qdisc devices to exclude (mutually exclusive to
                                 device-include).
      --[no-]collector.rapl.enable-zone-label
                                 Enables service unit metric unit_start_time_seconds
      --collector.runit.servicedir="/etc/service"
                                 Path to runit service directory.
      --collector.slabinfo.slabs-include=".*"
                                 Regexp of slabs to include in slabinfo collector.
      --collector.slabinfo.slabs-exclude=""
                                 Regexp of slabs to exclude in slabinfo collector.
      --[no-]collector.stat.softirq
                                 Export softirq calls per vector
      --collector.supervisord.url="http://localhost:9001/RPC2"
                                 XML RPC endpoint. ($SUPERVISORD_URL)
      --collector.sysctl.include=COLLECTOR.SYSCTL.INCLUDE ...
                                 Select sysctl metrics to include
      --collector.sysctl.include-info=COLLECTOR.SYSCTL.INCLUDE-INFO ...
                                 Select sysctl metrics to include as info metrics
      --collector.systemd.unit-include=".+"
                                 Regexp of systemd units to include. Units must both match include and
                                 not match exclude to be included.
      --collector.systemd.unit-exclude=".+\\.(automount|device|mount|scope|slice)"
                                 Regexp of systemd units to exclude. Units must both match include and
                                 not match exclude to be included.
      --[no-]collector.systemd.enable-task-metrics
                                 Enables service unit tasks metrics unit_tasks_current and
                                 unit_tasks_max
      --[no-]collector.systemd.enable-restarts-metrics
                                 Enables service unit metric service_restart_total
      --[no-]collector.systemd.enable-start-time-metrics
                                 Enables service unit metric unit_start_time_seconds
      --collector.tapestats.ignored-devices="^$"
                                 Regexp of devices to ignore for tapestats.
      --collector.textfile.directory= ...
                                 Directory to read text files with metrics from, supports glob matching.
                                 (repeatable)
      --collector.vmstat.fields="^(oom_kill|pgpg|pswp|pg.*fault).*"
                                 Regexp of fields to return for vmstat collector.
      --collector.wifi.fixtures=""
                                 test fixtures to use for wifi collector metrics
      --[no-]collector.arp       Enable the arp collector (default: enabled).
      --[no-]collector.bcache    Enable the bcache collector (default: enabled).
      --[no-]collector.bonding   Enable the bonding collector (default: enabled).
      --[no-]collector.btrfs     Enable the btrfs collector (default: enabled).
      --[no-]collector.buddyinfo
                                 Enable the buddyinfo collector (default: disabled).
      --[no-]collector.cgroups   Enable the cgroups collector (default: disabled).
      --[no-]collector.conntrack
                                 Enable the conntrack collector (default: enabled).
      --[no-]collector.cpu       Enable the cpu collector (default: enabled).
      --[no-]collector.cpu_vulnerabilities
                                 Enable the cpu_vulnerabilities collector (default: disabled).
      --[no-]collector.cpufreq   Enable the cpufreq collector (default: enabled).
      --[no-]collector.diskstats
                                 Enable the diskstats collector (default: enabled).
      --[no-]collector.dmi       Enable the dmi collector (default: enabled).
      --[no-]collector.drbd      Enable the drbd collector (default: disabled).
      --[no-]collector.drm       Enable the drm collector (default: disabled).
      --[no-]collector.edac      Enable the edac collector (default: enabled).
      --[no-]collector.entropy   Enable the entropy collector (default: enabled).
      --[no-]collector.ethtool   Enable the ethtool collector (default: disabled).
      --[no-]collector.fibrechannel
                                 Enable the fibrechannel collector (default: enabled).
      --[no-]collector.filefd    Enable the filefd collector (default: enabled).
      --[no-]collector.filesystem
                                 Enable the filesystem collector (default: enabled).
      --[no-]collector.hwmon     Enable the hwmon collector (default: enabled).
      --[no-]collector.infiniband
                                 Enable the infiniband collector (default: enabled).
      --[no-]collector.interrupts
                                 Enable the interrupts collector (default: disabled).
      --[no-]collector.ipvs      Enable the ipvs collector (default: enabled).
      --[no-]collector.ksmd      Enable the ksmd collector (default: disabled).
      --[no-]collector.lnstat    Enable the lnstat collector (default: disabled).
      --[no-]collector.loadavg   Enable the loadavg collector (default: enabled).
      --[no-]collector.logind    Enable the logind collector (default: disabled).
      --[no-]collector.mdadm     Enable the mdadm collector (default: enabled).
      --[no-]collector.meminfo   Enable the meminfo collector (default: enabled).
      --[no-]collector.meminfo_numa
                                 Enable the meminfo_numa collector (default: disabled).
      --[no-]collector.mountstats
                                 Enable the mountstats collector (default: disabled).
      --[no-]collector.netclass  Enable the netclass collector (default: enabled).
      --[no-]collector.netdev    Enable the netdev collector (default: enabled).
      --[no-]collector.netstat   Enable the netstat collector (default: enabled).
      --[no-]collector.network_route
                                 Enable the network_route collector (default: disabled).
      --[no-]collector.nfs       Enable the nfs collector (default: enabled).
      --[no-]collector.nfsd      Enable the nfsd collector (default: enabled).
      --[no-]collector.ntp       Enable the ntp collector (default: disabled).
      --[no-]collector.nvme      Enable the nvme collector (default: enabled).
      --[no-]collector.os        Enable the os collector (default: enabled).
      --[no-]collector.perf      Enable the perf collector (default: disabled).
      --[no-]collector.powersupplyclass
                                 Enable the powersupplyclass collector (default: enabled).
      --[no-]collector.pressure  Enable the pressure collector (default: enabled).
      --[no-]collector.processes
                                 Enable the processes collector (default: disabled).
      --[no-]collector.qdisc     Enable the qdisc collector (default: disabled).
      --[no-]collector.rapl      Enable the rapl collector (default: enabled).
      --[no-]collector.runit     Enable the runit collector (default: disabled).
      --[no-]collector.schedstat
                                 Enable the schedstat collector (default: enabled).
      --[no-]collector.selinux   Enable the selinux collector (default: enabled).
      --[no-]collector.slabinfo  Enable the slabinfo collector (default: disabled).
      --[no-]collector.sockstat  Enable the sockstat collector (default: enabled).
      --[no-]collector.softirqs  Enable the softirqs collector (default: disabled).
      --[no-]collector.softnet   Enable the softnet collector (default: enabled).
      --[no-]collector.stat      Enable the stat collector (default: enabled).
      --[no-]collector.supervisord
                                 Enable the supervisord collector (default: disabled).
      --[no-]collector.sysctl    Enable the sysctl collector (default: disabled).
      --[no-]collector.systemd   Enable the systemd collector (default: disabled).
      --[no-]collector.tapestats
                                 Enable the tapestats collector (default: enabled).
      --[no-]collector.tcpstat   Enable the tcpstat collector (default: disabled).
      --[no-]collector.textfile  Enable the textfile collector (default: enabled).
      --[no-]collector.thermal_zone
                                 Enable the thermal_zone collector (default: enabled).
      --[no-]collector.time      Enable the time collector (default: enabled).
      --[no-]collector.timex     Enable the timex collector (default: enabled).
      --[no-]collector.udp_queues
                                 Enable the udp_queues collector (default: enabled).
      --[no-]collector.uname     Enable the uname collector (default: enabled).
      --[no-]collector.vmstat    Enable the vmstat collector (default: enabled).
      --[no-]collector.watchdog  Enable the watchdog collector (default: enabled).
      --[no-]collector.wifi      Enable the wifi collector (default: disabled).
      --[no-]collector.xfrm      Enable the xfrm collector (default: disabled).
      --[no-]collector.xfs       Enable the xfs collector (default: enabled).
      --[no-]collector.zfs       Enable the zfs collector (default: enabled).
      --[no-]collector.zoneinfo  Enable the zoneinfo collector (default: disabled).
      --web.telemetry-path="/metrics"
                                 Path under which to expose metrics.
      --[no-]web.disable-exporter-metrics
                                 Exclude metrics about the exporter itself (promhttp_*, process_*,
                                 go_*).
      --web.max-requests=40      Maximum number of parallel scrape requests. Use 0 to disable.
      --[no-]collector.disable-defaults
                                 Set all collectors to disabled by default.
      --runtime.gomaxprocs=1     The target number of CPUs Go will run on (GOMAXPROCS) ($GOMAXPROCS)
      --[no-]web.systemd-socket  Use systemd socket activation listeners instead of port listeners
                                 (Linux only).
      --web.listen-address=:9100 ...
                                 Addresses on which to expose metrics and web interface. Repeatable
                                 for multiple addresses. Examples: `:9100` or `[::1]:9100` for http,
                                 `vsock://:9100` for vsock
      --web.config.file=""       Path to configuration file that can enable TLS or authentication. See:
                                 https://github.com/prometheus/exporter-toolkit/blob/master/docs/web-configuration.md
      --log.level=info           Only log messages with the given severity or above. One of: [debug,
                                 info, warn, error]
      --log.format=logfmt        Output format of log messages. One of: [logfmt, json]
      --[no-]version             Show application version.

```

> + `Node Exporter`'ın etkinleştirebileceğimiz birçok eklentisi var.
> + Bu kurulumda `--collector.logind` eklentiyi etkinleştireceğiz.

---

```shell
sudo vim /etc/systemd/system/node_exporter.service
```

**node_exporter.service:**

```systemd
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=node_exporter
Group=node_exporter
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/node_exporter \
	--collector.logind

[Install]
WantedBy=multi-user.target
```


> [!NOTE]
> 1. `node_exporter`'da `--collector.logind` parametresi, systemd'nin **logind** hizmetiyle ilgili metrikleri toplamayı sağlayan bir kolektördür.
> 2. **Temel Bilgiler:**
> 	- Kolektör Adı: `logind`
> 	- Bağımlılık: Systemd-logind servisinin çalışıyor olması gerekir (`dbus` üzerinden iletişim kurar)
> 3. **Topladığı Metrikler:**
> 	1. Oturum Bilgileri:
> 		+ Oturum durumları (aktif, arka planda çalışan vb.)
> 	2. Kullanıcı Bilgileri:
> 		+ Her kullanıcı için oturum sayıları
> 		+ Kullanıcı oturum türleri (graphical, tty vb.)
> 	3. Sistem Durumu:
> 		+ Sistemin askıya alınma/uyku durumları
> 		+ Yeniden başlatma/kapatma işlemleri


> [!NOTE]
> 1. **Genellikle bu direktifler birlikte kullanılır:**
> 	- `StartLimitBurst`: Zaman aralığı içinde izin verilen maksimum başlatma sayısı
> 	- `StartLimitIntervalSec`: Bu sayının hangi zaman aralığında geçerli olduğu (saniye cinsinden)
> 2. **Örnek:**
> 	- `StartLimitIntervalSec=10s` (10 saniye)
> 	- `StartLimitBurst=5` (5 deneme)
> 3. **Örnek Açıklaması:**
> 	- 10 sanide içerisinde en fazla 5 kez yeniden başlatılabilir.
> 	- `6.` başlatma denemesi yapıldığında, sistem loglarında  `start request repeated too quickly` hatası görülür.
> 4. **Limit Aşıldığında:**
> 	- Servis artık başlatılmaz.
> 	- `systemctl status` çıktısında "start-limit-hit" hatası görünür.
> 	- Servisi tekrar çalıştırabilmek için:
> ```shell
> sudo systemctl reset-failed servis-adi.service
> ```


```shell
sudo systemctl enable node_exporter.service
```

```shell
sudo systemctl start node_exporter.service
```

```shell
sudo systemctl status node node_exporter.service
```

```shell
sudo vim /etc/prometheus/prometheus.yml
```

```yml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]


  - job_name: node_export                   # <----
    static_configs:
      - targets: ["localhost:9100"]
```


```shell
promtool check config /etc/prometheus/prometheus.yml
```

```shell
curl -X POST http://localhost:9090/-/reload
```

## Grafana:

```shell
sudo apt-get install -y apt-transport-https software-properties-common wget
```

```shell
sudo mkdir -p /etc/apt/keyrings/
```

```shell
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

+ stable

```shell
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

+ Beta

```shell
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```



```shell
# Updates the list of available packages
sudo apt-get update
```

```shell
# Installs the latest OSS release:
sudo apt-get install grafana
```

```shell
# Installs the latest Enterprise release:
sudo apt-get install grafana-enterprise
```

```shell
sudo systemctl enable grafana-server
```

```shell
sudo systemctl start grafana-server
```

```shell
sudo vim /etc/grafana/provisioning/datasources/datasources/datasources.yaml
```

**datasources.yaml**

```yaml
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
    url: http://localhost:9090
    isDefault: true
```


```shell
sudo systemctl restart grafana-server
```


## Pushgateway:

```shell
sudo useradd \
	--system \
	--no-create-home \
	--shell /bin/false pushgateway
```

```shell
wget https://github.com/prometheus/pushgateway/releases/download/v1.11.1/pushgateway-1.11.1.linux-amd64.tar.gz
```

```shell
tar -xvf pushgateway-1.11.1.linux-amd64.tar.gz
```

```shell
sudo cp -v pushgateway-1.11.1.linux-amd64/pushgateway /usr/local/bin
```

```shell
sudo vim /etc/systemd/system/pushgateway.service
```

```systemd
[Unit]
Description=Pushgateway
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=pushgateway
Group=pushgateway
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/pushgateway

[Install]
WantedBy=multi-user.target
```


```shell
sudo systemctl enable pushgateway.service
```

```shell
sudo systemctl start pushgateway.service
```

```shell
sudo vim /etc/prometheus/prometheus.yml
```

```yaml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]


  - job_name: node_export
    static_configs:
      - targets: ["localhost:9100"]


  - job_name: pushgateway           # <<---
    honor_labels: true
    static_configs:
      - targets: ["localhost:9091"]
```

```shell
promtool check config /etc/prometheus/prometheus.yml
```

```shell
curl -X POST http://localhost:9090/-/reload
```

```shell
echo "jenkins_job_duration_seconds 15.98" | curl --data-binary @- http://localhost:9091/metrics/job/backup
```

## Promethous Temel Auth:

```shell
sudo apt-get -y install python3-bcrypt
```

**generate_password.py:**

```python
import getpass
import bcrypt

password = getpass.getpass("password: ")
hashed_password = bcrypt.hashpw(
	password.encode("utf-8"), bcrypt.gensalt()
)
print(hashed_password.decode())
```

```shell
python3 generate_password.py
```

```shell
sudo vim /etc/prometheus/web.yml
```

```yaml
basic_auth_users:
	admin: # generate_password.py hash çıktısı
```

```shell
sudo vim /etc/systemd/system/prometheus.service
```

```yml
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=prometheus
Group=prometheus
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/prometheus \
	--config.file=/etc/prometheus/prometheus.yml \
	--storage.tsdb.path=/data \
	--web.console.templates=/etc/prometheus/consoles \
	--web.console.libraries=/etc/prometheus/console_libraries \
	--web.listen-address=0.0.0.0:9090 \
	--web.enable-lifecycle \
	--web.config.file=/etc/prometheus/web.yml

[Install]
WantedBy=multi-user.target
```

```shell
sudo systemctl daemon-reload
```

```shell
sudo systemctl restart prometheus.service
```

```shell
sudo vim /etc/grafana/provisioning/datasources/datasources.yml
```

**datasources.yml:**

```yaml
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
    url: http://localhost:9090
    isDefault: true
    basicAuth: true
    basicAuthUser: admin
    secureJsonData:
	  basicAuthPassword: 1234tyo
```


```shell
sudo systemctl restart grafana-server
```

```shell
sudo vim /etc/prometheus/prometheus.yml
```

**prometheus.yml:**

```yaml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"
	basic_auth:                  # <<---
	  username: admin            # <<---
	  password: 1234tyo          # <<---

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]


  - job_name: node_export
    static_configs:
      - targets: ["localhost:9100"]


  - job_name: pushgateway         
    honor_labels: true
    static_configs:
      - targets: ["localhost:9091"]
```

```shell
promtool check config /etc/prometheus/prometheus.yml
```

```shell
curl -X POST -u admin:1234tyo http://localhost:9090/-/reload
```

## alertmanager:

```shell
sudo useradd \
	--system \ 
	--no-create-home \
	--shell /bin/false alertmanager 
```

```shell
wget https://github.com/prometheus/alertmanager/releases/download/v0.28.1/alertmanager-0.28.1.linux-amd64.tar.gz
```

```shell
tar -xvf alertmanager-0.28.1.linux-amd64.tar.gz
```

```shell
sudo mkdir -p /alertmanager-data /etc/alertmanager
```

```shell
sudo mv alertmanager-0.28.1.linux-amd64/alertmanager /usr/local/bin
```

```shell
sudo vim /etc/systemd/system/alertmanager.service
```

```systemd
[Unit]
Description=Alertmanager
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=alertmanager
Group=alertmanager
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/alertmanager \
	--storage.path=/alertmanager-data \
	--config.file=/etc/alertmanager/alertmanager.yml

[Install]
WantedBy=multi-user.target
```

```shell
sudo systemctl enable alertmanager
```

```shell
sudo systemctl start alertmanager
```

```shell
sudo systemctl status alertmanager
```


```shell
sudo vim /etc/prometheus/dead-mans-snitch-rule.yml
```

```yaml
---
groups:
- name: dead-mans-snitch
  rules:
  - alert: DeadMansSnitch
    annotations:
      message: This alert is integrated with DeadMansSnitch.
    expr: vector(1)
```

```shell
sudo vim /etc/prometheus/prometheus.yml
```

**prometheus.yml:**

```yaml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
	      - localhost:9093   # <<----------------  
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  - dead-mans-snitch-rule.yml
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"
	basic_auth:            
	  username: admin
	  password: 1234tyo

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]


  - job_name: node_export
    static_configs:
      - targets: ["localhost:9100"]


  - job_name: pushgateway         
    honor_labels: true
    static_configs:
      - targets: ["localhost:9091"]
```

```shell
promtool check config /etc/prometheus/prometheus.yml
```

```shell
sudo systemctl restart prometheus.service
```

## Kaynak:
1. [How to Install Prometheus and Grafana on Ubuntu? (Node Exporter & Alertmanager & Pushgateway](https://www.youtube.com/watch?v=Z7GxBf6us8Y)
	1. 