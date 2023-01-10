# rpbd_zhgulev_3281

1. Выведите на экран любое сообщение.
```SQL
DO $$
BEGIN
	RAISE NOTICE ' Do exercises ';
END;
$$;
```


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
DO $$
DECLARE i int := 20;
BEGIN
	WHILE i < 31 LOOP
		RAISE NOTICE 'sqrt(%) = %', i, i * i;
		i := i + 1;
	END LOOP;
END;
$$;
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

-----------------------
<br><br>

6. Последовательность Коллатца. Берётся любое натуральное число. Если чётное - делим его на 2, если нечётное, то умножаем его на 3 и прибавляем 1. Такие действия выполняются до тех пор, пока не будет получена единица. Гипотеза заключается в том, что какое бы начальное число n не было выбрано, всегда получится 1 на каком-то шаге. Задания: написать функцию, входной параметр - начальное число, на выходе - количество чисел, пока не получим 1; написать процедуру, которая выводит все числа последовательности. Входной параметр - начальное число.
```SQL
CREATE OR REPLACE FUNCTION cal(x integer) RETURNS integer 
LANGUAGE plpgsql
AS $$
DECLARE i int := 0;
BEGIN
	WHILE x != 1 LOOP
		IF mod(x,2) = 0 THEN
			x := x / 2;
		ELSE x := x * 3 + 1;
		END IF;
	i := i + 1;
	END LOOP;
	RETURN i;
END;
$$;

SELECT * FROM cal(3)
```

```SQL

CREATE OR REPLACE PROCEDURE f(x integer)
LANGUAGE plpgsql
AS $$
DECLARE i int := 1;
BEGIN
	RAISE NOTICE '0 step -- %', x;
	WHILE x != 1 LOOP
		IF mod(x,2) = 0 THEN
			x := x / 2;
			RAISE NOTICE '% step -- %', i, x;
		ELSE 
			x := x * 3 + 1; 
			RAISE NOTICE '% step -- %', i, x;
		END IF;
	i := i + 1;
	END LOOP;
END;
$$;

CALL f(3)

```


-----------------------
<br><br>

7. Числа Люка. Объявляем и присваиваем значение переменной - количество числе Люка. Вывести на экран последовательность чисел. Где L0 = 2, L1 = 1 ; Ln=Ln-1 + Ln-2 (сумма двух предыдущих чисел). Задания: написать фунцию, входной параметр - количество чисел, на выходе - последнее число (Например: входной 5, 2 1 3 4 7 - на выходе число 7); написать процедуру, которая выводит все числа последовательности. Входной параметр - количество чисел.

```SQL
CREATE OR REPLACE FUNCTION Luke(x integer) RETURNS integer 
LANGUAGE plpgsql
AS $$
DECLARE
Ln_0 int := 2;
Ln_1 int := 1;
Ln int; 
BEGIN
	FOR x IN 3..x LOOP
		Ln := Ln_0 + Ln_1;
		Ln_0 := Ln_1; 
		Ln_1 := Ln;
	END LOOP;
	RETURN Ln;
END;
$$;

SELECT * FROM Luke(5)
```


```SQL
CREATE OR REPLACE PROCEDURE Luka(x integer)
LANGUAGE plpgsql
AS $$
DECLARE
Ln_0 int := 2;
Ln_1 int := 1;
Ln int; 
BEGIN
	RAISE NOTICE '#1 -- %', Ln_0;
	RAISE NOTICE '#2 -- %', Ln_1;
	FOR x IN 3..x LOOP
		Ln := Ln_0 + Ln_1;
		Ln_0 := Ln_1; 
		Ln_1 := Ln;
		RAISE NOTICE '#% -- %',x, Ln;
	END LOOP;
END;
$$;

CALL Luka(5)
```


-----------------------
<br><br>

8. Напишите функцию, которая возвращает количество человек родившихся в заданном году.

```SQL
CREATE OR REPLACE FUNCTION B_count(x int) RETURNS int 
AS $$
DECLARE
	Bd_count int;
BEGIN
	SELECT COUNT(p.id) INTO Bd_count
	FROM people p
	WHERE EXTRACT(YEAR FROM p.birth_date) = x;
	RETURN Bd_count;
END
$$ 
LANGUAGE plpgsql;
SELECT B_count(1995) As People_Count
```

