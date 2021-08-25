Lesson_3

/* Задача 1
Написать Cкрипт, добавляющий в БД vk, которую создали на занятии, 3 новые таблицы (с перечнем полей, указанием индексов и внешних ключей)
*/

DROP TABLE IF EXISTS users_statuses;
CREATE TABLE users_statuses(
	id SERIAL,
	user_id BIGINT UNSIGNED NOT NULL,
	name VARCHAR(255),
	created_at DATETIME DEFAULT NOW(),
	updated_at DATETIME ON UPDATE CURRENT_TIMESTAMP,
	FOREIGN KEY (user_id) REFERENCES users(id));

DROP TABLE IF EXISTS users_storys;
CREATE TABLE users_storys(
	id SERIAL,
	user_id BIGINT UNSIGNED NOT NULL,
	story_type_id BIGINT UNSIGNED NOT NULL,
	body VARCHAR(255),
	filename VARCHAR(255),
	metadata JSON,
	created_at DATETIME DEFAULT NOW(),
	updated_at DATETIME ON UPDATE CURRENT_TIMESTAMP,
	FOREIGN KEY (user_id) REFERENCES users(id),
	FOREIGN KEY (story_type_id) REFERENCES users_storys(id));

DROP TABLE IF EXISTS users_music;
CREATE TABLE users_music(
	id SERIAL,
	user_id BIGINT UNSIGNED NOT NULL,
	music_type_id BIGINT UNSIGNED NOT NULL,
	communitiy_id BIGINT UNSIGNED NOT NULL,
	track_name VARCHAR(255),
	metadata JSON,
	created_at DATETIME DEFAULT NOW(),
	updated_at DATETIME ON UPDATE CURRENT_TIMESTAMP,
	FOREIGN KEY (user_id) REFERENCES users(id),
	FOREIGN KEY (communitiy_id) REFERENCES communities(id));

