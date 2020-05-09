---
title: "Coding Test of Kakao Internship 2020 # 1"
categories: 
  - Programmers
last_modified_at: 2020-05-09T18:03:00+09:00
toc: true
---

프로그래머스 카카오 인턴십 코딩테스트 1번 문제를 풀이합니다.<br/>

<br/>

Source Code : 
~~~
#include <string>
#include <vector>
#include <iostream>
#include <map>
#include <cstdlib>

using namespace std;


int getDist(int x, int y) {
   int distance = 0;
   int new_y = y;
   if (x < new_y) {
      if (new_y - x > 1) {
         while (new_y - 3 >= x-1) {
            new_y -= 3;
            distance++;
         }
      }
   }
   else {
      if (x - new_y > 1) {
         while (new_y + 3 <= x + 1) {
            new_y += 3;
            distance++;
         }
      }
   }
   distance += abs(new_y - x);

   return distance;
}


string solution(vector<int> numbers, string hand) {
   string answer = "";
   // map<string,string> currLoc;
   map<string, int> currLoc;

   // currLoc.insert(map<string,string>::value_type("L","*"));
   // currLoc.insert(map<string,string>::value_type("R","#"));
   currLoc.insert(map<string, int>::value_type("L", 10));
   currLoc.insert(map<string, int>::value_type("R", 12));

   for (int i = 0; i< numbers.size(); i++) {
      if (numbers[i] == 0) {
         numbers[i] = 11;
      }
      if (numbers[i] % 3 == 2) {    // 2,5,8,0
         int a = getDist(numbers[i], currLoc["L"]);
         int b = getDist(numbers[i], currLoc["R"]);

         if (a > b) {
            answer += "R";
            currLoc["R"] = numbers[i];
         }
         else if (a < b) {
            answer += "L";
            currLoc["L"] = numbers[i];
         }
         else {   // ==
            if (hand.compare("left") == 0) {
               answer += "L";
               currLoc["L"] = numbers[i];
            }
            else {
               answer += "R";
               currLoc["R"] = numbers[i];
            }
         }
      }
      else if (numbers[i] % 3 == 0) {   // 3,6,9
         answer += "R";
         //currLoc.insert(map<string, int>::value_type("R", numbers[i]));
         currLoc["R"] = numbers[i];
         continue;
      }
      else if (numbers[i] % 3 == 1) {  // 1,4,7
         answer += "L";
         //currLoc.insert(map<string, int>::value_type("L", numbers[i]));
         currLoc["L"] = numbers[i];
         continue;
      }
   }

   return answer;
}
~~~