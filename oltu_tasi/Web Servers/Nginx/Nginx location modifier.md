#nginx 
```nginx
location [modifier] [URI] {
  ...
  ...
}
```

> [!INFO] Bilgi
> Location bloğunun genel şablonu

### Regex Case Sensitive Eşleşme:
```nginx
location ~ [URI] {
	...
	...
}
```

###### Örnek 1:
```nginx
location ~ \.(png) {
	try_files $uri $uri/ =404;
	add_header Cache-Control no-store;
}
```
> **Explanation:**
> tilda(~) ifadesi : case sensitive regular expression yani küçük büyük harfe duyarlı ve düzenli ifadeleri dikkate almaktadır.
> [[Nginx Directives#Cache-Control|Cache-Control no-store]] bakınız. 