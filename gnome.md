
We can use `gsettings` to configure via command line

For example, to use a single workspace, exec
```
gsettings set org.mate.Marco.general num-workspaces 1
```
and to verify shortcuts for default terminal application
```
gsettings list-recursively org.mate.terminal
```

# login shell

Very surprisingly, when you open a gnome terminal, the shell command executed whithin is not a login shell,
and you must [configure explicitly](https://askubuntu.com/a/40313), or your _profile_ files won't get sourced

# tmux

When using tmux, terminal tabs are a bit useless, as they are replaced by windows.
But we cannot use standard keybindings for tab change in tmux because they are captured by the terminal prior to be processed by tmux. We can explore alternative terminals or just free that combination with
```
gsettings set org.mate.terminal.keybindings prev-tab disabled
gsettings set org.mate.terminal.keybindings next-tab disabled

tmux bind-key -n C-PageUp previous-window
tmux bind-key -n C-PageDown next-window
```

