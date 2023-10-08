# Домашнее задание к занятию "Индексы" - `Нагорнов Антон Алексеевич`

### Задание 1

SELECT (SUM(INDEX_LENGTH) / SUM(DATA_LENGTH)) * 100 AS table_index  
from information_schema.TABLES  
WHERE TABLE_SCHEMA = 'sakila';  
<img src = "files/1.png" width = 100%>

### Задание 2

После анализа запроса было выявлено, что много времени тратиться на обработку лишних таблиц (inventory, rental, film). Данные из этих таблиц для выполнения запроса вообще не нужны, т.к. подсчитывается платежи за конкретную дату. Поэтому из запроса их можно просто удалить и мы получаем абсолютно те же данные, что и в исходном запросе, только быстрее в 5 раз минимум. На обработку исходного запроса ушло порядка 6 секунд, оптимизированный запрос выполнился моментально.

select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id)
from payment p, customer c
where date(p.payment_date) = '2005-07-30' and p.customer_id = c.customer_id;
<img src = "files/2.png" width = 100%>
