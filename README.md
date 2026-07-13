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
