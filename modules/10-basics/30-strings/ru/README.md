
В эликсир есть два вида строк. Строки в одинарных кавычках представляют собой последовательность Unicode символов, где каждый символ представлен 32-х разрядным числом. То есть, он занимает 4 байта. Такие строки используются нечасто.

Гораздо чаще используются строки в двойных кавычках, которые представляют собой бинарные данные в формате UTF-8. В этом формате символы латинского алфавита занимают 1 байт, символы кириллицы занимают 2 байта, а символы других алфавитов занимают от 1 до 4-х байт. То есть, такая строка занимает значительно меньше памяти.

Для склеивания двух строк применяется оператор `<>`:

```elixir
"Hello" <> " " <> "World!"  # "Hello World!"
```

Модуль `String` из стандартной библиотеки содержит функции для работы со строками. Например, функцию для определения длины строки `String.length(my_str)`, функцию для разбиения строки на части `String.split(my_str, separator)` функцию для удаления пробельных символов `String.trim(my_str)` и еще несколько десятков функций.

Одна из операций над строками, которая на первый взгляд кажется простой, это перевод строки в верхний или нижний регистр. На самом деле для некоторых алфавитов эта операция должна учитывать контекст, а не просто один символ. А для некоторых других алфавитов она не имеет смысла.

Функция `String.upcase(str, mode)` работает в трех разных режимах. В режиме `:default` она переводит в верхний регистр все символы, для которых это возможно. В режиме `:ascii` она переводит только символы латинского алфавита:

```elixir
String.upcase("hello мир!", :default) # "HELLO МИР!"
String.upcase("hello мир!", :ascii) # "HELLO мир!"
```

Третий режим -- `:greek` используется для греческого алфавита, где, как раз, эта операция зависит от контекста.