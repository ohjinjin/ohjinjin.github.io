---
title: "DataStructure_traverse tree_1991"
categories: 
  - BaekJoon
last_modified_at: 2020-03-18T20:39:00+09:00
toc: true
---
백준 자료구조의 1991번 문제 트리 순회를 풀이해보도록 하겠습니다.<br/>

문제 URL : [https://www.acmicpc.net/problem/1991](https://www.acmicpc.net/problem/1991)
<br/>

선수지식으로는 트리 추상 자료구조와 그 연산의 이해겠네요!<br/>
저는 노드의 중복 저장에 다소 몰두해서 풀이를 했습니다.<br/>

Source Code : 
~~~
#include<iostream>
#include<string>
/*#include<vector>
#include<algorithm>
#include<queue>
#include<set>
#include<map>
#include<cstring>
#include<functional>
#include<cmath>
#include<stack>*/

// #define SIZE 1010

using namespace std;

// typedef long long int ll;

class Node {
	string data;
	Node *left;
	Node *right;

public:
	Node() {
		data = "";
		left = right = NULL;
	}
	string getData() {
		return data;
	}
	void setData(string data) {
		this->data = data;
	}
	void setLeft(Node *left) {
		this->left = left;
	}
	void setRight(Node *right) {
		this->right = right;
	}
	void static preorder(Node *root) {
		if (root != NULL) {
			cout << root->data;
			preorder(root->left);
			preorder(root->right);
		}
	}
	void static inorder(Node *root) {
		if (root != NULL) {
			inorder(root->left);
			cout << root->data;
			inorder(root->right);
		}
	}
	void static postorder(Node *root) {
		if (root != NULL) {
			postorder(root->left);
			postorder(root->right);
			cout << root->data;
		}
	}
};

int main(void) {
	ios::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);

	/* 변수 선언 */
	int n;
	string str;

	/* 입력 */
	cin >> n;

	Node *T = new Node[n];
	
	for (int i = 0; i < n; i++) {
		cin >> str;
		int j;
		for (j = 0; j < n; j++) {
			if ((T[j].getData() == str)||(T[j].getData() == "")) {
				break;
			}
		}
		if (T[j].getData() == "") {
			T[j].setData(str);
		}

		cin >> str;
		if (str != ".") {
			int k;
			for (k = 0; k < n; k++) {
				if ((T[k].getData() == str) || (T[k].getData() == "")) {
					break;
				}
			}
			if (T[k].getData() == "") {
				T[k].setData(str);
			}
			T[j].setLeft(&T[k]);
		}
		
		cin >> str;
		if (str != ".") {
			int k;
			for (k = 0; k < n; k++) {
				if ((T[k].getData() == str) || (T[k].getData() == "")) {
					break;
				}
			}
			if (T[k].getData() == "") {
				T[k].setData(str);
			}
			T[j].setRight(&T[k]);
		}
	}
	/* 처리 & 출력 */
	Node::preorder(T);
	cout << endl;
	Node::inorder(T);
	cout << endl;
	Node::postorder(T);
	cout << endl;
	
	//cin >> n;
	return 0;
}
~~~

<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200316baekjoon_datastructure/capture3.JPG" alt=""> {% endraw %}<br/>

<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>