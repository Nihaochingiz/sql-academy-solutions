# Решение задач курса


### Модуль 2

https://sql-academy.org/ru/guide/basic-syntax-sql-query


1. Вывод строки

С помощью оператора SELECT выведите текст "Hello world"

```sql
SELECT "Hello world"
```
2. SELECT по всем столбцам

Выведите все столбцы из таблицы Payments.

```sql
SELECT * FROM Payments
```

3. SELECT по нескольким столбцам

Выведите поля member_id, member_name и status из таблицы FamilyMembers.

```sql
SELECT member_id, member_name, status FROM FamilyMembers
```

4. Вывод с псевдонимами
Выведите поле name из таблицы Passenger. При выводе данного поля используйте псевдоним "passengerName"

```sql
SELECT name AS passengerName FROM Passenger
```


https://sql-academy.org/ru/guide/using-functions

1. Вывод строки в нижнем регистре
Выведите текст "Hello world" в нижнем регистре с помощью соответствующей функции.
Для вывода текста используйте псевдоним lower_string.

```sql
SELECT LOWER("Hello world") AS lower_string;
```

2. Вывод года из даты
Выведите полное имя члена семьи и его год рождения, используя функцию YEAR.
Для вывода года рождения используйте псевдоним year_of_birth.

```sql
SELECT member_name, YEAR(birthday) AS year_of_birth
FROM FamilyMembers;
```

3. Вычисление длины фамилии
Выведите полное имя члена семьи и длину его фамилии.
Для вывода длины фамилии используйте псевдоним lastname_length.

```sql
SELECT member_name,
	LENGTH(member_name) - INSTR(member_name, ' ') AS lastname_length
FROM FamilyMembers;
```

https://sql-academy.org/ru/guide/distinct-operator

1. Вывод уникальных имён
Выведите только уникальные имена first_name студентов из таблицы Student.

```sql
SELECT DISTINCT first_name FROM Student;
```

2. Вывод уникальных пар колонок
Выведите только уникальные пары значений идентификатор учителя teacher и идентификатор предмета subject из таблицы Schedule. Пара 2, 3 отличается от 3, 2

```sql
SELECT DISTINCT teacher, subject FROM Schedule;
```

https://sql-academy.org/ru/guide/conditional-where-operator


1. Простая фильтрация по числам
Выведите идентификаторы товаров (поле good) из таблицы Payments, стоимость которых больше 2000 единиц. Стоимость товара хранится в поле unit_price.

```sql
SELECT good 
FROM Payments 
WHERE unit_price > 2000;
```

2. Простая фильтрация по строкам
Выведите имена (поле member_name) членов семьи из таблицы FamilyMembers, чей статус (поле status) равен "father".

```sql
SELECT member_name
FROM FamilyMembers
WHERE status = 'father';
```
3. Логическое ИЛИ
Выведите имя (поле member_name) и дату рождения (поле birthday) членов семьи из таблицы FamilyMembers, чей статус (поле status) равен "father" или "mother".

```sql
SELECT member_name, birthday
FROM FamilyMembers
WHERE status = 'father' OR status = 'mother';
```

4. Логическое И

Необходимо получить все комнаты, в которых есть как кухня (поле has_kitchen), так и интернет (поле has_internet). Напишите запрос, удовлетворяющий вышеописанному условию, который выводит все поля из таблицы Rooms.
Наличие обозначается 1 или true, а отсутствие 0 или false.

```sql
SELECT *
FROM Rooms
WHERE has_kitchen = 1 && has_internet = 1;
```

https://sql-academy.org/ru/guide/is-null-between-in-operators

1. Вывод записей, содержащих NULL

Выведите имена first_name и фамилии last_name студентов из таблицы Student, у кого отсутствует отчество middle_name

```sql
SELECT first_name,last_name 
FROM Student 
WHERE middle_name IS NULL;
```

2. Поиск значений в указанном промежутке
Выведите резервации комнат (поля room_id, start_date, end_date) из таблицы Reservations, у которых итоговая стоимость аренды (поле total) находится в промежутке от 500 до 1200 включительно.

```sql
SELECT room_id, start_date, end_date
FROM Reservations
WHERE total BETWEEN 500 AND 1200;
```

3. Поиск значений, входящий в определенный список

