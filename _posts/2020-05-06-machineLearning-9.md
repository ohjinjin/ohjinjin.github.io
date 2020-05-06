---
title: "Artificial Neural Network_Machine Learning(9)"
categories: 
  - MachineLearning
last_modified_at: 2020-05-06T15:10:00+09:00
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

이번 시간에는 지난 시간 배웠던 퍼셉트론을 기반으로 ANN, 인공신경망을 배웁니다.
<br/>

ANN(Artificial Neural Network)
---
Neural Network를 우리말로는 신경망이라고 부릅니다.<br/>
ANN은 뇌세포를 본따 만들어진 '퍼셉트론'으로 이루어진 네트워크입니다.<br/>
그리고 사람이 만든 뉴런들의 네트워크입니다. 그래서 인공신경망이라고 말합니다.<br/>

중요한 특징들이 있습니다.<br/>
첫째로는 블랙박스같다는 것이죠. 그래서 의사결정나무처럼 명확한 의사결정 규칙이 보이지 않지만 많은 분야에서 훌륭한 성능을 보이고 있습니다.<br/>

중요한 특징 두번째는 feed-forward로, 한 쪽 방향으로 흘러간다는 것입니다.<br/>
보통 1개 이상의 hidden layer를 갖습니다.<br/>
hidden layer의 개수가 많을 수록 deep한 neural network가 되는 것입니다.<br/>
딥러닝이라는 말도 여기서 파생된것이지요.<br/>

하나하나의 노드가 퍼센트론이라고 보시면됩니다<br/>.
그리고 각 층들의 입장에서봣을때 좌우에 있는 모든노드들과 연결된것을 fully connected이다라고 말합니다.<br/>

그리고 같은 층 사이에는 연결이없는데 이러한 그래프를 bi-partite graph라고 합니다.<br/>

입력이있고 출력이 있는 것은 알겠는데 이 hidden layer는 무엇일까요?<br/>
질문을 바꿔서 입력에서 바로 출력으로 간다면 어떤 문제가 있을까요?<br/>
지난시간 잠시 보았던 것처럼 XOR와 같은 비선형 문제를 풀 수 없습니다. 단순한 선형 문제만을 풀 수 있어지죠.<br/>
이러한 단층 퍼셉트론의 선형문제만을 풀지못한다는 단점을 이슈화해서 머신러닝의 암흑기가 찾아오기도했었지요.<br/>

멀티레이어 네트워크는 한층한층 오른쪽으로 갈수록 즉 출력층으로 갈수록 모종의 집약된 또는 점점 더 고도화된 정보만을 보고 판단하는 것으로, 비선형 문제 해결에 접근할 수 있습니다.<br/>
선형으로 분류가 안되는 케이스는 단층이 아닌 다층 신경망을 적용하면 해결이 가능합니다.<br/>
모델이 고차원의 패턴을 인지할 수 있는 것입니다.<br/>


