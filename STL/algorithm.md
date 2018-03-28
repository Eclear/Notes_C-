# C++ STL Algorithm
## 1. Sum
To get the sum of elements is STL,  
eg:  
```
#include<numeric>
...
int sum = accumulate(vec.begin() , vec.end() , 42);
```
accumulate带有三个形参：头两个形参指定要累加的元素范围，第三个形参则是累加的初值
