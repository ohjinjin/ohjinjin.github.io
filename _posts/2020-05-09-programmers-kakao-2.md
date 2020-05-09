---
title: "Coding Test of Kakao Internship 2020 # 2"
categories: 
  - Programmers
last_modified_at: 2020-05-09T18:07:00+09:00
toc: true
---

프로그래머스 카카오 인턴십 코딩테스트 2번 문제를 풀이합니다.<br/>

<br/>

Source Code : 
~~~
#include<iostream>
#include<vector>
#include<algorithm>
#include<queue>
#include<string>
#include<set>
#include<map>
#include<cmath>
#include<stack>
#include<utility>
#include<string.h>
#include<sstream>

#define INF 210000000
#define SIZE 100005

using namespace std;

vector<string> per;
string fir, sec, thi;

long long solution(string expression) {
    long long answer = 0;
    int size = expression.size();

    //*, +, - 경우의 수 순열로 만듬
    per.push_back("*");
    per.push_back("+");
    per.push_back("-");

    //next permutation 사용
    do {
        vector<string> ex; //각각 숫자와 연산자를 벡터에 저장
        string str;

        //나온 순서대로 우선순위 정함
        fir = per[0];
        sec = per[1];
        thi = per[2];

        //문자열을 나눔 +, -, *가 나오기전까지 각각에 자릿수를 문자열로 합침
        for (int i = 0; i < size; i++) {
            if (expression[i] != '+' && expression[i] != '-' && expression[i] != '*') {
                str += expression[i];
            }
            else {//연산자 나오면 합쳐놓은 문자열과 연산자를 벡터에 담음
                ex.push_back(str);
                if (expression[i] == '+') {
                    ex.push_back("+");
                }
                else if (expression[i] == '-') {
                    ex.push_back("-");
                }
                else if (expression[i] == '*') {
                    ex.push_back("*");
                }
                str = "";
            }
        }

        ex.push_back(str);
        int len = ex.size();
        long long val; // 계산된 값

        //연산자가 나오면 연산자 앞 숫자와 뒷 숫자를 연산자에 맞게 계산하고
        //앞숫자, 뒷숫자, 연산자 3개를 지우고 연산된 수로 변경
        //연산자 순서대로 3번 계산
        for (int i = 0; i < ex.size(); i++) {
            if (fir == ex[i]) {
                if (fir == "*") {
                    val = stoll(ex[i - 1]) * stoll(ex[i + 1]);
                }
                else if (fir == "+") {
                    val = stoll(ex[i - 1]) + stoll(ex[i + 1]);
                }
                else if (fir == "-") {
                    val = stoll(ex[i - 1]) - stoll(ex[i + 1]);
                }
                ex.erase(ex.begin() + (i - 1), ex.begin() + (i + 2));
                if (i == 0) {
                    ex.insert(ex.begin(), to_string(val));
                }
                else {
                    ex.insert(ex.begin() + (i - 1), to_string(val));
                }
                i = 0;
            }
        }

        for (int i = 0; i < ex.size(); i++) {
            if (sec == ex[i]) {
                if (sec == "*") {
                    val = stoll(ex[i - 1]) * stoll(ex[i + 1]);
                }
                else if (sec == "+") {
                    val = stoll(ex[i - 1]) + stoll(ex[i + 1]);
                }
                else if (sec == "-") {
                    val = stoll(ex[i - 1]) - stoll(ex[i + 1]);
                }
                ex.erase(ex.begin() + (i - 1), ex.begin() + (i + 2));
                if (i == 0) {
                    ex.insert(ex.begin(), to_string(val));
                }
                else {
                    ex.insert(ex.begin() + (i - 1), to_string(val));
                }
                i = 0;
            }
        }

        for (int i = 0; i < ex.size(); i++) {
            if (thi == ex[i]) {
                if (thi == "*") {
                    val = stoll(ex[i - 1]) * stoll(ex[i + 1]);
                }
                else if (thi == "+") {
                    val = stoll(ex[i - 1]) + stoll(ex[i + 1]);
                }
                else if (thi == "-") {
                    val = stoll(ex[i - 1]) - stoll(ex[i + 1]);
                }
                ex.erase(ex.begin() + (i - 1), ex.begin() + (i + 2));
                if (i == 0) {
                    ex.insert(ex.begin(), to_string(val));
                }
                else {
                    ex.insert(ex.begin() + (i - 1), to_string(val));
                }
                i = 0;
            }
        }

        //연산자 우선 순위대로 식 계산해서 나온 값과 answer값 중에 max값 찾아 넣음
        answer = max(answer, abs(stoll(ex[0])));

    } while (next_permutation(per.begin(), per.end()));

    return answer;
}
~~~