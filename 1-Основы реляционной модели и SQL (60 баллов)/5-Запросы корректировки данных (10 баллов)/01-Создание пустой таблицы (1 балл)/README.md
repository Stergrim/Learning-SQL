# Создание пустой таблицы

Создание таблицы осуществляется с помощью запроса `CREATE`, подробно рассмотренного в первом уроке модуля.

**Задание**

Создать таблицу поставок (`supply`), которая имеет ту же структуру, что и таблиц `book`.

| **Поле**  | **Тип, описание**              |
|:----------|:-------------------------------|
| supply_id | INT PRIMARY KEY AUTO_INCREMENT |
| title     | VARCHAR(50)                    |
| author    | VARCHAR(30)                    |
| price     | DECIMAL(8, 2)                  |
| amount    | INT                            |

Введите SQL запрос

*Результат:*

```mysql
Affected rows: 0
```

```mysql
CREATE TABLE supply (supply_id INT PRIMARY KEY AUTO_INCREMENT,
                     title VARCHAR(50),
                     author VARCHAR(30),
                     price DECIMAL(8,2),
                     amount INT);
```

Вы получили: 1 балл из 1
