# [3.To Lower Case](<https://leetcode.com/problems/to-lower-case/>)

```C++
#include <iostream>
#include <string>

using namespace std;

class Solution {
public:
    string toLowerCase(string str) {
        for(int i=0; i< str.size(); i++){
            if(str[i]>='A'&&str[i]<='Z'){
                str[i]+=32;
            }
        }
        return str;
    }
};
```

