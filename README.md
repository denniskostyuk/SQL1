# Домашнее задание к занятию «SQL. Часть 1» - Костюк Денис

## Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

### Ответ 1

SELECT DISTINCT district as район
FROM address
WHERE district LIKE 'K%a' AND district NOT LIKE '% %';

## Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

### Ответ 2

В задании не было, но я еще упорядочил по дате, чтобы удобнее было проверять

SELECT * 
FROM payment
WHERE (CAST(payment_date as date) BETWEEN "2005-06-15" AND "2005-06-18") AND amount > 10
ORDER BY payment_date;

## Задание 3
Получите последние пять аренд фильмов.

### Ответ 3

SELECT *
FROM rental
ORDER BY rental_date DESC
LIMIT 5;

## Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

•	все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,

•	замените буквы 'll' в именах на 'pp'.

### Ответ 4

SELECT *
FROM customer
WHERE (first_name = "Kelly" OR first_name = "Willie") AND active = 1;

SELECT customer_id, store_id, LOWER(first_name), LOWER(last_name), email, address_id, active, create_date, last_update  
FROM customer
WHERE (first_name = "Kelly" OR first_name = "Willie") AND active = 1;

SELECT customer_id, store_id, REPLACE(LOWER(first_name),'ll','pp'), REPLACE(LOWER(last_name),'ll','pp'), email, address_id, active, create_date, last_update  
FROM customer
WHERE (first_name = "Kelly" OR first_name = "Willie") AND active = 1;

## Задание 5*
Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

### Ответ 5

SELECT SUBSTRING_INDEX(email, '@', 1), RIGHT(email,LENGTH(email)-LENGTH(SUBSTRING_INDEX(email, '@', 1))-1), email 
FROM customer;

## Задание 6*
Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

### Ответ 6

SELECT CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', 1),1)),LOWER(RIGHT(SUBSTRING_INDEX(email, '@', 1),LENGTH(SUBSTRING_INDEX(email, '@', 1))-1))),CONCAT(UPPER(LEFT(RIGHT(email,LENGTH(email)-LENGTH(SUBSTRING_INDEX(email, '@', 1))-1),1)),LOWER(RIGHT(RIGHT(email,LENGTH(email)-LENGTH(SUBSTRING_INDEX(email, '@', 1))-1),LENGTH(RIGHT(email,LENGTH(email)-LENGTH(SUBSTRING_INDEX(email, '@', 1))-1))-1))), email 
FROM customer;




