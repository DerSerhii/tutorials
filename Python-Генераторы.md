# Генератор

Генератор — это [функция](Python-Функции.md), у которой вместо `return` — `yeild`.

Это такая вещь которая умеет принимать и отдавать контроль управления.

Функция выполняется до `return`, в момент выполнения `return` - она вернула 
результат выполнения и забыла, что она выполнялась.

Функция-генератор помнит и может заново принять на себя контроль управления, работает
от `yeild` до `yeild`. 



