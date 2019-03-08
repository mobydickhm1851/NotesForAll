# Tmux (config) Notes

## Contents
- [Tmux Cheat Sheet](#tmux-cheat-sheet)
- [Tmux Customized Config](#tmux-customized-config)
- [Tmux Plugin Manager](tmux-plugin-manager)
- [Nord Color Theme](#nord-color-theme)


## Tmux Cheat Sheet


## Tmux Plugin Manager

#### Installation

Clone TPM :
    git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

Put this at the bottom of `~/.tmux.conf`:

```
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run -b '~/.tmux/plugins/tpm/tpm'
```

Reload TMUX environment so TPM is sourced:
```
# type this in terminal if tmux is already running
$ tmux source ~/.tmux.conf
```

Source: [Tmux Plugin Manager][TPM]

[TPM]: https://github.com/tmux-plugins/tpm


## Nord Color Theme

#### Nord GNOME Terminal
Nord GNOME Terminal is needed for Nord Tmux.
##### Installation
- Run the `nord.sh` shell script to install. (git clone the repo)
##### Activation
- Activate it by go to Terminal --> Preferences --> Profiles then select `Nord`. (also select `Nord` in `Profile used when launching a new terminal:`)

#### Nord Tmux
##### Installation
First the `Tmux Plugin Manager` and `Nord GNOME Terminal` are needed
Add Nord tmux to your ~/.tmux.conf:

    set -g @plugin 'arcticicestudio/nord-tmux'

and press the default key binding `prefix` + `I` to fetch and install the plugin.

#### Tmux Prefix Hightlight
Add plugin to the list of TPM plugins:

    set -g @plugin 'tmux-plugins/tmux-prefix-highlight'


Source: [Nord GNOME Terminal][gnome], [Nord Tmux][tmux] and [Tmux Prefix Hightlight][ph].

[gnome]:https://github.com/arcticicestudio/nord-gnome-terminal
[tmux]:https://github.com/arcticicestudio/nord-tmux
[ph]:https://github.com/tmux-plugins/tmux-prefix-highlight




## Tmux Customized Config

```
# bind new prefix
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix


# reload config file (change file location to your the tmux.conf you want to use)
bind r source-file ~/.tmux.conf


# open pane or window at the same path
bind '"' split-window -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
bind c new-window -c "#{pane_current_path}"


# Rule out that tmux might be waiting for escape characters
set -sg escape-time 0


# don't rename windows automatically (never happened to me, just in case)
set-option -g allow-rename off


# navigation between panes by alt+hjkl
#bind -n M-h select-pane -L
#bind -n M-j select-pane -D
#bind -n M-k select-pane -U
#bind -n M-l select-pane -R

bind -n M-Left select-pane -L
bind -n M-Down select-pane -D
bind -n M-Up select-pane -U
bind -n M-Right select-pane -R


# display
set -g default-terminal "screen-256color" # colors!
set -g display-panes-time 2000 # longer pane indicators display time
set -g display-time 1000 # longer status messages display time
set -g base-index 1           # start windows numbering at 1
setw -g pane-base-index 1 # make pane numbering consistent with windows
setw -g automatic-rename on   # rename window to reflect current program
set -g renumber-windows on    # renumber windows when a window is closed
set -g set-titles on # set terminal title
set -g status-interval 10 # redraw status line every 10 seconds


## statusbar
set -g status-position bottom
set -g status-justify left
set -g status-left ' '
set -g status-right '#[fg=colour233,bg=colour3,bold] %d/%m #[fg=colour233,bg=colour8,bold] %H:%M:%S '


# mouse
#set-environment -g CHERE_INVOKING 1
set -g mouse on # mouse-resize-pane/select-pane/select-window


## Copy mode
setw -g mode-keys vi 
#unbind -T copy-mode-vi Enter # binding of `Enter` to also use copy-pipe
#bind-key -T copy-mode-vi Enter send-keys -X copy-pipe-and-cancel "xclip -selection c"
#bind-key -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel "xclip -in -selection clipboard"


#############
#### tpm ####
############# 

# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'arcticicestudio/nord-tmux'
set -g @plugin 'tmux-plugins/tmux-prefix-highlight'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com/user/plugin'
# set -g @plugin 'git@bitbucket.com/user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run -b '~/.tmux/plugins/tpm/tpm'
      
```

Sources: [pepelepew][pepe] and [Ham Vocke][hv]

[pepe]:
[hv]:https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/


