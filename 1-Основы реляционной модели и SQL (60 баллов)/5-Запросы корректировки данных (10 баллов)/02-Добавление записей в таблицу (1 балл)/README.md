# Добавление записей в таблицу

Добавление одной записи в таблицу осуществляется с помощью запроса `INSERT`, подробно рассмотренного в первом уроке. Запросы обязательно разделять точкой с запятой.

Допускается вставка нескольких записей одновременно, для этого используется SQL запрос следующего вида:

```mysql
INSERT INTO имя_таблицы(столбец_1, столбец_2, ..., столбец_N)
VALUES
    (значение_1_1, значение_1_2, ..., значение_1_N),
    (значение_2_1, значение_2_2, ..., значение_2_N),
    ...
    (значение_M_1, значение_M_2, ..., значение_M_N);
```

Например, чтобы добавить в таблицу `book` две новые записи используется запрос:

```mysql
INSERT INTO book (title, author, price, amount) 
VALUES 
    ('Война и мир','Толстой Л.Н.', 1070.20, 2),
    ('Анна Каренина', 'Толстой Л.Н.', 599.90, 3);
```

**Задание**

Занесите в таблицу `supply` четыре записи, чтобы получилась следующая таблица:

| **supply_id** | **title**      | **author**       | **price**   | **amount** |
|:--------------|:---------------|:-----------------|:------------|:-----------|
| 1             | Лирика         | Пастернак Б.Л.   | 518.99      | 2          |
| 2             | Черный человек | Есенин С.А.      | 570.20      | 6          |
| 3             | Белая гвардия  | Булгаков М.А.    | 540.50      | 7          |
| 4             | Идиот          | Достоевский Ф.М. | 360.80      | 3          |

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 4
```

```mysql
INSERT INTO supply(title, author, price, amount) 
VALUES 
  (
    'Лирика', 'Пастернак Б.Л.', 
    518.99, 2
  ), 
  (
    'Черный человек', 'Есенин С.А.', 
    570.20, 6
  ), 
  (
    'Белая гвардия', 'Булгаков М.А.', 
    540.50, 7
  ), 
  (
    'Идиот', 'Достоевский Ф.М.', 
    360.80, 3
  );
```

Вы получили: 1 балл из 1