Выведите информацию о студентах из таблицы Student, у которых год рождения соответствует одному из перечисленных: 2000, 2002 и 2004.

```sql
SELECT * FROM Student
WHERE YEAR(birthday) IN (2000, 2002, 2004);
```

https://sql-academy.org/ru/guide/operator-like


1. Поиск по строковому шаблону

Найдите всех членов семьи с фамилией "Quincey" и выведите поле member_name

```sql
SELECT member_name 
FROM FamilyMembers
WHERE member_name LIKE '%Quincey%';
```

https://sql-academy.org/ru/guide/sorting



1. Сортировка по убыванию

Для каждого отдельного платежа выведите идентификатор товара и сумму, потраченную на него, в отсортированном по убыванию этой суммы виде. Список платежей находится в таблице Payments.
Для вывода суммы используйте псевдоним sum.

```sql
SELECT good, 
       amount * unit_price AS 'sum'
FROM Payments
ORDER BY sum DESC;
```

2. Сортировка по нескольким столбцам

Выведите все данные членов семьи с фамилией Quincey из таблицы FamilyMembers и отсортируйте их по возрастанию сначала по столбцу status, а затем по member_name.

```sql
SELECT * 
FROM FamilyMembers
WHERE member_name LIKE '%Quincey%'
ORDER BY status, member_name ASC;
```

https://sql-academy.org/ru/guide/groupping

1. Количество комнат по типам

Сгруппируйте данные из таблицы Rooms по полю home_type и выведите тип жилья и количество объектов каждого типа. Используйте псевдоним count_rooms для количества объектов.

```sql
SELECT home_type, COUNT(id) AS count_rooms 
FROM Rooms
GROUP BY home_type;
```

2. Средняя цена по типу жилья и ТВ

Сгруппируйте данные из таблицы Rooms по полям home_type и has_tv. Выведите тип жилья, признак наличия телевизора (поле has_tv) и среднюю цену для каждой группы. Используйте псевдоним avg_price для средней цены.

```sql
SELECT home_type, has_tv, AVG(price) as avg_price
FROM Rooms
GROUP BY home_type, has_tv;
```

https://sql-academy.org/ru/guide/aggregate-functions

1. Группировка и сортировка

Подсчитайте количество учеников в каждом классе, а также отсортируйте их по убыванию количества учеников. Принадлежность ученика к конкретному классу вы можете получить из таблицы Student_in_class. В качестве результата необходимо вывести идентификатор класса (поле class) и количество учеников в этом классе.

Для вывода количества учеников используйте псевдоним count.

```sql
SELECT class, count(id) AS count 
FROM Student_in_class 
GROUP BY class
ORDER BY count DESC;
```

2. Агрегатные функции MIN и MAX

Для каждого из существующих статусов (поле status) найдите самого старого человека (используйте поле birthday). Выведите статус и дату рождения.
Для вывода даты рождения используйте псевдоним birthday.

```sql
SELECT status, MIN(birthday) as birthday
FROM FamilyMembers
GROUP BY status;
```

3. Агрегатная функция AVG

Получите среднее время полётов, совершённых на каждой из моделей самолёта. Выведите поле plane и среднее время полётов в секундах.
Для вывода времени используйте псевдоним time.
Чтобы получить разницу во времени в секундах между двумя датами используйте:
Для MySQL: TIMESTAMPDIFF(second, time_out, time_in)
Для PostgreSQL: EXTRACT(EPOCH FROM (time_in - time_out))

```sql
SELECT plane, AVG(TIMESTAMPDIFF(second, time_out, time_in)) AS time
FROM Trip
GROUP BY plane;
```

4. Выборка с использованием нескольких агрегатных функций

Выведите идентификатор комнаты (поле room_id), среднюю стоимость за один день аренды (поле price, для вывода используйте псевдоним avg_price), а также количество резерваций этой комнаты (используйте псевдоним count). Полученный результат отсортируйте в порядке убывания сначала по количеству резерваций, а потом по средней стоимости.

```sql
SELECT room_id, AVG(price) AS avg_price, 
COUNT(room_id) AS count from Reservations
GROUP BY room_id
ORDER BY count DESC, avg_price DESC;
```


https://sql-academy.org/ru/guide/operator-having

