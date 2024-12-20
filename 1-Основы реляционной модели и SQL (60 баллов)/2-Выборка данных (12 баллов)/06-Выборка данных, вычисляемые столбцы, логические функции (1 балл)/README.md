# Выборка данных, вычисляемые столбцы, логические функции

В SQL реализована возможность заносить в поле значение в зависимости от условия. Для этого используется функция `IF()`:

```mysql
IF(логическое_выражение, выражение_1, выражение_2)
```

Функция вычисляет `логическое_выражение`, если оно истина – в поле заносится значение `выражения_1`, в противном случае –  значение `выражения_2`. Все три параметра `IF()` являются обязательными.

Допускается использование вложенных функций, вместо `выражения_1` или `выражения_2` может стоять новая функция `IF`.

**Пример**

Для каждой книги из таблицы `book` установим скидку следующим образом: если количество книг меньше 4, то скидка будет составлять 50% от цены, в противном случае 30%.

*Запрос:*

```mysql
SELECT title, amount, price, 
    IF(amount<4, price*0.5, price*0.7) AS sale
FROM book;
```

*Результат:*

```mysql
+-----------------------+--------+--------+---------+
| title                 | amount | price  | sale    |
+-----------------------+--------+--------+---------+
| Мастер и Маргарита    | 3      | 670.99 | 335.495 |
| Белая гвардия         | 5      | 540.50 | 378.350 |
| Идиот                 | 10     | 460.00 | 322.000 |
| Братья Карамазовы     | 2      | 799.01 | 399.505 |
| Стихотворения и поэмы | 15     | 650.00 | 455.000 |
+-----------------------+--------+--------+---------+ 
```

Цена по скидке должна отображаться с двумя знаками после запятой, добавим в запрос округление:

```mysql
SELECT title, amount, price, 
    ROUND(IF(amount<4, price*0.5, price*0.7),2) AS sale
FROM book;
```

*Результат:*

```mysql
+-----------------------+--------+--------+--------+
| title                 | amount | price  | sale   |
+-----------------------+--------+--------+--------+
| Мастер и Маргарита    | 3      | 670.99 | 335.50 |
| Белая гвардия         | 5      | 540.50 | 378.35 |
| Идиот                 | 10     | 460.00 | 322.00 |
| Братья Карамазовы     | 2      | 799.01 | 399.51 |
| Стихотворения и поэмы | 15     | 650.00 | 455.00 |
+-----------------------+--------+--------+--------+
```

**Пример**

Усложним вычисление скидки в зависимости от количества книг. Если количество книг меньше 4 , то скидка составляет 50%, для остальных книг, количество которых меньше 11, скидка 30%, для всех оставшихся – 10%. И еще укажем какая именно скидка на каждую книгу.

*Запрос:*

```mysql
SELECT title, amount, price,
    ROUND(
     IF(amount < 4, price * 0.5, 
         IF(amount < 11, price * 0.7, price * 0.9)),
     2) AS sale,
    IF(amount < 4, 'скидка 50%', 
      IF(amount < 11, 'скидка 30%', 'скидка 10%')
     ) AS Ваша_скидка
FROM book;
```

*Результат:*

```mysql
+-----------------------+--------+--------+--------+-------------+
| title                 | amount | price  | sale   | Ваша_скидка |
+-----------------------+--------+--------+--------+-------------+
| Мастер и Маргарита    | 3      | 670.99 | 335.50 | скидка 50%  |
| Белая гвардия         | 5      | 540.50 | 378.35 | скидка 30%  |
| Идиот                 | 10     | 460.00 | 322.00 | скидка 30%  |
| Братья Карамазовы     | 2      | 799.01 | 399.51 | скидка 50%  |
| Стихотворения и поэмы | 15     | 650.00 | 585.00 | скидка 10%  |
+-----------------------+--------+--------+--------+-------------+
```

**Задание**

При анализе продаж книг выяснилось, что наибольшей популярностью пользуются книги Михаила Булгакова, на втором месте книги Сергея Есенина. Исходя из этого решили поднять цену книг Булгакова на 10%, а цену книг Есенина - на 5%. Написать запрос, куда включить автора, название книги и новую цену, последний столбец назвать `new_price`. Значение округлить до двух знаков после запятой.

*Результат:*

```mysql
+------------------+-----------------------+-----------+
| author           | title                 | new_price |
+------------------+-----------------------+-----------+
| Булгаков М.А.    | Мастер и Маргарита    | 738.09    |
| Булгаков М.А.    | Белая гвардия         | 594.55    |
| Достоевский Ф.М. | Идиот                 | 460.00    |
| Достоевский Ф.М. | Братья Карамазовы     | 799.01    |
| Есенин С.А.      | Стихотворения и поэмы | 682.50    |
+------------------+-----------------------+-----------+
```

Введите SQL запрос

```mysql
SELECT 
  author, 
  title, 
  ROUND(
    IF(
      author = 'Булгаков М.А.', 
      price * 1.1, 
      IF(
        author = 'Есенин С.А.', price * 1.05, 
        price
      )
    ), 
    2
  ) AS new_price 
FROM 
  book;
```

Вы получили: 1 балл из 1
