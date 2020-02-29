# Setup Files In Linux

## .bashrc

```
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

#cd ~/moby_ws/moby_stage/src/

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
	# We have color support; assume it's compliant with Ecma-48
	# (ISO/IEC-6429). (Lack of such support is extremely rare, and such
	# a case would tend to support setf rather than setaf.)
	color_prompt=yes
    else
	color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi
POWERLINE_SCRIPT=/usr/share/powerline/bindings/bash/powerline.sh
if [ -f $POWERLINE_SCRIPT ]; then
  source $POWERLINE_SCRIPT
fi

# Gazebo environment setting
export GAZEBO_MODEL_PATH=/home/liuyc/moby_ws/SOLAMR/src/amr_gazebo/models:$GAZEBO_MODEL_PATH
#export GAZEBO_RESOURCE_PATH=/home/liuyc/moby_ws/SOLAMR/src/amr_gazebo

# ROS environment parameters settings
source /opt/ros/kinetic/setup.bash
#source /home/liuyc/moby_ws/solabot/devel/setup.bash
#source /home/liuyc/moby_ws/solabot_simulator/devel/setup.bash
#source /home/liuyc/moby_ws/obstacle_detector/devel/setup.bash
#source /home/liuyc/moby_ws/moby_simulator/devel/setup.bash
#source /home/liuyc/moby_ws/play_ground/devel/setup.bash
#source /home/liuyc/moby_ws/moby_stage/devel/setup.bash
#source /home/liuyc/moby_ws/intersection_simulator/devel/setup.bash
#source /home/liuyc/moby_ws/turtlebot3/devel/setup.bash
#source /home/liuyc/moby_ws/SOLAMR/devel/setup.bash
source /home/liuyc/moby_ws/zed_ros_wrapper/devel/setup.bash

# add ros-package from source


# ROS local machine setting
export ROS_MASTER_URI=http://localhost:11311
#export ROS_MASTER_URI=http://`hostname -I`:11311
#export ROS_IP=`hostname -I`
# for turtlebot3
#export TURTLEBOT3_MODEL=burger
#export TURTLEBOT3_MODEL=waffle
#export TURTLEBOT3_MODEL=waffle_pi

# Multi-machine setting for solabot and solabot2 
# solabot setting
#export ROS_MASTER_URI=http://192.168.50.203:11311
# solabot2 setting
#export ROS_MASTER_URI=http://192.168.50.229:11311

# rpi4 setting
# LOCAL network
#export ROS_MASTER_URI=http://192.168.1.112:11311
# Global network
#export ROS_MASTER_URI=http://140.112.14.200:11311


# CUDA
export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}$ 
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

## .vimrc

```
set laststatus=2
set t_Co=256
python3 from powerline.vim import setup as powerline_setup
python3 powerline_setup()
python3 del powerline_setup
set clipboard^=unnamed


filetype plugin indent on
" show existing tab with 4 spaces width
set tabstop=4
" when indenting with '>', use 4 spaces width
set shiftwidth=4
" On pressing tab, insert 4 spaces
set expandtab

"set background=dark
colorscheme Tomorrow-Night-Eighties
set mouse=a
set showmatch " show the matching part of the pair for [] {} and ()
set autochdir " set working directory same with current editing file
set history=1024
set nu 

set timeoutlen=1000
set ttimeoutlen=000

set pastetoggle=<C-p>


nnoremap <F3> a<C-R>=strftime("%Y-%m-%d %I:%M:%S")<CR><Esc>
hi CursorLine   cterm=NONE ctermbg=grey ctermfg=black guibg=darkred guifg=white
set cursorline

```

## .tmux.conf

```
# 2019-02-22 08:55:41


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

