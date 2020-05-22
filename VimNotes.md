# Vim Notes
## Function Settings
### Paste code without auto-indent
When pasting a page of codes into vim, auto-indent would be added and becoming a mess:
```
code line1
   code line2
      code line3
         ...
```
To solve this, we have to initiate insert-paste mode:
1. Do this one-time in vim:
   - type `:set paste` to enter the insert-paste mode
   - press `p` to paste the code you just copied
   - type `:set nopaste` to exit the insert-paste mode
   
2. add this line into `.vimrc` permanently, and use shortcut `Ctrl + p`
   ```
   " Set Ctrl + p as shortcut into insert-paste mode
   set pastetoggle = <C-p>
   ```
   
### Copy and past across terminals (__also work from vim to external programs!__)
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
#### Delete till some word
```
d/<string-to-delete>
# add \ if / is included in the <string-to-delete>
```
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

" Set Ctrl + p as shortcut into insert-paste mode
set pastetoggle = <C-p>

" comment shortcut for python, # for comment, -# for un-comment
vnoremap <silent> # :s/^/#/<cr>:noh<cr>
vnoremap <silent> -# :s/^#//<cr>:noh<cr>

```

Sources: [pepelepew][pepe] and [John Hawthorn][JH] 
(color theme : [Tomorrow-Night-Eighties][Tomorrow], put this file in ~/.vim/colors)

[pepe]:https://github.com/pepelepew71
[JH]:https://www.johnhawthorn.com/2012/09/vi-escape-delays/
[Tomorrow]:https://github.com/chriskempson/vim-tomorrow-theme/blob/master/colors/Tomorrow-Night-Eighties.vim
