gcd(a,b)表示a,b的最大公因数。

lcm(a,b)表示a,b的最小公倍数。
# 唯一分解定理
N = p1^a1 * ....... (n个质因子)
一个数可以分成多个质数相乘
		a <= b     gcd(a,b) = gcd(a,b-a)
		 a * b  = gcd(a,b) * lcm(a,b)
```cpp
ll gcd(ll a, ll b){return b == 0 ? a : gcd(b,a % b);}
ll lcm(ll a, ll b){return a / gcd(a,b) * b;}
```