# Задание

**Задание**

Включить нового человека в таблицу с клиентами. Его имя **Попов Илья**, его email **popov@test**, проживает он в **Москве**.

**Фрагмент логической схемы базы данных:**

<p float="left">
<img src="cx23.jpg" width="200" />
</p>

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 1
```

```mysql
INSERT INTO client (name_client, city_id, email)
SELECT 'Попов Илья', city_id, 'popov@test'
FROM city
WHERE name_city = 'Москва';
```

Вы получили: 1 балл из 1
