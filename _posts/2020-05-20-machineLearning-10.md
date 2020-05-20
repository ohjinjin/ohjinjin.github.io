---
title: "Support Vector Machine_Machine Learning(10)"
categories: 
  - MachineLearning
last_modified_at: 2020-05-20T23:28:00+09:00
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

* [Machine Learning(6) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-6/)<br/>

* [Machine Learning(7) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-7/)<br/>

* [Machine Learning(8) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-8/)<br/>

* [Machine Learning(9) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-9/)<br/>

이번 시간에는 SVM을 배웁니다.<br/>
머신러닝하는데 SVM 모르면 안됩니다.<br/>
<br/>

SVM(Support Vector Machine)
---
SVM의 motivation을 보겠습니다.<br/>

SVM은 Supervised learning 의 classification 문제 해결모델입니다.<br/>

그래서 데이터를 잘 나누는 Decision boundary를 찾아주는 것이 목적인데요,<br/>

SVM에서 찾고자 하는 decision boundary는 
서로 다른 클래스 간의 거리가 최대가 되게 하는 것입니다.<br/>

그래서 Max\-margin이라고도 부릅니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture94.JPG" alt=""> {% endraw %}

이 boundary는 두 개의 경계(노란선)의 중간선이 되며, '유일한' 두개의 경계선을 만족하기 위해서는 데이터의 feature 개수와 상관없이 최소 2개의 데이터가 노란 선에 위치해야합니다.<br/>
이 예제에서는 세개가 존재하네요.<br/>

점 두개간의 거리를 구할 때 직선으로 잇는 거리를 구하는 것과 같은 방식입니다. 어렵지 않아요.<br/> 

어쨌든 이 데이터(벡터)들을 Support Vector라고 부릅니다.<br/>

Decision boundary를 표현하는 수식은 아래와 같습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture95.JPG" alt=""> {% endraw %}

Decision boundary에 정확히 위치한 데이터를 위 수식에 대입했을 때만이 =0을 만족합니다.<br/>

위 수식을 이해하기 위한 선형대수학 기초지식을 아래에 실어드립니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture96.JPG" alt=""> {% endraw %}

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture97.JPG" alt=""> {% endraw %}


SVM의 분류방법
---
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture98.JPG" alt=""> {% endraw %}

Decision boundary에 데이터를 적용한 '부호'로 판별합니다. 임의의 데이터 (벡터)u를 decision boundary 수식에 적용하면, 벡터w*벡터u+b <0이 되므로 '\-' 클래스로 분류가 됩니다.(이 때 *는 곱하기가 아닌 다트연산을 의미합니다.)<br/>

더 정확히 표현하자면 boundary 까지의 '거리' 개념을 도입하여 설명합니다.<br/>
벡터u를 벡터w에 projection 하고 나서, 그 길이가 boundary까지 닿는가 안닿는가를 보는 것입니다.<br/>

좀더 formal 하게 정리하면, boundary와 노란색 선까지의 거리를 1이라고 가정하여 아래와 같이 수식을 세울 수 있겠습니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture99.JPG" alt=""> {% endraw %}

전자에 해당하면 \-, 후자에 해당하면 \+ 클래스로 분류되겠지요.<br/>

잘 분류해낼 수 있는 SVM을 얻기 위해서는 데이터를 기반으로 학습과정을 거쳐 w와 b를 계산해야합니다.<br/>

본격적으로 수식을 이해하기 이전에 앞서서 선형대수학의 기본 개념을 먼저 다지겠습니다.
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture100.JPG" alt=""> {% endraw %}

노란벡터에 대한 법선벡터 검정벡터를 구하는 과정을 보이고 있습니다.
내적 공식에 의하면 x의 norm * y의 norm * cos세타인데, cos세타는 사이각이 90일 때 0이고, 0도를 이룰때 1이 되지요. (이 때 *는 곱하기를 의미합니다)<br/>

법선벡터와 원벡터는 사이각이 90도 이므로 0을 갖게하는 법선벡터를 찾을 수 있게되는 것입니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture101.JPG" alt=""> {% endraw %}

이번엔 거리를 구하기 위한 과정을 보이고 있습니다.<br/>
벡터의 삼각공식이라고 하던가요?<br/>
한 벡터a의 종점이 다른 벡터b의 시점이 되는 경우 두 벡터의 합 연산의 해는 a의 시점을 시점으로 갖고 b의 종점을 종점으로 갖는 벡터 c가 되었었죠?<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture102.JPG" alt=""> {% endraw %}

이러한 위치벡터 w로 부터 그의 법선벡터인 g(x)를 구하는 것입니다.<br/>

Decision boundary에 정확히 위치한 데이터를 위 수식에 대입했을 때만이 =0을 만족하기 때문에
~~~
g(x)=r*w^t*w/|w|
~~~
가 되며 이 식을 r에 대해 정리하면 
~~~
r=g(x)*|w|
~~~
로 정리되는 것입니다.<br/>

이를 통해 두 데이터(벡터) x와 xp사이의 거리를 구할 수 있습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture103.JPG" alt=""> {% endraw %}

거리를 정의하는 곳을 보면 w 벡터에 사영시켜서 w축만을 기준으로 좌표값을 구해 차이를 구하고 있네요.<br/>
그리고 w 벡터의 크기로 나눕니다.<br/>
그림에서 보면 각 support vector로부터 decision boundary까지의 거리는 1이었으니 직선거리 2가 나왔을 것이구요.<br/>

max margin을 구하기 위해서는 직선거리(위 예제에서는 2)를 벡터w의 크기로 나눴을 때가 최대가 되려면 w의 norm은 최소값을 가져야한다는 말을 하고 있습니다.<br/>

최적화를 시키는 계산을 위해서 convex형태로 만들기 위해 제곱해주고 미분시 편의를 고려해 1/2를 곱해주었네요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture104.JPG" alt=""> {% endraw %}

loss함수 정의가 특이하지요.<br/>

아직 완전히 이해하지 못해서 더 공부하고 이 포스팅을 갱신해두려고합니다.<br/>

(수정중)