---
title: "Coding Test of Kakao Internship Practice Test # 2"
categories: 
  - Programmers
last_modified_at: 2020-03-29T16:1:00+09:00
toc: true
---

프로그래머스 카카오 인턴십 코딩테스트 실전 모의고사 2번 문제 풀이합니다.<br/>

저는 미리 신청을 안해놔서 ㅠㅠ 같이 오프라인 알고리즘 스터디하는 분들하고 문제 공유하며 풀어본 거라서 기본 테스트케이스는 통과되는 것 같은데 삼중 포문이라(부끄럽네요..ㅎㅎ) 아래 코드로 숨은테스트 케이스 통과가 잘 되었을지는 의문입니다.<br/>
코드스멜이 너무 심한 코드입니다..ㅎㅎ<br/>

<br/>

Source Code : 
~~~
#include <iostream>
#include <string>
#include <vector>

using namespace std;

vector<int> solution(string s) {
   vector<int> answer;
   vector<vector<int>> tmp;

   for (int i = 1; i < s.size()-1; i++) {
      if (s[i] == '{') {
         i++;
         vector <int> innerTmp;
         int j = i;
         for (; s[j] != '}' && s[j] != ','; j++) {
            string tmpStr = "";
            if (s[j] == ',') {
               continue;
            }

            int l = j;
            for (; s[l] != ',' && s[l] != '}'; l++,i++,j++) {
               tmpStr += s[l];
            }
            /*if (s[j] == ',') {
               continue;
            }
            else {
               innerTmp.push_back(s[j]-'0');
            }*/
            innerTmp.push_back(atoi(tmpStr.c_str()));
         }
         tmp.push_back(innerTmp);
      }
      else {   // ','
         continue;
      }
   }
   /*
   int minIdx = 0;
   for (int i = 1; i < tmp.size(); i++) {
      if (tmp[i].size() >tmp[minIndx].size())
   }*/
   for (int k = 1; k <= tmp.size(); k++) {
      int i;
      for (i = 0; i<tmp.size(); i++) {
         if (tmp[i].size() == k) {
            break;
         }
      }
      for (int j = 0; j < tmp[i].size(); j++) {
         for (int l = 0; l < answer.size(); l++) {
            if (tmp[i][j] == answer[l]) {
               tmp[i][j] = 0;
            }
         }
         if (tmp[i][j] != 0) {
            answer.push_back(tmp[i][j]);
         }
      }
   }

   return answer;
}

int main(void) {
   ios::sync_with_stdio(false);
   cin.tie(NULL); cout.tie(NULL);

   //string s = "{{2}},{2,1},{2,1,3},{2,1,3,4}}";
   //string s = "{{1,2,3}},{2,1},{1,2,4,3},{2}}";
   //string s = "{{20,111}},{111}}";
   //string s = "{{123}}";
   string s = "{{4,2,3}},{3},{2,3,4,1},{2,3}}";
   vector<int> answer = solution(s);
   
   cout << "[" << answer[0];
   for (int i = 1; i < answer.size(); i++) {
      cout << ',';
      cout << answer[i];
   }
   cout << "]";

   int n;
   cin >> n;

   return 0;
}
~~~

<br/>


<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>