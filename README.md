Lesson_5

/* 
Практическое задание по теме “Операторы, фильтрация, сортировка и ограничение”
*/

/* Задача 1 
Пусть в таблице users поля created_at и updated_at оказались незаполненными. Заполните их текущими датой и временем.
*/

use lesson_5;

UPDATE users 
    SET created_at = NOW(); 

UPDATE users 
    SET updated_at = NOW(); 

/* Задача 2
Таблица users была неудачно спроектирована. Записи created_at и updated_at были заданы типом VARCHAR и в них долгое время помещались значения в формате "20.10.2017 8:10". Необходимо преобразовать поля к типу DATETIME, сохранив введеные ранее значения.
*/

use lesson_5;

ALTER TABLE users
ALTER COLUMN created_at DATETIME;

ALTER TABLE users
ALTER COLUMN updated_at DATETIME;

/* Задача 3
 В таблице складских запасов storehouses_products в поле value могут встречаться самые разные цифры: 0, если товар закончился и выше нуля, если на складе имеются запасы. Необходимо отсортировать записи таким образом, чтобы они выводились в порядке увеличения значения value. Однако, нулевые запасы должны выводиться в конце, после всех записей.
*/

use lesson_5;

INSERT INTO storehouses_products VALUES
('1', '1', '1', 0, NOW(), NOW()),
('2', '2', '2', 2500, NOW(), NOW()),
('3', '3', '3', 0, NOW(), NOW()),
('4', '4', '4', 30, NOW(), NOW()),
('5', '5', '5', 500, NOW(), NOW()),
('6', '6', '6', 1, NOW(), NOW());


SELECT * FROM storehouses_products WHERE value > 1 ORDER BY value ASC;

SELECT *
FROM storehouses_products
ORDER BY 
	IF(`value` > 0, 0, 1), `value`;

/* Задача 4
(по желанию) Из таблицы users необходимо извлечь пользователей, родившихся в августе и мае. Месяцы заданы в виде списка английских названий ('may', 'august')
*/

use lesson_5;

SELECT name, birthday_at, 
CASE 
 WHEN DATE_FORMAT(birthday_at, '%m') = 05 THEN 'may'
 WHEN DATE_FORMAT(birthday_at, '%m') = 08 THEN 'august'
    END AS mounth
FROM
    users WHERE DATE_FORMAT(birthday_at, '%m') = 05 OR DATE_FORMAT(birthday_at, '%m') = 08;
    
/* Задача 5
(по желанию) Из таблицы catalogs извлекаются записи при помощи запроса. SELECT * FROM catalogs WHERE id IN (5, 1, 2); Отсортируйте записи в порядке, заданном в списке IN.
*/

SELECT * FROM catalogs WHERE id IN (5, 1, 2);

SELECT * FROM catalogs WHERE id IN (5, 1, 2) 
ORDER BY CASE
    WHEN id = 5 THEN 0
    WHEN id = 1 THEN 1
    WHEN id = 2 THEN 2
END;

/*
Практическое задание теме “Агрегация данных”
*/

/* Задача 1
Подсчитайте средний возраст пользователей в таблице users
*/

SELECT ROUND(AVG((TO_DAYS(NOW()) - TO_DAYS(birthday_at)) / 365.25), 0) AS AVG_Age FROM users;

/* Задача 2
Подсчитайте количество дней рождения, которые приходятся на каждый из дней недели. Следует учесть, что необходимы дни недели текущего года, а не года рождения.
*/

SELECT DATE_FORMAT(DATE(CONCAT_WS('-', YEAR(NOW()), MONTH(birthday_at), DAY(birthday_at))), '%W') AS day, COUNT(*) AS total
FROM users
GROUP BY day
ORDER BY total DESC;

/* Задача 3
(по желанию) Подсчитайте произведение чисел в столбце таблицы
*/


CREATE TABLE numbers(value SERIAL PRIMARY KEY);

INSERT INTO numbers VALUES
(NULL),
(NULL),
(NULL),
(NULL),
(NULL)
;

SELECT ROUND(exp(SUM(log(value))), 0) AS factorial FROM numbers;





