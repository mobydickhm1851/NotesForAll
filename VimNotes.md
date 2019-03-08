# Vim Notes
## Copy and past across terminals (__also work from vim to external programs!__)
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
## Cheat Sheets

#### Indent

```
>>   Indent line by shiftwidth spaces
<<   De-indent line by shiftwidth spaces
5>>  Indent 5 lines
5==  Re-indent 5 lines

>%   Increase indent of a braced or bracketed block (place cursor on brace first)
=%   Reindent a braced or bracketed block (cursor on brace)
<%   Decrease indent of a braced or bracketed block (cursor on brace)
]p   Paste text, aligning indentation with surroundings

=i{  Re-indent the 'inner block', i.e. the contents of the block
=a{  Re-indent 'a block', i.e. block and containing braces
=2a{ Re-indent '2 blocks', i.e. this block and containing block

>i{  Increase inner block indent
<i{  Decrease inner block indent
```

## Cstimized config (LiuYC)

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



nnoremap <F3> a<C-R>=strftime("%Y-%m-%d %I:%M:%S")<CR><Esc>
hi CursorLine   cterm=NONE ctermbg=grey ctermfg=black guibg=darkred guifg=white
set cursorline

```

Sources: [pepelepew][pepe] and [John Hawthorn][JH]

[pepe]:
[JH]:https://www.johnhawthorn.com/2012/09/vi-escape-delays/

