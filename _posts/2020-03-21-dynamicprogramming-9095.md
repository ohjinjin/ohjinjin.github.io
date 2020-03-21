---
title: "DynamicProgramming_sumation of 1,2,3_9095"
categories: 
  - BaekJoon
last_modified_at: 2020-03-21T16:44:00+09:00
toc: true
---
백준 DP의 9095번 문제 1,2,3 더하기를 풀이해보도록 하겠습니다.<br/>

문제 URL : [https://www.acmicpc.net/problem/9095](https://www.acmicpc.net/problem/9095)
<br/>

저는 이렇게 문제 해결에 접근했습니다.<br/>

DP 문제를 풀 때에는 경우의 수를 다 그려보거나 나열해보곤하는데, 그러다보면 그 규칙이 보이기도 하기 때문이지요.<br/>

이번 문제는 크게 어렵지 않았습니다.<br/>

n이 5일 경우의 수를 쭉 적어보니 가장 첫 항이 1일 경우 뒷부분 항들은 모두 n이 4일 경우 1,2,3으로 표현가능한 모든 덧셈식들입니다.<br/>
또한 가장 첫 항이 2일 경우는 이후의 항들이 n이 3일경우와 일치했구요.<br/>
가장 첫 항이 3일 경우는 이후의 항들이 n이 2일 경우와 일치합니다.<br/>

하지만 이 문제가 1과 2와 3만이 피연산자로서 허용되므로 어떤 임의의 숫자 n보다 1 작은 수, 2 작은 수, 3 작은 수까지의 경우의 수만을 합해주면 됩니다.<br/>

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

int main(void) {
	ios::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);

	/* declare variables */
	int T;
	int arr[11] = { 0, };

	arr[0] = 1;
	arr[1] = 2;
	arr[2] = 4;

	/* input & process & output */
	cin >> T;

	for (int i = 0; i < T; i++) {
		int n;
		cin >> n;

		if (n > 2) {
			for (int j = 3; j < n; j++) {
				if (arr[j] != 0) {
					continue;
				}
				arr[j] = arr[j - 1] + arr[j - 2] + arr[j - 3];
			}
		}

		cout << arr[n - 1] << endl;
	}

	// cin >> T;
	return 0;
}
~~~

<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200316baekjoon_dynamicprogramming/capture2.JPG" alt=""> {% endraw %}<br/>

<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>