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