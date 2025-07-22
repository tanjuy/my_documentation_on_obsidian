
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
	--collector.logind \
	--collector.systemd \
	--collector.processes

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

> + `node_exporter` programın(bir diğer adı servis) makine her yeniden başlatıldığında yeniden başlaması için gereken komut. 

```shell
sudo systemctl start node_exporter.service
```

> + `node_exporter` programını(diğer adı servis) arka tarafta(`daemon`) başlatıyoruz.


> [!NOTE]
> + `systemctl enable` ve `systemctl start` komutlarını aynı anda çalıştırmak için komut:
> ```shell
> sudo systemctl enable --now node_exporter.service
> ```


```shell
sudo systemctl status node node_exporter.service
```

> + `node_exporter` servisin düzgün çalışıp çalışmadığını teyit ediyoruz.


> [!TIP]
> + Herhangi bir sorun yaşarsanız journalctl ile logları kontrol edin.
> ```shell
>  sudo journalctl -u node_exporter.service  -f --no-pager
> ```

---

+ Statik bir hedef oluşturmak için job_name'i static_configs ile birlikte eklemeniz gerekir.

```shell
sudo vim /etc/prometheus/prometheus.yml
```

**prometheus.yml:**

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


  - job_name: node_export                   # <---- Dikkat
    static_configs:
      - targets: ["localhost:9100"]
```

> + Varsayılan olarak `node_exporter` 9100 portundan dışarıya açıktır.

> [!NOTE]
> + Prometheus, izleme (monitoring) sistemidir ve farklı kaynaklardan (örneğin sunucular, uygulamalar, container’lar vb.) **veri toplamak için o kaynakların IP adreslerini ya da servis bilgilerini bilmesi gerekir**.
> + Bu kaynakları elle tek tek tanımlamak yerine, **Prometheus kendisi otomatik olarak bunları "keşfedebilir"**. İşte bu keşif yöntemlerine **"service discovery mechanisms"** denir.
> + Prometheus’un desteklediği bazı servis keşif yöntemleri şunlardır:
> 	- Static config (statik IP ya da hostname listesi)
> 	- **Kubernetes**: Pod’ları ve servisleri otomatik tanır.
> 	- Consul
> 	- **EC2 (Amazon AWS)**
> 	- **Azure, GCE (Google Cloud), OpenStack**
> 	- Docker Swarm veya file-based discovery
> + **Örnek Kullanımı:**
> ```yaml
> scrape_configs:
>  - job_name: 'my-kubernetes-job'
>    kubernetes_sd_configs:
>      - role: pod
> ```
> + Yukarıdaki örnekte, Prometheus **Kubernetes cluster’ındaki pod’ları otomatik keşfeder**.



> [!NOTE]
> **Service Discovery Mechanism (Servis Keşif Mekanizması)**
> + **Tanım:**
> 	- Dinamik altyapılarda (örneğin Kubernetes, AWS EC2, Docker) Prometheus’un **otomatik olarak hedefleri keşfetmesini sağlayan mekanizmadır**.
> + **Özellikler:**
> 	- Dinamik ortamlarda kullanılır.
> 	- Hedefler otomatik olarak eklenir veya çıkarılır.
> 	- Güncel duruma göre hedef listesi kendiliğinden değişir.
> + **Örneğin:**
> 	- Yeni bir pod eklendiğinde otomatik izlenmeye başlar.
> 	- Bir EC2 örneği kapatıldığında listeden düşer.
> ```yaml
> scrape_configs:
>  - job_name: 'my-kubernetes-job'
>    kubernetes_sd_configs:
>      - role: pod
> ```
> + Bu örnekte Prometheus, Kubernetes cluster'ındaki tüm node’ları **kendisi keşfeder**.


> [!NOTE]
> **Static Targets (Statik Hedefler)**
> + **Tanım:**
> 	- Manuel olarak yazdığın IP adresleri ya da hostname'lerdir. Prometheus sadece **senin belirttiğin hedeflere** gider.
> + **Özellikler:**
> 	- **Sabit yapılar için uygundur** (örneğin küçük sunucu grubu).
> 	- Yeni hedefler eklemek için **config dosyasını manuel olarak değiştirmek gerekir**.
> 	- Otomatik güncelleme yoktur.
> 	
> ```yaml
> scrape_configs:
>   - job_name: 'static_servers'
>     static_configs:
> 	  - targets: ['192.168.1.10:9100', '192.168.1.11:9100']
> ```

| Özellik                  | Service Discovery       | Static Targets                   |
| ------------------------ | ----------------------- | -------------------------------- |
| **Otomatik Keşif**       | ✔️                      | ❌ (manuel yazılır)               |
| **Dinamik Ortama Uygun** | ✔️ (örneğin Kubernetes) | ❌                                |
| **Manuel Konfigürasyon** | Hayır                   | Evet                             |
| **Esneklik**             | Yüksek                  | Düşük                            |
| **Yaygın Kullanım**      | Büyük altyapılar, cloud | Küçük sunucular, test sistemleri |

| Senaryo                                   | Kullan            |
| ----------------------------------------- | ----------------- |
| Kubernetes, AWS, Docker gibi sistemler    | Service discovery |
| 2-3 sabit IP adresi olan basit bir sistem | Static target     |

---

```shell
promtool check config /etc/prometheus/prometheus.yml
```

>+ Bu komut ile `prometheus.yml` dosyasının syntax hatası var mı  diye teyit ediyoruz.


**GET isteği:**

```shell
curl http://localhost:9090/api/v1/status/config | jq -r '.data.yaml'
```

> +  **Prometheus** sunucusunun şu anki yapılandırmasını (`prometheus.yml` dosyasının içeriğini) **API üzerinden sorgulamak** için kullanılır.
> + Prometheus'un o anda kullandığı yapılandırma dosyasının (`prometheus.yml`) tam içeriğini gösterir.
> + Bu komut, Prometheus API'sini kullanarak yapılandırmayı programlı bir şekilde çekmek isteyen senaryolarda (CI/CD, monitoring scriptleri) kullanılabilir.

**Curl Çıktısı:**

```yaml
global:
  scrape_interval: 15s
  scrape_timeout: 10s
  scrape_protocols:
  - OpenMetricsText1.0.0
  - OpenMetricsText0.0.1
  - PrometheusText0.0.4
  evaluation_interval: 15s
runtime:
  gogc: 75
alerting:
  alertmanagers:
  - follow_redirects: true
    enable_http2: true
    http_headers: null
    scheme: http
    timeout: 10s
    api_version: v2
...
```


---

```shell
curl -X POST http://localhost:9090/-/reload
```

> + `lifecycle management` yönetimini etkinleştirdiğimiz için, API çağrıları aracılığıyla  hizmeti yeniden başlatmadan ve kesintiye neden olmadan Prometheus yapılandırmasını yeniden yükleyebiliriz.
> + Konfigürasyon ayarlarını yeniden yüklemek için bir POST isteği gönderiyoruz.

## 3. Adım:

+ Metrikleri görselleştirmek için Grafana'yı kullanabiliriz.
+ Grafana'nın desteklediği birçok farklı veri kaynağı var, bunlardan biri de Prometheus'tur.
### Grafana:

+ Ön koşul paketleri yüklüyooruz.

```shell
sudo apt-get install -y apt-transport-https software-properties-common wget
```

---

+ GPG anahtarını içe aktarın:

```shell
sudo mkdir -p /etc/apt/keyrings/
```

```shell
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

