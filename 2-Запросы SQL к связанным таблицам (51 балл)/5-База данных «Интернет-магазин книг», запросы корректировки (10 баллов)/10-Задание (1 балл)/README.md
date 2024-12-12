# Задание

**Задание**

Придумайте один или несколько запросов корректировки данных для предметной области «Интернет-магазин книг» (в таблицы занесены данные, как на этом шаге). Проверьте, правильно ли они работают

**Логическая схема базы данных:**

<p float="left">
<img src="shop4.jpg" width="700" />
</p>

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 1

Affected rows: 1
```

```mysql
UPDATE book JOIN buy_book USING(book_id)
SET book.amount=book.amount+buy_book.amount
WHERE buy_id=(SELECT buy.buy_id
              FROM buy_book
                   JOIN buy USING(buy_id)
                   JOIN buy_step USING(buy_id)
                   JOIN step USING(step_id)
              WHERE name_step='Оплата' AND date_step_end IS NULL);
DELETE FROM buy
WHERE buy_id=(SELECT buy_step.buy_id
              FROM buy_step JOIN step USING(step_id)
              WHERE name_step='Оплата' AND date_step_end IS NULL);
```

Вы получили: 1 балл из 1
