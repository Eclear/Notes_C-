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
    cout << n << endl;
    stream.str("");
    //stream.clear();
    stream << "def";
    string s;
    stream >> s;
    cout << s << endl;
    return 0;
}
```
