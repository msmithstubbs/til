# Set and clear colours in a zsh prompt


zsh uses escape codes to set foreground and background colours for the prompt.

```sh
SET PS1="%F{red}>%f"
```

`%F{red}` is used to set the foreground colour to red. `%f` then resets it. `%K{}` is used for background colours (`%k` to reset).
