
Ручная реализация протоколов для всех типов может быстро стать повторяющейся и утомительной. В таких случаях Elixir предоставляет два варианта: можно явно вывести (derive) реализацию протокола для наших типов или автоматически реализовать протокол для всех типов. В обоих случаях необходимо реализовать протокол для `Any`.

Опишем явное выведение (derive) протокола из примера `Typer` прошлого модуля:

```elixir
defprotocol Typer do
  @spec type(t) :: String.t()
  def type(value)
end

defimpl Typer, for: Any do
  def type(_value), do: "something"
end
```

Конечно, реализация получилось странной, потому что для любого типа будет возвращаться `something`, однако это учебный пример. Теперь опишем пользователя и явно *выведем* для него протокол:

```elixir
defmodule SomeUser do
  @derive [Typer]
  defstruct [:name, :age]
end

Typer.type(%SomeUser{})
# => "something"
```

В другом случае, в протоколе указывается опция `fallback_to_any` и если не будет найден нужный протокол под тип, то будет использована реализация протокола для `Any`:

```elixir
defprotocol Typer do
  @fallback_to_any true

  def type(value)
end

defimpl Typer, for: Any do
  def type(_value), do: "something new"
end

defmodule AnotherUser do
  defstruct [:name]
end

Typer.type(%AnotherUser{})
# => "something new"
```

Как было сказано выше, не всегда реализация протокола для `Any` необходима, так как может не иметь смысла для некоторых типов данных. Например, протокол `Size` имеет смысл для перечислимых типов данных, но не для чисел. Поэтому зачастую выброс ошибки при отсутствии необходимой реализации протокола является ожидаемым поведением.

Какой выбрать из вариантов между явным выведением (derive) или опцией `fallback_to_any` зависит от ситуации. Тем не менее явное лучше, чем неявное, поэтому зачастую в Elixir библиотеках используется подход с `derive`.