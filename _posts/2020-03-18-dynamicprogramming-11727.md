---
title: "DynamicProgramming_2XN tiling2_11727"
categories: 
  - BaekJoon
last_modified_at: 2020-03-18T20:32:00+09:00
toc: true
---
백준 DP의 11727번 문제 2XN 타일링 2를 풀이해보도록 하겠습니다.<br/>

문제 URL : [https://www.acmicpc.net/problem/11727](https://www.acmicpc.net/problem/11727)
<br/>

저는 이렇게 문제 해결에 접근했습니다.<br/>

시행착오 : +1칸이되었으니 이전 경우에 오른쪽이나 왼쪽에 1X2 짜리 블록을 추가하는 경우에서 모든 중복의 경우를 빼고 2X2짜리 블록 한개나 2X1짜리 블록 두개로 대체되는 경우를 일일이 세는 방법?으로 접근하려하니 점화식이 매우 복잡해지더라구요.
게다가 맞지도 않았구요.

DP 문제는 완전탐색이나 순환따위로 해결할 경우에 스택이 터질 수 있어 가장 끝부분만가지고 유추를 해낼 수 있다는 것이 핵심이라고 배웠고 그렇기 때문에 점화식을 잘 세워줘야한다는 것을 알고있었습니다.<br/>

하지만 이런 점화식이 어떻게 나오게된 것인지를 설명할 수 있어야하는데 억지로 끼워맞추기식으로 나온 점화식이 답을 도출하긴하는데 직관적이지 못한 데다가 스스로 납득이 안되서 한참 고민하다가 결국 다른분들의 풀이를 확인해봤습니다.<br/>

결국 이해는 할 수 있었는데 이를 기록해보겠습니다.<br/>

이 문제를 전환된 생각으로 다시 보면, 2 X N칸만큼의 공간에 세 종류의 블록(세로로 긴 1 X 2짜리 한개 or 2 X 2짜리 한개 or 가로로 긴 2 X 1짜리 두개)만을 이용하여 꽉 채우는 문제를 풀고 있는 것 입니다.<br/>

번번히 꽉 끼워 맞춰야할 퍼즐의 공간은 1칸 만큼씩 늘어날 것이고, 결국 우리는 가장 오른쪽부분을 먼저 완성시키며 접근하는 것이지요.<br/>

참고로 이때 가로로 긴 2X1짜리 한개만으로는 오른쪽부분을 완성시킬 수 없다는 것을 직관적으로 알 수 있습니다.<br/>

다시 정리해보겠습니다.<br/>
전체 퍼즐 테두리의 가로 공간은 N크기를 가졌습니다.<br/>
왼쪽부분이 어떻게든 완성이 되었던 부분이죠. 그러니 중요한 부분은 오른쪽 끝부분입니다.<br/>

퍼즐의 가장 오른쪽을 완성시키는 방법은 역시 세가지 입니다.<br/>

만약 세 블록 유형 중 첫번째 유형인 1X2 블록 한개로 오른쪽 끝부분을 완성시키기 위해서는 퍼즐공간은 N-1칸까진 어떤 방법으로든 완성되어있어야한다는 가정이 필요합니다.<br/>

두번째 유형인 2X2 블록 한개로 오른쪽 끝부분을 완성시키기 위해서는 퍼즐공간은 N-2칸까지 어떤 방법으로든 완성되어있어야한다는 가정이 필요합니다.<br/>

세번째 유형인 2X1 블록 두개로 오른쪽 끝부분을 완성시키기 위해서는 퍼즐공간은 N-2칸까지 어떤 방법으로든 완성되어있어야한다는 가정이 필요합니다.<br/>

다시 반대로 말하면,<br/>
N-1칸까지 완성되어있었다면 1X2짜리를 가져다 완성시키는 경우 1가지, N-2칸까지 완성되어있었다면 2X2짜리를 가져다 완성시키거나, 2X1짜리 두개를 가져다 완성시키는 경우 2가지 경우의 수가 존재합니다.<br/>

그래서 점화식은 아래와 같습니다.<br/>
1) N-1칸까지 완성될 수 있는 경우의 수 X 1<br/>
2) N-2칸까지 완성될 수 있는 경우의 수 X 2<br/><br/>
따라서
N까지의 완성시킬 수 있는 모든 경우의 수 = 1) + 2)<br/>

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
	int n;
	vector <int> arr;
	arr.push_back(1);	// when n=1
	arr.push_back(3);	// when n=2

	/* input */
	cin >> n;

	/* process */
	if (n > 2) {
		for (int i = 2; i < n; i++) {
			arr.push_back((arr[i - 1] + arr[i - 2] * 2) % 10007);
		}
	}

	/* output */
	cout << arr[n - 1]  << endl;

	// cin >> n;
	return 0;
}
~~~

<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200316baekjoon_dynamicprogramming/capture1.JPG" alt=""> {% endraw %}<br/>

<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>