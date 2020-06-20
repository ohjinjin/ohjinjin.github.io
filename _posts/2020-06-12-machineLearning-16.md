---
title: "Machine Learning(16)"
categories: 
  - MachineLearning
last_modified_at: 2020-06-12T23:18:00+09:00
toc: true
published: false
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

* [Machine Learning(6) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-6/)<br/>

* [Machine Learning(7) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-7/)<br/>

* [Machine Learning(8) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-8/)<br/>

* [Machine Learning(9) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-9/)<br/>

* [Machine Learning(10) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-10/)<br/>

* [Machine Learning(11) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-11/)<br/>

* [Machine Learning(12) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-12/)<br/>

* [Machine Learning(13) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-13/)<br/>

위 링크들 중 ANN 모델에 대한 설명은 Machine Learning(9)에 있습니다.<br/>
<br/>


토픽모델링에 대해서 한 번 더 설명하겠습니다.

LDA라는 모델을 보고있는데요, 그구조가 이렇게 생겼습니다.

우ㄱ리가 분석해야할 이 문서들은 저 과정들을 통해서 만들어졌을 거야 라고 가설을 세웁니다.

그러한 생각을 모델로 설계를 한거죠.


저 자동차는 내부적으로 이렇게 이렇게 생겼을거야 하고 짐작하는거에요. 실제로자동차 내부를 본적도 없으면서 외관만 보고 가정해가는 것이지요

 

사람마다 다르게 생각할 수 있겠죠?

다른 구조를 가진 모델로 설계를 할 수도 있는 거에요.

다른 아이디어나 관점에 의해서 설계를 하게 되는 것입니다.

그런데 그 데이터나 특성에 잘 맞아떨어졌다면 훌륭하져

 

LDA라는 모델은 최초 probability이다보니? 가장 많이 사용되며 graphical하게 보여줄 수 있습니다.

그럭저럭 괜찮게 잘 설계를 했기 때문입니다.

 

 

이미 외관을 이미 보고 있다구. 아직 자동차가 없다고 생각하고 이렇게이렇게하다보면 바퀴가 돌아가는 걸껄? 이런 가정을 하는거거든여?

 

지금 이런 단어들이 없다고 가정을 하고 한장한장 살펴볼거에ㅛ??

전체 범주?를 가정하고 단어들의 분포를 가정하고 토픽마다 있는거니까세타는ㅇㅇ 서로다른 분포가 있을거고 이게 이미 존재한다고 이미학습이 다 되어있다고 가정하는거에요.

Z가 단어마다 하나씩 존재하기 때문에 N이고

Z는 토픽을 이야기하는거고 w는단어를 말합니다. 먼저 토픽을 결정하고 단어를 결정하죠.

Planning 토픽이라고 골라내져 앞서 z가 플래닝이라고 가정하고  또 하고 또하고단어마다 ㅇㅇ

 

 

하지만 실제로는 도큐머트에 대한 세타와 파이값은 다 없고 uniform합니다.

서로가 똑 같은 분포를 가진상태로 시작한거야

오로지 단어만 가지고 ㅇㅇ 세타와 피들을 찾아가는거에요. 그래서 이게대단한겁니다.

여기서 하나 잼는걸 짚고넘어갈건데요

 

단어들만 주어졌을 텐데 어케 세타와 피를 구해나가는 것일까?

 

Z가 바로 그 역할을하게합니다.

왜 단어마다 굳이 토픽을 설정하게 하는걸까에 핵심이 있습니다.

Random variable로서 w라고되어있는 단어들만가지고 세타와 피를 찾아가게하는 핵심이 z입니다.

그래서 z가 단어마다 존재한는 것이며

각 단어마다 무슨토픽인지를 맞추게되는것이면 다된거야

 

세타는 문서에대한 토픽의 분포죠.

각단어마다 서로다른색으로 칠하면 문서내 토픽들을 취합하여 그 분포를 볼 수 있어지니까 끝난거잖아여

더 많이 나타난 단어들에 가중치를 더 크게 둘 수도 있는거지 않겠어요? 그러다보니z라는애를 통해서 세타와 피는 자동으로 구해집니다.

수식은 다 이해하지 않아도 마지막에 z로부터 세타와 파이를 구하게된다는것이죠.

Doument1에서 나온 단어들간의 순서는 중요하지 않아요

단어들간 서로의 상대적인 위치를 전혀 고려하지 않아

Bag of words 단어의 가방

LDA는 도규먼트를 백오프워드로 취급합니다

 

 

실습오렌지

현업에서 데이터를 수집해야한느 시점이 되었다 하면

가장 안전한 방법은 가능한 많은 데이터 feature들을 확보하는것입니다.

나중에가서 새로운 feature하나 추가하려면 다 없애야해여 그전관측값들은

 

merge해서 쓰는 경우랑 무슨 차이가 있을까요?

우리가 두개의 테이블이있음 join해서 가로로 merge 할 때 기준 열이 있어야하자나

merge하여 가로로 추가한다고 하면 feature를 추가하는 셈이 되는 것 같은데 어느 한 기준열이 같다고하면 새로 수집하지 않아도 된다는 것

 

 

EM,GMM

EM 알고리즘 보고 히든마코프? 봅니다.

 

어려울 거에요. 정말 머신러닝스러운 것들을 배우는 거에요.

EM을 설명하면서 동시에 gMM을설명할 거에요 GMM은 클러스터링에 쓰이는 기술입니다. GMM을이용해학습시킬 수 있는 알고리즘이 EM알고리즘입니다.

이거 배우다보면 토픽모델 LDA에서 z를 구하면 나머지를 구하게 되는 것과 비슷한 내용을 볼 수 있게 됩니다.

 

EM 알고리즘의 간단한 예제

영화추천을 가정하고 예제를 살펴봅시다. 영화가 만족스러웠으면 1 아니면 0으로 표기합시다.

K가 영화의 총 개수입니다.

홍길동이라는 사용자가 1,2,3번 영화를 보고나서 각각 101점을 줬습니다.

남은 두가지 영화들은 어떻게 평가를 할지에 대한 확률값을 계산하여 추천을 하게 될 겁니다.

P(y4=1 | y1=1,y2=0,y3=1)과 P(y5=1 | y1=1,y2=0,y3=1)를 구하는 것잊.

Joint Probability는 아래와 같이 정의됩니다.

P(y1=a,y2=b,y3=c,y4=d,y5=e):=파이abcde

a~e는 각각 1또는 0 값을 갖게됩니다.

 

E-step에서는 파이값을 이용하여 conditional probability를 계산하게 됩니다.


M-step에서는 Jointprobability를 이용해 파이값을 업데이트하게 됩니다.

E-step과 M-step을계속 반복하면, 수렴(coverage) 상태에 다다르게 됩니다.

그래서 이것도 iterative에요.

이 예제에서의 Em 알고리즘의 목표는 결국 파이를 계산하여 얻는 것을말합니다.

 

Expectation Maximization Algorithm도 Likelihood 최대화시키는 파라메터 찾기가 목적입니다. 그래서MLE랑 알고리즘이랑 같아보일 수 있습니다.

하지만 MLE는 최적 파라메터를 직접 계산한다면,  EMdms E-step, M-step을반복(iterative process)하여 파라메터를 점차적으로 최적화하게됩니다.

MLE로 직접 계싼하기 어려운 경우에 사용되게 됩니다. 예를 들면 미분 불가하다거나, 모델이 복잡한 경우(mixture model) 즉 convex형태가 아닌 경우에 해당합니다.

 

 