
# Alertmanager:

## Örnek 1: alertmanager.yml

```shell
sudo vim /etc/alertmanager/alertmamager.yml
```

**alertmanager.yml**

```yaml
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

### Genel Yapısı:

+ **Bu yapılandırma üç ana bölümden oluşuyor:**
	1. **`route:`** → Alarmların nasıl gruplandığı ve hangi alıcıya gönderileceği. 
	2. **`receivers:`** → Alarmların gönderileceği hedef sistemler (örneğin webhook, e-posta, Slack).
	3. **`inhibit_rules:`** → Belirli uyarıların diğerlerini bastırma (susturma) kuralları.

### `group_by: ['alertname']`:

+ `group_by: ['alertname']` ifadesi Alertmanager'ın **aynı uyarı türünden gelen alarmları gruplayarak tek bir bildirimde göndermesini** sağlar.
+ **Aynı `alertname` etiketine sahip olan alarmları tek bir grup halinde topla ve beraber bildir.**
+ Prometheus'tan gelen alarmlar, genellikle şu şekilde etiketler içerir:

```yaml
labels:
  alertname: HighCPUUsage
  instance: server1
  severity: warning
```

+ Eğer 3 farklı sunucuda aynı `alertname` ile alarm tetiklenirse:

| Sunucu | alertname    | instance |
| ------ | ------------ | -------- |
| srv1   | HighCPUUsage | srv1     |
| srv2   | HighCPUUsage | srv2     |
| srv3   | HighCPUUsage | srv3     |

> [!NOTE]
> **Normalde:**
> + 3 ayrı alarm tetiklenir.
> + Alertmanager 3 bildirim yollar.
> 
> `group_by: ['alertname']` ile:
> + Hepsi **tek bildirim** içinde gruplanır: "**Alert: HighCPUUsage — srv1, srv2, srv3**"


> [!TIP]
> Bu yapı sayesinde:
> + ✅ Daha **az bildirim** oluşur.
> + ✅ Slack/mail gibi ortamlarda **daha sade ve toplu mesajlar** görünür.
> + ✅ Spam azalır.
> + ✅ Operasyonel ekip daha net bilgi alır.

#### Diğer Etiketlerle Kullanımı:

+ Sadece `alertname` değil, başka etiketlerle de gruplayabilirsin:

```yaml
group_by: ['alertname', 'instance', 'severity']
```

> + Bu durumda sadece hem alertname **hem instance hem de severity** aynıysa grup yapılır.

#### Diğer Parametrelerle Etkileşim:

+ Bu ayar şunlarla **beraber** çalışır:

| Parametre         | Açıklama                                                                     |
| ----------------- | ---------------------------------------------------------------------------- |
| `group_wait`      | Yeni grup ilk oluştuğunda ne kadar beklenir (başka alarmlar gelecek mi diye) |
| `group_interval`  | Aynı grup için ne kadar süreyle tekrar bildirim yapılmaz                     |
| `repeat_interval` | Alarm çözülmediyse ne kadar sonra tekrar bildirilir                          |
##### Basit Örnek:

```yaml
group_by: ['alertname']
group_wait: 30s
group_interval: 5m
repeat_interval: 1h
```

> 1. `HighCPUUsage` uyarısı srv1'den geldi → Alertmanager 30 saniye bekler.
> 2. Bu sürede srv2 ve srv3'ten de aynı `alertname` ile alarm geldiyse
> 3. Tümünü **tek bildirim** olarak Slack veya e-postaya gönderir.

| Amaç                            | group_by Ayarı                                                       |
| ------------------------------- | -------------------------------------------------------------------- |
| Daha az bildirim                | `['alertname']` yeterli                                              |
| Sunucu bazlı ayrım da önemliyse | `['alertname', 'instance']`                                          |
| Tam kontrol istiyorsan          | `['alertname', 'severity', 'team', 'instance']` gibi çoğaltabilirsin |
