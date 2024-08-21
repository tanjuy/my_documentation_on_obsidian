#ansible 
###### Örnek 1: 
```
[web_servers]
192.168.1.128
192.168.1.133

[db_servers]
192.168.1.132

[file_servers]
192.168.1.136
```
> **Explanation:**
> Sunucularımızı yukarıda göründüğü gibi gruplamış olduk. Örneğin; ==web_servers== veya ==db_servers== grubu şeklinde grupladık. Böylelikle [[Playbook Config#Örnek 1 Targeting specific Node|playbook]] dosyasında *hosts=web_servers* kullanarak yapacağımız işlemi tüm sunuculara değil sadece ==web_servers'e== uygulamış oluyoruz.

