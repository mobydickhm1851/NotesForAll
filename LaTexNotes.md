# LaTex Notes
## Configuration of making a table
### Spacing horizontally and vertically
  Use a default `tabular` environment without package `booktabs` and add right before and after the environment:
    
    
     \bgroup
     \def\arraystretch{1.5}%  1 is the default, change whatever you need
     \begin{tabular}{|c|...}
     ...
     \end{tabular}
     \egroup
    
    
and also use column type `c` instead of `l`, If you want more horizontal space between the columns then use `\setlength\tabcolsep{<whatever length>}`
    
ref:[Column and row padding in tables][spacing]

## Centering issue
### Tables not centering
   Sometimes if the table is too wide `\centering` or `\begin{center}` won't work, so we have to move table to the left manually.
   ```
   \hspace*{-2cm}
   ```
  See this [answer][center] for more solution (like `\makebox`)

### Caption not centering 
   Use caption package
    ```
    \usepackage{caption} 
    ```
   And set desiered arrangements, for examples:
   ```
   \captionsetup{justification=centering}
    or
   \captionsetup{justification=centering,margin=2cm}
   ```
   [Answers is here][1]

[spacing]:https://tex.stackexchange.com/questions/31672/column-and-row-padding-in-tables
[center]:https://tex.stackexchange.com/questions/4926/table-will-not-center-and-it-is-spilling-off-the-right-side-of-the-page
[1]:https://tex.stackexchange.com/questions/95207/how-to-center-a-specific-caption
