kmp算法分为三个部分，匹配串，模式串，next数组，
首先先用模式串算出next数组，next数组对应的是匹配失败后退回到什么地方。
```cpp
    vector<int> getNext(string str)
    {
		int n = str.length();
		vector<int> next(n,-1);
		for(int i = 1; i < n; i++)
        {
            int j = fail[i - 1];
            while(j != -1 && s[j + 1] != s[i]) j = fail[j];
            if(s[j + 1] == s[i])fail[i] = j + 1;
        }
    }
```