# How to add `cascade delete` to an existing constraint

When I forget to add `on_delete: :delete_all` I need to recreate the constraint with a new Ecto migration.

Set the `from:` option to recreate the constraint without explicitly declaring `up` and `down`:

```elixir
def change do
  alter table(:address) do
    modify :person_id, references(:person, on_delete: :delete_all),
      from: references(:person, on_delete: :nothing)
  end
end
```


