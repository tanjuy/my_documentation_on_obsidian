#database 
> [!CAUTION]
> `sudo -i -u postgres` komut ile posgres kullanıcısına geçmeniz gerekmektedir

```
$ createdb -U postgres database_name
```
> **Explanation:**
> + createdb script ile bir veritabanı oluşturuyoruz
> + -U username (--username=username) 
> + User name to connect as.


```
$ postgres@ottoman:~$ psql -d test
test=# CREATE DATABASE join_kavrami;
test=# \l
```
> **Explanation:**
> + Önce test veritabanına bağlandık, bu herhangi bir veritabanı da olabilirdi
> + Sonraki komuta join_kavrami adında veritabani oluşturduk.
> + \l ile database'leri listeledik.


