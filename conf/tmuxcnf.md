---
title: Tmux Conf
description: A customized tmux configuration
published: true
date: 2021-10-09T16:19:01.860Z
tags: cfg, tmux
editor: markdown
dateCreated: 2021-10-09T16:18:40.327Z
---

```plaintext
# ~/.tmux.conf
# Maintained by: Shubham Gaur
# Resources
# https://github.com/JohnMurray/dotfiles/blob/master/.tmux.conf
#
# set command prefix for tmux
set-option -g prefix C-a
unbind C-a

# set default shell to zsh
# set-option -g default-shell /usr/bin/bash
set -g default-terminal screen-256color

# 0 is too far from ` ;)
set -g base-index 1

# Automatically set window title
set-window-option -g automatic-rename on
set-option -g set-titles on

#set -g default-terminal screen-256color
set -g status-keys vi
set -g history-limit 10000

setw -g mode-keys vi
setw -g mouse on
setw -g monitor-activity on

bind-key v split-window -h
bind-key s split-window -v

bind-key J resize-pane -D 5
bind-key K resize-pane -U 5
bind-key H resize-pane -L 5
bind-key L resize-pane -R 5

bind-key M-j resize-pane -D
bind-key M-k resize-pane -U
bind-key M-h resize-pane -L
bind-key M-l resize-pane -R

# Vim style pane selection
bind h select-pane -L
bind j select-pane -D 
bind k select-pane -U
bind l select-pane -R

# Use Alt-vim keys without prefix key to switch panes
bind -n M-h select-pane -L
bind -n M-j select-pane -D 
bind -n M-k select-pane -U
bind -n M-l select-pane -R

# Use Alt-arrow keys without prefix key to switch panes
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Shift arrow to switch windows
bind -n S-Left  previous-window
bind -n S-Right next-window

# No delay for escape key press
set -sg escape-time 0

# bind a swap window key
bind W                            \
  set -g renumber-windows on\;    \
  new-window\; kill-window\;      \
  set -g renumber-windows off\;   \
  display-message "Windows reordered..."
  

# bind a reload key
bind R source-file ~/.tmux.conf \; display-message "  Config reloaded..".

# THEME
  # status bar colors
  set -g status-bg black
  set -g status-fg white

  # alignment settings
  set-option -g status-justify centre

  # status left options
  set-option -g status-left '#[fg=green][#[bg=black,fg=cyan]#S#[fg=green]]'
  set-option -g status-left-length 20

  # window list options
  setw -g automatic-rename on
  set-window-option -g window-status-format '#[fg=cyan,dim]#I#[fg=blue]:#[default]#W#[fg=grey,dim]#F'
  set-window-option -g window-status-current-format '#[bg=blue,fg=cyan,bold]#I#[bg=blue,fg=cyan]:#[fg=colour230]#W#[fg=dim]#F'
  set -g base-index 1

  # status right options
  set -g status-right '#(gitmux "#{pane_current_path}") #[fg=green][#[fg=blue]%Y-%m-%d #[fg=white]%H:%M#[default]#[fg=green]]'
```