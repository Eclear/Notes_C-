# C++整形、字符串互转
## C++11 to_string()
```
#include <iostream>
#include <string>

int main()
{
    double f = 23.43;
    std::string f_str = std::to_string(f);
    std::cout << f_str << '\n';
}
```
## C++11 stoi/stof/stod/stol/stoll...
C++11 中可以直接转化为int/float/long...
```
string s("12"); 
int i = stoi(s);
cout<< i<< endl;
```

## 使用sstream(stringstream)
```
#include <iostream>
#include <sstream>
using namespace std;
int test_sstream()
{
    stringstream stream;

    stream << "12abc";
    int n;
    stream >> n;//这里的n将保持未初始化时的随机值
    cout << n << endl；
    //stream.clear();
    stream << "def";
    string s;
    stream >> s;
    cout << s << endl;
    return 0;
}
```
```
string val;
stringstream in("abc cde f");
in>>val;
cout<<val;   //"abc"
```

