

# Creation de deux sessions tmux

```
tmux new -AD -s left
tmux new -AD -s right
```

Sur le layout de la session kitty
```
set-option -g allow-passthrough on
```

# Switch une fenetre d'une session

```
tmux select-window  -t left:1
```

# link d'une fenetre entre deux sessions

```
tmux link-window -s left:2 -t right
```
