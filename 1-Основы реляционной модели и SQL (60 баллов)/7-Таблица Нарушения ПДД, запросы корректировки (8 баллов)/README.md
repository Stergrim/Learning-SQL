# Таблица "Нарушения ПДД", запросы корректировки

В этом уроке на каждом шаге используется таблица,  в которой представлена информация о начисленных водителям штрафах за нарушения правил дорожного движения (ПДД). С помощью запросов корректировки необходимо выполнить следующие действия:
- создать таблицу с информацией о штрафах ;
- заполнить ее;
- занести сумму штрафа за каждое новое нарушение ПДД;
- если водитель на определенной машине совершил повторное нарушение, то сумму его штрафа за данное нарушение нужно увеличить в два раза (часть 1, часть 2) ;
- если водитель оплатил свой штраф в течение 20 дней со дня нарушения, то значение его штрафа уменьшить в два раза;
- создать новую таблицу,  в которую включить информацию о всех неоплаченных штрафах;
- удалить  информацию о нарушениях, совершенных раньше некоторой даты.

На четвертом шаге рассматривается временное именование таблиц (алиасы).

**Структура и наполнение таблицы**

В таблице `fine` представлена информация о начисленных водителям штрафах за нарушения правил дорожного движения (ПДД) (фамилия водителя, номер машины, описание нарушения, сумма штрафа, дата совершения нарушения и дата оплаты штрафа):

| **fine_id**                    | **name**        | **number_plate** | **violation**                       | **sum_fine** | **date_violation** | **date_payment** |
|:-------------------------------|:----------------|:-----------------|:------------------------------------|:-------------|:-------------------|:-----------------|
| INT PRIMARY KEY AUTO_INCREMENT | VARCHAR(30)     | VARCHAR(6)       | VARCHAR(50)                         | DECIMAL(8,2) | DATЕ               | DATЕ             |
| 1                              | Баранов П.Е.    | Р523ВТ           | Превышение скорости (от 40 до 60)   | 500.00       | 2020-01-12         | 2020-01-17       |
| 2                              | Абрамова К.А.   | О111АВ           | Проезд на запрещающий сигнал        | 1000.00      | 2020-01-14         | 2020-02-27       |
| 3                              | Яковлев Г.Р.    | Т330ТТ           | Превышение скорости (от 20 до 40)   | 500.00       | 2020-01-23         | 2020-02-23       |
| 4                              | Яковлев Г.Р.    | М701АА           | Превышение скорости (от 20 до 40)   |              | 2020-01-12         |                  |
| 5                              | Колесов С.П.    | К892АХ           | Превышение скорости (от 20 до 40)   |              | 2020-02-01         |                  |
| 6                              | Баранов П.Е.    | Р523ВТ           | Превышение скорости (от 40 до 60)   |              | 2020-02-14         |                  |
| 7                              | Абрамова К.А.   | О111АВ           | Проезд на запрещающий сигнал        |              | 2020-02-23         |                  |
| 8                              | Яковлев Г.Р.    | Т330ТТ           | Проезд на запрещающий сигнал        |              | 2020-03-03         |                  |

В таблицу `traffic_violation` занесены нарушения ПДД и соответствующие штрафы (в рублях): 

| **violation_id**               | **violation**                     | **sum_fine** |
|:-------------------------------|:----------------------------------|:-------------|
| INT PRIMARY KEY AUTO_INCREMENT | VARCHAR(50)                       | DECIMAL(8,2) |
| 1                              | Превышение скорости (от 20 до 40) | 500.00       |
| 2                              | Превышение скорости (от 40 до 60) | 1000.00      |
| 3                              | Проезд на запрещающий сигнал      | 1000.00      |
