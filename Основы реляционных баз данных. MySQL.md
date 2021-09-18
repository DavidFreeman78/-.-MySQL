Lesson_6

/* 
Практическое задание по теме “Операторы, фильтрация, сортировка и ограничение. Агрегация данных”.
Работаем с БД vk и данными, которые вы сгенерировали ранее
*/

/* Задача 1 
Пусть задан некоторый пользователь. Из всех пользователей соц. сети найдите человека, 
который больше всех общался с выбранным пользователем (написал ему сообщений).
*/

use vk;


SELECT (
	SELECT firstname from users WHERE id = best_friend_by_message_id) AS best_fiend,
        MAX(count_messages) as count_messages 
FROM (
SELECT best_friend_by_message_id, COUNT(*) AS count_messages FROM (
	SELECT to_user_id AS best_friend_by_message_id FROM messages WHERE from_user_id = 2
	union ALL
	SELECT from_user_id  FROM messages WHERE to_user_id = 2
) AS T
GROUP BY best_friend_by_message_id
) AS F
GROUP BY best_fiend
ORDER BY  count_messages DESC
LIMIT 1;


/* Задача 2 
Подсчитать общее количество лайков, которые получили пользователи младше 10 лет..
*/

SELECT COUNT(*) as 'Likes' FROM profiles WHERE (YEAR(NOW())-YEAR(birthday)) < 10;

/* Задача 3 
Определить кто больше поставил лайков (всего): мужчины или женщины.
*/

SELECT gender, COUNT(*) as 'Кол-во' FROM profiles GROUP BY gender;
 
-- Или
    
SELECT 
    CASE(gender)
        WHEN 'm' THEN 'мужчины'
        WHEN 'f' THEN 'женщины'
        ELSE 'нет'
    END as gender
    , COUNT(*) as 'Кол-во:' FROM profiles GROUP BY gender;






