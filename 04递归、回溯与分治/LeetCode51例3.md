LeetCode51 N皇后

第一步：根据方向数组，确认某个皇后在棋盘mark上的攻击范围

```cpp
void put_down_the_queen(int x, int y, vector<vector<int>>& mark) {
	static const int dx[] = { -1,1,0,0,-1,-1,1,1 };
	static const int dy[] = { 0,0,-1,1,-1,1,-1,1 };
	mark[x][y] = 1;
	for (int i = 1; i < mark.size(); i++) {
		for (int j = 0; j < 8; j++) {
			int new_x = x + dx[j] * i;
			int new_y = y + dy[j] * i;
			if (new_x >= 0 && new_x < mark.size() && new_y >= 0 && new_y < mark.size()) {
				mark[new_x][new_y] = 1;
			}
		}
	}
}
```

方向数组：皇后在棋盘上的攻击范围是上下左右和左右对角线。所以可以用数组将这八个方向表示出来，将x和y的值分别填充在两个数组中。

填充指定方向上的数据：由八个变量的方向数组确定方向，每个方向扩展直到棋盘边界(为了方便，直接向外扩展N-1个)，再加一个判断，只要是属于棋盘内部的区域，都填充为1。

第二步回溯算法

```cpp
void generate(int k, int n, vector<string>& location, vector<vector<string>>& result, vector<vector<int>>& mark) {
	if (k == n) {
		result.push_back(location);
		return;
	}
	for (int i = 0; i < n; i++) {
		if (mark[k][i] == 0) {
			vector<vector<int>>temp_mark = mark;
			location[k][i] = 'Q';
			put_down_the_queen(k, i, mark);
			generate(k + 1, n, location, result, mark);
			mark = temp_mark;
			location[k][i] = '.';
		}
	}
    return;
}

```

k表示完成了几个皇后的放置，将某次的结果储存在location中，最终结果存储在result中，mark是棋盘的标志数组。

当放置完全部皇后，将记录本次的结果location存到result中，返回。

进入到循环中，如果当前位置可以放皇后，那么记录此刻的mark，将皇后的位置用q标记，附加此皇后的攻击范围。递归进入到下一个皇后的放置，直到放置完全部皇后或者当前行没有位置可以放置皇后。

假设一头扎进去，一路全是正确情况，到达最后一层放置完成后，就可以将放置的location存放在结果中。然后开始回退，恢复到最后一行未放置的情况，将之前放置皇后的位置标记为不可放置，然后寻找当前行下一个可放置的位置。如果没有可放置的位置，则需要恢复到倒数第二行未放置的情况，已经放置过皇后的位置标为不可放置后，继续遍历当前行后面的位置，如果可以放置则进入递归，不断深入。如果不能放置，则继续回退。

整个放置的顺序就是先在第一行放第一个位置，然后深入进去，一直到底，到不能放置的时候，就回退到上一行，继续遍历深入。相当于进入一个分支，全部遍历完，然后再进入另一个分支，再遍历一次下面的内容。

```cpp
vector<vector<string>> solveNQueens(int n) {
	vector<vector<string>>result;
	vector<vector<int>>mark;
	vector<string>location;
	for (int i = 0; i < n; i++) {
		mark.push_back(vector<int>());
		for (int j = 0; j < n; j++) {
			mark[i].push_back(0);
		}
		location.push_back("");
		location[i].append(n, '.');
	}
	generate(0, n, location, result, mark);
	return result;
}
```

result用来储存最终的放置结果，mark标记棋盘是否可以放置皇后，location储存某个摆放结果，如果可以递归到底，就可以将放置的结果存放在result结果中。