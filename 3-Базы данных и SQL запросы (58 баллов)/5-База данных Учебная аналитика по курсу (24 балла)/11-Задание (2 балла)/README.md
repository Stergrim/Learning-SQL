# Задание

**Задание**

Для студента с именем `student_59` вывести следующую информацию по всем его попыткам:
- информация о шаге: номер модуля, символ '.', позиция урока в модуле, символ '.', позиция шага в модуле;
- порядковый номер попытки для каждого шага - определяется по возрастанию времени отправки попытки;
- результат попытки;
- время попытки (преобразованное к формату времени) - определяется как разность между временем отправки попытки и времени ее начала, в случае если попытка длилась более 1 часа, то время попытки заменить на среднее время всех попыток пользователя по всем шагам без учета тех, которые длились больше 1 часа;
- относительное время попытки  - определяется как отношение времени попытки (с учетом замены времени попытки) к суммарному времени всех попыток  шага, округленное до двух знаков после запятой  .

Столбцы назвать `Студент`, `Шаг`, `Номер_попытки`, `Результат`, `Время_попытки` и `Относительное_время`. Информацию отсортировать сначала по возрастанию `id` шага, а затем по возрастанию номера попытки (определяется по времени отправки попытки).

**Важно.** Все вычисления производить в секундах, округлять и переводить во временной формат только для вывода результата.

**Фрагмент логической схемы базы данных:**

<p float="left">
<img src="5_1.png" width="400" />
</p>

Введите SQL запрос

*Результат:*