-----------------------
<br><br>

9. Напишите функцию, которая возвращает количество человек с заданным цветом глаз.

```SQL
CREATE OR REPLACE FUNCTION Eyeclrcount(x varchar) RETURNS int 
AS $$
DECLARE
	eyeCount int;
BEGIN
	SELECT COUNT(p.id) INTO eyeCount
	FROM people p
	WHERE  p.eyes = x;
	RETURN eyeCount;
END
$$ 
LANGUAGE plpgsql;
SELECT Eyeclrcount('brown') As eyesClr
```

-----------------------
<br><br>

10. Напишите функцию, которая возвращает ID самого молодого человека в таблице.
```SQL
CREATE OR REPLACE FUNCTION youngest() RETURNS int AS $$
DECLARE
	pid int;
BEGIN
	SELECT p.id INTO pid
	FROM people p
	WHERE p.birth_date = (SELECT MAX(people.birth_date) FROM people);
	RETURN pid;
END
$$ LANGUAGE plpgsql;
SELECT youngest() As theYoungest
```
-----------------------
<br><br>

11. Напишите процедуру, которая возвращает людей с индексом массы тела больше заданного. ИМТ = масса в кг / (рост в м)^2.

```SQL
CREATE OR REPLACE PROCEDURE ChoseWeight(x int) AS $$
DECLARE
	chosen people%ROWTYPE;
BEGIN
FOR chosen IN SELECT * FROM people
	LOOP
		IF chosen.weight/((chosen.growth*chosen.growth)/10000) > x THEN 
		RAISE NOTICE ' % ', chosen;
		END IF;	
	END LOOP;
END
$$ LANGUAGE plpgsql;
CALL ChoseWeight(25)
```

-----------------------
<br><br>

12. Измените схему БД так, чтобы в БД можно было хранить родственные связи между людьми. Код должен быть представлен в виде транзакции (Например (добавление атрибута): BEGIN; ALTER TABLE people ADD COLUMN leg_size REAL; COMMIT;). Дополните БД данными.

```SQL
BEGIN;
CREATE TABLE people_family (people_id int REFERENCES people(id), family_member_id int REFERENCES people(id));
INSERT INTO people_family (people_id, family_member_id)
VALUES (3, 4), (3, 5), (4, 5), (2, 6);
COMMIT;
```
-----------------------
<br><br>

13. Напишите процедуру, которая позволяет создать в БД нового человека с указанным родством.

```SQL
CREATE OR REPLACE PROCEDURE NewFamilyMentor(name varchar, surname varchar, birth_date date, growth real, weight real, eyes varchar, hair varchar, family_member_id int) AS $$
DECLARE
	person_id int;
BEGIN
	INSERT INTO people (name, surname, birth_date, growth, weight, eyes, hair)
	VALUES (name, surname, birth_date, growth, weight, eyes, hair) RETURNING id INTO person_id;
	
	INSERT INTO people_family (people_id, family_member_id)
	VALUES (person_id, family_member_id);
	INSERT INTO people_family (people_id, family_member_id)
	VALUES (family_member_id, person_id);
END
$$ LANGUAGE plpgsql;

CALL NewFamilyMentor('vitaliy', 'ivanov', '2010.04.29', 150.4, 56.1, 'green', 'blond', 1)
```
-----------------------
<br><br>

14. Измените схему БД так, чтобы в БД можно было хранить время актуальности данных человека (выполнить также, как п.12).

```SQL
BEGIN;
ALTER TABLE people ADD COLUMN actual_data TIMESTAMP DEFAULT NOW();
COMMIT;
```

-----------------------
<br><br>

15. Напишите процедуру, которая позволяет актуализировать рост и вес человека.

```SQL
CREATE OR REPLACE PROCEDURE actual_data(pid INT, Ngrowth REAL, Nweigth REAL)
AS $$
BEGIN
	UPDATE people SET growth = Ngrowth, weight = Nweigth, actual_data = NOW()
	WHERE people.id = pid;
END

$$ LANGUAGE plpgsql;
CALL actual_data(5, 190.2, 103.8);
```