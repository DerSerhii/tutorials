# SOLID

`S `

Принцип единой ответственности

>Не надо заставлять дворника быть еще и охранником. Плохая идея!

`O `

Открыт для расширения - закрыт для модификации !
> Работает - не трогай ! <br>
> Если уже что-то работает и нужен новый функционал, напиши новый другой модуль! <br>
> Старый не трогай ! Можно сломать !

`L`

Принцип подстановки Барбары Лисков
> Потомка можно заменить на родителя и все будет ОК!

`I`

Принцип разделения интерфейсов

> Не надо изобретать волшебную кнопку! 

> Руль - для поворота колес<br>
> Коробка передач - для выбора передач<br>
> Переключение передач при помощи руля - плохая идея!

> Кофемашина:<br>
> Кнопка "латте", кнопка "еспрессо"<br>
> общая кнопка - одно нажатие "латте", два - "еспрессо" - плохая идея! 

`D `

Привязываем классы к абстракциям, а не абстракции к классам 
> Есть класс - "машина"<br>
> В нем есть аттрибут "цвет"<br>
> При создании мы знаем, что есть цвет у машины, но еще не знаем какой<br>
> Это детали<br>
> Реализуем детали потом, когда будут нужны
