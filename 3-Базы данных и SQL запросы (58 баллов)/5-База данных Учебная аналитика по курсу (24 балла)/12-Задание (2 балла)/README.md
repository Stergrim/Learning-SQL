# Задание

**Задание**

Online курс обучающиеся могут проходить по различным траекториям, проследить за которыми можно по способу решения ими заданий шагов курса. Большинство обучающихся за несколько попыток  получают правильный ответ 
и переходят к следующему шагу. Но есть такие, что остаются на шаге, выполняя несколько верных попыток, или переходят к следующему, оставив нерешенные шаги.

Выделив эти "необычные" действия обучающихся, можно проследить их траекторию работы с курсом и проанализировать задания, для которых эти действия выполнялись, а затем их как-то изменить. 

Для этой цели необходимо выделить группы обучающихся по способу прохождения шагов:
- **I группа** - это те пользователи, которые после верной попытки решения шага делают неверную (скорее всего для того, чтобы поэкспериментировать или проверить, как работают примеры);
- **II группа** - это те пользователи, которые делают больше одной верной попытки для одного шага (возможно, улучшают свое решение или пробуют другой вариант);
- **III группа** - это те пользователи, которые не смогли решить задание какого-то шага (у них все попытки по этому шагу - неверные).

Вывести группу (`I, II, III`), имя пользователя, количество шагов, которые пользователь выполнил по соответствующему способу. Столбцы назвать `Группа, Студент, Количество_шагов`. Отсортировать информацию по возрастанию номеров групп, потом по убыванию количества шагов и, наконец, по имени студента в алфавитном порядке.

**Фрагмент логической схемы базы данных:**

<p float="left">
<img src="5_1 (1).png" width="200" />
</p>

Введите SQL запрос

*Результат:*

```mysql
Query result:
+--------+------------+------------------+
| Группа | Студент    | Количество_шагов |
+--------+------------+------------------+
| I      | student_15 | 2                |
| I      | student_53 | 2                |
| I      | student_11 | 1                |
| I      | student_34 | 1                |
| I      | student_35 | 1                |
| I      | student_40 | 1                |
| I      | student_57 | 1                |
| I      | student_62 | 1                |
| I      | student_9  | 1                |
| II     | student_53 | 4                |
| II     | student_62 | 4                |
| II     | student_34 | 3                |
| II     | student_60 | 3                |
| II     | student_20 | 2                |
| II     | student_35 | 2                |
| II     | student_9  | 2                |
| II     | student_11 | 1                |
| II     | student_15 | 1                |
| II     | student_30 | 1                |
| II     | student_36 | 1                |
| II     | student_39 | 1                |
| II     | student_40 | 1                |
| II     | student_46 | 1                |
| II     | student_57 | 1                |
| II     | student_59 | 1                |
| III    | student_24 | 3                |
| III    | student_33 | 1                |
| III    | student_42 | 1                |
| III    | student_50 | 1                |
| III    | student_51 | 1                |
| III    | student_59 | 1                |
| III    | student_64 | 1                |
+--------+------------+------------------+
Affected rows: 32
```

```mysql
SELECT Группа, student_name AS Студент, COUNT(*) AS Количество_шагов
FROM (SELECT "I" AS Группа, student_name,
             LAG(result,1,"wrong") OVER (PARTITION BY student_id, step_id ORDER BY submission_time) AS prev_result,
             result
      FROM step_student JOIN student USING(student_id)) AS one_group_ext
WHERE prev_result = "correct" AND result = "wrong"
GROUP BY student_name
UNION
SELECT Группа, student_name AS Студент, COUNT(*) AS Количество_шагов
FROM (SELECT "II" AS Группа, student_name
      FROM step_student JOIN student USING(student_id)
      WHERE result = "correct"
      GROUP BY student_name, step_id
      HAVING COUNT(*) > 1) AS two_group_ext
GROUP BY student_name
UNION
SELECT Группа, student_name AS Студент, COUNT(*) AS Количество_шагов
FROM (SELECT "III" AS Группа, student_name,
             SUM(CASE WHEN result = 'wrong' THEN 1 ELSE 0 END) AS sum_result
      FROM step_student JOIN student USING(student_id)
      GROUP BY student_name, step_id
      HAVING sum_result = COUNT(*)) three_group_ext
GROUP BY student_name
ORDER BY Группа, Количество_шагов DESC, Студент;
```

Вы получили: 2 балл из 2
