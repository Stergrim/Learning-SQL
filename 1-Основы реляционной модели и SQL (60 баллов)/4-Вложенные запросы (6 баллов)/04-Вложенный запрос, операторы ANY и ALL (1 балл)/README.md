# Вложенный запрос, операторы ANY и ALL

Вложенный запрос, возвращающий несколько значений одного столбца, можно использовать для отбора записей с помощью операторов `ANY` и `ALL` совместно с операциями отношения (=, <>, <=, >=, <, >).

Операторы `ANY` и `ALL` используются  в SQL для сравнения некоторого значения с результирующим набором вложенного запроса, состоящим из одного столбца. При этом тип данных столбца, возвращаемого вложенным запросом, должен совпадать с типом данных столбца (или выражения), с которым происходит сравнение.

При использовании оператора `ANY` в результирующую таблицу будут включены все записи, для которых  выражение со знаком отношения верно хотя бы для одного элемента результирующего запроса. Как работает оператор `ANY`:
- `amount > ANY (10, 12)` эквивалентно `amount > 10`
- `amount < ANY (10, 12)` эквивалентно `amount < 12`
- `amount = ANY (10, 12)` эквивалентно `(amount = 10) OR (amount = 12)`, а также `amount IN  (10,12)`
- `amount <> ANY (10, 12)` вернет все записи с любым значением `amount`, включая 10 и 12

При использовании оператора `ALL` в результирующую таблицу будут включены все записи, для которых  выражение со знаком отношения верно для всех элементов результирующего запроса. Как работает оператор `ALL`:
- `amount > ALL (10, 12)` эквивалентно `amount > 12`
- `amount < ALL (10, 12)` эквивалентно `amount < 10`
- `amount = ALL (10, 12)` не вернет ни одной записи, так как эквивалентно `(amount = 10) AND (amount = 12)`
- `amount <> ALL (10, 12)` вернет все записи кроме тех,  в которых `amount` равно 10 или 12

**Важно!** Операторы `ALL` и `ANY` можно использовать **только с вложенными запросами**. В примерах выше (10, 12) приводится как результат вложенного запроса просто для того, чтобы показать как эти операторы работают. В запросах так записывать нельзя.

**Пример**

Вывести информацию о тех книгах, количество которых меньше самого маленького среднего количества книг каждого автора.

*Запрос:*

```mysql
SELECT title, author, amount, price
FROM book
WHERE amount < ALL (
        SELECT AVG(amount) 
        FROM book 
        GROUP BY author 
      );
```

*Результат:*

```mysql
+--------------------+------------------+--------+--------+
| title              | author           | amount | price  |
+--------------------+------------------+--------+--------+
| Мастер и Маргарита | Булгаков М.А.    | 3      | 670.99 |
| Братья Карамазовы  | Достоевский Ф.М. | 3      | 799.01 |
+--------------------+------------------+--------+--------+
```

**Пример**

Вывести информацию о тех книгах, количество которых меньше самого большого среднего количества книг каждого автора.

*Запрос:*

```mysql
SELECT title, author, amount, price
FROM book
WHERE amount < ANY (
        SELECT AVG(amount) 
        FROM book 
        GROUP BY author 
      );
```

*Результат:*

```mysql
+--------------------+------------------+--------+--------+
| title              | author           | amount | price  |
+--------------------+------------------+--------+--------+
| Мастер и Маргарита | Булгаков М.А.    | 3      | 670.99 |
| Белая гвардия      | Булгаков М.А.    | 5      | 540.50 |
| Идиот              | Достоевский Ф.М. | 10     | 460.00 |
| Братья Карамазовы  | Достоевский Ф.М. | 3      | 799.01 |
| Игрок              | Достоевский Ф.М. | 10     | 480.50 |
+--------------------+------------------+--------+--------+
```

**Задание**

Вывести информацию о книгах(автор, название, цена), цена которых меньше самой большой из минимальных цен, вычисленных для каждого автора.

Введите SQL запрос

*Результат:*

```mysql
Query result:
+------------------+---------------+--------+
| author           | title         | price  |
+------------------+---------------+--------+
| Булгаков М.А.    | Белая гвардия | 540.50 |
| Достоевский Ф.М. | Идиот         | 460.00 |
| Достоевский Ф.М. | Игрок         | 480.50 |
+------------------+---------------+--------+
Affected rows: 3
```

```mysql
SELECT author, title, price
FROM book
WHERE price < ANY (SELECT MIN(price)
                   FROM book
                   GROUP BY author);
```

Вы получили: 1 балл из 1
