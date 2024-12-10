# Поиск по ключевым словам

На данном шаге можно найти шаги курса, в которых встречаются ключевые слова SQL, которые рассматриваются в курсе.

Для этого скопируйте один из запросов в окно решений, укажите нужные ключевые слова и запустите запрос. В окне решений будут выведены ссылки на соответствующие шаги.

Это **НЕ ЗАДАНИЕ**, а просто запросы, с помощью которых можно найти шаги, в которых встречаются те или иные ключевые слова. Выполнять не обязательно (это задание оценивается в 0 баллов). Это ПРОСТО ПОМОЩЬ для навигации по курсу.

**Запрос 1.** Поиск шагов, в которых встречается заданное ключевое слово, в примере **MAX**:

```mysql
SELECT 
   keyword_name AS Поиск,
   CONCAT(module_id, ".", lesson_position, ".",step_position, " ", 
          CONCAT(LEFT(step_name, 23), "...")) AS Шаг,
   link AS Ссылка_на_шаг
FROM step
        INNER JOIN lesson USING(lesson_id)
        INNER JOIN module USING(module_id)
        INNER JOIN step_keyword USING(step_id)
        INNER JOIN keyword USING(keyword_id)
WHERE keyword_name = "MAX"
ORDER BY 2;
```

**Запрос 2.** Поиск шагов, в которых встречаются два заданных ключевых слова одновременно, в примере **MAX** и **AVG**:

```mysql
SELECT 
   GROUP_CONCAT(keyword_name) AS Поиск,
   CONCAT(module_id,".",lesson_position,".",step_position," ", 
          CONCAT(LEFT(step_name, 23), "...'")) AS Шаг, 
   link AS Ссылка_на_шаг
FROM step
        INNER JOIN lesson USING(lesson_id)
        INNER JOIN module USING(module_id)
        INNER JOIN step_keyword USING(step_id)
        INNER JOIN keyword USING(keyword_id)
WHERE keyword_name IN ("MAX", "AVG")
GROUP BY ШАГ, Ссылка_на_шаг
HAVING count(*) = 2
ORDER BY 2;
```

**Запрос 3.** Поиск шагов, в которых встречаются три заданных ключевых слова одновременно, в примере **MAX**, **MIN** и **AVG**:

```mysql
SELECT 
   GROUP_CONCAT(keyword_name) AS Поиск,
   CONCAT(module_id, ".", lesson_position, ".", step_position, " ", 
          CONCAT(LEFT(step_name, 20), "...")) AS Шаг,
   link AS Ссылка_на_шаг
FROM step
        INNER JOIN lesson USING(lesson_id)
        INNER JOIN module USING(module_id)
        INNER JOIN step_keyword USING(step_id)
        INNER JOIN keyword USING(keyword_id)
WHERE keyword_name IN ("MAX", "AVG", "MIN")
GROUP BY ШАГ, link
HAVING COUNT(*) = 3
ORDER BY 2;
```

Введите SQL запрос

*Результат:*

```mysql
Query result:
+--------------------------------------------------------------+------------------------------------------------+
| Шаг                                                          | Примечание                                     |
+--------------------------------------------------------------+------------------------------------------------+
| 1.2.7 Выборка данных, вычисляемые столбцы, логические фу...  | NULL                                           |
| 1.7.4 Задание. Занести сумму штрафа за каждое новое нару...  | NULL                                           |
| 1.7.7 Задание. Уменьшение штрафа за оплату вовремя...        | Используется в решении (синтаксис раздела SET) |
| 2.4.11 Задание. Вывести заказы, доставленные с опозданием... | Используется в решении                         |
| 3.1.8 Задание. Вывести вопросы, на которые отвечал опред...  | Используется в решении                         |
| 3.3.7 Задание. Посчитать, сколько дополнительных баллов ...  | Можно использовать в решении                   |
| 3.4.7 Задание. Формирование списка рекомендованных к зач...  | NULL                                           |
| 3.5.12 Задание. Статистика по всем попыткам обучающегося...  | Используется в решении                         |
| 3.5.13 Задание. Выделить группы обучающихся по способу пр... | Используется в решении                         |
+--------------------------------------------------------------+------------------------------------------------+
Affected rows: 9
```

```mysql
SELECT CONCAT(module_id,'.',lesson_position,".",step_position," ", CONCAT(LEFT(step_name, 50), '...')) AS Шаг,
       note AS Примечание
FROM step INNER JOIN lesson USING(lesson_id)
          INNER JOIN module USING(module_id)
          INNER JOIN step_keyword USING(step_id)
          INNER JOIN keyword USING(keyword_id)
WHERE keyword_name = 'IF'
ORDER BY 1;
```

Вы получили: 1 балл из 1
