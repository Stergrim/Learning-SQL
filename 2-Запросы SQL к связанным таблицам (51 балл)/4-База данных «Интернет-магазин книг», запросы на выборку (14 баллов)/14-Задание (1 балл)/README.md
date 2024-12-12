# Задание

**Задание**

Придумайте один или несколько запросов на выборку для предметной области «Интернет-магазин книг» (в таблицы занесены данные, как на первом шаге урока). Проверьте, правильно ли они работают.

**Логическая схема базы данных:**

<p float="left">
<img src="shop4.jpg" width="700" />
</p>

Введите SQL запрос

*Результат:*

```mysql
Query result:
+---------------+------------------+-----------------------+-------+--------------------+
| name_client   | name_author      | title                 | Сумма | Сумма_клиент_автор |
+---------------+------------------+-----------------------+-------+--------------------+
| Абрамова Катя | Достоевский Ф.М. | Братья Карамазовы     | NULL  | 920.00             |
| Абрамова Катя | Достоевский Ф.М. | Игрок                 | NULL  | 920.00             |
| Баранов Павел | Булгаков М.А.    | Белая гвардия         | NULL  | 670.99             |
| Баранов Павел | Достоевский Ф.М. | Братья Карамазовы     | NULL  | 940.50             |
| Баранов Павел | Есенин С.А.      | Стихотворения и поэмы | NULL  | 1140.40            |
+---------------+------------------+-----------------------+-------+--------------------+
Affected rows: 5
```

```mysql
SELECT name_client, query_in_1.name_author, title, Сумма, Сумма_клиент_автор
FROM (SELECT name_client, name_author
      FROM city
           INNER JOIN client USING (city_id)
           INNER JOIN buy USING (client_id)
           INNER JOIN buy_book USING (buy_id)
           INNER JOIN book USING (book_id)
           INNER JOIN genre USING (genre_id)
           INNER JOIN author USING (author_id)
      GROUP BY name_client, name_author
      ORDER BY name_client, name_author) query_in_1
    INNER JOIN (SELECT name_author, title
                FROM book INNER JOIN author USING (author_id)) query_in_2 USING (name_author)
    LEFT JOIN (SELECT name_client, name_author, title, SUM(book.price * buy_book.amount) AS Сумма
               FROM city
                    INNER JOIN client USING (city_id)
                    INNER JOIN buy USING (client_id)
                    INNER JOIN buy_book USING (buy_id)
                    INNER JOIN book USING (book_id)
                    INNER JOIN genre USING (genre_id)
                    INNER JOIN author USING (author_id)
               GROUP BY name_client, name_author, title) query_in_3 USING (name_client, name_author, title)
    LEFT JOIN (SELECT name_client, name_author, SUM(book.price * buy_book.amount) AS Сумма_клиент_автор
               FROM city
                    INNER JOIN client USING (city_id)
                    INNER JOIN buy USING (client_id)
                    INNER JOIN buy_book USING (buy_id)
                    INNER JOIN book USING (book_id)
                    INNER JOIN genre USING (genre_id)
                    INNER JOIN author USING (author_id)
               GROUP BY name_client, name_author) query_in_4 USING (name_client, name_author)
WHERE Сумма IS NULL AND Сумма_клиент_автор > 0             
ORDER BY name_client, query_in_1.name_author, title;
```

Вы получили: 1 балл из 1