```mysql
Query result:
+------------+--------+---------------+-----------+---------------+---------------------+
| Студент    | Шаг    | Номер_попытки | Результат | Время_попытки | Относительное_время |
+------------+--------+---------------+-----------+---------------+---------------------+
| student_59 | 1.2.2  | 1             | correct   | 0:00:28       | 100.00              |
| student_59 | 1.2.3  | 1             | correct   | 0:01:11       | 100.00              |
| student_59 | 1.2.4  | 1             | correct   | 0:06:09       | 100.00              |
| student_59 | 1.2.5  | 1             | correct   | 0:02:24       | 100.00              |
| student_59 | 1.2.6  | 1             | wrong     | 0:09:42       | 90.37               |
| student_59 | 1.2.6  | 2             | wrong     | 0:00:05       | 0.78                |
| student_59 | 1.2.6  | 3             | wrong     | 0:00:23       | 3.57                |
| student_59 | 1.2.6  | 4             | wrong     | 0:00:10       | 1.55                |
| student_59 | 1.2.6  | 5             | correct   | 0:00:20       | 3.11                |
| student_59 | 1.2.6  | 6             | correct   | 0:00:04       | 0.62                |
| student_59 | 1.2.7  | 1             | wrong     | 0:11:44       | 98.88               |
| student_59 | 1.2.7  | 2             | correct   | 0:00:08       | 1.12                |
| student_59 | 1.2.8  | 1             | correct   | 0:02:23       | 100.00              |
| student_59 | 1.2.9  | 1             | wrong     | 0:04:53       | 92.72               |
| student_59 | 1.2.9  | 2             | correct   | 0:00:23       | 7.28                |
| student_59 | 1.2.10 | 1             | wrong     | 0:03:19       | 76.83               |
| student_59 | 1.2.10 | 2             | wrong     | 0:00:07       | 2.70                |
| student_59 | 1.2.10 | 3             | correct   | 0:00:53       | 20.46               |
| student_59 | 1.2.11 | 1             | wrong     | 0:15:50       | 79.56               |
| student_59 | 1.2.11 | 2             | wrong     | 0:00:06       | 0.50                |
| student_59 | 1.2.11 | 3             | wrong     | 0:00:10       | 0.84                |
| student_59 | 1.2.11 | 4             | wrong     | 0:00:29       | 2.43                |
| student_59 | 1.2.11 | 5             | wrong     | 0:00:07       | 0.59                |
| student_59 | 1.2.11 | 6             | wrong     | 0:00:08       | 0.67                |
| student_59 | 1.2.11 | 7             | wrong     | 0:00:04       | 0.34                |
| student_59 | 1.2.11 | 8             | wrong     | 0:00:24       | 2.01                |
| student_59 | 1.2.11 | 9             | wrong     | 0:00:07       | 0.59                |
| student_59 | 1.2.11 | 10            | wrong     | 0:00:10       | 0.84                |
| student_59 | 1.2.11 | 11            | wrong     | 0:02:11       | 10.97               |
| student_59 | 1.2.11 | 12            | correct   | 0:00:08       | 0.67                |
| student_59 | 1.2.12 | 1             | correct   | 0:07:10       | 100.00              |
| student_59 | 2.2.2  | 1             | correct   | 0:08:52       | 100.00              |
| student_59 | 2.2.3  | 1             | wrong     | 0:11:31       | 98.86               |
| student_59 | 2.2.3  | 2             | correct   | 0:00:08       | 1.14                |
| student_59 | 2.2.4  | 1             | wrong     | 0:17:46       | 93.18               |
| student_59 | 2.2.4  | 2             | wrong     | 0:00:51       | 4.46                |
| student_59 | 2.2.4  | 3             | wrong     | 0:00:15       | 1.31                |
| student_59 | 2.2.4  | 4             | wrong     | 0:00:08       | 0.70                |
| student_59 | 2.2.4  | 5             | wrong     | 0:00:04       | 0.35                |
| student_59 | 2.2.5  | 1             | correct   | 0:07:10       | 100.00              |
| student_59 | 2.2.6  | 1             | correct   | 0:24:35       | 100.00              |
| student_59 | 2.2.7  | 1             | wrong     | 0:53:14       | 99.29               |
| student_59 | 2.2.7  | 2             | correct   | 0:00:23       | 0.71                |
| student_59 | 2.2.8  | 1             | wrong     | 0:07:10       | 48.31               |
| student_59 | 2.2.8  | 2             | correct   | 0:07:40       | 51.69               |
| student_59 | 2.2.9  | 1             | correct   | 0:31:13       | 100.00              |
| student_59 | 2.4.2  | 1             | correct   | 0:03:31       | 100.00              |
| student_59 | 2.4.3  | 1             | correct   | 0:08:21       | 100.00              |
| student_59 | 2.4.5  | 1             | correct   | 0:07:10       | 100.00              |
| student_59 | 2.4.6  | 1             | correct   | 0:13:38       | 100.00              |
| student_59 | 2.4.7  | 1             | correct   | 0:21:18       | 100.00              |
| student_59 | 2.4.8  | 1             | correct   | 0:33:02       | 100.00              |
| student_59 | 2.4.9  | 1             | wrong     | 0:18:12       | 71.75               |
| student_59 | 2.4.9  | 2             | correct   | 0:07:10       | 28.25               |
| student_59 | 2.4.10 | 1             | correct   | 0:05:32       | 100.00              |
| student_59 | 2.4.11 | 1             | correct   | 0:40:27       | 100.00              |
| student_59 | 2.4.12 | 1             | correct   | 0:07:10       | 100.00              |
| student_59 | 2.4.13 | 1             | correct   | 0:07:15       | 100.00              |
+------------+--------+---------------+-----------+---------------+---------------------+
Affected rows: 58
```

```mysql
WITH mean_time AS
(SELECT @mean_time := AVG(submission_time - attempt_time)
FROM step_student JOIN student USING(student_id)
WHERE student_name = "student_59" AND submission_time - attempt_time < 3600),
step_table AS
(SELECT step_id, student_name AS Студент, CONCAT(module_id,'.',lesson_position,'.',step_position) AS Шаг,
        ROW_NUMBER() OVER (PARTITION BY step_id ORDER BY submission_time) AS Номер_попытки,
        result AS Результат,
        CASE WHEN submission_time - attempt_time < 3600 THEN submission_time - attempt_time
        ELSE @mean_time END AS time_try
 FROM step_student
      JOIN student USING(student_id)
      JOIN step USING(step_id)
      JOIN lesson USING(lesson_id)
      CROSS JOIN mean_time
WHERE student_name = "student_59"
ORDER BY module_id, lesson_position, step_position)
SELECT Студент, Шаг, Номер_попытки, Результат, SEC_TO_TIME(ROUND(time_try,0)) AS Время_попытки,
CAST(ROUND(100*time_try/(SUM(time_try) OVER (PARTITION BY step_id)),2)AS DECIMAL(5, 2)) AS Относительное_время
FROM step_table
ORDER BY step_id, Номер_попытки;
```

Вы получили: 2 балл из 2
