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
