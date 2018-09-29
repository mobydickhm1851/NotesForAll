# Vim Notes
## Copy and past across terminals
   1. first check if clipboard function is available (echo in vim)
      ```
      :echo has('clipboard')
      ```
      if it returns `1` then it means your vim has clipboard function, jump to `3.`
   2. install `vim-gtk` or `vim-gnome`
   3. you can either
      - do this
        ```
        "*y     in source Vim
        "*p     in destination Vim
        ```
      - or go to `.vimrc` and add this line
        ```
        set clipboard^=unnamed
        ```
