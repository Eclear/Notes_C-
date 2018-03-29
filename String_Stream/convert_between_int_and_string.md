# C++整形、字符串互转
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
