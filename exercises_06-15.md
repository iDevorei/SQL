Задание: 6.

Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.

Решение:

`SELECT DISTINCT p.maker, speed
FROM product AS p
JOIN laptop AS lp ON p.model = lp.model
WHERE hd >= 10`

-------------------------------------

Задание: 7.

Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).

Решение:

`SELECT p.model, price
FROM product AS p JOIN pc AS Pc ON p.model = Pc.model
WHERE maker = 'B'
UNION
SELECT p.model, price
FROM product AS p JOIN laptop AS lp ON p.model = lp.model
WHERE maker = 'B'
UNION
SELECT p.model, price
FROM product AS p JOIN printer AS pr ON p.model = pr.model
WHERE maker = 'B'`

-------------------------------------

Задание: 8.

Найдите производителя, выпускающего ПК, но не ПК-блокноты.

Решение:

`SELECT maker
FROM product
WHERE type IN ('pc')
EXCEPT
SELECT maker
FROM product
WHERE type IN('laptop')`

----------------------------------------

Задание: 9.

Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker

Решение:

`SELECT DISTINCT maker
FROM product AS p JOIN pc ON p.model = pc.model
WHERE speed >= 450`

----------------------------------------

Задание: 10.

Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price

Решение:

`SELECT model, price
FROM printer
WHERE price >= (SELECT MAX(price) FROM printer)`

----------------------------------------

Задание: 11.

Найдите среднюю скорость ПК.

Решение:

`SELECT AVG(speed)
FROM pc`

----------------------------------------

Задание: 12.

Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.

Решение:

`SELECT AVG(speed)
FROM laptop
WHERE price > 1000`

----------------------------------------

Задание: 13.

Найдите среднюю скорость ПК, выпущенных производителем A.

Решение:

`SELECT AVG(speed)
FROM pc JOIN product AS p ON pc.model = p.model
WHERE maker IN ('A')`

----------------------------------------

Задание: 14.

Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.

Решение:

`SELECT sh.class, name, country
FROM Classes AS cl JOIN Ships AS sh ON cl.class = sh.class
WHERE numGuns >= 10`

----------------------------------------

Задание: 15.

Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD

Решение:

`SELECT hd
FROM pc
GROUP BY hd
HAVING COUNT(hd) > 1`

----------------------------------------