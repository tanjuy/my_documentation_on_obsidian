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
> **Explanation:**
> Temel taslağın sunmakta ve   tilda(~) URI küçük harf veya büyük harf duyarlığına bakar.
> Yani URI, *linux* olanla *Linux* olan aynı değildir.
###### Örnek 1:
```nginx
location ~ \.(png) {
	try_files $uri $uri/ =404;
	add_header Cache-Control no-store;
}
```
> **Explanation:**
> tilda(~) ifadesi : ==case sensitive regular expression== yani küçük büyük harfe duyarlı ve düzenli ifadeleri dikkate almaktadır. `\` backslash *nokta işaretinin* özel anlama gelmesini durduruyor. Yani Regex de *nokta işareti* her hangi bir karaktere karşılık geliyor. 
> [[Nginx Directives#Cache-Control|Cache-Control no-store]] bakınız. 

