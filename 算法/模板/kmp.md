kmp算法分为三个部分，匹配串，模式串，next数组，
首先先用模式串算出next数组，next数组对应的是匹配失败后退回到什么地方。
```cpp
  vector<int> commpute_next(string pattern){
        vector<int>next(pattern.size() + 1, 0);
        next[0] = -1;
        next[1] = 0; // 长度为1的字符串没有前后缀
        int i = 2; // i表示next数组的索引
        int k = 0; // 指针指向pattern的位置
        while (i < next.size()) {
         // 如果当前字符匹配成功
            if (pattern[i - 1] == pattern[k]) {// pattern索引比next索引小1
                next[i] = k + 1;
                k = next[i];
                ++i;
        // 如果指针已经指向pattern[0]却还没有匹配成功
            } else if (k == 0){
                next[i] = 0;
                ++i;
            } else{
                k = next[k]; //可以利用已匹配成功的信息，让指针不进行回退，查找next数组
            }
        }
        return next;
    }
  
int kmp(string str,string pattern){
        vector<int> next = commpute_next(pattern);
        int i = 0;
        int j = 0;
        while (i < str.size()) {
            if (str[i] != pattern[j]) {
                j = next[j];
                if (j == -1) { //表示当前没有已匹配字符
                    i++; //寻找下一个匹配的pattern首字母
                    j = 0; //指针移到pattern开头
                }
            }else{
                i++;
                j++;
                if (j == pattern.size()) {
                    return (int) (i - pattern.size());
                }
            }
        }
        return -1;
    }
```