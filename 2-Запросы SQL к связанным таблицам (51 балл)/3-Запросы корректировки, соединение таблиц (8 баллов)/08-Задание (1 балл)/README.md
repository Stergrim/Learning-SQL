# Задание

**Задание**

Придумайте один или несколько запросов корректировки данных для таблиц `book`, `author`, `genre` и `supply`. Проверьте, правильно ли они работают.

Добавим книги, которых нет в `book`, из `supply`. Для этого сначала добавим авторов в `author`, затем книги, затем вручную укажем жанр новым книгам.

Изменим цену книг в `book`, заменив ее на среднюю цену книг того же жанра. То есть в основном запросе на изменение цены `UPDATE book SET...` мы пишем подзапрос, который считает среднюю цену книг каждого жанра (`AVG(price), GROUP BY genre_id`) и обновляет цену в зависимости от того, к какому жанру принадлежит конкретная книга.

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 1

Affected rows: 2

Affected rows: 1

Affected rows: 1

Affected rows: 9
```

```mysql
INSERT INTO author (name_author)
SELECT supply.author
FROM author RIGHT JOIN supply on author.name_author = supply.author
WHERE name_author IS Null;

INSERT INTO book(title,author_id,price,amount)
SELECT supply.title, author_id, price, amount
FROM supply INNER JOIN author ON author.name_author = supply.author AND title NOT IN(SELECT title FROM book);
    
UPDATE book
SET genre_id = 1
WHERE title IN('Доктор Живаго');

UPDATE book
SET genre_id = 3
WHERE title IN('Остров сокровищ');
            
UPDATE book INNER JOIN (SELECT genre_id, AVG(price) AS newprice
                        FROM book
                        GROUP BY genre_id) AS q USING(genre_id)
SET book.price = q.newprice;
```

Вы получили: 1 балл из 1
