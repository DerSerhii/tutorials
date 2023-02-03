# Closure - Замыкание

***Сlosure (Замыкание)*** — [функция](Python-Функции.md) первого класса, в теле
которой присутствуют [переменные](Python-Переменные&Типы%20данных.md), 
объявленные вне тела этой функции и не являющиеся её параметрами. <br>
Говоря другим языком, <br>
***Замыкание*** — функция, которая ссылается на *свободные* переменные в своей 
области видимости.
```python
def average_numbers_im():
    summa = 0
    count = 0

    def inner(number):
        nonlocal summa
        nonlocal count
        summa += number
        count += 1
        return summa / count

    return inner
```

---
Замыкание на YouTube: [Egoroff1](https://www.youtube.com/watch?v=lA979PBb0TY),
[Egoroff2](https://www.youtube.com/watch?v=vrkLShOYwI0)