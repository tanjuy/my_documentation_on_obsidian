#docker 
## Compose Deploy Specification:

##### update_config:
Servislerin nasıl güncelleneceğini yapılandırır. rolling update yapılandırılması için kullanışlı.
1. `parallelism`: Aynı anda günçellencek container sayısı
	+ Aynı anda 2 container güncellenir (`parallelism: 2`).
2. `delay`: Bir container gurubun güncellenmesi arasında beklenen süre.
	+ Her iki container güncellendikten sonra 10 saniye beklenir (`delay: 10s`).



Kaynak: [Compose Deploy Specification](https://docs.docker.com/compose/compose-file/deploy/)