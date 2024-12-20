# Удаление записей, использование связанных таблиц

При удалении записей из таблицы можно использовать информацию из других связанных с ней таблиц. В этом случае синтаксис запроса имеет вид:

```mysql
DELETE FROM таблица_1
USING 
    таблица_1 
    INNER JOIN таблица_2 ON ...
WHERE ...
```

**Пример**

Удалить всех авторов из таблицы `author`, у которых есть книги, количество экземпляров которых меньше 3. Из таблицы `book` удалить все книги этих авторов.

*Запрос:*

```mysql
DELETE FROM author
USING 
    author 
    INNER JOIN book ON author.author_id = book.author_id
WHERE book.amount < 3;

SELECT * FROM author;

SELECT * FROM book;
```

*Результат:*

```mysql
Affected rows: 1

Query result:
+-----------+------------------+
| author_id | name_author      |
+-----------+------------------+
| 1         | Булгаков М.А.    |
| 2         | Достоевский Ф.М. |
| 3         | Есенин С.А.      |
| 5         | Лермонтов М.Ю.   |
| 6         | Стивенсон Р.Л.   |
+-----------+------------------+
Affected rows: 5

Query result:
+---------+-----------------------+-----------+----------+--------+--------+
| book_id | title                 | author_id | genre_id | price  | amount |
+---------+-----------------------+-----------+----------+--------+--------+
| 1       | Мастер и Маргарита    | 1         | 1        | 670.99 | 3      |
| 2       | Белая гвардия         | 1         | 1        | 540.50 | 12     |
| 3       | Идиот                 | 2         | 1        | 437.11 | 13     |
| 4       | Братья Карамазовы     | 2         | 1        | 799.01 | 3      |
| 5       | Игрок                 | 2         | 1        | 480.50 | 10     |
| 6       | Стихотворения и поэмы | 3         | 2        | 650.00 | 15     |
| 7       | Черный человек        | 3         | 2        | 570.20 | 12     |
| 10      | Стихотворения и поэмы | 5         | 2        | 255.90 | 4      |
| 11      | Остров сокровищ       | 6         | 3        | 599.99 | 5      |
+---------+-----------------------+-----------+----------+--------+--------+
```

Книги из таблицы `book` будут удалены автоматически, так как для столбца `author_id` из таблицы `book` установлено каскадное удаление записей.

**Задание**

Удалить всех авторов, которые пишут в жанре "Поэзия". Из таблицы `book` удалить все книги этих авторов. В запросе для отбора авторов использовать полное название жанра, а не его `id`.

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 3
```

```mysql
DELETE FROM author
USING author
      INNER JOIN book USING(author_id)
      INNER JOIN genre USING(genre_id)
WHERE name_genre = 'Поэзия';
```

Вы получили: 1 балл из 1