1. Фильтрация групп

Выведите типы комнат (поле home_type) и разницу между самым дорогим и самым дешевым представителем данного типа. В итоговую выборку включите только те типы жилья, количество которых в таблице Rooms больше или равно 2.
Для вывода разницы стоимости используйте псевдоним difference.

```sql
SELECT home_type, MAX(price) - MIN(price) AS difference
FROM Rooms
GROUP BY home_type
HAVING COUNT(*) >= 2;
```
### Модуль 3
### Модуль 3

https://sql-academy.org/ru/guide/inner-join

1. INNER JOIN
Объедините таблицы Class и Student_in_class с помощью внутреннего соединения по полям Class.id и Student_in_class.class. Выведите название класса (поле Class.name) и идентификатор ученика (поле Student_in_class.student).

```sql
SELECT Class.name, Student_in_class.student
FROM Class
INNER JOIN Student_in_class
ON Class.id = Student_in_class.class;
```

2. Многотабличный INNER JOIN
Дополните запрос из предыдущего задания, добавив ещё одно внутреннее соединение с таблицей Student. Объедините по полям Student_in_class.student и Student.id и вместо идентификатора ученика выведите его имя (поле first_name).

```sql
SELECT Class.name, Student.first_name
FROM Class
INNER JOIN Student_in_class
ON Class.id = Student_in_class.class
INNER JOIN Student
ON Student_in_class.student = Student.id
```


4. INNER JOIN с группировкой
Выведите идентификатор (поле room_id) и среднюю оценку комнаты (поле rating, для вывода используйте псевдоним avg_score), составленную на основании отзывов из таблицы Reviews.
Данная таблица связана с Reservations (таблица, где вы можете взять идентификатор комнаты) по полям reservation_id и Reservations.id.



https://sql-academy.org/ru/guide/outer-join

1. Внешнее левое соединение
Выведите имя first_name и фамилию last_name каждого учителя из таблицы Teacher, а также количество занятий, в которых он был назначен преподавателем. Если преподаватель не был назначен ни на одно занятие, то выведите 0.
Для вывода количества занятий используйте псевдоним amount_classes.


SELECT first_name, last_name, COUNT(Schedule.id) AS amount_classes
FROM Teacher
LEFT JOIN Schedule
ON Schedule.teacher = Teacher.id
GROUP BY Teacher.first_name, Teacher.last_name;


https://sql-academy.org/ru/guide/limit

1. Ограничение записей с начала таблицы

Отсортируйте список компаний (таблица Company) по их названию в алфавитном порядке и выведите первые две записи.

```sql
SELECT *
FROM Company
ORDER BY name ASC
LIMIT 2;
```


2. Ограничение количества записей со смещением

Выведите начало (поле start_pair) и окончание (поле end_pair) второго и третьего занятия из таблицы Timepair.

```sql
SELECT start_pair,end_pair
FROM Timepair
ORDER BY id
LIMIT 2 OFFSET 1;
```


# Многостолбцовые запросы

https://sql-academy.org/ru/guide/subquery-with-several-column#mnogostolbcovye-podzaprosy

1. Строковые подзапросы

Выведите список комнат (все поля, таблица Rooms), которые по своим удобствам (has_tv, has_internet, has_kitchen, has_air_con) совпадают с комнатой с идентификатором "11".

```sql
SELECT *
FROM Rooms
WHERE (has_tv, has_internet, has_kitchen, has_air_con) IN (
    SELECT has_tv, has_internet, has_kitchen, has_air_con 
    FROM Rooms 
    WHERE id = 11
);
```

http://sql-academy.org/ru/guide/correlated-subqueries

1. Получение самого дорогого купленного товара

```sql
SELECT 
    FamilyMembers.member_name,
    (
        SELECT MAX(Payments.unit_price)
        FROM Payments
        WHERE Payments.family_member = FamilyMembers.member_id
    ) AS good_price
FROM FamilyMembers;
```


https://sql-academy.org/ru/guide/combining-queries

1. Объединение учеников и учителей

Выведите полные имена (поля first_name, middle_name и last_name) всех студентов и преподавателей.

```sql
SELECT first_name, middle_name, last_name
FROM Student
UNION
SELECT first_name, middle_name, last_name
FROM Teacher;
```
Условная логика, оператор CASE

