---
title: "SVD_Machine Learning(6)"
categories: 
  - MachineLearning
last_modified_at: 2020-04-22T23:11:00+09:00
toc: true
---

Intro
---
학교 수강과목에서 학습한 내용을 복습하는 용도의 포스트입니다.<br/>
그래서 이 글은 순천향대학교 빅데이터공학과 소속 정영섭 교수님의 "머신러닝" 과목 강의를 기반으로 포스팅합니다.<br/>

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
참고로 1xn이나 nx1 행렬은 열벡터 또는 행벡터라고 부를수 있게되어서 그러한 행렬은 벡터라고 혼용해서 칭합니다.<br/>
우리는 고유값과 고유벡터를 사용함으로써 해당 기저의 고유공간에서 확대/축소, 회전 등의 변환을 할 수 있습니다.<br/>

벡터v에 대해 어떤 transformation을 적용해서 나온 결과 벡터 v를 람다v라고 표현하고 있네요.<br/>
예제를 들어 먼저 한번 설명해보겠습니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture27.JPG" alt=""> {% endraw %}


아래 그림처럼 결과행렬은 고유값과 고유벡터로 표현해낼 수 있는 것입니다.<br/>
[1 1 0]은 우리가 구하는 첫번째 고유벡터, 3은 우리가 구하는 첫번째 고유값이 됩니다.<br/>

고유벡터를 어떻게 구하는 방법이 궁금하실 겁니다.<br/>

어떠한 선형변환을 가하는 연산자 역할을 하는 것이 위 식에서 A 입니다.<br/>
고유벡터는 A 행렬을 곱함으로써 변환을 가하더라도 그 결과가 자기 자신 고유벡터로서 다시금 표현이 가능해야합니다.<br/>
그말인 즉슨, 변환 전의 벡터와 A를 적용해서 변환을 가한 후의 벡터가 서로 평행한 관계라는 조건을 갖는 것이 고유벡터가 가질 조건이라는 뜻 입니다.<br/>

평행하기 위한 조건은 또 무엇일까요? [1 1]과 [3 3]은 평행합니다.<br/>
[1 1]과 [-3 -3] 역시 평행합니다. 역방향 벡터더라도 몇배의 실수배를 하던지 간에 절대 접점이 없다면 평행하다 말할 수 있습니다.<br/>

이러한 조건을 만족하는 특수한 벡터가 바로 고유벡터인데, 일반적으로 임의의 정방행렬 nXn인 A 행렬에 대한 고유벡터는 n개입니다.<br/>

그래서 아래의 또 다른 예제를 보시게되면요,<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture28.JPG" alt=""> {% endraw %}

2x2 정방행렬 연산자인 A에 의해 고유벡터가 v1, v2 두개 나온 것을 확인하실 수 있습니다.<br/>
A\*v1은 어떤실수배\*v1으로 표현이가능하며, 이때 어떤실수배는 3이라는 스칼라값이 됩니다!<br/>
A\*v2 역시 -1이라는 스칼라값으로 변환 전인 v2벡터로 표현이 가능합니다.<br/>

바로 이러한 스칼라값이 **고유값**입니다.<br/>

고유벡터(EigenVector)와 고유값(EigenValue)는 우리가 곧 배울 SVD, EVD, PCA, spectral clustering, Eigenface 등 많은 곳에서 응용될 것이기 때문에 기초적으로 알고 계셔야합니다.<br/>


3. Rank<br/>
* Column Rank : 선형독립인 열 벡터의 최대개수<br/>
* Row Rank : 선형독립인 행 벡터의 최대개수<br/>
행렬의 Rank를 구하기 위해서는 행사다리꼴로 정의한 이후에야 비로소 한눈에 보실 수 있습니다.<br/>

(수정중)
