```sql
UPDATE table_name
SET
	col1 = val1, col2 = val2
WHERE
	condition
```

> **Explanation:**
> + UPDATE'in genel şablonu


```sql
UPDATE employee
SET
	salary = 25000
WHERE 
	salary > 25000
RETURNING *
```

> **Explanation:**
> - Eğer 25000 büyük değerler bulursa bu değerleri değiştirir ve değişen değerleri ekrana geri basar. Bu geri dönme işlemini  <span style="color:red"> RETURNING *  </span>yapar, burada \* tüm kolonları anlamındadır.


```sql
UPDATE employee
SET
	salary = 20000
WHERE
	salary > 20000
RETURNING "name"
```

> **Explanation :**
> - <span style=color:blue>RETURNING "name"</span> ifadesi ile sadece isim kolonu geri dönecektir.

```sql
UPDATE employee
SET
	email = 'temp@email.com'
WHERE
	email IS Null;
```
>[!CAUTION]
>email = Null ifadesi yanlıştır ama email IS Null ifadesi doğrudur.

