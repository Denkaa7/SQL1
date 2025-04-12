# Домашнее задание к занятию "`SQL. Часть 1`" - `Бедник Денис`

---

### Задание 1

`Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.`

```sql
SELECT DISTINCT district
FROM address
WHERE district LIKE "K%a"
ORDER BY district;
```


---

### Задание 2

`Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00`
```sql
SELECT *
FROM payment
WHERE payment_date BETWEEN '2005-06-15' AND '2005-06-18' 
AND amount > 10.00 ;
```

---

### Задание 3

`Получите последние пять аренд фильмов.`

```sql
SELECT * 
FROM rental
ORDER BY rental_id DESC
LIMIT 5;
```

---

### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.


```sql
SELECT REPLACE( LOWER(first_name), 'll', 'pp' ) , LOWER(last_name) 
FROM customer
WHERE active = 1 
AND ( first_name = 'Kelly' OR first_name = 'Willie' ) ;
```

---

### Задание 5
` Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.`



```sql
SELECT SUBSTRING_INDEX( email , '@', 1), 
       SUBSTRING_INDEX( email , '@', -1)
FROM customer;
```


## Подскажите как в этом задании сделать так, чтобы выводились значения которые не крайние? Например, иеется такая строка 1@2@3@4@5@6, как получить только 2 или 3 или 4 или 5?


---

### Задание 6

' Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.'

```sql
SELECT CONCAT( UPPER(SUBSTRING(email, 1 , 1)), LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', 1), 2))) , 
       SUBSTRING_INDEX( email , '@', -1)
FROM customer;
```
