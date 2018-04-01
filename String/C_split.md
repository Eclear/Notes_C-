# C语言使用split将字符换分割为字符串数组（C++没有这个函数）
* 语法：stringObject.split(separator,howmany);  
  * 参数介绍：
  * separator：必需。字符串或正则表达式，从该参数指定的地方分割stringObject。 
  * howmany：可选，该参数指定返回的数组的最大长度。如果设置了该参数，返回的子串不会多余这个参数指定的数组。如果没有设置该参数，整个字符串都会被分割，
  不考虑它的长度。
  * 返回值：一个字符串数组，该数组是通过在separator指定的边界处将字符串stringObject分割成子串创建的。返回的数组中的子串不包括separator自身。
* 例子：
```
string str="hello";
string[] a=str.split("");  // h e l l o
string str="123@456";
string[] a=str.split("@"); / 123 456
```
