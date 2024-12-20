# Выборка данных c вычислением, групповые функции

В качестве аргумента групповых функций  SQL может использоваться не только столбец, но и любое допустимое в SQL арифметическое выражение.

**Пример**

Вывести суммарную стоимость книг каждого автора.

*Запрос:*

```mysql
SELECT author, SUM(price * amount) AS Стоимость
FROM book
GROUP BY author;
```

*Результат:*

```mysql
+------------------+-----------+
| author           | Стоимость |
+------------------+-----------+
| Булгаков М.А.    | 4715.47   |
| Достоевский Ф.М. | 11802.03  |
| Есенин С.А.      | 9750.00   |
+------------------+-----------+
```

Групповые функции могут быть элементами выражений. Например, при вычислении средней стоимости книг каждого автора на предыдущем шаге получились значения с шестью знаками после запятой. А поскольку это деньги, значения нужно округлить до 2 знаков после запятой.

**Пример**

Найти среднюю цену книг каждого автора.

*Запрос:*

```mysql
SELECT author, ROUND(AVG(price),2) AS Средняя_цена
FROM book
GROUP BY author;
```

*Результат:*

```mysql
+------------------+--------------+
| author           | Средняя_цена |
+------------------+--------------+
| Булгаков М.А.    | 605.75       |
| Достоевский Ф.М. | 579.84       |
| Есенин С.А.      | 650.00       |
+------------------+--------------+
```

**Задание**

Для каждого автора вычислить суммарную стоимость книг **S** (имя столбца **Стоимость**), а также вычислить налог на добавленную стоимость  для полученных сумм (имя столбца **НДС**), который **включен в стоимость*** и составляет 18% (**k=18**),  а также стоимость книг (**Стоимость_без_НДС**) без него. Значения округлить до двух знаков после запятой. В запросе для расчета НДС(**tax**) и Стоимости без НДС(**S_without_tax**) использовать следующие формулы:

$$tax=\frac{S*\frac{k}{100}}{1+\frac{k}{100}},$$

$$S\\_without\\_tax=\frac{S}{1+\frac{k}{100}}$$

Введите SQL запрос

*Результат:*

```mysql
Query result:
+------------------+-----------+---------+-------------------+
| author           | Стоимость | НДС     | Стоимость_без_НДС |
+------------------+-----------+---------+-------------------+
| Булгаков М.А.    | 4715.47   | 719.31  | 3996.16           |
| Достоевский Ф.М. | 11802.03  | 1800.31 | 10001.72          |
| Есенин С.А.      | 9750.00   | 1487.29 | 8262.71           |
+------------------+-----------+---------+-------------------+
Affected rows: 3
```

```mysql
SELECT 
  author, 
  SUM(amount * price) 'Стоимость', 
  ROUND(
    SUM(
      (amount * price * 0.18)/(1 + 0.18)
    ), 
    2
  ) 'НДС', 
  ROUND(
    SUM(
      (amount * price)/(1 + 0.18)
    ), 
    2
  ) 'Стоимость_без_НДС' 
FROM 
  book 
GROUP BY 
  author;
```

Вы получили: 1 балл из 1
