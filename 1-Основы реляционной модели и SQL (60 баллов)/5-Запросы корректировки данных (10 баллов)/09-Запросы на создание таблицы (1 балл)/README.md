# Запросы на создание таблицы

Новая таблица может быть создана на основе данных из другой таблицы. Для этого используется запрос `SELECT`, результирующая таблица которого и будет новой таблицей базы данных. При этом имена столбцов запроса становятся именами столбцов новой таблицы. Запрос на создание новой таблицы имеет вид:

```mysql
CREATE TABLE имя_таблицы AS
SELECT ...
```

**Пример**

Создать таблицу заказ (`ordering`), куда включить авторов и названия тех книг, количество экземпляров которых в таблице `book` меньше 4. Для всех книг указать одинаковое количество экземпляров 5.

*Запрос:*

```mysql
CREATE TABLE ordering AS
SELECT author, title, 5 AS amount
FROM book
WHERE amount < 4;

SELECT * FROM ordering;
```

*Результат:*

```mysql
Affected rows: 2
Query result:
+------------------+--------------------+--------+
| author           | title              | amount |
+------------------+--------------------+--------+
| Булгаков М.А.    | Мастер и Маргарита | 5      |
| Достоевский Ф.М. | Братья Карамазовы  | 5      |
+------------------+--------------------+--------+
```

При создании таблицы можно использовать вложенные запросы как после `SELECT`, так и после `WHERE`.

**Пример**

Создать таблицу заказ (`ordering`), куда включить авторов и названия тех книг, количество экземпляров которых в таблице `book` меньше 4. Для всех книг указать одинаковое значение - среднее количество экземпляров книг в таблице `book`.

*Запрос:*

```mysql
CREATE TABLE ordering AS
SELECT author, title, 
   (
    SELECT ROUND(AVG(amount)) 
    FROM book
   ) AS amount
FROM book
WHERE amount < 4;

SELECT * FROM ordering;
```

*Результат:*

```mysql
Affected rows: 2
Query result:
+------------------+--------------------+--------+
| author           | title              | amount |
+------------------+--------------------+--------+
| Булгаков М.А.    | Мастер и Маргарита | 7      |
| Достоевский Ф.М. | Братья Карамазовы  | 7      |
+------------------+--------------------+--------+
```

**Задание**

Создать таблицу заказ (`ordering`), куда включить авторов и названия тех книг, количество экземпляров которых в таблице `book` меньше среднего количества экземпляров книг в таблице `book`. В таблицу включить столбец `amount`, в котором для всех книг указать одинаковое значение - среднее количество экземпляров книг в таблице `book`.

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 3
```

```mysql
CREATE TABLE ordering AS
SELECT author, title, (SELECT ROUND(AVG(amount)) FROM book) AS amount
FROM book
WHERE amount < (SELECT AVG(amount) FROM book);
```

Вы получили: 1 балл из 1
