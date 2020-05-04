---
title: "Perceptron_Machine Learning(8)"
categories: 
  - MachineLearning
last_modified_at: 2020-05-04T21:19:00+09:00
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

이번 시간에는 딥러닝 기술의 시초였던 퍼셉트론을 배웁니다.
<br/>

Perceptron
---
사람을 생물학점 관점으로 보았을때 Neuron 을 모방한 것이 바로 퍼셉트론의 착안점입니다.
<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture65.JPG" alt=""> {% endraw %}

생물학적 관점에서의 뉴런은 덴드라이트를 통해 전기신호가 전달되어온다고합니다.<br/>
여러 덴드라이트로 부터 들어온 전기신호를 시냅스를 통해서 통합하여 그 신호가 임계값 이상이되면 액슨을 통해 다음 시냅스로 전달됩니다.<br/> 전기신호가 전달되는 정도는 시냅스의 굵기와 비례합니다.<br/>

여기서 통합하는 부분이 바로 Perceptron에서의 Net input function입니다.<br/>
입력되어오는 n개의 x에 대해서 feature들이 n+1개의 weight와 곱하여 summation 되어 하나의 신호로 통합합니다. 왜 n+1이냐하면, 마지막 한 개는 bias이기 때문입니다.(prior 역할이에요)<br/>

Acritvation function은 순 입력함수에서 나온 결과 scalar value으로부터 특정임계값과 비교해서 최종 결과값을 생성하는 임의의 함수를 말합니다.<br/>
아주 간단하게는 threshold보다 작으면 -1 크면 1의 결과값을 생성하는 함수로 예를 들 수 있습니다.<br/>
그렇게 나온 최종결과가 바로 예측값인데, 이 값과 실제값이 다를 경우 weight를 개선시킬 필요가 있다고 판단하고 개선하며 학습이 이루어지는 것이지요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture62.JPG" alt=""> {% endraw %}

Perceptron은 뉴런의 임계값과 비교하는 부분을 생략하여 간단하게 표현한 세 개의 층(입력층, 중간층, 출력층)을 가지는 구조를 말합니다.<br/>

단층 퍼셉트론과 다층 퍼셉트론(인공신경망)의 차이는 중간층이 몇 개있냐 입니다.<br/>

전단계의 층과 다음 단계 층 두 layer의 전체 노드와 빠짐없이 연결되어있으면 fully connected layer라고 합니다.<br/>

출력층도 입력층도 아닌 계층을 중간층 또는 은닉층이라고 합니다.<br/>
입력과 출력층은 지도학습이기때문에 다 오픈되어있지만, 은닉층은 어떤 입력을 받아 어떤 출력을 뱉게되는지 그 내용을 알수가 없지요. 그래서 은닉층(hidden layer)라는 별명이 붙게되었습니다.<br/>

W0을 bias라고 하고 W1~Wn을 n-dimensional input이라고 가정합시다.<br/>
이 모델은 입력층의 값들을 하나의 신호로 통합한 후, 이를 바탕으로 출력 값을 생성하는 forword passing으로 계산해나갈 것입니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture66.JPG" alt=""> {% endraw %}

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture67.JPG" alt=""> {% endraw %}

앞서 살펴본 퍼셉트론 학습알고리즘은 학습이 진행될 때 데이터의 오차 정도를 고려하지 않고 무조건 빼거나 더하므로, 최적의 W(파라메터)를 찾지 못할 수도 있습니다.<br/>
그래서 perceptron 학습 알고리즘에 variation을 적용하게 됩니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture68.JPG" alt=""> {% endraw %}

바로 학습률(learning rate)이라는 하이퍼 파라미터를 넣어주는 것입니다.<br/>
학습률을 이용하면 오버슈팅으로 인한 발산의 경우나 핑퐁핑퐁하게되어 최저점에 수렴하지 못하는 경우들도 방지할 수 있게 되지만, 간혹 학습률이 지나치게 작을 경우에는 오히려 과적합이 될 가능성도 있기때문에 하이퍼파라미터를 잘 조절해주어야합니다.<br/>

퍼셉트론은 지도학습 모델중 하나입니다.<br/>
왜냐하면 마지막층에 정답레이블과 비교를 하잖아요? 오차도 거기서 나오구요.<br/>

단층퍼셉트론은 선형 패턴만을 풀수 있습니다.<br/>수식으로 보면 직관적으로 이 말을 이해할 수 있습니다.<br/>
그래서 XOR 문제는 풀 수 없습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture63.JPG" alt=""> {% endraw %}

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture69.JPG" alt=""> {% endraw %}

네트워크라고 해서 다 같은 네트워크가 아닙니다. 뉴럴 네트워크와 먼저 배웠던 베이즈 네트워크를 비교해봅시다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture64.JPG" alt=""> {% endraw %}

feed-forward라는 점에서 generative하다고 말할 수 있으며, 같은 층끼리는 간선이 있을 수 없다는 점이나, 기본적으로 설명이 불가능하다는 점에서 둘은 연관된 것처럼 보입니다.<br/>

