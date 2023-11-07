## substr

**substr()是C++语言函数，主要功能是复制子字符串，要求从指定位置开始，并具有指定的长度。如果没有指定长度\_Count或\_Count+\_Off超出了源字符串的长度，则子字符串将延续到源字符串的结尾。** &#x20;

##### 语法

[`substr`](https://so.csdn.net/so/search?q=substr\&spm=1001.2101.3001.7020)`(size_type _Off = 0,size_type _Count = npos)`\
一种构造string的方法\
形式 ： `s.substr(pos, len)`\
返回值： ==string，包含s中从pos开始的len个字符的拷贝（pos的默认值是0，len的默认值是s.size() - pos，即不加参数会默认拷贝整个s）==\
异常 ：==若pos的值超过了string的大小，则substr函数会抛出一个out\_of\_range异常；若pos+n的值超过了string的大小，则substr会调整n的值，只拷贝到string的末尾==
