# Use Oban.Testing.perform_job/3 to test jobs

When writing a test for an Oban job I found myself writing a lot of boilerplate code: new job, specify args, insert into the db.

[perform_job/3](https://hexdocs.pm/oban/Oban.Testing.html#perform_job/3) creates a job and executes it:

```elixir
defmodule MyApp.ObanJobTest do
  use MyApp.DataCase, async: true
  use Oban.Testing, repo: MyApp.Repo

  test "it works" do
    assert :ok = Oban.Testing.perform_job(ObanJob, args)
  end
end
```

Particularly useful when running Oban in `testing: :manual` mode and you want to actually validate the side effects of a job.

`perform_job` also asserts the worker implements `Oban.Worker` and returns a valid response.
