# Внешнее соединение LEFT и RIGHT OUTER JOIN

Оператор внешнего соединения `LEFT OUTER JOIN`  (можно использовать `LEFT JOIN`) соединяет две таблицы. Порядок таблиц для оператора важен, поскольку оператор не является симметричным.

```mysql
SELECT
 ...
FROM
    таблица_1 LEFT JOIN таблица_2
    ON условие
...
```

Результат запроса формируется так:
- в результат включается внутреннее соединение (`INNER JOIN`) первой и второй таблицы в соответствии с условием;
- затем в результат добавляются те записи первой таблицы, которые не вошли во внутреннее соединение на шаге 1, для таких записей соответствующие поля второй таблицы заполняются значениями `NULL`.

Соединение `RIGHT JOIN` действует аналогично, только в пункте 2 первая таблица меняется на вторую и наоборот.

**Пример**

Вывести название всех книг каждого автора, если книг некоторых авторов в данный момент нет на складе – вместо названия книги указать `Null`.

*Запрос:*

```mysql
SELECT name_author, title 
FROM author LEFT JOIN book
     ON author.author_id = book.author_id
ORDER BY name_author;  
```

*Результат:*

```mysql
+------------------+-----------------------+
| name_author      | title                 |
+------------------+-----------------------+
| Булгаков М.А.    | Мастер и Маргарита    |
| Булгаков М.А.    | Белая гвардия         |
| Достоевский Ф.М. | Игрок                 |
| Достоевский Ф.М. | Идиот                 |
| Достоевский Ф.М. | Братья Карамазовы     |
| Есенин С.А.      | Стихотворения и поэмы |
| Есенин С.А.      | Черный человек        |
| Лермонтов М.Ю.   | NULL                  |
| Пастернак Б.Л.   | Лирика                |
+------------------+-----------------------+
```

Так как в таблице `book` нет книг Лермонтова, напротив этой фамилии стоит `Null`.

**Задание**

Вывести все жанры, которые не представлены в книгах на склад

**Логическая схема базы данных:**

<p float="left">
<img src="cx1.jpg" width="400" />
</p>

Введите SQL запрос

*Результат:*

```mysql
Query result:
+-------------+
| name_genre  |
+-------------+
| Приключения |
+-------------+
Affected rows: 1
```

```mysql
SELECT name_genre
FROM genre LEFT JOIN book ON genre.genre_id = book.genre_id
WHERE book.genre_id IS NULL;
```

Вы получили: 1 балл из 1