{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture70.JPG" alt=""> {% endraw %}

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture71.JPG" alt=""> {% endraw %}

<br/><br/>

Activaiton Function
---
하지만 multi-layer이기만 하면 될까요?<br/>
linear한 것들을 통합하는 함수가 여전히 linear하다면 linear한 것들을 아무리 여러개 모아봤자 소용이 없어집니다.<br/>
선형대수학적으로 이야기를 하자면 같은 차원끼리 덧/뺄셈을 해봤자 그 벡터의 차원이 달라지지 않는 것과 같습니다.<br/>
그래서 활성화함수(activation function)을 바꿔줄 필요가 있습니다.<br/>

선형합을 한 다음 비선형패턴도 풀어낼 수 있는 비선형함수를 활성화함수로서 사용해주어 해결합니다.<br/>
하지만 아무함수라고 다 되는것이 아니라 최적화를 위해 미분가능한 함수여야 합니다.<br/>

대표적인 활성화함수가 sigmoid입니다. 선형 활성함수로 썼던 gating function과 굉장히 비슷한 트렌드를 갖습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture72.JPG" alt=""> {% endraw %}

ANN을 분류문제에서 사용하는 경우 때문에 hidden layer에서는 sigmoid를 사용하고, output layer에서는 **softmax function**을 많이 사용합니다.<br/>
참고로 회귀문제에서는 f(x)=x 를 사용합니다.<br/>

softmax는 각 노드(출력층의 모든 노드는 각 클래스가 될 것임)에 대한 확률값을 주게 됩니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture73.JPG" alt=""> {% endraw %}

하지만 multi label 문제 해결에는 소프트맥스는 적적하지 않습니다. <br/>
그럴 때는 시그모이드를 아웃풋레이어에 사용하는 것이 더 낫기도 합니다.<br/>

이 소프트맥스함수는 지수함수이다보니 컴퓨터가 계산하다보면 오버플로우가 발생할 우려가 있습니다.<br/>
그래서 개선식을 사용하곤합니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture74.JPG" alt=""> {% endraw %}

활성함수의 입력값으로 사용되는 가중합(weighted sum)을 하는 이유는 무엇일까요? 그냥 더하면 안되는 걸까요? bias의 역할은 무엇일까요?<br/>

더 중요하고 덜 중요한 애들을 구분하여 더 똑똑한 결정을하기위해 가중치를 두는 작업의 핵심요소가 바로 weight입니다.<br/>

물론 은닉층에서의 각 노드가 무슨 역할일지 설명이 불가능하여 엔지니어가 직접 weight를 조정하기가 어려운 것이 사실이지만, 놀랍게도 ANN에서 학습이 진행되면서 정체가 뭔진 모르겠지만 특정 노드에 있어서 가장 적절한 weight를 찾아주게 됩니다.<br/>
이 말을 고급지게 표현하면 feature를 자동으로 학습한다 라고 표현할 수 있습니다.<br/>

노드 자체에 대한 중요도 즉 prior 정보를 주기 위해 사용하는 것이 bias입니다.<br/>

bias 역시 weight처럼 개선되게 됩니다.<br/>
wx+b로 표기하게 되니까 bias도 선형합을 할 때 함께 개선됩니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture75.JPG" alt=""> {% endraw %}

우리는 여태 배운 다른 분류기 머신러닝 모델을 적용할 때 feature 정의를 해주게됩니다.<br/>
sift니 surf(speeded up robust features)니 하는 feature를 예쁘게 뽑아내줄 툴도 개발이 되어있습니다.<br/>
이미지 데이터라고 하면 밝기 조절도 좀 해줘야하고 노출값도 만져줘야하고 그런 과정이 필요한 것이지요.<br/>

속된말로는 머신러닝 모델이 좋은 성능을 낼 수 있게 하게 엄청 노력해서 떠먹여줘야하는거에요.<br/>
그런데 딥러닝 모델은 (물론 떠먹여줘도되지만) 숟가락만 줘도 알아서 떠먹습니다.<br/>

하지만 왜 그런 결과가 나왔는지 설명할 수는 없지요..<br/>
explainable한 AI model 을 만드는 것이 현재 AI 세계의 공통 목표라고도 할 수 있습니다.<br/>

<br/><br/>

Weight Matrix and Bias
---
우리가 ANN을 쓰는 이유를 다시 상기시켜봅시다.<br/>
"패턴인지"였지요 그러려면 "패턴 학습"이 필요할 것인데, 학습이 되는 것은 뭘까요?<br/>
바로 각 층사이를 잇는 weight matrix입니다.<br/>
그리고 각 층의 bias 까지요!<br/>

1. weight matrix 의미와 역할
두 개 층의 각 노드쌍 사이의 관계 중요도입니다.<br/>
해당 노드쌍이 함께 등장한 빈도수(두 노드가 관측 가능한 경우)에 기반합니다.<br/>

2. bias 의미와 역할
각 노드 자체의 중요도로 해당 노드 빈도수(해당 노드가 관측 가능한 경우)에 기반합니다.<br/>

<br/><br/>

ANN 학습 : Backpropagation
---
관측가능한 값은 모델 특성상 Input, Output layer에만 존재하므로, 먼거리(?)에 놓인 이 두 개의 Layer 사이의 Co-occurrence 를 기반으로 weight matrix, bias들을 학습할 방법이 필요합니다.<br/>

ANN의 한계라고 할 수 있지요.<br/>
아래 캡처에서 알 수 있듯이 단순한 모델은 한번에 가능해요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture76.JPG" alt=""> {% endraw %}

ANN 모델 파라미터는 이런식으로 학습할 수는 없을까요?<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture77.JPG" alt=""> {% endraw %}

층이 깊어질 수록 성능이 더 좋다는 연구 결과가 있습니다.<br/>
하지만 바로 편미분을 하는건 네트워크가 깊어지면 깊어질수록 매우 어려워지겠지요?<br/>

그래서 수학적 체인룰을 적용합니다.<br/>
**backpropagation** 알고리즘이라고 부릅니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture79.JPG" alt=""> {% endraw %}
고등학교 이과수학 커리에서 배우셨을거에요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture78.JPG" alt=""> {% endraw %}

MSE는 Mean Squared Error이며, 교차엔트로피 오차는 CSE(Cost Entropy Error)입니다.<br/>

하지만 층이 너무나 깊게 형성되어있으면 역전파시에 1 이하의 값들이 곱해지다 보니 그라디언트 값이 입력층으로 갈수록 너무 미미해집니다.<br/>
이 현상을 **gradient vanish**라고 합니다.<br/>

이러한 문제들이 있다보니까 어떻게 더 효율적으로 층을 깊게 쌓을지에 대한 많은 연구들이 진행되고 있습니다.<br/>

(수정중)