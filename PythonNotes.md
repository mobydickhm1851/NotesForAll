# Python Notes

## Contents
- [Useful Packages](#useful-packages)
- [Questions and Exercises](#questions-and-exercises)

   
## Useful Packages
- Numpy: Python做多維陣列（矩陣）運算時的必備套件，比起Python內建的list，Numpy的array有極快的運算速度優勢
- Pandas：有了Pandas可以讓Python很容易做到幾乎所有Excel的功能了，像是樞紐分析表、小記、欄位加總、篩選
- Matplotlib：基本的視覺化工具，可以畫長條圖、…
- Seaborn：另一個知名的視覺化工具，個人認為畫起來比matplotlib好看
- SciKit-Learn: Python 關於機器學習的model基本上都在這個套件，像是SVM, Random Forest…

Source:[Teh James Medium][1]

[1]:https://medium.com/@yehjames/%E8%B3%87%E6%96%99%E5%88%86%E6%9E%90-%E6%A9%9F%E5%99%A8%E5%AD%B8%E7%BF%92-%E7%AC%AC%E4%B8%80%E8%AC%9B-python%E6%87%B6%E4%BA%BA%E5%8C%85-anaconda-%E4%BB%8B%E7%B4%B9-%E5%AE%89%E8%A3%9D-f8199fd4be8c



## Tricks
### Simplification for loops
- `List Comprehension`
``` python
def list_doubler(lst):
    doubled = []
    for num in lst:
        doubled.append(num*2)
    return doubled
    
# using list comprehension
def list_doubler(lst):
    return [num * 2 for num in lst]
```
Used with __conditions__
```python
def long_words(lst):
    words = []
    for word in lst:
        if len(word) > 5:
           words.append(word)
    return words

#using list comprehension
def long_words(lst):
    return [word for word in lst if len(word) > 5]
```

- `Dictionary Comprehension`
- `Set Comprehension`

Source:[Python single line for loop][lc]

[lc]:https://blog.teamtreehouse.com/python-single-line-loops



## Questions and Exercises
- [50+ Data Structure and Algorithms Interview Questions for Programmers][50+]

[50+]:https://hackernoon.com/50-data-structure-and-algorithms-interview-questions-for-programmers-b4b1ac61f5b0
