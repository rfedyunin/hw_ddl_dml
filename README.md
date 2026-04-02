# Домашнее задание к занятию "`Работа с данными (DDL/DML)`" - `Федюнин Р.Ю.`

---

### Задание 1

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

![sql_1_3.jpg](https://github.com/rfedyunin/hw_ddl_dml/blob/main/img/sql_1_3.jpg)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

![sql_1_5.jpg](https://github.com/rfedyunin/hw_ddl_dml/blob/main/img/sql_1_5.jpg)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

![sql_1_8.jpg](https://github.com/rfedyunin/hw_ddl_dml/blob/main/img/sql_1_8.jpg)

```sql
-- Создание пользователя
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'sys_temp';

-- Просомтр пользователей
SELECT * FROM mysql.user

-- Выдача прав
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';

-- Просмотр прав
SELECT * FROM mysql.user where user = 'sys_temp';

-- Смена типа аутентификации
ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'sys_temp';
```

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

---

### Задание 2

Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```
```sql
SELECT
tc.TABLE_NAME,
kc.COLUMN_NAME AS PRIMARY_KEY
FROM information_schema.TABLE_CONSTRAINTS tc INNER JOIN information_schema.KEY_COLUMN_USAGE kc ON tc.CONSTRAINT_NAME = kc.CONSTRAINT_NAME
AND tc.TABLE_SCHEMA = kc.TABLE_SCHEMA
AND tc.TABLE_NAME = kc.TABLE_NAME
WHERE tc.CONSTRAINT_TYPE = 'PRIMARY KEY' AND tc.TABLE_SCHEMA = 'sakila'
```

[table_primary.txt](https://github.com/rfedyunin/hw_ddl_dml/blob/main/files/table_primary.txt)

---
