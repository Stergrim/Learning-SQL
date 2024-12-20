# Выборка данных, вычисляемые столбцы, математические функции

В SQL реализовано множество  [математических функций](https://learn.microsoft.com/ru-ru/sql/t-sql/functions/mathematical-functions-transact-sql?view=sql-server-ver15) для работы с числовыми данными. В таблице приведены некоторые из них.

| **Функция**       | **Описание**                                                                                                | **Пример**                               |
|:------------------|:------------------------------------------------------------------------------------------------------------|:-----------------------------------------|
| `CEILING(x)`      | возвращает наименьшее целое число, большее или равное **x** (округляет до целого числа в большую сторону)   | `CEILING(4.2)=5`, `CEILING(-5.8)=-5`     |
| `ROUND(x, k)`     | округляет значение **x** до **k** знаков после запятой, если **k** не указано – **x** округляется до целого | `ROUND(4.361)=4`, `ROUND(5.86592,1)=5.9` |
| `FLOOR(x)`        | возвращает наибольшее целое число, меньшее или равное **x** (округляет до  целого числа в меньшую сторону)  | `FLOOR(4.2)=4`, `FLOOR(-5.8)=-6`         |
| `POWER(x, y)`     | возведение **x** в степень **y**                                                                            | `POWER(3,4)=81.0`                        |
| `SQRT(x)`         | квадратный корень из **x**                                                                                  | `SQRT(4)=2.0`, `SQRT(2)=1.41...`         |
| `DEGREES(x)`      | конвертирует значение **x** из радиан в градусы                                                             | `DEGREES(3) = 171.8...`                  |
| `RADIANS(x)`      | конвертирует значение **x** из градусов в радианы                                                           | `RADIANS(180)=3.14...`                   |
| `ABS(x)`          | модуль числа **x**                                                                                          | `ABS(-1) = 1`, `ABS(1) = 1`              |
| `PI()`            | pi = 3.1415926...                                                                                           |                                          |

**Пояснение**. Существуют разные способы округления чисел. В SQL реализовано **математическое округление**. Для округления вещественного числа нужно в записи числа выбрать разряд в дробной части, до которого производится округление. Цифра, записанная в выбранном разряде: не меняется, если следующая за ней справа цифра - 0, 1, 2, 3 или 4; увеличивается на единицу, если следующая за ней справа цифра - 5,6,7,8 или 9.

**Пример**

Для каждой книги из таблицы `book` вычислим налог на добавленную стоимость (имя столбца `tax`) , который включен в цену и составляет k = 18%,  а также цену книги (`price_tax`) без него. Формулы для вычисления:

$$tax=\frac{price*\frac{k}{100}}{1+\frac{k}{100}},$$

$$price\\_tax=\frac{price}{1+\frac{k}{100}}$$

Значение НДС в 18% взято для ПРИМЕРА, чтобы показать как использовать функции округления.

Эта формула НДС отвечает на вопрос "Какую сумму увеличили на 18%, чтобы получить текущее значение"

*Запрос:*

```mysql
SELECT title, price, 
    (price*18/100)/(1+18/100) AS tax, 
    price/(1+18/100) AS price_tax 
FROM book;
```

*Результат:*

```mysql
+-----------------------+--------+----------------+------------+
| title                 | price  | tax            | price_tax  |
+-----------------------+--------+----------------+------------+
| Мастер и Маргарита    | 670.99 | 102.3544067797 | 568.635593 |
| Белая гвардия         | 540.50 | 82.4491525424  | 458.050847 |
| Идиот                 | 460.00 | 70.1694915254  | 389.830508 |
| Братья Карамазовы     | 799.01 | 121.8828813559 | 677.127119 |
| Стихотворения и поэмы | 650.00 | 99.1525423729  | 550.847458 |
+-----------------------+--------+----------------+------------+ 
```

Сумма налога и цена книги без налога – это деньги, поэтому количество знаков после запятой у этих чисел должно быть 2. Следовательно необходимо округлить полученные значения.

*Запрос:*

```mysql
SELECT title, 
    price, 
    ROUND((price*18/100)/(1+18/100),2) AS tax, 
    ROUND(price/(1+18/100),2) AS price_tax 
FROM book;
```

*Результат:*

```mysql
+-----------------------+--------+--------+-----------+
| title                 | price  | tax    | price_tax |
+-----------------------+--------+--------+-----------+
| Мастер и Маргарита    | 670.99 | 102.35 | 568.64    |
| Белая гвардия         | 540.50 | 82.45  | 458.05    |
| Идиот                 | 460.00 | 70.17  | 389.83    |
| Братья Карамазовы     | 799.01 | 121.88 | 677.13    |
| Стихотворения и поэмы | 650.00 | 99.15  | 550.85    |
+-----------------------+--------+--------+-----------+
```

**Задание**

В конце года цену каждой книги на складе пересчитывают – снижают ее на 30%. Написать SQL запрос, который из таблицы `book` выбирает названия, авторов, количества и вычисляет новые цены книг. Столбец с новой ценой назвать `new_price`, цену округлить до 2-х знаков после запятой.

*Результат:*

```mysql
+-----------------------+------------------+--------+-----------+
| title                 | author           | amount | new_price |
+-----------------------+------------------+--------+-----------+
| Мастер и Маргарита    | Булгаков М.А.    | 3      | 469.69    |
| Белая гвардия         | Булгаков М.А.    | 5      | 378.35    |
| Идиот                 | Достоевский Ф.М. | 10     | 322.00    |
| Братья Карамазовы     | Достоевский Ф.М. | 2      | 559.31    |
| Стихотворения и поэмы | Есенин С.А.      | 15     | 455.00    |
+-----------------------+------------------+--------+-----------+
```

Введите SQL запрос

```mysql
SELECT 
  title, 
  author, 
  amount, 
  ROUND(price - price * 0.3, 2) AS new_price 
FROM 
  book;
```

Вы получили: 1 балл из 1
