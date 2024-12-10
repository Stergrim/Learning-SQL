# Задание

**Задание**

В таблице `fine` увеличить в два раза сумму неоплаченных штрафов для отобранных на предыдущем шаге записей.

**Важно!** Если в запросе используется несколько таблиц или запросов, включающих одинаковые поля, то применяется полное имя столбца, включающего название таблицы через символ «**.**». Например, `fine.name` и `query_in.name`.

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 2

Affected rows: 2
```

```mysql
CREATE TABLE query_in (SELECT name, number_plate, violation
                       FROM fine
                       GROUP BY name, number_plate, violation
                       HAVING COUNT(*) > 1
                       ORDER BY name, number_plate, violation);

UPDATE fine, query_in
SET fine.sum_fine = fine.sum_fine*2
WHERE fine.name = query_in.name AND fine.number_plate = query_in.number_plate AND
      fine.violation = query_in.violation AND date_payment IS NULL;
```

Вы получили: 1 балл из 1
