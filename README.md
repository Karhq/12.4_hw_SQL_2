# Домашнее задание к занятию «SQL. Часть 2» - Карпов Роман
---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

#### Ответ:  
```sql  
select concat(s.first_name, ' ', s.last_name), c.city, count(c2.customer_id) as COUNTC from staff s
join address a ON s.address_id = a.address_id 
join city c ON a.city_id = c.city_id
join store s2 on s2.store_id = s.store_id 
join customer c2 on s2.store_id = c2.store_id 
group by s.first_name, s.last_name, c.city 
HAVING COUNTC > 300
```  
![скрин](https://github.com/Karhq/12.4_hw_SQL_2/blob/main/Nom1.png)  

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

#### Ответ:  
```sql
select count(f.`length`)  from film f
where length >  (select avg(f2.`length`) from film f2)
```

![скрин](https://github.com/Karhq/12.4_hw_SQL_2/blob/main/Nom2.png)
  
### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

#### Ответ:  
```sql
select MONTH (p.payment_date) AS Месяц, COUNT(p.payment_id) AS Количество_аренд, SUM(p.amount) AS Сумма_платежей 
from payment p 
group by month(payment_date)
order by sum(p.amount) DESC 
limit 1
```

![скрин](https://github.com/Karhq/12.4_hw_SQL_2/blob/main/Nom3.png)
