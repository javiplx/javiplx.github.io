
Main reason to choose tmux is the ability to [resurrect after crash or restarts](https://github.com/tmux-plugins/tmux-resurrect/blob/master/README.md).
But the shell history resurrection didn't work as smooth as expected

We opted to use a customized history file based on the pane ID, which is an environment variable hosting the unique identifier across the tmux session,
and we also flush at every prompt
```
HISTFILE=${HISTFILE}${TMUX_PANE:+.${TMUX_PANE#%}}
[ x$TMUX_PANE != x ] && PROMPT_COMMAND="${PROMPT_COMMAND:+$PROMPT_COMMAND$'\n'}history -a"
```
This is apparently enough and worked well for some time, but there are two drawbacks
* the first pane (with zero ID) is not handled well, although that is hard to notice while performing initial trial & error setup
* you cannot delete panes, because the IDs will get rearranted on the next resurrection mismatching pane content & history
and both items can be fixed [by patching resurrect](https://github.com/tmux-plugins/tmux-resurrect/pull/318)

