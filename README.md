# 12.4 SQL. Часть 2

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

#### *Ответ:*
```sql
SELECT CONCAT(s.first_name , " ", s.last_name) AS 'Сотрудник магазина', cm.city AS 'Город нахождения магазина', COUNT(c.customer_id) AS 'Количество покупателей'
FROM staff AS s
JOIN address AS a ON a.address_id = s.address_id
JOIN city AS cm ON cm.city_id = a.city_id
JOIN store AS st ON st.store_id = s.store_id
JOIN customer AS c ON c.store_id = s.store_id
GROUP BY staff_id
HAVING COUNT(c.customer_id) > 300;
```
![1.1](https://github.com/IMiroxxI/SQL-2/blob/main/img/1.1.png)
Делаем то же самое через DBeaver.
![1.2](https://github.com/IMiroxxI/SQL-2/blob/main/img/1.2.png)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

#### *Ответ:*
```sql
SELECT COUNT(length) AS 'Количество фильмов больше средней продолжительности'
FROM film
WHERE length > (SELECT AVG(length) FROM film);
```
![2.1](https://github.com/IMiroxxI/SQL-2/blob/main/img/2.1.png)
Делаем то же самое через DBeaver.
![2.2](https://github.com/IMiroxxI/SQL-2/blob/main/img/2.2.png)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

#### *Ответ:*
```sql
SELECT DATE_FORMAT(payment_date, '%Y.%m') AS 'Год и месяц c наибольшей суммой платежей', COUNT(rental_id) AS 'Количество аренд за месяц'
FROM payment
GROUP BY DATE_FORMAT(payment_date, '%Y.%m')
ORDER BY SUM(amount) DESC
LIMIT 1;
```
![3.1](https://github.com/IMiroxxI/SQL-2/blob/main/img/3.1.png)
Делаем то же самое через DBeaver.
![3.2](https://github.com/IMiroxxI/SQL-2/blob/main/img/3.2.png)

---
