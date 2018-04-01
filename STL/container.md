# C++ STL -- container  
## set  
跟vector的唯一区别就是，set里面的元素是有序的且唯一的，只要你往set里添加元素，它就会自动排序，而且，如果你添加的元素set里面本来就存在，
那么这次添加操作就不执行。  
>可以用于取得有序唯一序列，另一种方法是在小数据规模时创建存在状态数组

* set声明时不需大小，使用insert插入元素
* set不能直接cout或下标遍历，遍历需要用iterator
  ```
  set<int>::iterator ite1 = iset.begin();
  set<int>::iterator ite2 = iset.end();
  for(;ite1!=ite2;ite1++)
  {
      cout<<*ite1;
  }
  ```

* set的各成员函数列表如下:

1. begin()--返回指向第一个元素的迭代器

2. clear()--清除所有元素

3. count()--返回某个值元素的个数

4. empty()--如果集合为空，返回true

5. end()--返回指向最后一个元素的迭代器

6. equal_range()--返回集合中与给定值相等的上下限的两个迭代器

7. erase()--删除集合中的元素

8. find()--返回一个指向被查找到元素的迭代器

9. get_allocator()--返回集合的分配器

10. insert()--在集合中插入元素

11. lower_bound()--返回指向大于（或等于）某值的第一个元素的迭代器

12. key_comp()--返回一个用于元素间值比较的函数

13. max_size()--返回集合能容纳的元素的最大限值

14. rbegin()--返回指向集合中最后一个元素的反向迭代器

15. rend()--返回指向集合中第一个元素的反向迭代器

16. size()--集合中元素的数目

17. swap()--交换两个集合变量

18. upper_bound()--返回大于某个值元素的迭代器

19. value_comp()--返回一个用于比较元素间的值的函数

## map
* Map是STL的一个关联容器，它提供一对一（其中第一个可以称为关键字，每个关键字只能在map中出现一次，第二个可能称为该关键字的值）的数据处理能力，由于这个特性，它完成有可能在我们处理一对一数据的时候，在编程上提供快速通道。map内部自建一颗红黑树(一 种非严格意义上的平衡二叉树)，这颗树具有对数据自动排序的功能，所以在map内部所有的数据都是有序的。
* 特点是增加和删除节点对迭代器的影响很小，除了那个操作节点，对其他的节点都没有什么影响。对于迭代器来说，可以修改实值，而不能修改key。
* 功能
  自动建立Key － value的对应。key 和 value可以是任意你需要的类型。  
  根据key值快速查找记录，查找的复杂度基本是Log(N)，如果有1000个记录，最多查找10次，1,000,000个记录，最多查找20次。  
  快速插入Key -Value 记录。  
  快速删除记录  
  根据Key 修改value记录。  
  遍历所有记录。
* 访问方式：
1. 用key： m_map[m_key]  
2. iterator:   
    `ite1 = m_map.begin(); ite1->first;`    
* 插入数据：
1. 用insert函数插入pair数据  
```
mapStudent.insert(pair<int, string>(3, "student_three")); 
```  
2. 用insert函数插入value_type数据  
```
mapStudent.insert(map<int, string>::value_type (1, "student_one")); 
```
3. 用数组方式插入数据  
```
mapStudent[1] = "student_one"; 
```  

## 堆(heap)
STL中并没有把heap作为一种容器组件，heap的实现亦需要更低一层的容器组件（诸如list,array,vector）作为其底层机制。Heap是一个类属算法，包含在algorithm头文件中。虽然STL中关于heap默认调整成的是大顶堆，但却可以让用户利用自定义的compare_fuction函数实现大顶堆或小顶堆。heap的低层机制vector本身就是一个类模板，heap基于vector便实现了对各种数据类型（无论基本数据类型还是用户自定义的数据类型）的堆排（前提是用户自定义的数据类型要提供比较机制compare_fuction函数）。
