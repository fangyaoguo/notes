属于递推，从已知到未知 
例题
![[Pasted image 20240218143831.png]]
![[Pasted image 20240218150008.png]] 
code： 
```cpp
const int N  = 1e5 + 9;
int a[N];
const int D = 5e5 + 9;
bool dp[D];
void solve()
{	
	int n ; cin >> n;
	dp[0] = 1; 
	for(int i = 1; i <= n; i++)cin >> a[i];
	for(int i = 1; i <= n; i++)
	{
		for(int j = D - 1; j >= a[i]; j--)
		{
			dp[j] |= dp[j - a[i]];
		}
	}
	long long ans = 0;
	for(int i = 0; i < D - 1; i++)if(dp[i])ans++;
	cout<<ans;
}
```
复杂度o(n) * 5e5