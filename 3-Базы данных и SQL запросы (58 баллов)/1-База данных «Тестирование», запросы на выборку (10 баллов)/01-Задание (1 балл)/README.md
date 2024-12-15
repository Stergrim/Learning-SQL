# Задание

**Задание**

Вывести студентов, которые сдавали дисциплину «Основы баз данных», указать дату попытки и результат. Информацию вывести по убыванию результатов тестирования.

**Фрагмент логической схемы базы данных:**

<p float="left">
<img src="cx_4_3.jpg" width="400" />
</p>

Введите SQL запрос

*Результат:*

```mysql
Query result:
+-----------------+--------------+--------+
| name_student    | date_attempt | result |
+-----------------+--------------+--------+
| Яковлева Галина | 2020-04-21   | 100    |
| Баранов Павел   | 2020-03-23   | 67     |
| Яковлева Галина | 2020-03-26   | 0      |
+-----------------+--------------+--------+
Affected rows: 3
```

```mysql
SELECT name_student, date_attempt, result
FROM student
     INNER JOIN attempt USING(student_id)
     INNER JOIN subject USING(subject_id)
WHERE name_subject = 'Основы баз данных'
ORDER BY result DESC;
```

Вы получили: 1 балл из 1
