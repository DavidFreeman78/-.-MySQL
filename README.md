Lesson_2

/* Задача 1
Установите СУБД MySQL. Создайте в домашней директории файл .my.cnf, задав в нем логин и пароль, который указывался при установке.
*/

[mysql]
user=root
password=*********

сохранить файл в дерикторию C:\Windows\

/* Задача 2
Создайте базу данных example, разместите в ней таблицу users, состоящую из двух столбцов, числового id и строкового name
*/

mysql> CREATE DATABASE example;
mysql> USE example;
mysql> CREATE TABLE users (id INT UNSIGNED, name VARCHAR(255) NOT NULL UNIQUE);

/* Задача 3
Создайте дамп базы данных example из предыдущего задания, разверните содержимое дампа в новую базу данных sample.
*/

mysqldump example > example.sql

mysql> CREATE DATABASE sample;

mysql sample < example.sql

/* Задача 4
(по желанию) Ознакомьтесь более подробно с документацией утилиты mysqldump. Создайте дамп единственной таблицы help_keyword базы данных mysql. Причем добейтесь того, чтобы дамп содержал только первые 100 строк таблицы.
*/

