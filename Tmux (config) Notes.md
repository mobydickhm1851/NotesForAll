# Tmux (config) Notes

## Contents
- [Tmux Cheat Sheet](#tmux-cheat-sheet)
- [Tmux Customized Config](#tmux-customized-config)
- [Tmux Plugin Manager](tmux-plugin-manager)
- [Nord Color Theme](#nord-color-theme)


## Tmux Cheat Sheet


## Tmux Customized Config

```
  # remap prefix from 'C-b' to 'C-a'
  unbind C-b
  set-option -g prefix C-a
  bind-key C-a send-prefix
  
  # reload config file (change file location to your the tmux.conf you want to use)
  bind r source-file ~/.tmux.conf
  
  # switch panes using Alt-arrow without prefix
  bind -n M-Left select-pane -L
  bind -n M-Right select-pane -R
  bind -n M-Up select-pane -U
  bind -n M-Down select-pane -D
  
  # Enable mouse control (clickable windows, panes, resizable panes)
  # (for versions before tmux 2.1)
  # set -g mouse-select-window on
  # set -g mouse-select-pane on
  # set -g mouse-resize-pane on
  
  # Enable mouse mode (tmux 2.1 and above)
  set -g mouse on
  
  # don't rename windows automatically (never happened to me, just in case)
  set-option -g allow-rename off
      
```

Sources: [pepelepew][pepe] and [Ham Vocke][hv]

[pepe]:
[hv]:https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/


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
