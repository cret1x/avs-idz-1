# ИДЗ №1
## Амирханов Никита БПИ219

### Структура папок
 - `/asm` содержит исходный код на ассембеле без использования си функций
 - `/asm/lib` содержит файлы с дополнительными функциями
 -- `array.s` - работа с массивами
 -- `io.s` - ввод/вывод из консоли/файлов
 -- `str.s` - работа со строками
 -- `time.s` - замер времени
 - `/asm/main.s` - главный файл программы
 - `/c-stuff` содержит исходный код на языке си
 - `/tests` папка с тестами
 - Файл `make-tests.py` позволяет создавать тесты необходимой длины

### Запуск ассемблерного кода
```sh
make compile
make build
make run или ./main <input_file> <output_file>
```
Если запускать программу без параметров то будет ручной ввод/вывод - иначе ввод из `<input_file>` и вывод в `<output_file>`

### Сравнение прогамм на си и asm
1. Размер исполняемого файла
размер `asm` файла `TODO` против `TODO` у си-файла
2. Время работы программ
 - На тесте в 100000 элементов:
 ```
 asm:										c:
 Read: 										
 Calculations:
 Write:
 ```
  - На тесте в 1000000 элементов:
 ```
 asm:										c:
 Read: 
 Calculations:
 Write:
 ```
  - На тесте в 10000000 элементов:
 ```
 asm:										c:
 Read: 
 Calculations:
 Write:
 ```
  - На тесте в 100000000 элементов:
 ```
 asm:										c:
 Read: 
 Calculations:
 Write:
 ```