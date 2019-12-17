
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

When using tmux, terminal tabs are a bit useless, as they are replaced by tmux windows. But using the standard
keybindings whithin tmux (tab change for example) is not possible as they are captured by the terminal. Although
we can explore alternative terminals, we can just modify some configuration
```
gsettings set org.mate.terminal.keybindings prev-tab disabled
gsettings set org.mate.terminal.keybindings next-tab disabled
gsettings set org.mate.terminal.keybindings new-tab disabled

tmux bind-key -n C-PageUp previous-window
tmux bind-key -n C-PageDown next-window
tmux bind-key -n C-S-PageUp swap-window -t -1
tmux bind-key -n C-S-PageDown swap-window -t +1
tmux bind -n C-T new-window
```

