#nginx 
```
client_body_buffer_size 10M
```
> **Explanation:**
> client’dan post isteğini gönderildiğinde buffer da tutulacağı boyut miktarını belirliyor.Bu, sunucunun tek seferde 10 MB'a kadar olan request body verilerini geçici olarak belleğe almasına izin verir.

---
## add header:
### Cache-Control:
```
add_header Cache-Control: max-age=120
```
> **Explanation:**
>  + max-age isteği yönergesi, bir kaynağın önbelleğe alınmış bir kopyasının süresinin dolması için gereken süreyi saniye cinsinden tanımlar.
>  + Yanıtın belirli bir süre (saniye cinsinden) önbelleğe alınmasını belirtir
>  + 120 saniye sonra ==tarayıcı== kendi önbellekten almayarak tekrardan sunucudan istek yapacaktır.

---
```
add_head Cache-Control: no-cache
```
> **Explanation:**
> + no-cache directive, tarayıcının bir yanıtı önbelleğe alabileceği ancak önce bir kaynak sunucuya bir doğrulama isteği göndermesi gerektiği anlamına gelir.
> + no-cache yönergesinde, tarayıcı önbelleğe almıyor anlama gelmesin, bu yönergede ==önbellekleme yapmaktedır.==

```
add_header Cache-Control: no-store
```
> **Explanation:**
> + Yanıt, hiçbir zaman önbelleğe alınmamalıdır. Her istek yapıldığında sunucudan çekiliyor.
> + Bu ayar geneliikle hasas veriler için kullanılır. Örneğin; kişisel banka detayları için
> + Server veya Client tarafında önbellek depolaması yapmayacak

```
add_header Cache-Control: Public
```
> **Explanation:**
> + Bir kaynak herhangi bir önbellek tarafından önbelleğe alınabilir. Örneğin; ortadaki bir sunucuda olabilir, sunucunun kendisi veya tarayıcı tarafında da olabilir.
> + Yanıt, herhangi bir önbellek tarafından önbelleğe alınabilir.

```
add_header Cache-Control: Private
```
> **Explanation:**
> + Yanıt sadece istemciye özel olarak önbelleğe alınabilir, proxy önbelleklerinde tutulmamalıdır.
> + Ortadaki sunucu önbelleğe almayacaktır.