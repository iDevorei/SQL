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

Здесь будет условие.

Решение:

```
no
```

----------------------------------------

Задание: 21.

Здесь будет условие.

Решение:

```
no
```

----------------------------------------

Задание: 22.

Здесь будет условие.

Решение:

```
no
```

----------------------------------------

Задание: 23.

Здесь будет условие.

Решение:

```
no
```

----------------------------------------

Задание: 24.

Здесь будет условие.

Решение:

```
no
```

----------------------------------------

Задание: 25.

Здесь будет условие.

Решение:

```
no
```

----------------------------------------