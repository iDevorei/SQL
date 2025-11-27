Задание: 6.

Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.

Решение:

```
SELECT DISTINCT p.maker, speed
FROM product AS p
JOIN laptop AS lp ON p.model = lp.model
WHERE hd >= 10
```

-------------------------------------

Задание: 7.

Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).

Решение:

```
SELECT p.model, price
FROM product AS p JOIN pc AS Pc ON p.model = Pc.model
WHERE maker = 'B'
UNION
SELECT p.model, price
FROM product AS p JOIN laptop AS lp ON p.model = lp.model
WHERE maker = 'B'
UNION
SELECT p.model, price
FROM product AS p JOIN printer AS pr ON p.model = pr.model
WHERE maker = 'B'
```

-------------------------------------

Задание: 8.

Найдите производителя, выпускающего ПК, но не ПК-блокноты.

Решение:

```
SELECT maker
FROM product
WHERE type IN ('pc')
EXCEPT
SELECT maker
FROM product
WHERE type IN('laptop')
```

----------------------------------------

Задание: 9.

Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker

Решение:

```
SELECT DISTINCT maker
FROM product AS p JOIN pc ON p.model = pc.model
WHERE speed >= 450
```

----------------------------------------

Задание: 10.

Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price

Решение:

```
SELECT model, price
FROM printer
WHERE price >= (SELECT MAX(price) FROM printer)
```

----------------------------------------

Задание: 11.

Найдите среднюю скорость ПК.

Решение:

```
SELECT AVG(speed)
FROM pc
```

----------------------------------------

Задание: 12.

Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.

Решение:

```
SELECT AVG(speed)
FROM laptop
WHERE price > 1000
```

----------------------------------------

Задание: 13.

Найдите среднюю скорость ПК, выпущенных производителем A.

Решение:

```
SELECT AVG(speed)
FROM pc JOIN product AS p ON pc.model = p.model
WHERE maker IN ('A')
```

----------------------------------------

Задание: 14.

Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.

Решение:

```
SELECT sh.class, name, country
FROM Classes AS cl JOIN Ships AS sh ON cl.class = sh.class
WHERE numGuns >= 10
```

----------------------------------------

Задание: 15.

Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD

Решение:

```
SELECT hd
FROM pc
GROUP BY hd
HAVING COUNT(hd) > 1
```

----------------------------------------

Задание: 16.

Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.

Решение:

```
SELECT DISTINCT A.model AS mod_1, B.model AS mod_2, A.speed, A.ram
FROM pc AS A, pc AS B
WHERE A.speed = B.speed
AND A.ram = B.ram
AND A.model > B.model
```

<!-- По этому решению есть вопросики в плане читаемости -->

----------------------------------------

Задание: 17.

Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК.
Вывести: type, model, speed

Решение:

```
SELECT DISTINCT 'laptop' AS type, lp.model, lp.speed
FROM laptop AS lp
WHERE lp.speed < (SELECT MIN(speed) FROM pc)
```

----------------------------------------

Задание: 18.

Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price

Решение:

```
SELECT DISTINCT p.maker, pr.price
FROM printer AS pr 
JOIN product AS p ON pr.model = p.model
WHERE pr.color = 'y'
AND pr.price = (
SELECT MIN(price)
FROM printer
WHERE color = 'y')
```

----------------------------------------

Задание: 19.

Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов.
Вывести: maker, средний размер экрана.

Решение:

```
SELECT p.maker, AVG(lp.screen) AS avg_screen
FROM product p JOIN laptop lp ON p.model = lp.model
GROUP BY p.maker
```

----------------------------------------

Задание: 20.

Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.

Решение:

```
SELECT p.maker, COUNT(DISTINCT p.model) AS cm
FROM product p
WHERE p.type = 'pc'
GROUP BY p.maker
HAVING COUNT(DISTINCT p.model) >= 3
```

----------------------------------------

Задание: 21.

Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC.
Вывести: maker, максимальная цена.

Решение:

```
SELECT p.maker, MAX(pc.price) AS max
FROM product p JOIN pc ON p.model = pc.model
GROUP BY p.maker
```

----------------------------------------

Задание: 22.

Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.

Решение:

```
SELECT pc.speed, AVG(pc.price) AS avg_p
FROM pc
WHERE pc.speed > 600
GROUP BY pc.speed
```

----------------------------------------

Задание: 23.

Найдите производителей, которые производили бы как ПК
со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц.
Вывести: Maker.

Решение:

```
SELECT p.maker
FROM product p JOIN pc ON p.model = pc.model
WHERE speed >= 750
INTERSECT
SELECT p.maker
FROM product p JOIN laptop lp ON p.model = lp.model
WHERE lp.speed >= 750
```

----------------------------------------

Задание: 24.

Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.

Решение:

```
SELECT model
FROM (
SELECT model, price
FROM pc
UNION
SELECT model, price
FROM laptop
UNION
SELECT model, price
FROM printer
) AS max_model
WHERE price = (
SELECT MAX(price)
FROM (
SELECT price
FROM pc
UNION
SELECT price
FROM laptop
UNION
SELECT price
FROM printer
) AS max_price
)

```

----------------------------------------

Задание: 25.

Найдите производителей принтеров, которые производят ПК с наименьшим объемом RAM и с самым быстрым процессором среди всех ПК, имеющих наименьший объем RAM. Вывести: Maker

Решение:

```
SELECT DISTINCT maker
FROM product
WHERE type = 'printer'
AND maker IN (
SELECT maker
FROM product
WHERE model IN (
SELECT model
FROM pc
WHERE ram = (SELECT MIN(ram) FROM pc)
AND speed = (
SELECT MAX(speed) FROM pc WHERE ram = (SELECT MIN(ram) FROM pc))))
```

----------------------------------------

Задание: 26.

Найдите среднюю цену ПК и ПК-блокнотов, выпущенных производителем A (латинская буква). Вывести: одна общая средняя цена.

Решение:

```
SELECT AVG(price) AS avg
FROM (
SELECT price, model
FROM pc
UNION ALL
SELECT price, model
FROM laptop
) AS avg_price
JOIN product AS p ON p.model = avg_price.model
WHERE maker = 'A'
```

----------------------------------------

Задание: 11.

Найдите средний размер диска ПК каждого из тех производителей, которые выпускают и принтеры. Вывести: maker, средний размер HD.

Решение:

```
SELECT p.maker, AVG(pc.hd) AS avg_hd
FROM product p JOIN pc ON p.model = pc.model
WHERE p.maker IN (SELECT maker FROM product WHERE type = 'printer')
GROUP BY p.maker
```

----------------------------------------

Задание: 11.

Условие.

Решение:

```
no
```

----------------------------------------

Задание: 11.

Условие.

Решение:

```
no
```

----------------------------------------

Задание: 11.

Условие.

Решение:

```
no
```

----------------------------------------

Задание: 11.

Условие.

Решение:

```
no
```

----------------------------------------

Задание: 11.

Условие.

Решение:

```
no
```

----------------------------------------

Задание: 11.

Условие.

Решение:

```
no
```

----------------------------------------

Задание: 11.

Условие.

Решение:

```
no
```

----------------------------------------