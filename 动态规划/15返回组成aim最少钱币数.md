### 题目

arr是面值数组，其中的值都是正数且没有重复。再给定一个正数aim。

每个值都认为是一种面值，且认为张数是无限的。

返回组成aim的**最少货币数**。

### 暴力递归-从左到右的范围尝试模型-斜率优化

将每种可能性穷举出来，然后找到最小值。

比如说先选第一个面值一张，然后接下来的可能性，第二张还选第一个面值，或者选第二个面值，不断列举，直到目标钱数为0。

所以写一下尝试函数process，参数有面值数组arr，当前选到哪个位置index，当前剩余钱数。

主函数中调用的是arr，0，aim

再分析basecase

当index来到最后一个arr元素位置，判断此时rest是否为0，如果为0，说明已经达成目标，返回0代表成功；如果rest不等于0，说明目标没有达成，返回整数最大。

分析普遍情况

设置一个变量ans表示达成目标最少的张数，每次process返回的时候都判断是否成功，如果成功就比较一下之前的张数和当前方案的张数，谁的少就更新。

开始枚举，从当前这个面值需要0张开始，直到剩余目标数小于张数x面值。next接收当前位置选zhang数，然后开始尝试下一个面值的返回值。只要返回值不为整数最大，那么就认为后续方案可行，比较后取更小的值即可。

```cpp
int process(vector<int>& arr, int index, int rest) {
	if (index == arr.size()) {
		return rest == 0 ? 0 : INT_MAX;
	}
	else {
		int ans = INT_MAX;
		for (int zhang = 0; zhang * arr[index] <= rest; zhang++) {
			int next = process(arr, index + 1, rest - zhang * arr[index]);
			if (next != INT_MAX) {
				ans = min(ans, zhang + next);
			}
		}
		return ans;
	}
}
int mincoin(vector<int>& arr, int aim) {
	return process(arr, 0, aim);
}
```

### 动态规划

有两个可变参数，一个是index，范围是0-arr.size；另一个是rest，范围是0-aim

分析basecase，当选到最后一个面值时，rest为0，则此时值为0.如果选到最后一个面值，那么此时剩余不为0，说明不满足要求，值设为整数最大。

然后分析位置依赖关系，上一行的依赖下一行的。右边的依赖左边的。

所以行从最后一行开始往上，列从左往右。

每个位置的值，通过枚举来确定，计算得到最小值后，确定值。

最终返回要求的点，即从0开始达成aim目标值。

```cpp
int dp(vector<int>& arr, int aim) {
	if (aim == 0) {
		return 0;
	}
	int N = arr.size();
	vector<vector<int>>dp(N + 1, vector<int>(aim + 1, 0));
	dp[N][0] = 0;
	for (int j = 1; j <= aim; j++) {
		dp[N][j] = INT_MAX;
	}
	for (int index = N - 1; index >= 0; index--) {
		for (int rest = 0; rest <= aim; rest++) {
			int ans = INT_MAX;
			for (int zhang = 0; zhang * arr[index]<=rest; zhang++) {
				int next = dp[index + 1][rest - zhang * arr[index]];
				if (next != INT_MAX) {
					ans = min(ans, zhang+next);
				}
			}
			dp[index][rest] = ans;
		}
	}
	return dp[0][aim];
}
```

### 斜率优化

分析左下方的位置依赖关系。

当前位置的值，取决于当前位置、左侧位置的值+1，其中的最小值。但是需要判断左侧的值是否越界，并且是否值为有效值。

```cpp
int dp2(vector<int>& arr, int aim) {
	if (aim == 0) {
		return 0;
	}
	int N = arr.size();
	vector<vector<int>>dp(N + 1, vector<int>(aim + 1, 0));
	dp[N][0] = 0;
	for (int j = 1; j <= aim; j++) {
		dp[N][j] = INT_MAX;
	}
	for (int index = N - 1; index >= 0; index--) {
		for (int rest = 0; rest <= aim; rest++) {
			dp[index][rest] = dp[index + 1][rest];
			if (rest - arr[index] >= 0 && dp[index][rest - arr[index]] != INT_MAX) {
				dp[index][rest] = min(dp[index][rest], dp[index][rest - arr[index]] + 1);
			}
		}
	}
	return dp[0][aim];
}
```



