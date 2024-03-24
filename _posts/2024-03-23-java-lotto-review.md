---
title: java lotto review
date: 2024-03-23 17:26:19 +0900
categories: [Alom Spring Course, POJO]
tags: [java]
seo:
  date_modified: 2024-03-23 17:26:19 +0900
---

## POJO(Plain Old Java Object)

My Code

```
#include<bits/stdc++.h>
using namespace std;
int n, tmp;
string in;
double ans;

const int MX = 1000004;
struct Node {
	char k; //노드의 값
	bool w; //단어 여부 boolean 값 (단어면 true)
	vector<Node*>v; //알파벳 소문자 26개여서 배열로 관리하려고 했는데
	//순회할 때랑 갈림길(=내 밑 알파벳이 2개 이상)인지 체크가 힘들어서 그냥 백터로 함
};

Node* Root;
int NodeCnt = 0;
Node NodePool[MX];

Node* CreateNode(char z) {
	NodePool[NodeCnt].k = z;
	NodePool[NodeCnt].w = false;
	NodePool[NodeCnt].v.clear();
	return &NodePool[NodeCnt++];
}

void init() {
	Root = nullptr;
	NodeCnt = 0;
}

void insert(string input) {
	Node* ptr = Root;
	for (int i = 0; i < input.size(); i++) {
		char z = input[i];
		bool flag = false;
		for (auto& c : ptr->v) {
			if (c->k == z) {  //이미 있어서 다음 칸으로 넘어가기
				ptr = c;
				flag = true;
				break;
			}
		}
		if (!flag) { //없어서 만들어야 하는 경우
			ptr->v.push_back(CreateNode(z)); //만들고
			ptr = ptr->v.back(); //넘어가기
		}
	}
	ptr->w = true; //단어의 끝 표시
}


void traverse(Node* ptr, int cnt) {
	tmp = 0;
	if (ptr->v.size() > 1 || ptr->w) //(갈림길 or 단어면) 나의 다음 노드 cnt에 + 1
		tmp += 1;
	for (auto& c : ptr->v) {
		traverse(c, cnt + tmp); //dfs
	}
	if (ptr->w) //내가 단어면 더해줌
		ans += cnt;
}

int main() {
	cin.tie(0);
	ios::sync_with_stdio(0);
	cout.tie(0);

	//소수점 2자리 출력
	cout.setf(ios::fixed);
	cout.precision(2);

	while (cin>>n) { //EOF    아니 cin.eof()로 했다가 틀렸음 뭐지 ,,
		//초기화
		ans = 0;
		init(); 

		//Root 설정
		Root = CreateNode('R');

		//입력받고 트리 형성
		for (int i = 0; i < n; i++) {
			cin >> in;
			insert(in);
		}

		//순회
		for (auto& c : Root->v) {
			traverse(c, 1);
		}

		//출력
		cout << round(ans/n*100)/100 << '\n';
	}
	return 0;
}
```

I used Trie Data Structure.

I solved this on my own. I'm proud of myself. Happy!

My English might be awkward. If you have any inconvenience, please send me an email so that I can correct it.

Email: deld4@icloud.com

Thank you for reading my post.

