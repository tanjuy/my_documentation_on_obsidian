# Prometheus-Grafana ve Docker-Compose

+ Bu proje, Docker Compose kullanarak Prometheus ve Grafana servislerini hızlıca çalıştırmak için hazırlanmıştır. 
+ Zamanla yeni servisler (Node Exporter, Alertmanager vb.) eklenerek geliştirilecektir.

## İçindekiler

- [Özellikler](##özellikler)
- [Kurulum](##Kurulum)
- [Belgelendirme](##Belgelendirme)

## Özellikler

- Prometheus: Metrik toplama ve saklama.
- Grafana: Verileri görselleştirme ve dashboard desteği.
- Docker Compose ile tek komutla çalıştırma.

## Kurulum:
### Monitoring Sunucu:


1. Bu repository'yi klonlayın:

```shell
git https://github.com/tanjuy/prometheus-grafana-compose.git
```


> [!NOTE]
> + Host makineye indirilen prometheus-grafana-compose projenin yapısı:
> ```shell
> prometheus-grafana-compose
>├── DOC.md
>├── LICENSE
>├── Pictures
>│   ├── docker_compose_grafana_DS.png
>│   ├── docker_compose_grafana_dashboard.png
>│   ├── docker_compose_grafana_dashboard1.png
>│   ├── docker_compose_grafana_dashboard3.png
>│   ├── docker_compose_grafana_dashboard4.png
>│   └── docker_compose_prometheus_DS.png
>├── README.md
>├── docker-compose.yml
>└── prometheus
>   └── prometheus.yml
>
> 2 directories, 11 files
> ```


2. İndirilen git dosyasına giriniz:

```shell
cd prometheus-grafana-compose
```

3. Servisleri başlatın:

```shell
docker compose up -d
```

4. Servis portları:
	+ Prometheus: [http://localhost:9090](http://localhost:9090)
	+ Grafana: [http://localhost:3000](http://localhost:3000) (Varsayılan kullanıcı: `admin`, şifre: `admin`)

### Node Sunucuları:


## Belgelendirme:

+ Prometheus-Grafana-Compose hakkında daha fazla bilgi almak için