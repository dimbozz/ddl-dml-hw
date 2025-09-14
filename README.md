# Домашнее задание к занятию "`Работа с данными (DDL/DML)`" - `Цаберябый Дмитрий`

---

### Решение 1

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

![скриншот-1](https://github.com/dimbozz/ddl-dml-hw/blob/main/img/img_7.png)

```sql
SELECT VERSION();
```

1.2. Создайте учётную запись sys_temp.
```sql
CREATE USER 'sys_temp'@'localhost';
```

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
```sql
SELECT User, Host FROM mysql.user;
```
![скриншот-2](https://github.com/dimbozz/ddl-dml-hw/blob/main/img/img_1.png)

1.4. Дайте все права для пользователя sys_temp.
```sql
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';
```

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
```sql
SHOW GRANTS FOR 'sys_temp'@'localhost';
```
![скриншот-3](https://github.com/dimbozz/ddl-dml-hw/blob/main/img/img_2.png)

1.6. Переподключитесь к базе данных от имени sys_temp.
Для смены типа аутентификации с sha2 используйте запрос:
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
SYSTEM mysql -u sys_temp -p;
SELECT current_user();
```

1.7. Восстановите дамп в базу данных.
```sh
mysql -u root -p sakila < sakila-schema.sql
mysql -u root -p sakila < sakila-data.sql 
```

1.8. Команда для получения всех таблиц базы данных
```sql
use sakila;
SHOW FULL TABLES;
```
![скриншот-4](https://github.com/dimbozz/ddl-dml-hw/blob/main/img/img_4.png)
---

### Решение 2

```sql
SELECT TABLE_NAME, COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_SCHEMA = 'sakila' AND COLUMN_KEY = 'PRI' ORDER BY TABLE_NAME;
```
![скриншот-5](https://github.com/dimbozz/ddl-dml-hw/blob/main/img/img_5.png)

---

### Решение 3

```sql
GRANT ALL PRIVILEGES ON sakila.* TO sys_temp@localhost;
REVOKE INSERT, UPDATE, DELETE ON sakila.* FROM sys_temp@localhost;
SHOW GRANTS FOR sys_temp@localhost;
```
![скриншот-6](https://github.com/dimbozz/ddl-dml-hw/blob/main/img/img_6.png)
