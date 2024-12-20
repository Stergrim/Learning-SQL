# Выборка данных, логические операции

Логическое выражение после ключевого слова `WHERE` кроме операторов сравнения  и выражений может включать **логические операции** (И «**and**», ИЛИ «**or**», НЕ «**not**») и круглые скобки, изменяющие приоритеты выполнения операций.

Приоритеты операций:

1. круглые скобки
2. умножение  (*),  деление (/)
3. сложение  (+), вычитание (-)
4. операторы сравнения (=, >, <, >=, <=, <>)
5. NOT
6. AND
7. OR

**Пример**

Вывести название, автора и цену тех книг, которые написал Булгаков, ценой больше 600 рублей.

*Запрос:*

```mysql
SELECT title, author, price 
FROM book
WHERE price > 600 AND author = 'Булгаков М.А.';
```

*Результат:*

```mysql
+--------------------+---------------+--------+
| title              | author        | price  |
+--------------------+---------------+--------+
| Мастер и Маргарита | Булгаков М.А. | 670.99 |
+--------------------+---------------+--------+
```

**Пример**

Вывести название, цену  тех книг, которые написал Булгаков или Есенин, ценой больше 600 рублей.

*Запрос:*

```mysql
SELECT title, author, price 
FROM book
WHERE (author = 'Булгаков М.А.' OR author = 'Есенин С.А.') AND price > 600;
```

*Результат:*

```mysql
+-----------------------+---------------+--------+
| title                 | author        | price  |
+-----------------------+---------------+--------+
| Мастер и Маргарита    | Булгаков М.А. | 670.99 |
| Стихотворения и поэмы | Есенин С.А.   | 650.00 |
+-----------------------+---------------+--------+
```

*Запрос:*

```mysql
SELECT title, author, price 
FROM book
WHERE author = 'Булгаков М.А.' OR author = 'Есенин С.А.' AND price > 600;
```

*Результат (сравните с предыдущим):*

```mysql
+-----------------------+---------------+--------+
| title                 | author        | price  |
+-----------------------+---------------+--------+
| Мастер и Маргарита    | Булгаков М.А. | 670.99 |
| Белая гвардия         | Булгаков М.А. | 540.50 |
| Стихотворения и поэмы | Есенин С.А.   | 650.00 |
+-----------------------+---------------+--------+
```

**Задание**

Вывести название, автора,  цену  и количество всех книг, цена которых меньше 500 или больше 600, а стоимость всех экземпляров этих книг больше или равна 5000.

*Результат:*

```mysql
+-----------------------+-------------+--------+--------+
| title                 | author      | price  | amount |
+-----------------------+-------------+--------+--------+
| Стихотворения и поэмы | Есенин С.А. | 650.00 | 15     |
+-----------------------+-------------+--------+--------+
```

Введите SQL запрос

```mysql
SELECT 
  title, 
  author, 
  price, 
  amount 
FROM 
  book 
WHERE 
  (
    price NOT BETWEEN 500 
    AND 600
  ) 
  AND amount * price >= 5000;
```

Вы получили: 1 балл из 1
