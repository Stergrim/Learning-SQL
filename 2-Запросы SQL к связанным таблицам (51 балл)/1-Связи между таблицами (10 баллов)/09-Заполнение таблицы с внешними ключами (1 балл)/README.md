# Заполнение таблицы с внешними ключами

На предыдущих шагах были созданы и заполнены таблицы `author`:

| **author_id** | **name_author**  |
|:--------------|:-----------------|
| 1             | Булгаков М.А.    |
| 2             | Достоевский Ф.М. |
| 3             | Есенин С.А.      |
| 4             | Пастернак Б.Л.   |

и `genre`:

| **genre_id** | **name_genre** |
|:-------------|:---------------|
| 1            | Роман          |
| 2            | Поэзия         |

Эти таблицы являются главными для таблицы `book` и связаны с ней через внешние ключи:

<p float="left">
<img src="cx1.jpg" width="400" />
</p>

При заполнении таблицы `book` в связанные столбцы необходимо заносить значения ключей главной таблицы. Например, Книгу «Игрок» написал Достоевский, поэтому значение поля `author_id` для этой записи должно быть 2, так как значение ключа для этого автора в таблице `author` равно 2. Значение поля `genre_id` для книги «Игрок» – 1, так как эта книга относится к жанру «Роман».

**Задание**

Для каждой строки таблицы `book` занесите значения в поля `author_id` и `genre_id`. Считать, что книга Есенина относится к жанру «Поэзия», остальные книги – к жанру «Роман».

Через запятую перечислены значения полей `book_id`, `title`, `author_id`, `genre_id`, `price`, `amount` каждой записи таблицы `book`. Заполните пропуски.

Авторы и их произведения:

| **Название книги**    | **Автор**        | **Цена**  | **Количество** |
|:----------------------|:-----------------|:----------|:---------------|
| Мастер и Маргарита    | Булгаков М.А.    | 670.99    | 3              |
| Белая гвардия         | Булгаков М.А.    | 540.50    | 5              |
| Идиот                 | Достоевский Ф.М. | 460.00    | 10             |
| Братья Карамазовы     | Достоевский Ф.М. | 799.01    | 3              |
| Игрок                 | Достоевский Ф.М. | 480.50    | 10             |
| Стихотворения и поэмы | Есенин С.А.      | 650.00    | 15             |

**Заполните пропуски**

1, Мастер и Маргарита,`1`✅, `1`✅, 670.99, 3<br>
2, Белая гвардия,`1`✅, `1`✅, 540.50, 5<br>
3, Идиот,`2`✅, `1`✅, 460.00, 10<br>
4, Братья Карамазовы,`2`✅, `1`✅, 799.01, 3<br>
5, Игрок,`2`✅, `1`✅, 480.50, 10<br>
6, Стихотворения и поэмы,`3`✅, `2`✅, 650.00, 15

Вы получили: 1 балл из 1
