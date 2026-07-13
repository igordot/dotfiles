# dotfiles
dotfiles, system setup, etc.

## system (macOS)

### .bash_profile

```sh
# Linux terminal emulators launch non-login interactive shells (read ~/.bashrc)
# macOS Terminal.app and iTerm2 launch login shells by default (read ~/.bash_profile)
source ~/.bashrc
```

### .bashrc

```sh
# disable bash session (new macOS 10.11)
export SHELL_SESSION_HISTORY=0
# silence the warning that the default interactive shell is now zsh (macOS 10.15)
export BASH_SILENCE_DEPRECATION_WARNING=1
# append to the history file, don't overwrite it
shopt -s histappend
# history size
export HISTSIZE=99999
export HISTFILESIZE=99999
# don't save duplicate lines
export HISTCONTROL=ignoredups
# flush bash_history after every command
export PROMPT_COMMAND="history -a"
# add ll
alias ll='ls -lG'

# homebrew
eval "$(/opt/homebrew/bin/brew shellenv bash)"
export HOMEBREW_AUTO_UPDATE_SECS=3600

# rig
. "$HOME/.local/bin/rigenv"

# fnm node manager
eval "$(fnm env --use-on-cd --shell bash)"
```

### .inputrc

```sh
# History search on arrow keys (works in "application cursor key" mode)
"\e[A": history-search-backward
"\eOA": history-search-backward
"\e[B": history-search-forward
"\eOB": history-search-forward

# Single Tab completes the common prefix and lists candidates when ambiguous
set show-all-if-ambiguous on

# Case-insensitive completion
set completion-ignore-case on

# Color completion candidates by file type, like ls --color.
set colored-stats on

# Color the matched prefix portion of each candidate.
set colored-completion-prefix on

# Append a type indicator (/, *, @, etc.) to completion candidates.
set visible-stats on

# Don't ask "Display all N possibilities?" until there are this many.
set completion-query-items 100
```

## tools

### .gitconfig

```
[user]
	name = [...]
	email = [...]@users.noreply.github.com
[core]
	editor = nano
[diff]
	algorithm = histogram
[filter "lfs"]
	process = git-lfs filter-process
	required = true
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
```

### .tmux.conf

```
# set -g default-terminal "screen-256color"
# set -g mode-mouse on

# sane scrolling
set -g terminal-overrides 'xterm*:smcup@:rmcup@'

# set window notifications
setw -g monitor-activity on
set -g visual-activity on

# remap PREFIX to C-a
# set -g prefix C-a

# send C-a
# bind C-a send-prefix

# windows/panes count from 1 as God intended
set -g base-index 1
setw -g pane-base-index 1

# change default delay
# set -sg escape-time 0

# # move between panes
# bind h select-pane -L
# bind j select-pane -D
# bind k select-pane -U
# bind l select-pane -R
#
# # resize panes
# bind H resize-pane -L 5
# bind J resize-pane -D 5
# bind K resize-pane -U 5
# bind L resize-pane -R 5

# highlight active pane
set -g pane-border-fg green
set -g pane-border-bg black
set -g pane-active-border-fg white
set -g pane-active-border-bg yellow

# status bar
set -g status-fg colour248
set -g status-bg colour233

# set the color of the window list
setw -g window-status-fg cyan
setw -g window-status-bg default
setw -g window-status-attr dim
setw -g window-status-current-fg colour81
setw -g window-status-current-bg colour238

# set colors for the active window
# setw -g window-status-current-fg white
# setw -g window-status-current-bg red
# setw -g window-status-current-attr bright
#
# # Command / message line
# set -g message-fg white
# set -g message-bg black
# set -g message-attr bright

# Reload the file with Prefix r
bind r source-file ~/.tmux.conf \; display "Reloaded!"
```
