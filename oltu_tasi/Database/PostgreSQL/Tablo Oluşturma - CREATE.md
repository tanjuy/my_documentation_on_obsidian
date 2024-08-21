```sql
CREATE INTO employee (
	"id" SERIAL PRIMARY KEY,
	"name" VARCHAR(50),
	age INT,
	salary INTEGER,
	department_id INT REFERENCES department("id")  -- FOREIGN KEY burası
);
```
>**Explanation**:
> employee tablosunda ==FOREIGN KEY== kullanılmış departmet_id, department tablosundaki id'den değerleri alıyor.

```sql
CREATE INTO employe (
	"id" SERIAL PRIMARY KEY,
	"name" VARCHAR(50),
	age INT,
	salary INTEGER,
	department_id INTEGER,
	FOREIGN KEY(department_id) REFERENCES department("id")
);
```
>[!TIP] ipucu
> FOREIGN KEY kullanımında bir çok alternatif yol mevcuttur. Bir yukarıdaki komut ile aynı işlemi yapar.

---
