# Learning-SQL

Обучение на Stepik.<br>
Ссылка на курс "Интерактивный тренажер по SQL": https://stepik.org/course/63054/syllabus

Используется MySQL версии 8.0.21.


Для каждой книги из таблицы `book` вычислим налог на добавленную стоимость (имя столбца `tax`) , который включен в цену и составляет k = 18%,  а также цену книги (`price_tax`) без него. Формулы для вычисления:

$$tax=\frac{price*\frac{k}{100}}{1+\frac{k}{100}},$$

$$price\\_tax=\frac{price}{1+\frac{k}{100}}$$

Значение НДС в 18% взято для ПРИМЕРА, чтобы показать как использовать функции округления.

