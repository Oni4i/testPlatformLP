# testPlatformLP

### Социальная сеть

Допустим, мы разрабатываем социальную сеть для студентов. У нас есть 2 таблицы в базе данных.
Students (ID, name, grade) - студенты (ID, имя, средний балл)
Likes (like_ID, liked_ID) - лайки одного студента страницы другого. like_ID - это ID того, кто поставил лак. liked_ID - ID того, кого "лайкнули".
Нужно выполнить несколько задач.
Получить имена и средний балл всех студентов, которые были "лайкнуты" более чем одним студентом.
Получить имена и средний балл студентов А, которые лайкнули студентов В, но при этом студенты В не поставили лайк ни на одной из страниц других студентов.
Вернуть имена и средний балл всех студентов, которые не лайкали чужие страницы и не были лайкнуты другими пользователями.
Реализуйте все три пункта с помощью PHP и SQL запросов.

```
SELECT s.name, s.grade
FROM Students s
INNER JOIN Likes l on l.like_ID = s.id
GROUP BY s.name, s.grade
HAVING count(l.like_id) > 1
```
```
SELECT s.name, s.grade
FROM Students s
INNER JOIN Likes l on l.like_ID = s.id
WHERE l.liked_id not in (select like_id from Likes)
GROUP BY s.name, s.grade;
```
```
SELECT s.name, s.grade
FROM students s
WHERE s.id NOT IN(SELECT liked_ID FROM Likes GROUP BY liked_ID)
AND s.id NOT IN(SELECT like_ID FROM Likes GROUP BY like_ID)
```
