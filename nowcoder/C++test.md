牛客网测试题C++语法笔记
====
## 7：reinterpret_cast<int *>  
  类型转化，指针所指位置不变
## 9:sizeof(p)=4  

指针的大小为4，不论所指变量  

## 11：变量的生命周期和作用域  
  ### 全局变量    
  作用域：全局作用域（全局变量只需在一个源文件中定义，就可以作用于所有的源文件。）  
  生命周期：程序运行期一直存在  
  引用方法：其他文件中要使用必须用extern 关键字声明要引用的全局变量。  
  注意：如果在两个文件中都定义了相同名字的全局变量，连接出错：变量重定义  
  内存分布：全局数据区  
  eg：  
  ```
  //defime.cpp  
  int g_iValue = 1;  

  //main.cpp  
  extern int g_iValue;  

  int main()  
  {  
      cout << g_iValue;  
      return 0;  
  }  
  ```
  ### 全局静态变量  
  作用域：文件作用域（只在被定义的文件中可见。）  
  生命周期：程序运行期一直存在  
  内存分布：全局数据区  
  定义方法：static关键字，const 关键字  
  注意：只要文件不互相包含，在两个不同的文件中是可以定义完全相同的两个静态变量的，它们是两个完全不同的变量  
  eg:  
  ```
  const int iValue_1;  
  static const int iValue_2;  
  static int iValue_3;  

  int main()  
  {  
      return 0;  
  }
  ```
  ### 静态局部变量  
  作用域：局部作用域（只在局部作用域中可见）  
  生命周期：程序运行期一直存在  
  内存分布：全局数据区  
  定义方法：局部作用域用中用static定义  
  注意：只被初始化一次，多线程中需加锁保护  
  eg：  
  ```
  void function()  
  {  
      static int iREFCounter = 0;  
  }
  ```  
  ### 局部变量  
  作用域：局部作用域（只在局部作用域中可见）  
  生命周期：程序运行出局部作用域即被销毁  
  内存分布：栈区  
  注意：auto指示符标示  
  >1. 若全局变量仅在单个C文件中访问，则可以将这个变量修改为静态全局变量，以降低模块间的耦合度
  >2. 若全局变量仅由单个函数访问，则可以将这个变量改为该函数的静态局部变量，以降低模块间的耦合度
  >3. 设计和使用访问动态全局变量、静态全局变量、静态局部变量的函数时，需要考虑重入问题，因为他们都放在静态数据存储区，全局可见
  >4. 如果我们需要一个可重入的函数，那么，我们一定要避免函数中使用static变量(这样的函数被称为：带“内部存储器”功能的的函数  
  >5. 函数中必须要使用static变量情况:比如当某函数的返回值为指针类型时，则必须是static的局部变量的地址作为返回值，若为auto类型，则返回为错指针  
## C++中全局变量的默认值
在GCC编译器下各个类型的全局变量的默认值：  
  
表示数字的变量类型默认值都为0  
  
bool型默认值为false  
  
string型默认值为空字符串  
  
char 型比较特殊。char类型默认值为'\0'， 即字符串结束标志，其整数值为0。如果用printf("%d")输出时值为 0， 但用printf("%c"),或cout 输出时显示为"a"， char型数组默认值为空字符串，其中的每个元素与单个char类型相同，所以用puts() 和printf("%s") 输出都是空字符串。  
## new运算符只是申请分配一个内存空间而已
int *pia = new int[10];    // 10个未初始化int
int *pia2 = new int[10](); // 10个值初始化为0的int  
##  12C++类所占大小的问题
1. 在类中，如果什么都没有，则类占用一个字节，一旦类中有其它成员，则这个字节就不在计算之类，例如如果一个类含有一个int类型，则占用4个字节而非5个字节。  
2. 如果只有成员函数，则还是只占一个字节，因为类函数不占用空间。  
3. sizeof的本质是得到某个类型的大小，就是创建这个类型的一个对象（或变量）时，需要为其分配空间的大小。而类也可以理解为int或float这样的一种类型。当出现static成员变量的时候，静态成员是存储在静态存储区中的，它是一个共享的量，所以是这个类实例对象时无需再为static成员变量分配空间的。  
4. 类中一旦有virtual修饰的成员函数，编译器会构建虚函数表，在该类中会存放一个指向虚函数表的指针，在
 32位机中该指针和其他指针一样占用4字节。  
5. 字节对齐
   * 关于数据类型自身的对齐值，不同类型会按不同的字节来对齐。  
   
      |类型|	对齐值(字节)|  
      |--|--|  
      |char|1|  
      |short|2|
      |int|4|
      |float|4|
      |double|4|
   * 类、结构体的自身对齐字节值。对于结构体类型与类对象的对齐原则：使用成员当中最大的对齐字节来对齐。比如在Struct A中，int a的对齐字节为4，比char,short都大，所以A的对齐字节为4
   * 指定对齐字节值。意思是指使用了宏 #pragma pack(n)来指定的对齐值
   * 有效对齐要求数据成员存放的地址值能被有效对齐值整除，即：地址值%有效对齐值=0
## 关于继承中的函数重写
父类指针指向子类实例对象，调用普通重写方法时，会调用父类中的方法。而调用被子类重写虚函数时，会调用子类中的方法。  
再次说明了，子类中被重写的虚函数的运行方式是动态绑定的，与当前指向类实例的父类指针类型无关，仅和类实例对象本身有关。  
例：  
```
class A
{
public:
 void FuncA()
 {
     printf( "FuncA called\n" );
 }
 virtual void FuncB()
 {
     printf( "FuncB called\n" );
 }
};
class B : public A
{
public:
 void FuncA()
 {
     A::FuncA();
     printf( "FuncAB called\n" );
 }
 virtual void FuncB()
 {
     printf( "FuncBB called\n" );
 }
};
void main( void )
{
 B  b;
 A  *pa;
 pa = &b;
 A *pa2 = new A;
 pa->FuncA(); （ 3）
 pa->FuncB(); （ 4）
 pa2->FuncA(); （ 5）
 pa2->FuncB();
 delete pa2;
}
```
输出结果：
```
FuncA called
FuncBB called
FuncA called
FuncB called
```
## 17sprintf()函数  
向字符串中打印。  
例子：字符串ABABA，此时 p1 指向 A BABA，p2 指向 ABABA ； sprintf 重定向修改 ABABA ， B 变为 1 ，且跟随一个 ‘\0’ （该函数自动产生的） , 此时，字符串变为 A1‘\0’BA 。
## 18auto关键字
C++11 auto  
auto可以在声明变量的时候根据变量初始值的类型自动为此变量选择匹配的类型，类似的关键字还有decltype。举个例子：  
```
#include<string>
#include<vector>
int main()
{
    std::vector<std::string> vs;
    for (std::vector<std::string>::iterator i = vs.begin(); i != vs.end(); i++)
    {
        //...
    }
}
```
可替换成：  
```
#include<string>
#include<vector>
int main()
{
    std::vector<std::string> vs;
    for (auto i = vs.begin(); i != vs.end(); i++)
    {
        //..
    }
}
```
## 拷贝函数和赋值运算符
```
C MyClass obj3 = obj1;
obj3还不存在，所以调用拷贝构造函数输出2，
如果obj3存在，obj3=obj，则调用复制运算符重载函数，输出3
```
## 20函数若想返回指针，则需要使用new或malloc申请内存空间，否则函数结束后返回的是野指针
