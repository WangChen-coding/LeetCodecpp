

```c++
#include <stdio.h>
#include<iostream>
#include<set>
#include<map>
#include<vector>
using namespace std;
class Node {
public:
	int val;
	Node* next;
	Node* random;

	Node(int _val) {
		val = _val;
		next = NULL;
		random = NULL;
	}
};


class Solution {
public:
	Node* copyRandomList(Node* head) {
		map<Node*, int>Node_map;
		vector<Node*>Node_vec;
		Node* ptr = head;
		int i = 0;
		while (ptr) {
			Node_vec.push_back(new Node(ptr->val));
			Node_map[ptr] = i;
			ptr = ptr->next;
			i++;
		}
		Node_vec.push_back(0);
		ptr = head;
		i = 0;
		while (ptr) {
			Node_vec[i]->next = Node_vec[i + 1];
			if (ptr->random) {
				int id = Node_map[ptr->random];
				Node_vec[i]->random = Node_vec[id];
			}
			i++;
			ptr = ptr->next;

		}
		return Node_vec[0];

	}
};
int main() {
	Node a(10);
	Node b(20);
	Node c(30);
	Node d(40);
	Node e(50);
	Node w(60);
	Node y(70);
	Node z(80);

	a.next = &b;
	b.next = &c;
	c.next = &d;
	d.next = &e;
	e.next = &w;
	w.next = &y;
	y.next = &z;
	z.next = NULL;

	a.random = &c;
	b.random = &e;
	c.random = &a;
	d.random = &z;
	e.random = NULL;
	w.random = &a;
	y.random = &y;
	z.random = &z;
	Solution solve;
	Node* head = solve.copyRandomList(&a);
	while (head) {
		printf("val=%d", head->val);
		if (head->random) {
			printf("rand=%d\n", head->random->val);
		}
		else {
			printf("rand=NULL\n");
		}
		head = head->next;
	}
}

```



思路：

1. 创建一个map用于保存链表的节点地址和对应的序号，创建一个vector用于保存新链表的节点地址。
2. 遍历原链表，将节点地址和序号存入到map中，同时创建节点pushback到vector中
3. 依次连接vector的next关系，同时获取原链表中的random关系，获取当前节点指向的节点的地址，转化为ID。
4. 将vector中的元素根据ID的指示，指向对应random