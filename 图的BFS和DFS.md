```cpp
void BFS(Node* head) {
	if (head == NULL)return;
	queue<Node*>q;
	unordered_set<Node*>s;
	q.push(head);
	s.insert(head);
	while (!q.empty()) {
		Node* cur = q.front();
		cout << cur->value << " ";
		q.pop();
		for (Node* n : cur->nexts) {
			if (s.find(n) == s.end()) {
				s.insert(n);
				q.push(n);
			}
		}
	}
}

void DFS(Node* head) {
	if (head == NULL)return;
	stack<Node*>st;
	unordered_set<Node*>se;
	st.push(head);
	se.insert(head);
	cout << head->value << " ";
	while (!st.empty()) {
		Node* cur = st.top();
		st.pop();
		for (Node* n : cur->nexts) {
			if (se.find(n) == se.end()) {
				st.push(cur);
				st.push(n);
				se.insert(n);
				cout << n->value << " ";
				break;
			}
		}
	}
}
```

