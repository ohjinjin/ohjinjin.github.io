---
title: "Coding Test of Kakao Internship Practice Test # 1"
categories: 
  - Programmers
last_modified_at: 2020-03-29T16:14:00+09:00
toc: true
---

프로그래머스 카카오 인턴십 코딩테스트 실전 모의고사 1번 문제 을 풀이합니다.<br/>

<br/>

Source Code : 
~~~
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int solution(vector<vector<int>> board, vector<int> moves) {
   vector <int> arr;
   int count = 0;

   for (int i = 0; i < moves.size(); i++) {
      int tmp = moves[i]-1;

      for (int j = 0; j < board.size();j++) {
         if (board[j][tmp]) {
            arr.push_back(board[j][tmp]);
            board[j][tmp] = 0;
            if (arr.size() > 1) {
               if (arr[arr.size() - 1] == arr[arr.size() - 2]) {
                  arr.pop_back();
                  arr.pop_back();
                  count += 2;
               }
            }
            break;
         }

      }
   }
   return count;
}

int main(void) {
   ios::sync_with_stdio(false);
   cin.tie(NULL); cout.tie(NULL);

   vector<vector<int>> board = { { 0, 0, 0, 0, 0 },{ 0, 0, 1, 0, 3 },{ 0, 2, 5, 0, 1 },{ 4, 2, 4, 4, 2 },{ 3, 5, 1, 3, 1 } };
   vector<int> moves = { 1, 5, 3, 5, 1, 2, 1, 4 };
   cout << solution(board, moves);

   int n;
   cin >> n;

   return 0;
}
~~~

<br/>


<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>