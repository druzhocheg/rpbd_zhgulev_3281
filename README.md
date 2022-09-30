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
![Задание ](путь)