---

+ **Kararlı sürümler** için bir depo eklemek üzere aşağıdaki komutu çalıştırın:

```shell
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

+ **Beta sürümleri** için bir depo eklemek üzere aşağıdaki komutu çalıştırın:

```shell
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

+ Mevcut paketlerin listesini güncellemek için aşağıdaki komutu çalıştırın:

```shell
# Updates the list of available packages
sudo apt-get update
```

+ **Grafana OSS'yi** yüklemek için aşağıdaki komutu çalıştırın:

```shell
# Installs the latest OSS release:
sudo apt-get install grafana
```

+ **Grafana Enterprise'ı** yüklemek için aşağıdaki komutu çalıştırın:

```shell
# Installs the latest Enterprise release:
sudo apt-get install grafana-enterprise
```

---


```shell
sudo systemctl enable grafana-server
```

> + `systemctl enable` komutu ile ubuntu makinesi yeniden başlatıldığında otomatik olarak grafana çalıştırılacaktır. 

```shell
sudo systemctl start grafana-server.service
```

> + `grafana-server` servisini arka planda çalıştırıyoruz.


> [!TIP]
> + `systemctl enable` ve `systemctl start` komutlarını aşağıdaki komutlar ile aynı anda çalıştırabiliriz:
> ```shell
> sudo systemctl enable --now grafana-server.service
> ```
> + `systemctl status` komut ile daemon'ın durumunu kontrol ediyoruz:
> ```shell
> sudo systemctl status grafana-server.service
> ```

+ Tarayıcıyı açın ve varsayılan kimlik bilgilerinizi kullanarak Grafana'ya giriş yapın.
+ Kullanıcı adı admin, şifre ise admin'dir.
+ İlk defa giriş yaptığınızda şifrenizi değiştirme imkânına sahip oluyorsunuz.

![grafana_login](./Pictures/grafana_login.png)


> [!NOTE]
> 1. **Grafana'nın `admin` şifresini sıfırla**
> 	+ Aşağıdaki komut ile `admin` kullanıcısının şifresini terminalden sıfırlayabilirsin:
> 	```shell
> 	grafana-cli admin reset-admin-password yeni_şifre
> 	```
> 2. **Eğer `grafana-cli` komutu bulunamıyorsa:**
> 	+ Debian/Ubuntu’da şöyle yüklenmiş olabilir:
> 	```shell
> 	sudo /usr/sbin/grafana-cli admin reset-admin-password yeni_şifre
>	 ```
>	 + Ya da doğrudan `find` ile bulabilirsin:
>	 ```shell
>	 sudo find / -name grafana-cli
>	```
> 3. **Alternatif: SQLite veritabanı üzerinden manuel sıfırlama**
> 	+ Eğer komutla sıfırlayamıyorsan, Grafana’nın `grafana.db` veritabanı dosyası içindeki `admin` kullanıcısını değiştirebilirsin (riskli, önerilmez ama mümkündür).
> 	+ Grafana genelde kullanıcıları aşağıdaki veritabanında saklar:
> 	```shell
>	/var/lib/grafana/grafana.db  # SQLite DB
>	```

| Durum                               | Çözüm                                          |
| ----------------------------------- | ---------------------------------------------- |
| Varsayılan kullanıcı şifresi        | `admin` / `admin`                              |
| Şifre değiştirildi ve unutuldu      | `grafana-cli admin reset-admin-password`       |
| CLI yoksa                           | `find` ile yerini bul veya paketi tekrar yükle |
| Veritabanı müdahalesi (en son çare) | `grafana.db` dosyasını düzenle                 |


+ Metrikleri görselleştirmek için öncelikle bir veri kaynağı(`data source`) eklemeniz gerekir.

![grafana_data_source](./Pictures/grafana_data_source.png)

+ Veri kaynağı ekle'ye tıklayın ve Prometheus'u seçin.

![gradana_prometheus](./Pictures/grafana_prometheus.png)

+ URL için http://localhost:9090 girin ve `save and test` tıklayın.

![grafana_prometheus_URL](./Pictures/grafana_prometheus_URL.png)


> [!TIP]
> + `Production` ortamlarında genellikle tüm konfigürasyonları Git'te saklarsınız.
> + Alternatif olarak, veri kaynağını(`data source`) terminal ile konfigürasyon ekleyebiliriz.
> + Yeni bir `datasources.yaml` dosyası oluştuyoruz.
> ```shell
> sudo vim /etc/grafana/provisioning/datasources/datasources.yaml
> ```
> 
> ```yaml
> apiVersion: 1
> 
> datasources:
>   - name: Prometheus
>     type: prometheus
>     url: http://localhost:9090
>     isDefault: true
> ```
> + Ayarların geçerli olabilmesi için grafana servisini yeniden başlatıyoruz. 
> ```shell
> sudo systemctl restart grafana-server
> ```


+ `scrape_duration_seconds` metrik örneği: 
+ `scrape_duration_seconds`, **Prometheus’un bir hedeften (target) metrik verilerini toplamasının (scrape etmesinin) ne kadar sürdüğünü saniye cinsinden ölçen bir metriktir.**

![prometheus_scrape](./Pictures/prometheus_scrape.png)


> [!NOTE]
> + Prometheus, her hedefe belirli aralıklarla HTTP isteği (`/metrics` endpointine) gönderir ve metrik verilerini alır.
> + Bu işlem sırasında geçen süreyi ölçer ve bunu `scrape_duration_seconds` adlı metrikte saklar.
> ```prometheus
> scrape_duration_seconds{instance="localhost:9100", job="node_export"}    0.003135206
> ```
> + `job="node_export"`: İzlenen iş (örneğin node exporter)
> + `instance="localhost:9100"`: Hedef adres
> + `0.003135206`: Veri toplama (scrape) işlemi 0.045 saniye sürmüş


> [!TIP]
> + **Performans analizi**: Hedef sistem yanıt verirken ne kadar gecikiyor görebilirsin.
> + Ağ gecikmeleri veya yük altında kalan sistemleri tespit edebilirsin

+ `scrape_duration_seconds` metriği Grafana'da basit bir grafik oluşturmak için kullanacağız.

![grafana_dashboard](./Pictures/grafana_dashboard.png)

+ `Add visualization` butonuna tıklayarak yeni bir panel oluşturuyoruz.

![grafana_dashboard2](./Pictures/grafana_dashboard2.png)


![grafana_dashboard3](./Pictures/grafana_dashboard3.png)


![grafana_dashboard5](grafana_dashboard5.png)


![grafana_dashboard6](grafana_dashboard6.png)

