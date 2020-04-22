---
title: "SVD_Machine Learning(6)"
categories: 
  - MachineLearning
last_modified_at: 2020-04-22T22:18:00+09:00
toc: true
---

Intro
---
학교 수강과목에서 학습한 내용을 복습하는 용도의 포스트입니다.<br/>

기존에 수강했던 인공지능과목을 통해서나 혼자 공부했던 내용이 있지만 거기에 머신러닝 수업을 들어서 보충하고 싶어서 수강하게 되었습니다.<br/>

gitlab과 putty를 이용하여 교내 서버 호스트에 접속하여 실습하는 내용도 함께 기록하려고 합니다.<br/>

* [원격 실습환경구축 따라하기](https://ohjinjin.github.io/git/gitlab/)<br/>

* [Machine Learning(1) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-1/)<br/>

* [Machine Learning(2) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-2/)<br/>

* [Machine Learning(3) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-3/)<br/>

* [Machine Learning(4) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-4/)<br/>

* [Machine Learning(5) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-5/)<br/>

이번 주제는 SVD에 대한 theory입니다.<br/>
<br/>

SVD에 대해 배우기 전에 선수 지식으로 Linear Algebra의 기반 지식들을 정리하고 갑니다.<br/>


Linear Algebra 배경지식
---
1. 기저, 좌표계<br/>
임의의 벡터집합 S에 속하는 것들이 서로 1차 독립이면서 어떤 벡터공간 V를 생성하면, S를 V의 **기저**라고 합니다.<br/>좌표계가 생성되지요.<br/>

우리가 흔히 알고있는 2차원 좌표계의 기저는 x축과 y축이되며, 3차원 좌표계의 기저는 x,y,z축이됩니다.<br/>

2. 고유값, 고유벡터<br/>
행렬 A에 대해서 Ax = 람다 x를 만족할때
람다는 고유값(scalar), x는 고유벡터입니다.<br/>
우리는 고유값과 고유벡터를 사용함으로써 해당 기저의 고유공간에서 확대/축소, 회전 등의 변환을 할 수 있습니다.<br/>

벡터v에 대해 어떤 transformation을 적용해서 나온 결과 벡터 v를 람다v라고 표현하고 있네요.<br/>
예제를 들어 한번 설명해보겠습니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture27.JPG" alt=""> {% endraw %}


아래 그림처럼 결과행렬은 고유값과 고유벡터로 표현해낼 수 있는 것입니다.<br/>
3은 우리가 구하는 첫번째 고유값이 됩니다.<br/>
우리가 곧 배울 SVD, EVD, PCA, spectral clustering, Eigenface 등 많은 곳에서 응용될 것이기 때문에 기초적으로 알고 계셔야합니다.<br/>


3. Rank<br/>
* Column Rank : 선형독립인 열 벡터의 최대개수<br/>
* Row Rank : 선형독립인 행 벡터의 최대개수<br/>
행렬의 Rank를 구하기 위해서는 행사다리꼴로 정의한 이후에야 비로소 한눈에 보실 수 있습니다.<br/>

(수정중)
