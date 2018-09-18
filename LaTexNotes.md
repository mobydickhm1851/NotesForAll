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
  
  
  




[spacing]:https://tex.stackexchange.com/questions/31672/column-and-row-padding-in-tables
