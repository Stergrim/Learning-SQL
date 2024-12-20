# Запросы на удаление

Запросы корректировки данных позволяют удалить одну или несколько записей из  таблицы. Простейший запрос на удаление имеет вид:

```mysql
DELETE FROM таблица;
```

Этот запрос удаляет все записи из указанной после `FROM` таблицы.

**Пример**

После того, как информация о книгах из таблицы `supply` перенесена в `book`, необходимо очистить таблицу `supply`.

*Запрос:*

```mysql
DELETE FROM supply;

SELECT * FROM supply;
```

*Результат:*

```mysql
Affected rows: 4
Affected rows: 0
```

Из таблицы удалены все записи. Запрос на выборку отобрал 0 записей.

Запрос на удаления позволяет удалить не все записи таблицы, а только те, которые удовлетворяют условию, указанному после ключевого слова `WHERE`:

```mysql
DELETE FROM таблица
WHERE условие;
```

**Пример**

Удалить из таблицы `supply` все книги, названия которых есть в таблице `book`.

*Запрос:*

```mysql
DELETE FROM supply 
WHERE title IN (
        SELECT title 
        FROM book
      );


SELECT * FROM supply;
```

*Результат:*

```mysql
Affected rows: 2

Query result:
+-----------+--------------------------+------------------+--------+--------+
| supply_id | title                    | author           | price  | amount |
+-----------+--------------------------+------------------+--------+--------+
| 1         | Лирика                   | Пастернак Б.Л.   | 518.99 | 2      |
| 2         | Черный человек           | Есенин С.А.      | 570.20 | 6      |
+-----------+--------------------------+------------------+--------+--------+
```

Из таблицы `supply` удалены две записи о книгах «Белая гвардия» и «Идиот».

**Задание**

Удалить из таблицы `supply` книги тех авторов, общее количество экземпляров книг которых в таблице `book` превышает 10.

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 2
```

```mysql
DELETE FROM supply
WHERE author IN(SELECT author
                FROM book
                GROUP BY author
                HAVING SUM(amount) > 10);
```

Вы получили: 1 балл из 1