+ CPU, Bellek, Ağ ve diğer bir sürü ölçümü görselleştirmek için açık kaynaklı bir gösterge tablosunu(`dashboard`) içe aktarabiliriz.
+ Açık kaynaklı gösterge tablosu(`dashboard`) [web sitesi](https://grafana.com/grafana/dashboards/)
+ Örnek için [`open-source Node Exporter Full`](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)'u kullanacağız 

![grafana_dashboard_template](./Pictures/grafana_dashboard_template.png)

---

+  [`Node Exporter Full`](https://grafana.com/grafana/dashboards/1860-node-exporter-full/) sitesinde `Copy ID to clipboard` butonunu tıklayarak 
+ Aşağıdaki gösterildiği gibi siteden kopyalan ID'yi kutucuğa kopyalayarak, load butonuna tıklayarak dashboard yüklemesi yapabiliriz.

![grafana_dashboard7](./Pictures/grafana_dashboard7.png)


![grafana_dashboard8](./Pictures/grafana_dashboard8.png)

+ Burada node exporter'dan gelen her türlü metrik var.

![grafana_Node_Exporter_Full](./Pictures/grafana_Node_Exporter_Full.png)

## 4. Adım:

+ Pushgateway, scrape (çekilme) yapılamayan işler (job'lar) için metriklerin Prometheus'a gönderilmesini (push edilmesini) sağlayan bir servistir.
+ Normalde Prometheus, metrik verileri **kendisi çekerek (scrape)** alır.  
+ Yani Prometheus gidip bir servise `/metrics` isteği gönderir ve o servis de metrikleri döner.
+ Ancak bazı işler (örneğin kısa ömürlü batch script'ler, jenkins, cron job'lar, bir defaya mahsus çalışan komutlar) **çalışırken ortada uzun süre kalmadıkları için** Prometheus bu job’ları **zamanında bulamaz ve scrape edemez**.
+ İşte burada **Pushgateway** devreye girer.

### Pushgateway:

+ Kurulum süreci Prometheus ve Node exporter'a oldukça benzerdir.

```shell
sudo useradd \
	--system \
	--no-create-home \
	--shell /bin/false pushgateway
```

---

+ Pushgateway programını yerel makinemize indiriyoruz.
+ Pushgateway resmi [indirme](https://prometheus.io/download/) sayfası.

```shell
wget https://github.com/prometheus/pushgateway/releases/download/v1.11.1/pushgateway-1.11.1.linux-amd64.tar.gz
```

---

```shell
tar -xvf pushgateway-1.11.1.linux-amd64.tar.gz
```

+ cp komutu ile Pushgateway ikili dosyasını `/usr/local/bin` dizinine taşıyın.

```shell
sudo cp -v pushgateway-1.11.1.linux-amd64/pushgateway /usr/local/bin
```

---

+ pushgateway adında bir servis oluşturuyoruz:

```shell
sudo vim /etc/systemd/system/pushgateway.service
```

**pushgateway.service:**

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


> [!NOTE]
> `Type=simple`
> 1. **Varsayılan Değer**: Eğer `Type` belirtilmezse, systemd varsayılan olarak `simple` kabul eder.
> 2. **Davranış**:
> 	- systemd, `ExecStart` komutunu çalıştırır ve hemen bir sonraki işleme geçer.
> 	- Servis sürecinin başarılı şekilde başlayıp başlamadığını kontrol etmez.
> 	- Süreç çalışıyorsa "active (running)" durumunu gösterir


```shell
sudo systemctl enable pushgateway.service
```

```shell
sudo systemctl start pushgateway.service
```


> [!TIP]
> + Pushgateway'e 9091 numaralı porttan ulaşılabilir

+ Prometheus'a hedef(`target`) olarak Pushgateway'i ekleyelim.

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

+ Yukarıdaki `prometheus.yml` dosyasının söz dizimi(`systax`) doğru olup olmadığını kontrol ediyoruz.

```shell
promtool check config /etc/prometheus/prometheus.yml
```

**Çıktı:**

```shell
Checking /etc/prometheus/prometheus.yml
 SUCCESS: /etc/prometheus/prometheus.yml is valid prometheus config file syntax
```

---

**POST isteği:**

+ `curl -X POST http://localhost:9090/-/reload`, **Prometheus** sunucusuna yapılandırma dosyasını (`prometheus.yml`) **yeniden yüklemesi** için gönderilen bir HTTP isteğidir.
+ Bu komut, Prometheus'un çalışırken (restart gerektirmeden) yapılandırma değişikliklerini uygulamasını sağlar.

```shell
curl -i -X POST http://localhost:9090/-/reload
```

**Curl Çıktıs:**

```shell
HTTP/1.1 200 OK
Date: Tue, 15 Jul 2025 17:27:36 GMT
Content-Length: 0

```


> [!NOTE]
> 1. **Yapılandırma Değişikliklerini Uygular**:
> 	- `prometheus.yml` dosyasında değişiklik yaptığınızda (örneğin, yeni bir scrape job eklediğinizde), Prometheus'un bu değişiklikleri algılaması için bu komutu kullanabilirsiniz.
> 	- Prometheus, dosyayı tekrar okuyarak yeni ayarları uygular.
> 2. **Servisi Restart Etmeye Gerek Kalmaz**
> 	- Geleneksel yöntemde servisi yeniden başlatmak gerekir (`systemctl restart prometheus`), ancak bu komutla **kesinti olmadan** değişiklikler aktive edilir.
> 3. **Sadece Yapılandırmayı Yeniden Yükler**
> 	- Toplanan metrik verileri veya çalışan sorguları **etkilemez**. Yalnızca yapılandırma dosyası yeniden okunur.


> [!CAUTİON]
> 1. **`-web.enable-lifecycle` Etkin Olmalı**
> 	+ Prometheus'un bu özelliği desteklemesi için başlatma komutunda bu flag'in olması gerekir. Örnek:
> 	```shell
> 	prometheus --config.file=/etc/prometheus/prometheus.yml --web.enable-lifecycle
>	 ```
>	 + Systemd kullanıyorsanız, servis dosyasını (`/etc/systemd/system/prometheus.service`) düzenlemeniz gerekebilir.
> 2. **Güvenlik Riski**
> 	+ Bu API, Prometheus'un konfigürasyonunu değiştirebildiği için **dış erişime açık olmamalıdır**.
> 	+ Sadece `localhost` (127.0.0.1) üzerinden erişilebilir olması önerilir.
> 	+ Eğer uzaktan erişim gerekiyorsa, bir `reverse proxy (Nginx/Apache)` ile yetkilendirme eklenmelidir.
> 3. **Diğer Yeniden Yükleme Yöntemleri**
> 	+ **SIGHUP Sinyali**: Prometheus'a `kill -SIGHUP <PID>` göndererek de yeniden yükleme yapılabilir.
> 	+ **Servis Restart**: En garantili yöntemdir, ancak kısa bir kesintiye neden olur: `sudo systemctl restart prometheus.service`

+ API üzerinden POST ile yeniden yükleme(`reload`) sonucunda aşağıdaki resimde de görüldüğü üzeri `pushgateway target` görünmektedir. 

![pushgateway_targets](./Pictures/pushgateway_targets.png)

---

+ Metrikleri Pushgateway'e göndermek için, http://localhost:9091/metrics/job/backup uç noktasına(`endpoint`'a) bir POST isteği göndermeniz yeterlidir.
+ backup, etiket olarak görünecek keyfi bir isimdir. Yani, dilerseniz `backup` yerine başka bir ifade veya etiket kullanabilirsiniz.
+ `curl` komutunu kullanın ve dizeyi `echo` ile `Pushgateway`'e yönlendiriyoruz(`pipe`).
+ Jenkins'in backup adını verdiğimiz işinin(`job`'ın) yaklaşık 16 saniyede tamamlandığını düşünelim.

```shell
echo "jenkins_job_duration_seconds 15.98" | curl --verbose --data-binary @- http://localhost:9091/metrics/job/backup
```

> 1. `echo`, `"jenkins_job_duration_seconds 15.07"` metnini stdout'a yazar.
> 2. Pipe (`|`) bu çıktıyı `curl` komutuna stdin olarak iletir.
> 3. `curl --data-binary @-`, stdin'den gelen bu metni alır ve `http://localhost:9091/metrics/job/backup` adresine **POST eder**.

**Çıktı:**

```shell
*   Trying 127.0.0.1:9091...
* Connected to localhost (127.0.0.1) port 9091 (#0)
> POST /metrics/job/backup HTTP/1.1
> Host: localhost:9091
> User-Agent: curl/7.81.0
> Accept: */*
> Content-Length: 34
> Content-Type: application/x-www-form-urlencoded
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Wed, 16 Jul 2025 17:45:22 GMT
< Content-Length: 0
<
* Connection #0 to host localhost left intact
```


> [!TIP]
> Bir metrik dosyasını (`metrics.txt`) Prometheus PushGateway'ine göndermek istiyorsunuz. Dosya içeriği aşağıdaki gibi olsun: (**Yukarıdaki komuta alternatifdir.**)
> 1. **`metrics.txt` Dosyasını Oluşturma:**
> 	```shell
> 	echo 'jenkins_job_duration_seconds 15.7' > metrics.txt
>	 ```
>	 + Bu komut, `metrics.txt` adlı bir dosya oluşturur ve içine 1 metrik ekler.
> 2. **`curl --data-binary @metrics.txt` ile Gönderme:**
> 	```shell
> 	curl --data-binary @metrics.txt http://localhost:9091/metrics/job/backup
> 	```
> 	+ `metrics.txt` dosyasının içeriğini **binary (ham veri)** olarak alır.
> 	+ `http://localhost:9091/metrics/job/backup` adresine **HTTP POST** isteği ile gönderir.
> 	+ PushGateway, bu metrikleri `job="backup"` etiketiyle kaydeder.
> 3. **`@metrics.txt` vs `@-` Farkı:** 
> 	+ `curl --data-binary @metrics.txt` : Dosyalardan veri okur.
> 	+ `curl --data-binary @-` : **Standart girdiden (stdin)** veri okur. önceki komutun çıktısını pipe(`|`) ile alır. 


> [!NOTE]
> 4. `--data-binary`:
> 	- Bu seçenek, curl'e gönderdiğiniz verinin **ham (binary) formda** olduğunu ve herhangi bir işlem yapılmadan sunucuya iletilmesi gerektiğini söyler.
> 	- `--data` veya `-d` seçeneğinden farkı, veride özel karakterlerin (örneğin `@`, `&`, boşluklar) yorumlanmamasıdır.
> 5. **`@-`**:
> 	- `@` işareti, `curl`'e bir dosyadan veri okumasını söyler.
> 	- `-` özel bir dosya adıdır ve **standart girdi (stdin)** anlamına gelir. Yani, komutun öncesinde pipe (`|`) ile gelen veriyi alır.


> [!TIP]
> + Promethues'dan bir metrik veriyi aşağıdaki komut ile silebiliriz:
> ```shell
>  curl  -v -X 'DELETE' http://localhost:9091/metrics/job/backup2
> ```
> + Çıktısı:
> ```shell
> *   Trying 127.0.0.1:9091...
> * Connected to localhost (127.0.0.1) port 9091 (#0)
> DELETE /metrics/job/backup2 HTTP/1.1
> Host: localhost:9091
> User-Agent: curl/7.81.0
> Accept: */*
>
> * Mark bundle as not supporting multiuse
> < HTTP/1.1 202 Accepted
> < Date: Wed, 16 Jul 2025 17:58:07 GMT
> < Content-Length: 0
> <
>  * Connection #0 to host localhost left intact
>  ```


+ Bu metriği `Prometheus`'ta bulabilirsiniz.

![prometheus_metric](./Pictures/prometheus_metric.png)



## 5. Adım:

+ Prometheus'u kurduğunuzda, uç noktayı(`endpoint`'ı) bilen herkese açık olacaktır.
+ Prometheus yakın zamanda her HTTP isteğine temel kimlik doğrulaması eklemenin bir yolunu tanıttı.
+ Eskiden Prometheus'un önüne nginx gibi bir proxy kurup temel kimlik doğrulamasını orada yapılandırmanız gerekiyordu.
+ Artık Prometheus'un kendisinde bulunan yerleşik kimlik doğrulama mekanizmasını kullanabilirsiniz.

### Promethous Temel Auth:

+ Şifrenin hash'ini oluşturmak için python modülünü yükleyelim.
+ Prometheus şifrelerinizi saklamayacak; hash'i hesaplayacak ve bunu belirtilen kullanıcı için var olan hash ile karşılaştıracak.

```shell
sudo apt-get -y install python3-bcrypt
```

---

+ Şimdi, girdi isteyecek(`input`) ve parola için hash değerini döndürecek basit bir betik oluşturun.

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

---

**Python3 Çalıştır:**

```shell
python3 generate_password.py
```

> + Betiği(`script`) çalıştırdık ve şifre olarak `12345` girdik

**Python Çıktısı:**

```shell
$2b$12$9bJgAbKW9gxmGXZFXSKcIOAVYFk1CupVT.vDU1se2a2Xl.EBBssVy
```

---

+ Bu hash'i kopyaladık ve ek bir Prometheus konfigürasyon dosyası oluşturduk.

```shell
sudo vim /etc/prometheus/web.yml
```

**web.yml**

+ Dosyaya birden fazla kullanıcı ekleyebilirsiniz

```yaml
basic_auth_users:
  # generate_password.py hash çıktısı
  admin: $2b$12$9bJgAbKW9gxmGXZFXSKcIOAVYFk1CupVT.vDU1se2a2Xl.EBBssVy
```


> [!CAUTION]
> + `web.yml` dosyası bir yaml dosyası olduğu için girintilere(`indention`) dikkat edilmesi gerekir.
> + Aksi takdirde hata verebilir. 
> + Genellikle, yaygın kullanılan girinti tarzı, `space` tuşuna iki kere basarak iki boşluk vermektir. 

```shell
promtool check web-config web.yml  # web.yml SUCCESS
```

> + Eğer `SUCCESS` çıktısını veriyorsa `web.yml` dosyasını söz dizimi doğrudur. 

---

+ Şimdi bu konfigürasyonu Prometheus servisi içeresinde tanımlamamız  gerekiyor.
+ Systemd servis tanımını güncelleyelim.

```shell
sudo vim /etc/systemd/system/prometheus.service
```

**prometheus.service:**

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
	--web.config.file=/etc/prometheus/web.yml   # <<--- Sadece bu eklendi

[Install]
WantedBy=multi-user.target
```

> Daha önceden oluşturmuş olduğumuz `prometheus` servisine `--web-config.file=/etc/prometheus/web.yml` parametresini ekliyoruz.

---

+ Systemd servisini her güncellediğinizde, onu yeniden yüklemeniz gerekir.

```shell
sudo systemctl daemon-reload
```

+ Ayrıca, prometheus servisini de yeniden başlatmanız gerekmektedir:

```shell
sudo systemctl restart prometheus.service
```

+ Servisin düzgün çalışıp çalışmadığını kontrol edelim:

```shell
sudo systemctl status prometheus.service
```

---

+ Prometheus'a gidin ve sayfayı yeniden yükleyin.
+ Kullanıcı adınızı ve şifrenizi girin.

![prometheus_password](./Pictures/prometheus_password.png)


> [!TIP]
> + Tarayıcıya alternatif olarak cURL ile komut satırından da test edebilirsiniz.
> + Kurulumunuzla etkileşim kurmak için cURL kullanabilirsiniz. Şu isteği deneyin:
> ```shell
> curl --head http://localhost:9090/graph
> ```
> + Geçerli bir kullanıcı adı ve parola sağlamadığınız için bu, `401 Unauthorized` yanıtı döndürecektir.


> [!TIP]
> + Temel kimlik doğrulamayı kullanarak Prometheus endpoints'a başarıyla erişmek için, örneğin; `/metrics` endpoint gibi, 
> + -u bayrağını kullanarak doğru kullanıcı adını girin ve istendiğinde şifreyi girin
> ```
> curl -u admin http://localhost:9090/metrics
> Enter host password for user 'admin':
> ```
> + Aşağıdakine benzer bir çıktı üretecektir:
> ```shell
>  # HELP go_gc_duration_seconds A summary of the GC invocation durations.
>  # TYPE go_gc_duration_seconds summary
>  go_gc_duration_seconds{quantile="0"} 0.0001343
>  go_gc_duration_seconds{quantile="0.25"} 0.0002032
>  go_gc_duration_seconds{quantile="0.5"} 0.0004485
> ```


---

+ `Targets` bölümüne(`status->targets`) giderseniz `Prometheus target`'ın düştüğünü göreceksiniz.
+ Prometheus'un kendinden veri çekebilmesi(`scrape`) için de kullanıcı adı ve şifreye ihtiyacı var.

![promeheus_unauthorized](./Pictures/prometheus_unauthorized.png)

+ Grafana, prometheus'a ulaşabilmesi için `grafana datasource`'una kullanıcı ve şifre vererek güncellememiz gerekiyor.

![grafana_unaauthorized](./Pictures/grafana_unauthorized.png)

+ Test butonuna tıkladığınızda `401 Unauthorized` bir hata alırsınız.

![prometheus_unauthorized_2.png](./Pictures/prometheus_unauthorized_2.png)

---

+ Grafana için veri kaynağı yapılandırmasını(`data source konfigürasyonunu`) temel kimlik doğrulamayı(`authorized`) içerecek şekilde güncelleyelim.

```shell
sudo vim /etc/grafana/provisioning/datasources/datasources.yaml
```

**datasources.yml:**

+ Bu `/etc/grafana/provisioning/datasources/datasources.yaml` dosyası, **Grafana**'ya **otomatik olarak veri kaynağı (datasource)** tanımlamak için kullanılan bir yapılandırma (provisioning) dosyasıdır.
+ `Prometheus` gibi izleme/veri toplama sistemlerini Grafana’ya tanıtmak için kullanılır.

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
	  basicAuthPassword: 1234
```

> + `apiVersion: 1` : Bu dosyanın **YAML API sürümünü** belirtir. Şu an sadece `apiVersion: 1` destekleniyor.
> + `datasources`: Tanımlanacak veri kaynaklarının listesi.
> + `name: Prometheus`: Grafana arayüzünde görünecek olan veri kaynağının adı. İstediğin bir isim verebilirsin.
> + `type:` Veri kaynağının türünü belirtir. `prometheus`, `mysql`, `postgres`, `influxdb` gibi değerler alabilir. Burada Prometheus kullanıldığını gösteriyor.
> + `url:` Prometheus sunucusunun adresi. `localhost:9090`, Prometheus'un çalıştığı makinenin IP'si ve portudur. Grafana, bu URL üzerinden Prometheus ile iletişim kurar.
> + `isDefault:` Bu kaynak, **varsayılan veri kaynağı** olarak ayarlanır. Eğer birden fazla datasource varsa ve bir panelde özel bir kaynak belirtilmemişse, Grafana bu kaynağı kullanır.
> + `basicAuth:` Temel HTTP kimlik doğrulaması kullanılacağını belirtir.
> + `basicAuthUser:` Kullanıcı adı "admin" olarak ayarlanmış.
> + `secureJsonData:` Şifre gibi hassas bilgiler `secureJsonData` altında tanımlanır.
> + `basicAuthPassword: Burada `admin` kullanıcısının şifresi `1234` olarak girilmiş. 


```shell
sudo systemctl restart grafana-server.service
```

> + `datasources.yaml` dosyasında yaptığımız değişklerin gerçerli olabilmesi için `grafana-server` servisini yeniden başlatıyoruz.

---

+ Prometheus target'ını **kullanıcı adı(username)** ve **parolayı(password)** içerecek şekilde güncelleyelim.

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
	  password: 1234             # <<---

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

---

+ Yukarıdan düzenlemiş olduğumuz `prometheus.yml` dosyasını söz dizininde(`syntax`) hata var mı diye kontrol ediyoruz:

```shell
promtool check config /etc/prometheus/prometheus.yml
```

**promtool Çıktısı:**

```shell
Checking /etc/prometheus/prometheus.yml
 SUCCESS: /etc/prometheus/prometheus.yml is valid prometheus config file syntax
```

--- 
+ Bu komut, `curl` kullanarak **Prometheus sunucusuna yapılandırmayı yeniden yüklemesi** için HTTP POST isteği gönderir.

```shell
curl -v -X POST -u admin:1234 http://localhost:9090/-/reload
```

> + Bu komut, **Prometheus yapılandırma dosyası (`prometheus.yml`) değiştirilmişse**, yeni yapılandırmanın Prometheus tarafından tekrar okunmasını sağlar.
> + Yani `prometheus.yml` dosyasını yeniden başlatmadan (restart yapmadan) uygulamak için kullanılır.

```shell
*   Trying 127.0.0.1:9090...
* Connected to localhost (127.0.0.1) port 9090 (#0)
* Server auth using Basic with user 'admin'
> POST /-/reload HTTP/1.1
> Host: localhost:9090
> Authorization: Basic YWRtaW46MTIzNHR5bw==
> User-Agent: curl/7.81.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Fri, 18 Jul 2025 17:04:57 GMT
< Content-Length: 0
<
* Connection #0 to host localhost left intact
```


> [!TIP]
> + Yukarıdaki komuta alternatif olarak API üzerinden yapılacak POST isteği:
> ```shell
>  curl -v -X POST http://admin:1234tyo@localhost:9090/-/reload
> ```


> [!TIP]
> **Kimlik Doğrulama Notu:**
> + Eğer Prometheus üzerinde **Basic Auth** (kullanıcı adı/şifre) yapılandırılmadıysa, `-u admin:1234` kısmına gerek yoktur ve hatta bu istek başarısız olur.
> + Varsayılan Prometheus kurulumu genelde **kimlik doğrulama içermez**, yani bu komutun sade hali genelde yeterlidir:
> ```shell
> curl -X POST http://localhost:9090/-/reload
> ```


> [!CAUTION]
> + `/-/reload` komutu çalışabilmesi için Prometheus’un `--web.enable-lifecycle` parametresiyle başlatılmış olması gerekir:
> ```shell
> ./prometheus --config.file=prometheus.yml --web.enable-lifecycle
> ```


## 6. Adım

+ Alertmanager, alarmların yinelenmesini önlemek (deduplication), gruplanması (grouping) ve doğru alıcıya yönlendirilmesi (routing) işlemlerini gerçekleştirir — bu alıcılar e-posta, PagerDuty ya da bizim durumumuzda Slack olabilir.

| Parça                                              | Anlamı                                                                                                                       |
| -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Alertmanager takes care of**                     | Alertmanager şunları halleder / yönetir                                                                                      |
| **deduplicating**                                  | Aynı uyarının tekrar tekrar bildirilmesini önler (örneğin bir alarm sürekli tetikleniyorsa tek bir bildirimle sınırlandırır) |
| **grouping**                                       | Benzer uyarıları bir araya toplar (örneğin aynı servisle ilgili 5 ayrı uyarıyı tek bir bildirimde gruplar)                   |
| **routing**                                        | Hangi uyarının hangi kişiye ya da platforma gideceğini belirler (e-posta, Slack, vs.)                                        |
| **receiver integration**                           | Uyarıların gönderileceği hedef sistem (e-posta sunucusu, Slack webhook'u, vs.)                                               |
| **such as email, PagerDuty, or in our case Slack** | Alıcı sistemlere örnekler: e-posta, PagerDuty, **ve bizim örneğimizde Slack**                                                |

+ `High Availability`(Yüksek erişilebilirlik) elde etmek için birden fazla Uyarı Yöneticisi ayarlayabilirsiniz.

### alertmanager:

+ Öncelikle Alertmanager için bir sistem kullanıcısı oluşturalım.

```shell
sudo useradd \
	--system \
	--no-create-home \
	--shell /bin/false alertmanager 
```

+ Daha sonra aynı indirme sayfasından Alertmanager'ı indirelim.

```shell
wget https://github.com/prometheus/alertmanager/releases/download/v0.28.1/alertmanager-0.28.1.linux-amd64.tar.gz
```

+ `gz` ile sıkıştırılmış binaray alertmanager arşiv dosyasını çıkaralım.

```shell
tar -xvf alertmanager-0.28.1.linux-amd64.tar.gz
```

---

+ Alertmanager için depolama alanına ihtiyacımız var.

```shell
sudo mkdir -p /alertmanager-data /etc/alertmanager
```

> + Alertmanager için bir veri dizini zorunludur (varsayılan olarak `data/` klasörü kullanılır) ve bu dizin, bildirim durumları ile susturma (silence) bilgilerini saklamak için kullanılır.


> [!NOTE]
> **Alertmanager:**
> + Uyarılar için **durum bilgisi** tutar (örneğin "bu uyarı gönderildi mi, hala aktif mi").
> + Kullanıcıların ayarladığı **silence (susturma)** ayarlarını dosya sistemi üzerinde saklar.
> + Bu bilgiler **kalıcı (persisted)** tutulur, böylece Alertmanager yeniden başlatılsa bile bu ayarlar kaybolmaz.


> [!NOTE]
> + Varsayılan olarak Alertmanager şunları bu klasöre yazar:
> ```shell
> data/
  ├── notification.log
  └── silences.json
> ```
> + Hangi alarmlar tetiklendi ve ne zaman gönderildi?
> + Hangi susturmalar aktif?


> [!WARNING]
> + Bu durum bilgisi (state) olmadan — ya da silinirse — Alertmanager yeniden başlatıldığında hangi susturma (silence) kurallarının oluşturulduğunu veya hangi bildirimlerin (notification) zaten gönderildiğini bilemez.

---

+ Alermanager'ın ikili dosyasını yerel bin'e(`/usr/local/bin`) taşıyalım ve örnek yapılandırmayı kopyalayalım.

```shell
sudo cp -v alertmanager-0.28.1.linux-amd64/alertmanager /usr/local/bin
```


```shell
sudo cp -v alertmanager-0.28.1.linux-amd64/alertmanager.yml /etc/alertmanager/
```

**alertmanager.yml**

```yml
route:
  group_by: ['alertname']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 1h
  receiver: 'web.hook'
receivers:
  - name: 'web.hook'
    webhook_configs:
      - url: 'http://127.0.0.1:5001/'
inhibit_rules:
  - source_match:
      severity: 'critical'
    target_match:
      severity: 'warning'
    equal: ['alertname', 'dev', 'instance']
```

> [!NOTE]
> 1. **`route:`** → Alarmların nasıl gruplandığı ve hangi alıcıya gönderileceği.
> 	+ **`group_by: ['alertname']`**
> 		- Aynı `alertname` (uyarı adı) olan alarmlar **tek grup** olarak işlenir.
> 		- Örneğin 3 farklı sunucuda `HighCPU` uyarısı varsa, bunlar tek bildirimde birleştirilir.
> 	+ **`group_wait: 30s`**
> 		- Yeni bir grup uyarı geldiğinde 30 saniye beklenir, böylece aynı gruba ait başka alarmlar da gelirse aynı bildirimde gönderilir.
> 	+ **`group_interval: 5m`**
> 		-  Aynı uyarı grubuna ait yeni alarmlar 5 dakika içinde tekrar bildirilmez (spam engelleme).
> 	+ **`repeat_interval: 1h`**
> 		-  Aynı alarm devam ediyorsa, 1 saatte bir tekrar gönderilir.
> 	+ **`receiver: 'web.hook'`**
> 		- Bu uyarılar `'web.hook'` adındaki alıcıya (receiver) yönlendirilir.


> [!NOTE]
> 2. **`receivers:`** → Alarmların gönderileceği hedef sistemler (örneğin webhook, e-posta, Slack).
> 	+ **`name: 'web.hook'`**
> 		- Bu, yukarıdaki route tarafından kullanılacak olan alıcı tanımı.
> 	+ **`webhook_configs:`**
> 		- Uyarılar, belirtilen HTTP adresine `POST` isteğiyle JSON formatında gönderilir.
> 	+ **`url: 'http://127.0.0.1:5001/'`**
> 		- Alertmanager, uyarı oluştuğunda bu URL'ye HTTP isteği gönderir.
> 		- Örneğin, bu adreste çalışan bir Flask/Python sunucu olabilir.


> [!NOTE]
> 3. **`inhibit_rules:`** → Belirli uyarıların diğerlerini bastırma (susturma) kuralları.
> 	+ Eğer bir **`critical` seviyesinde** alarm varsa (source),
> 	+ Aynı `alertname`, `dev`, ve `instance` etiketlerine sahip bir **`warning` seviyesindeki** alarm (target),
> 	+ **gönderilmez** (bastırılır), çünkü zaten daha ciddi (`critical`) versiyonu aktif.
> 	+ Aynı alarmın hem `warning` hem `critical` versiyonu varsa, yalnızca kritik olan bildirilsin diye kullanılır.
> 	+ Spam ve kafa karışıklığı engellenmiş olur.

|Bölüm|Görevi|
|---|---|
|`route:`|Alarmların nasıl gruplanacağı, ne zaman gönderileceği, hangi alıcıya yönlendirileceği|
|`receivers:`|Uyarıların nereye gönderileceğini tanımlar (örneğin bir webhook)|
|`inhibit_rules:`|Bazı uyarıların, daha kritik uyarılar varken bastırılmasını sağlar|

---

```shell
sudo vim /etc/systemd/system/alertmanager.service
```

**alertmanager.service**

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

> 1. **`--storage.path=/alertmanager-data`**
> 	+ **Alertmanager’ın verilerini** (state bilgisi) kaydedeceği dizindir.
> 	+ Bu dizin şunları saklar:
> 		- Aktif **silences** (susturulan alarmlar)
> 		- Gönderilmiş **bildirim geçmişi**
> 	+ Bu veri kalıcıdır, Alertmanager yeniden başlatıldığında alarm durumu hatırlanır.
> 	+ Eğer bu klasör silinirse, Alertmanager her şeyi **sıfırdan başlatır**.
> 	+ 📌 Eğer bu klasör silinirse, Alertmanager her şeyi **sıfırdan başlatır**.
> 2. **`--config.file=/etc/alertmanager/alertmanager.yml`**
> 	+ Alertmanager’ın **yapılandırma dosyasını** belirtir.
> 	+ Bu dosya:
> 		- Hangi alarmlar nereye gidecek?
> 		- Hangi alıcılar (receivers) var?
> 		- Susturma kuralları (inhibit rules)
> 		- Routing (yönlendirme) kuralları
> 		- Slack, e-posta, webhook tanımları gibi tüm ayarları içerir.
> 	+ 📌 Bu dosya, genellikle `/etc/alertmanager/` gibi bir sistem dizininde olur.


> [!NOTE]
> **Tüm Akış:** Bu komut çalıştığında;
> 1. Alertmanager açılır.
> 2. `/etc/alertmanager/alertmanager.yml` içeriğine göre yapılandırılır.
> 3. `/alertmanager-data` klasörüne alarm/silence bilgilerini yazar.
> 4. HTTP sunucusu başlar (`localhost:9093` varsayılan porttur).

+ Ubuntu işletim sistemin her yeniden başlatıldığında `alertmanager` servisin aktif olabilmesi için:

```shell
sudo systemctl enable alertmanager.service
```

+ `alertmanager` servisini çalıştırıyoruz:

```shell
sudo systemctl start alertmanager.service
```

+ `alertmanager` servisin çalışma durumunu kontrol ediyoruz:

```shell
sudo systemctl status alertmanager.service
```

---

+ Prometheus veya Alertmanager'da bir sorun olması durumunda, izleme sisteminizin kapalı olduğuna dair acil bir bildirim alırsınız.
+ Özellikle üretim(`Production`) ortamlarında oldukça kullanışlı bir hizmet.
+ Prometheus düzgün çalıştığı sürece bu alarm hep aktif olsun. Eğer bir gün bu alarm **gelmezse**, sistemde ciddi bir sorun var!

```shell
sudo vim /etc/prometheus/dead-mans-snitch-rule.yml
```

**dead-mans-snitch-rule:**

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

> 1. **`groups:`**
> 	+ Bu satır, **alarm kurallarını gruplamak** için kullanılır.
> 	+ Prometheus, bu grupları aynı anda işler. Her grup `name` ve `rules` içerir.
> 2.  **`name: dead-mans-snitch`**
> 	+ Bu, bu kurallar grubunun adıdır.
> 	+ Örneğin, Alertmanager loglarında veya arayüzde bu adla görünür.
> 	+ 📌 Anlamı: Bu grup, “Dead Man’s Snitch” tipi alarm kurallarını içeriyor.
> 3. **`rules:`**
> 	+ Bu grup altındaki alarmları listeler.
> 4. **`- alert: DeadMansSnitch`**
> 	+ Bu satır, bir alarm tanımlar.
> 	+ 📌 Alarm adı `DeadMansSnitch` olacak. Alertmanager ve Prometheus UI’de bu isimle görünür.
> 5. **`annotations:`**
> 	+ Alarm hakkında **açıklama, mesaj, yardım bilgisi** eklemek için kullanılır.
> 	+ Alertmanager bu bilgileri e-posta, Slack, webhook gibi yerlere yollar.
> 	```yaml
> 	message: This alert is integrated with DeadMansSnitch.
>	```
> 6. `expr: vector(1)`
> 	+ Bu satır **alarm koşulunu** tanımlar.
> 	+ Bu ifade **her zaman 1 döner**
> 	+ Yani bu alarm **sürekli tetiklenmiş (aktif) durumda olur**


> [!TIP]
> + Prometheus'un canlı olduğunu doğrulamak için
> + Alertmanager'ı test etmek için
> + Harici bir "Dead Man's Snitch" servisi kullanıyorsan (örneğin: [deadmanssnitch.com](https://deadmanssnitch.com))

|Alan|Anlamı|
|---|---|
|`expr: vector(1)`|Sürekli aktif bir alarm üretir|
|`alert: DeadMansSnitch`|Alarmın adı|
|`annotations.message`|Alarm açıklama mesajı|
|`groups.name`|Kural grubunun adı|

+ Alertmanager, 9093 portu üzerinde dışaryıya yayın vermekterdir.

![Alertmanager.png](./Pictures/Alertmanager.png)

---

+ Ayrıca Alertmanager'ın konumunu ve yeni kuralın yolunu belirtmek için Prometheus yapılandırmasını güncellemeniz gerekir.

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
alerting:                    # <<---------------
  alertmanagers:             # <<---------------
    - static_configs:        # <<---------------
        - targets:           # <<---------------
	      - localhost:9093   # <<---------------  
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

+ Yukarıdaki `prometheus.yml` dosyasında `Alertmanager configuration` detaylı inceleyelim:

```yaml
# Alertmanager configuration
alerting:                    # <<---------------
  alertmanagers:             # <<---------------
    - static_configs:        # <<---------------
        - targets:           # <<---------------
	      - localhost:9093   # <<---------------  
          # - alertmanager:9093
```

> 1. `alerting:`
> 	+ Bu blok, Prometheus’un **alertmanager entegrasyonunu** başlatır.
> 	+ Burada Prometheus’a “Uyarı varsa, şu Alertmanager’a gönder” dersin.
> 2. `alertmanagers:`
> 	+ Buraya bir veya birden fazla **Alertmanager adresi** tanımlayabilirsin.
> 3. `static_config:`
> 	+ Alertmanager adreslerini **elle (statik olarak)** tanımlamak için kullanılır.
> 	+ Alternatif: `kubernetes_sd_configs`, `dns_sd_configs` gibi dinamik yöntemler de vardır (daha gelişmiş).
> 4. `targets:`
> 	+ Alertmanager'ların **`host:port`** adreslerini listelersin.
> 	+ Prometheus, alarmları bu adreslere yollar.
> 	+ Bu satırda deniyor ki: “Alertmanager şu anda **aynı makinede (localhost)** ve **9093 portunda** çalışıyor.”
> 	+ 📌 Bu, Alertmanager'ın **varsayılan portudur**.


> [!NOTE]
> **Akış Nasıl İşler?**
> 1. Prometheus bir alarm üretir (örneğin CPU > %90).
> 2. `prometheus.yml` dosyasındaki bu yapı sayesinde:
> 	+ Alarm **Alertmanager’a** HTTP üzerinden (`localhost:9093/api/v1/alerts`) gönderilir.
> 3. Alertmanager, alarmları Slack, e-posta, webhook gibi yerlere yollar.

| Konu         | Açıklama                                                                              |
| ------------ | ------------------------------------------------------------------------------------- |
| Port         | Alertmanager varsayılan olarak **9093** portunda çalışır.                             |
| Hostname     | `localhost` yerine Docker içinde `alertmanager` gibi servis adları da kullanılabilir. |
| Multi-Target | Aynı anda birden fazla Alertmanager hedefi tanımlayabilirsin.                         |

+ Prometheus servisini yeniden başlatmadan önce Prometheus yapılandırmasını(`Prometheus Config`) kontrol etmek her zaman iyi bir fikirdir.

```shell
promtool check config /etc/prometheus/prometheus.yml
```

**promtool Çıktısı:**

```shell
Checking prometheus.yml
  SUCCESS: 1 rule files found
 SUCCESS: prometheus.yml is valid prometheus config file syntax

Checking dead-mans-snitch-rule.yml
  SUCCESS: 1 rules found
```

+ `prometheus.yml` dosyasında yapılan değişikliklerin geçerli olabilmesi için:

```shell
sudo systemctl restart prometheus.service
```

+ Tarayıcıdan `http://192.168.1.129:9090` adresine gittiğimizde `Alerts` bölümünde görüncektir. 

![Alertmanager_DeadMansSnitch](./Pictures/Alertmanager_DeadMansSnitch.png)

## 7. Adım:

### Alertmanager ile Slack Entegrasyonu:

+ Alertmanager'dan oluşan tüm alarmların gönderileceği bir Slack kanalı oluşturacağız.
+ `Create a new channel` butonu ile yeni bir `alert` adında bir channel oluşturuyoruz.

![slack_channel](./Pictures/slack_channel.png)

+ Aşağıdaki resimde de görüleceği üzeri `#alert channel` oluşturulmuştur. (*Resimde 3. Adım*)
+ Daha sonra sıfırdan yeni bir Slack uygulaması(`Slack Apps`) oluşturalım(*Resimde 4. Adım*)

![slack_alert_channel](./Pictures/slack_alert_channel.png)

![slack_Build](./Pictures/slack_Build.png)


![slack_create_an_app](./Pictures/slack_create_an_app.png)

+ İsmini `Prometheus` olarak veriyoruz ve bir çalışma alanı olarak `Grafana_Prometheus` seçiyoruz.

![](./Pictures/slack_Name_app.png)


![](./Pictures/slack_Incoming_Webhooks.png)

![slack_active_incoming_webhooks](./Pictures/slack_active_incoming_webhooks.png)


![slack_select_alerts](./Pictures/slack_select_alerts.png)



![slack_copy_URL](./Pictures/slack_copy_URL.png)

```shell
sudo vim /etc/alertmanager/alertmanager.yml
```

**alertmanager.yml**

```yaml
route:
  group_by: ['alertname']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 6m #1h
  receiver: 'web.hook'
  routes:
  - receiver: slack-notifications
    match:
      severity: warning
receivers:
  - name: 'web.hook'
    webhook_configs:
      - url: 'http://127.0.0.1:5001/'
  - name: slack-notifications
    slack_configs:
    - channel: "#alerts"
      send_resolved: true
      api_url: "https://hooks.slack.com/services/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"
      title: "{{ .GroupLabels.alertname }}"
      text: "{{ range .Alerts }}{{ .Annotations.message }}\n{{ end }}"
inhibit_rules:
  - source_match:
      severity: 'critical'
    target_match:
      severity: 'warning'
    equal: ['alertname', 'dev', 'instance']
```


```shell
sudo vim /etc/prometheus/batch-job-rules.yml
```

**batch-job-rules.yml**

```shell
groups:
- name: batch-job-rules
  rules:
  - alert: JenkinsJobExceededThreshold
    annotations:
      message: Jenkins job exceeded a threshold of 30 seconds.
    expr: jenkins_job_duration_seconds{job="backup"} > 30
    for: 1m
    labels:
      severity: warning
```


```shell
sudo vim /etc/prometheus/prometheus.yml
```

**prometheus.yml**

```shell
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
          - localhost:9093
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - dead-mans-snitch-rule.yml
  - batch-job-rules.yml
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

**Çıktı:**

```shell
Checking /etc/prometheus/prometheus.yml
  SUCCESS: 1 rule files found
 SUCCESS: /etc/prometheus/prometheus.yml is valid prometheus config file syntax

Checking /etc/prometheus/batch-job-rules.yml
  SUCCESS: 1 rules found

```


```shell
curl -v -X POST -u admin http://192.168.1.129:9090/-/reload
```

**Curl Çıktısı:**

```shell
*   Trying 192.168.1.129:9090...
* Connected to 192.168.1.129 (192.168.1.129) port 9090 (#0)
* Server auth using Basic with user 'admin'
> POST /-/reload HTTP/1.1
> Host: 192.168.1.129:9090
> Authorization: Basic YWRtaW46MTIzNHR5bw==
> User-Agent: curl/7.81.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Mon, 21 Jul 2025 15:22:27 GMT
< Content-Length: 0
<
* Connection #0 to host 192.168.1.129 left intact
```



```shell
echo "jenkins_job_duration_seconds 31.87" | curl --data-binary @- http://localhost:9091/metrics/job/backup
```



![slack_notification](./Pictures/slack_notification.png)

## Kaynak:
1. [How to Install Prometheus and Grafana on Ubuntu? (Node Exporter & Alertmanager & Pushgateway](https://www.youtube.com/watch?v=Z7GxBf6us8Y)
2. 