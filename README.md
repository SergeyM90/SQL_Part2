# Домашнее задание к занятию «SQL. Часть 2» Sergey Mironov-SYS-20

# Задание 1  
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:  

фамилия и имя сотрудника из этого магазина;  
город нахождения магазина;  
количество пользователей, закреплённых в этом магазине.  


select concat(staff.last_name, ' ' ,staff.first_name) as staff_member, city.city as store_address,  count(customer_id) as num_of_customers  
from store  
join customer on store.store_id = customer.store_id  
join address on store.address_id = address.address_id  
join city on address.city_id = city.city_id  
join staff on store.store_id = staff.store_id  
group by staff.staff_id, city.city_id  
having num_of_customers > 300;  

![image](https://github.com/SergeyM90/SQL_Part2/assets/84016375/71b985dd-51c8-44e9-91c0-9d7926b9e485)


# Задание 2  

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.  

select count(film_id)  
from film  
where film.length >  
      (select avg(film.length)  
       from film);  

![image](https://github.com/SergeyM90/SQL_Part2/assets/84016375/d91f3ec3-c699-4594-b7bc-ab010f66f7f4)


# Задание 3  
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.  

select  date_format(payment.payment_date, '%M-%Y') as month, count(payment.payment_id) as payments,  sum(payment.amount) as sum  
from payment  
group by date_format(payment.payment_date, '%M-%Y')  
order by sum(payment.amount) desc  
limit 1;  

![image](https://github.com/SergeyM90/SQL_Part2/assets/84016375/546b3e07-d871-47da-a9e7-4ef8a46d5899)

