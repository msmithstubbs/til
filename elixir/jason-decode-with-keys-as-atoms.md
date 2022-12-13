# Jason.deocde/2 with keys as as atoms

The [Jason](https://hexdocs.pm/jason/readme.html) library provides a `decode/2` for parsing JSON strings. It includes some useful options such as `keys: :atoms` to return a map with keys as atoms rather than strings.

```elixir
iex> Jason.decode("{\"name\": \"Alice\"}")
{:ok, %{"name" => "Alice"}}

iex> Jason.decode("{\"name\": \"Alice\"}", keys: :atoms)
{:ok, %{name: "Alice"}}
```
