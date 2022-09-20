# Дата и Время

## Форматирование дат и времени

Для форматирования объектов `date` и `time` в обоих этих классах предусмотрен 
метод `strftime(format)`. Этот метод принимает только один параметр, указывающий на 
формат, в который нужно преобразовать дату или время.

Для определения формата мы можем использовать один из следующих кодов форматирования:<br>
`%a` — аббревиатура дня недели. Например, Wed - от слова Wednesday (по умолчанию используются английские наименования)<br>
`%A` — день недели полностью, например, Wednesday<br>
`%b` — аббревиатура названия месяца. Например, Oct (сокращение от October)<br>
`%B` — название месяца полностью, например, October<br>
`%d` — день месяца, дополненный нулем, например, 01<br>
`%m` — номер месяца, дополненный нулем, например, 05<br>
`%y` — год в виде 2-х чисел<br>
`%Y` — год в виде 4-х чисел<br>
`%H` — час в 24-х часовом формате, например, 13<br>
`%I` — час в 12-ти часовом формате, например, 01<br>
`%M` — минута <br>
`%S` — секунда <br>
`%f` — микросекунда <br>
`%p` — указатель AM/PM <br>
`%c` — дата и время, отформатированные под текущую локаль <br>
`%x` — дата, отформатированная под текущую локаль <br>
`%X` — время, форматированное под текущую локаль <br>

Используем различные форматы:
```python
from datetime import datetime
now = datetime.now()
print(now.strftime("%Y-%m-%d"))             # 2017-05-03
print(now.strftime("%d/%m/%Y"))             # 03/05/2017
print(now.strftime("%d/%m/%y"))             # 03/05/17
print(now.strftime("%d %B %Y (%A)"))        # 03 May 2017 (Wednesday)
print(now.strftime("%d/%m/%y %I:%M"))       # 03/05/17 01:36
```

При выводе названий месяцев и дней недели по умолчанию используются английские 
наименования. Если мы хотим использовать текущую локаль, но то мы можем ее 
предварительно установить с помощью модуля `locale`:
```python
from datetime import datetime
import locale
locale.setlocale(locale.LC_ALL, "")
 
now = datetime.now()
print(now.strftime("%d %B %Y (%A)"))        # 03 Май 2017 (среда)
```

## Сложение и вычитание дат и времени

Нередко при работе с датами возникает необходимость добавить к какой-либо дате 
определенный промежуток времени или, наоборот, вычесть некоторый период. 
И специально для таких операций в модуле `datetime` определен класс `timedelta`. 
Фактически этот класс определяет некоторый период времени.

Для определения промежутка времени можно использовать конструктор `timedelta`:
```python
timedelta([days] [, seconds] [, microseconds] [, milliseconds] [, minutes] [, hours] [, weeks])
```
В конструктор мы последовательно передаем дни, секунды, микросекунды, миллисекунды, минуты, часы и недели.

Определим несколько периодов:
```python
from datetime import timedelta
 
three_hours = timedelta(hours=3)
print(three_hours)       # 3:00:00
three_hours_thirty_minutes = timedelta(hours=3, minutes=30)  # 3:30:00
 
two_days = timedelta(2)  # 2 days, 0:00:00
 
two_days_three_hours_thirty_minutes = timedelta(days=2, hours=3, minutes=30)  # 2 days, 3:30:00
```

Используя `timedelta`, мы можем складывать или вычитать даты. 
Например, получим дату, которая будет через два дня:
```python
from datetime import timedelta, datetime
 
now = datetime.now()
print(now)                      # 2017-05-03 17:46:44.558754
two_days = timedelta(2)
in_two_days = now + two_days
print(in_two_days)              # 2017-05-05 17:46:44.558754
```
Или узнаем, сколько было времени 10 часов 15 минут назад, 
то есть фактически нам надо вычесть из текущего времени 10 часов и 15 минут:
```python
from datetime import timedelta, datetime
 
now = datetime.now()
till_ten_hours_fifteen_minutes = now - timedelta(hours=10, minutes=15)
print(till_ten_hours_fifteen_minutes) 
```

## Свойства timedelta

Класс `timedelta` имеет несколько свойств, с помощью которых мы можем получить 
временной промежуток:
- `days`: возвращает количество дней <br>
- `seconds`: возвращает количество секунд <br>
- `microseconds`: возвращает количество микросекунд

Кроме того, метод `total_seconds()` возвращает общее количество секунд, куда входят 
и дни, и собственно секунды, и микросекунды.

Например, узнаем какой временной период между двумя датами:
```python
from datetime import timedelta, datetime
 
now = datetime.now()
twenty_two_may = datetime(2017, 5, 22)
period = twenty_two_may - now
print("{} дней  {} секунд   {} микросекунд".format(period.days, period.seconds, period.microseconds))
# 18 дней  17537 секунд   72765 микросекунд
 
print("Всего: {} секунд".format(period.total_seconds()))
# Всего: 1572737.072765 секунд
```

## Сравнение дат
Также как и строки и числа, даты можно сравнивать с помощью стандартных операторов 
сравнения:
```python
from datetime import datetime
 
now = datetime.now()
deadline = datetime(2017, 5, 22)
if now > deadline:
    print("Срок сдачи проекта прошел")
elif now.day == deadline.day and now.month == deadline.month and now.year == deadline.year:
    print("Срок сдачи проекта сегодня")
else:
    period = deadline - now
    print("Осталось {} дней".format(period.days))
```

## Свойства replace
```python
    def check_period_refund(self):
        current_time = timezone.now()
        time_purchase = self.purchase.time_purchase
        refund_end_time = time_purchase.replace(minute=time_purchase.minute + self.refund_period)
        check = current_time < refund_end_time
        return check
```

---
Часовые пояса в [Django](../Django/Django-Часовые%20пояса.md)