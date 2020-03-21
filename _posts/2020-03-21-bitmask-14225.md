---
title: "bitmask_sumation of subsequence_14225"
categories: 
  - BaekJoon
last_modified_at: 2020-03-21T18:38:00+09:00
toc: true
---
백준 조합의 14225번 문제 부분수열의 합을 비트마스크로 풀이해보도록 하겠습니다.<br/>

문제 URL : [https://www.acmicpc.net/problem/14225](https://www.acmicpc.net/problem/14225)
<br/>

1182번에서 조금만 변형해서 해결할 수 있었습니다.<br/>
[1182 풀이 보러가기](https://ohjinjin.github.io/baekjoon/bitmask-1182/)

2000001로 둔 이유는 n이 20개까지 들어올 수 있으며, 100000이 최대숫자였기때문에 다 더했을때 나올 수 있는 최대 수와 연관지어 크게 잡은 것이 이유입니다.<br/>
<br/>

Source Code : 
~~~
#include<iostream>
#include<vector>
/*#include<string>
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
int flags[2000001] = { 0, };

int main(void) {
	ios::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);

	/* declare variables */
	int n;
	vector <int> arr;

	/* input */
	cin >> n;
	for (int i = 0; i < n; i++) {
		int tmp;
		cin >> tmp;
		
		arr.push_back(tmp);
	}

	/* process */
	for (int i = 1; i < (1 << n); i++) {
		vector <int> v;
		// i = 00001
		// 00010
		// 00011
		// ...
		// 11111
		for (int j = 0; (1 << j) <= i; j++) {
			// j = 00001
			// 00010
			// 00011
			// ...
			// 11111
			if (i & (1 << j)) {
				v.push_back(j);	// [4] or [3] or [2] or [1] or [0]
			}
		}

		int sum = 0;
		for (int j = 0; j < v.size(); j++) {
			sum += arr[v[j]];
		}
		//if (sum == S) {
		//	count++;
		//}
		flags[sum] = 1;
	}

	for (int i = 1; i < 20000001; i++) {
		if (flags[i] == 0) {
			cout << i << endl;
			break;
		}
	}

	// cin >> n;
	return 0;
}
~~~

<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200316baekjoon_bitmask/capture2.JPG" alt=""> {% endraw %}<br/>

<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>