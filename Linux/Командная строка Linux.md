# Командная строка Linux

## Команды поиска и сортировки  
- `find` — поиск файла

`find /home - name "*.sql"` - поиск в директории /home по имени все с расширением sql <br>
`find /home - name "ci*.sql"` - поиск в директории /home по имени все, что начинается на ci с расширением sql <br>

- `wc` — word count (количество строк, слов, байт)

Пример:<br>
`wc linux.txt` <br>
Результат: `47 1047 7001 linux.txt` - количество: 47-строк, 1047-слов, 7001-символов

`wc -l linux.txt` - только строк <br>
`wc -w linux.txt` - только слов <br>
 
- `sort` — выводит отсортированный текст из файла

Пример:<br>
сортировка по символам (алфавиту):
```
serhii@DerSerhiiUbuntu:~$ cat names.txt
Serhii
Vlad
Alex

serhii@DerSerhiiUbuntu:~$ sort names.txt
Alex
Serhii
Vlad
```
сортировка по номерам:
```
serhii@DerSerhiiUbuntu:~$ cat numbers.txt
99
1
125

serhii@DerSerhiiUbuntu:~$ sort numbers.txt
1
125
99

serhii@DerSerhiiUbuntu:~$ sort -n numbers.txt
1
99
125
```

- `cut` — вывести определенное поле из текста

Синтаксис:<br>
`cut -d ">" -f 3 filesdata.txt`<br>
`-d` - разделитель ">" <br>
`-f` - поле(столбец) 3 <br>
`filesdata.txt` - файл

Можно добавить (pipe) | <br>
`cut -d ">" -f 3 filesdata.txt | sort` - дополнительно отсортирует <br>