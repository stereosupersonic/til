# tmux Basics

## config

### ~/.tmux.conf

```
# Setting the prefix from C-b to C-a
set -g prefix C-a

# Free the original Ctrl-b prefix keybinding
unbind C-b

#setting the delay between prefix and command
set -s escape-time 1

# Ensure that we can send Ctrl-A to other apps
bind C-a send-prefix

# Set the base index for windows to 1 instead of 0
set -g base-index 1

# Set the base index for panes to 1 instead of 0
setw -g pane-base-index 1

# Reload the file with Prefix r
bind r source-file ~/.tmux.conf \; display "Reloaded!"

# splitting panes with | and -
bind | split-window -h
bind - split-window -v
```

PREFIX now is CTRL+a 

*remap your CapsLock to CTRL*

### new session

tmux new -s *my_session*

### list session

tmux ls

### attach a session

tmux attach -t*my_session*

### kill a session

with *exit* inside a session

or 

tmux kill-session -t basic

### detach

inside a session: PREFIX + d

## Windows

### new 
PREFIX + c

### renaming 
PREFIX + ,

### visualize all windows
PREFIX + w

## Panes

### split window horzontal
PREFIX + -

### split window vertivcal
PREFIX + |

### Navigate between Panes
PREFIX + o