https://sql-academy.org/ru/guide/case-expression#uslovnaya-logika-operator-case

1. Категоризация отзывов

Из таблицы Reviews выведите идентификаторы отзывов (поле id) и их категорию: для рейтинга 4-5 проставьте категорию «positive», для 3 проставьте «neutral», а для 1-2 - «negative».

```sql
SELECT id, 
CASE 
  WHEN rating IN (5,4) THEN 'positive'
  WHEN rating = 3 THEN 'neutral'
  WHEN rating IN (1,2) THEN 'negative'
END AS rating
FROM Reviews;
```


https://sql-academy.org/ru/guide/if-function

Условная функция IF

1. Условный вывод строки

Из таблицы Rooms выведите идентификаторы сдаваемых жилых помещений (поле id) и наличие телевизора в помещении: если телевизор присутствует — выведите «YES», иначе «NO».

```sql
SELECT id, has_tv,
    IF (has_tv, 'YES', 'NO') AS has_tv
    FROM Rooms
```

2. Замена null на строку
Из таблицы Teacher выведите имена (поле first_name), отчества (поле middle_name) и фамилии (поле last_name) учителей. Если отчество у учителя отсутствует, выведите в поле middle_name значение «Empty».

```sql
SELECT first_name, middle_name, last_name,
    IFNULL(middle_name, 'Empty') AS middle_name
    FROM TEACHER;
```


https://sql-academy.org/ru/guide/operator-insert

Добавление данных, оператор INSERT

```sql
INSERT INTO Goods(good_id, good_name, type)

SELECT MAX(good_id) + 1, 'Table', (SELECT good_type_id FROM GoodTypes WHERE good_type_name = 'equipment')

FROM Goods;
```

https://sql-academy.org/ru/guide/operator-update

Обновление данных, оператор UPDATE

1. Обновление имени у пользователя

Измените имя у "Wednesday Addams" на новое "Tuesday Addams".

```sql
UPDATE FamilyMembers
SET member_name = "Tuesday Addams"
WHERE member_name = "Wednesday Addams";
```

2. Обновление стоимости у всего жилья

Обновите стоимость всех комнат в таблице (Rooms), добавив к текущей 10 единиц

```sql
UPDATE Rooms
SET price = price + 10;
```

https://sql-academy.org/ru/guide/operator-delete

Удаление данных, оператор DELETE

1. Удаление всех записей
Удалите все записи из таблицы Payments, используя оператор DELETE.

```sql
DELETE FROM Payments;
```

2. Удаление c условием
Удалить запись из таблицы Goods, у которой поле good_name равно "milk"
```sql
DELETE FROM Goods
WHERE good_name = 'milk';
```

3. Удаление c JOIN
Измените запрос так, чтобы удалить товары (Goods), имеющие тип деликатесов (delicacies).

```sql
DELETE Goods
FROM Goods
    INNER JOIN GoodTypes ON Goods.type = GoodTypes.good_type_id
WHERE GoodTypes.good_type_name = 'delicacies';
```
# Числовой тип данных в SQL

https://sql-academy.org/ru/guide/work-with-number-data-type

1. Округление до чисел, кратных 10-ти

```sql
SELECT ROUND(price / 10) * 10  AS rounded_price
FROM Rooms;
```

https://sql-academy.org/ru/guide/work-with-datetime-data-type

Дата и время в SQL

Извлеките значение часа (от 0 до 23) из времени '14:30:45' с помощью соответствующей функции. Используйте псевдоним hour_value для вывода значения.

```sql
SELECT HOUR('14:30:45') AS hour_value
```

2. Определение возраста
Выведите имена (поле member_name) и возраст для каждого человека из таблицы FamilyMembers.
Для вывода возраста используйте псевдоним age.

```sql
SELECT 
    member_name,
    TIMESTAMPDIFF(YEAR, birthday, NOW()) AS age
FROM 
    FamilyMembers;
```


https://sql-academy.org/ru/guide/partitions

Партиции в оконных функциях

1. Минимальная стоимость жилья в текущей категории

```sql
SELECT 
    home_type, 
    price,
    MIN(price) OVER(PARTITION BY home_type) AS min_price_by_type
FROM 
    rooms;
```