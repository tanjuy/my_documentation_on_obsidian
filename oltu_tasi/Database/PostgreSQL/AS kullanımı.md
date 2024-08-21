#database
```
SELECT employee."name" AS employee_name, department."name" department_name , city FROM employee
	INNER JOIN department ON employee.department_id = department.id;
```

> **Explanation:**
> employee tablosunda name kolon ismini AS ile employee_name olarak değiştirdik. department tablosunda ise AS anahtar ifadesini kullanmadan yaptık. Ayrıca ==City== sadece departmet tabloosunda olduğu için direk yazabilidik.

```sql
SELECT e."name" AS employee_name, d."name" department_name , city 
FROM employee AS e
	INNER JOIN department AS d ON e.department_id = d.id;
```
>[!CAUTION] Dikkat
>`FROM employee AS e` ve  `INNER JOIN department AS d` ile daha ileri bir takma isim işlemi yaptık.


