```sql
DELETE FROM table_name
WHERE
	condition
```
> **Explanation:**
> DELETE'in temel şablonu

---
```sql
DELETE FROM employee
WHERE
	id = 2;
```
>  **Explanation:**
>  employee'u tablosundan id'si 2 olanı siliyoruz
---

```sql
DELETE FROM employee;
```
> [!WARNING]  
> Çok dikkat edilmesi gerekir tüm tablo içeriğini siler

---

```sql
DELETE FROM employee
WHERE
	age > 25
RETURNING *;
```
>   **Explanation:**
>   <span style=color:red>RETURNING</span> ile employee tablosundan silinen verileri ekrana basar.



