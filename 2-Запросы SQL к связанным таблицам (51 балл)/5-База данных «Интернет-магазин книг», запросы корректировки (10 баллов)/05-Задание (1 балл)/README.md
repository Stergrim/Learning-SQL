# Задание

**Задание**

Создать счет (таблицу `buy_pay`) на оплату заказа с номером 5, в который включить название книг, их автора, цену, количество заказанных книг и  стоимость. Последний столбец назвать `Стоимость`. Информацию в таблицу занести в отсортированном по названиям книг виде.

**Фрагмент логической схемы базы данных:**

<p float="left">
<img src="cx19.jpg" width="250" />
</p>

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 2
```

```mysql
CREATE TABLE buy_pay
SELECT title, name_author, price, buy_book.amount, (price*buy_book.amount) AS Стоимость
FROM buy_book
     INNER JOIN book USING(book_id)
     INNER JOIN author USING(author_id)
WHERE buy_id = 5
ORDER BY title;
```

Вы получили: 1 балл из 1
