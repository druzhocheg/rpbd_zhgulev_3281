# rpbd_zhgulev_3281

1. Выведите на экран любое сообщение.
```SQL
DO $$
BEGIN
	RAISE NOTICE ' Do exercises ';
END;
$$;
```

![Задание 1](/Ex_1-15/ex_1.png)
-----------------------
<br><br>

2. Выведите на экран текущую дату.
```SQL

DO $$
DECLARE str varchar := CURRENT_DATE;
BEGIN
	RAISE NOTICE ' % ', str;
END;
$$;

```
![Задание 2](/Ex_1-15/ex_2.png)
-----------------------
<br><br>

3. Создайте две числовые переменные и присвойте им значение. Выполните математические действия с этими числами и выведите результат на экран.
```SQL
DO $$
DECLARE x real; y real;
BEGIN
	x := 3;
	y := 5;
	RAISE NOTICE 'x + y = % ', x + y;
	RAISE NOTICE 'x - y = % ', x - y;
	RAISE NOTICE 'x * y = % ', x * y;
	RAISE NOTICE 'x / y = % ', x / y;
END;
$$;


```
![Задание ](/Ex_1-15/ex_3.png)
-----------------------
<br><br>

4.Написать программу двумя способами 1 - использование IF, 2 - использование CASE. Объявите числовую переменную и присвоейте ей значение. Если число равно 5 - выведите на экран "Отлично". 4 - "Хорошо". 3 - Удовлетворительно". 2 - "Неуд". В остальных случаях выведите на экран сообщение, что введённая оценка не верна.
```SQL

DO $$
DECLARE x int := 4;
BEGIN
	IF x = 5 THEN
		RAISE NOTICE 'Отлично';
	ELSIF x = 4 THEN
		RAISE NOTICE 'Хорошо';
	ELSIF x = 3 THEN
		RAISE NOTICE 'Удовлетворительно';
	ELSIF x = 2 THEN
		RAISE NOTICE 'Неуд';
	ELSE RAISE NOTICE 'Введённая оценка не верна';
	END IF;
END;
$$;
```
```SQL
DO $$
DECLARE x int := ;
BEGIN
	 CASE x
	 	WHEN 5 THEN RAISE NOTICE 'Отлично';
		WHEN 4 THEN RAISE NOTICE 'Хорошо';
		WHEN 3 THEN RAISE NOTICE 'Удовлетворительно';
		WHEN 2 THEN RAISE NOTICE 'Неуд';
		ELSE RAISE NOTICE 'Введённая оценка не верна';
	END CASE;
END;
$$;
```
![Задание 4](/Ex_1-15/ex_4.png)
-----------------------
<br><br>

5. Выведите все квадраты чисел от 20 до 30 3-мя разными способами (LOOP, WHILE, FOR).
```SQL
DO $$
DECLARE i int := 20; 
BEGIN
	LOOP
	 	IF i < 31 THEN
			RAISE NOTICE ' sqr(%) = % ', i, i*i;
		ELSE EXIT;
		END IF;
		i := i + 1;
	END LOOP;
END;
$$;
```

```SQL
```


```SQL
DO $$
BEGIN
	 FOR i IN 20..30 LOOP
	 	RAISE NOTICE ' sqr(%) = % ', i, i*i;
	 END LOOP;
END;
$$;
```
![Задание ](/Ex_1-15/)
-----------------------
<br><br>