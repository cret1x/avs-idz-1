# ИДЗ №1 Вариант 29
## Амирханов Никита Русланович БПИ219

### Условия
Сформировать массив B из произведения соседних элементов A по
следующему правилу: B0=A0 * Am, B1=A1 * Am, ..., где m – либо номер первого
четного отрицательного элемента массива А, либо номер последнего
элемента, если в массиве А нет отрицательных элементов.

### Задание решено на 10 баллов.
 - Есть исходный код на си, скомпилированный с разными опциями, шаги рефакторинга ассемблероного кода пропущены т.к. писалась программа на ассемблере с нуля.
 - Есть сравнительные тесты показывающие скорость работы обоих программ.
 - Есть генератор случайных чисел с указанием границ
 - Есть ввод-вывод из файла
 - Есть измерение времени работы программы

### Структура папок
 - `/asm` содержит исходный код на ассембеле без использования си функций
 - `/asm/lib` содержит файлы с дополнительными функциями
 - - `array.s` - работа с массивами
 - - `io.s` - ввод/вывод из консоли/файлов
 - - `str.s` - работа со строками
 - - `time.s` - замер времени
 - - `rand.s` - генерация случайных чисел
 - `/asm/main.s` - главный файл программы
 - `/c-stuff` содержит исходный код на языке си
 - `/tests` папка с тестами
 - Файл `make-tests.py` позволяет создавать тесты необходимой длины

### Запуск ассемблерного кода
```sh
make compile    ; компилирует все дополнительные библиотеки
make build      ; компилирует основой код с добавлением библиотек
```
Далее, чтобы запустить ручной ввод/вывод необходимо выполнить просто `./main`. Для ввода и вывода в файл необходимо укзаать два аргумента `./main <input_file> <output_file>`. Для работы с генератором случайных чисел необходимо набрать `./main -r <count> <lower_bound> <upper_bound> <output_file>`. В таком случае на экран будет выведен сгенерированный массив.
Во всех случаях ограничение на длину массива 100000000 элементов. При вводе большего числа будет выведено сообщение. Ограничения на сами элементы нет. Но если будут введены числа по модулю большие чем `long` то не гарантируется верный ответ.

### Запуск си кода
```sh
gcc main.c -o main
```
В си программе отсутствует ручной ввод вывод. Для ввода и вывода необходимо укзаать два аргумента `./main <input_file> <output_file>`. Для работы с генератором случайных чисел необходимо набрать `./main -r <count> <lower_bound> <upper_bound> <output_file>`.

### Важно
Файлы которые подаются в вход программе **должны** содержать перенос строки в конце. Пример:
```
5
1
2
3
4
5

```

### Тестирование
 - Обычный тест
 ```
 5
 1
 2
 3
 4
 5

 ```
 Результат
 ```
5
10
15
20
25

```

### Сравнение прогамм на си и asm
1. Размер исполняемого файла
Размер ассемблероного файла сгенерированного из си кода при помощи флагов `-masm=intel -fno-asynchronous-unwind-tables -fno-jump-tables -fno-stack-protector -fno-exceptions -Os` составляет всего 243 строки. В то же время размер самописной программы на ассемблере составляет 413 строк в main файле + 530 строк в вспомогательных файлах. Однако размер исполняемого файла на ассемблере составляет 7,1K а у программы на си 13K.
2. Время работы программ
 - На тесте в 100000 элементов:
 ```
asm                         c:          c -Ofast asm     
----------------------------------------------------
Read:          0.78601389   | 0.004616  | 0.004694
Calculations:  0.263031     | 0.000126  | 0.000140
Write:         0.287058676  | 0.004586  | 0.004624
 ```
  - На тесте в 1000000 элементов:
 ```
asm:                        c:          c -Ofast asm
 ---------------------------------------------------
Read:          0.727040354  | 0.044912  | 0.046473
Calculations:  0.2503454    | 0.001279  | 0.001220
Write:         2.433563873  | 0.044850  | 0.044344
 ```
  - На тесте в 10000000 элементов:
 ```
asm:                        c:          c -Ofast asm
----------------------------------------------------
Read:          7.362924217  | 0.508615  | 0.447636
Calculations:  0.22556240   | 0.053719  | 0.010598
Write:         25.433004001 | 0.516155  | 0.452513
 ```
  - На тесте в 100000000 элементов:
 ```
asm:                        c:          c -Ofast asm
 ---------------------------------------------------
Read:          72.466802783 | 5.043507  | 4.470650
Calculations:  0.957936372  | 0.553682  | 0.136249
Write:         256.506313724| 5.078061  | 4.506198
 ```
 3. Обработка некорректных данных
  - Количество элементов больше 100000000
  - - Обе программы выводят сообщение об ошибке `Length is greater than 100000000!`
  - Вводимые элементы не помещаются в `long`
  - - В обоих случаях `undefined behavior`
  - Указанного файла не существует
  - - Программа на си выводит сообщение с ошибкой, программа на ассемблере выведет сообщение об ошибке и укажет код ошибки `Error while opening a file: 2`. В данном случае 2 означает `No such file or directory`.



### Вывод
Компилятор gcc осказался умнее меня. Скорость работы программы на чистом ассемблере оказалась больше чем на си в 4 раза. При этом время на операции ввода и вывода в 50 раз больше. Размер исполняемого файла на ассемблере оказлся меньше чем на си. При этом, написание когда на ассемблее во много раз дольше.