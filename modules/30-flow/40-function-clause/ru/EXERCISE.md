
Поиграем в "крестики-нолики". Игровая доска размером 3х3 ячеек представлена кортежем из 3-х кортежей:

```elixir
{
  {:x, :o, :f},
  {:f, :o, :f},
  {:f, :f, :f}
}
```

Каждая ячейка может находиться в одном из 3-х состояний:
- `:x` в ячейке стоит крестик;
- `:o` в ячейке стоит нолик;
- `:f` ячейка свободна.

Реализовать функцию `valid_game?(state)`, которая получает на вход состояние игры, и проверяет, является ли это состояние валидным. То есть, имеет ли состояние правильную структуру, и заполнены ли ячейки только валидными значениями. Функция возвращает булевое значение.

Реализовать функцию `check_who_win(state)`, которая получает состояние и возвращает победителя, если он есть. Функция должна определить наличие трех крестиков или трех ноликов по горизонтали, или по вертикали, или по диагонали. В случае победы крестиков функция возвращает `{:win, :x}`, в случае победы ноликов функция возвращает `{:win, :o}`, если победы нет, функция возвращает `:no_win`.

```elixir
Solution.valid_game?({{:x, :x, :x}, {:x, :x, :x}, {:x, :x, :x}})
# => true
Solution.valid_game?({{:f, :f, :f}, {:f, :f, :f}, {:f, :f, :f}})
# => true

Solution.valid_game?({{:x, :o, :some}, {:f, :x, :o}, {:o, :o, :x}})
# => false
Solution.valid_game?({{:x, :o, :f}, {:f, :x, :x, :o}, {:o, :o, :x}})
# => false

Solution.check_who_win({{:x, :x, :x}, {:f, :f, :o}, {:f, :f, :o}})
# => {:win, :x}
Solution.check_who_win({{:o, :x, :f}, {:o, :f, :x}, {:o, :f, :f}})
# => {:win, :o}
Solution.check_who_win({{:x, :f, :f}, {:f, :x, :x}, {:f, :f, :o}})
# => :no_win
```