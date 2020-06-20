---
title: "Machine Learning(18)"
categories: 
  - MachineLearning
last_modified_at: 2020-06-20T23:27:00+09:00
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

Feature 값의 scaling 방법은normalization과 standardization이있습니다.

 

L1,L2 regularization위해서는 feature normalization을 해줘야합니다.

Standardization은 Normal분포의 standard derivation 값을 가지고 변환시키는 방법을 말합니다.

 

Missing feature value가 있는경우 그들을 다루는 일반적인방법은 아래와 같습니다.

Distance 값이 0~1사이라고가정할 때 Categorical (nominal) feature 두 데이터 중 한쪽이라도 missing이면 1을 주고

Numerical feature의 경우에는 ㅇㅇㅇ

 

Imputation algorithm의 한 종류인 KNN은 k값이 성ㄴ능을 좌우하는 알고리즘이져

 

Entropy 기억나시죠?

Discrete case가 있고 Continuouscase가 있습니다.

 

KL(Kullback-Leibler) Divergence를 Relative entropy라고도 부릅니다. KL divergence는두개의 distribution 간의 차이를 measure하는것으로 같으면 0 다를수록 커집니다.

차이라는 말이 애매하지만 거리개념은 아니랍니다.

 


크로스엔트로피에서 자기자신 엔트로피를 뺀다는 것은 얼마나 잘섞여있고 정리되어있는가를 측정할 도구가 되는 것입니다.

엔트로피가 정보량이 많다 적다를 나타내는 값이었죠?

식이 저렇게 되다보니까 뭐에서 뭘빼냐는 것에 따라 달라집니다.


그렇기 때문에 거리의 개념으로 보기엔 애매합니다.

그래서 relative entropy라고 부르는 겁니다

Mutual information은 두 개의 random variable 들이 얼마나 의존적인지를 measure합니다.


얼마나 차이가 나니를 보는 거거였잖아요? 앞에껀 joint probability고 뒤에는 따로따로 존재하는 텀이잖아요? 그럼결국 의미하는 것은 ‘독립’성에 비해 얼마나 ‘의존’성이 강한지를 측정하고자하는 것이지요.

 

우리는 kl divergence가 뭐엿는지를 잘 기억해야합니다.


이거에 대한 자세한 수식은 바로 뒷장에 있어여

(12슬라이드 사진)

 

 


잘 떠올려보세요 EM LDA 이런알고리즘들 사이에서 우린 봤어요 Z라는 variable은 값이 계속 변할 수 있잖아 그건 말 그대로변수거든여 그런 식으로 샘플링해서 생기는 값을 random variable이라고하는 것입니다.

 

우리가 Hierarchical Clustering를 정리해봅시다

이 모델의 장점은 시각적 관점으로 해석하기에 아주 용이한 덴드로그램으로 표현해낼 수 있다는 것입니다. 또한 쉽습니다.

단점은 O(n^2)의 부담스러운 시간복잡도를 갖는다는 점입니다. 또한 계층적이라는 구조 특성상 앞선 단계에서 오판단을 할 경우 수정할 수 없다는 것입니다.

 

우리 배웠던 군집별 정책 중 Averagelink 방식이 가장 성능이좋았다는 연구결과가 있다합니다. 거의 대부분의 군집화 알고리즘들이 겪는 문제로 군집 개수를 결정하는문제가 있습니다.

ㅇㅇㅇ

 

 

GMM 11번슬라이드부터..

Uniform distribution으로 초기 파라메터 세타를 주고 Estep, Mstep을 거쳐서 반복하며 optimal한세타값을 구해갑니다.

 

Initial guess

EM 알고리즘은 global optimal을 구하게된다는 보장은 없습니다. Local optimum을 얻게되는 것이죠.그러다보니 초기값 영향을 크게 받습니다.

뮤값들 두개를 무작위로 선택하여 초기화할 수도 있고

그로부터 시그마값들은 초기화를 시킬 수 있겠죠? 그리고 파이를 0.5로 둠으로써 Estep에 진입합니다. Estep에서는 새로운 감마i를 구할거에요 감마i는 세타가 고정된 상황에서의 Z값 계산으로 조건부 확률에 의해 계산이이루어집니다.

 

교수님 11번 슬라이드에서 알고리즘 수도코드쪽  설명해주시다가 Uniformdistribution으로 초기 파라메터 세타를 준다고 했었잖아요? 이때 말하는 uniform 이라는게 단일값으로 통일시킨다는 건가여?

Uniform distribution을 찾아보면 알겨

단일값통일이라고 할수도 있고

예를들어 떡볶이를 친구들하고 먹었어요 3000원이 나왔는데n빵하는 상황을 uniform distribution이라고 합니다.

균등하게! 그게 uniform distribution입니다.

 


베이즈 이론에 의해 도출된 식전체는 Likelihood를 말합니다. 파란색은 Ci=1 인 경우에 해당하며 검정색은 Ci=2인 경우에 해당합니다.

분자에서 파이는 Gaussian 1일 자체 확률을 말하며 뒷부분은 얼마나 그럼직한지를 normal distribution에 의해 표현하고 있는거야.

이렇게 감마에 대해 구해서 Estep이 끝났어여

i번째 감마를 구하긴했지만 n개의 데이터가 있으면n개의 감마가 나오게됩니다.

사용되는 파라메터들 5개가 모두 사용되지요

이미 주어져있다고 가정하는거에요. 우리가 초기값을 줬으니까요!

특히 세타를 고정시키고 감마를 구했어요

Mstep에서는 이 세타를 구하게됩니다.

Estep에서 구한 감마를 고정시키고 세타를 구합니다.


알고리즘의 이름처럼 기대값을 최대화시키는 세타를 구한다는 것을 알 수 있습니다.

지금 파라메터 세타 안에 다섯개가 들어있잖아요?

그 중 뮤 1을 구하는 과정을 먼저 봅니다


=0로 두고 미분해서 구하고 있습니다.

감마의 값이 실수가 아니라 0또는 1이라고 생각해봅시다. 1번클러스터에 해당하는 애들만 다더하라는 거에여 Weight를 크게해서더하므로(Weighted sum) 그게 평균이 되는거에요

 

M1에 대해서 argmax하자나여

세타 전개 두번째줄수식보면 일반화해서 쓴거고

그걸 구체적으로 뮤원에 대해쓴게 for 뮤1 바로밑줄식이에요

미분해서 0으로 놓고 전개하면 저식이 나온다는겨

그렇게 비슷한방법으로 다섯개의 파라미터들을 다 구하고 다시 estep으로 가서 감마를 갱신시킵니다….

 

한걸음씩 가다가 특정 종료조건에 다다르면 학습을 그만하는거져

 

의외로 GMM이 음성인식에서 많이 사용됩니다

 

HMM(Hidden Markov Model)

뭐가 숨겨졌다는걸까여?

HMM은 군집화 모델이 아닙니다

과거의 경험(sequential pattern)을 토대로 현재의 의사결정을하는 것이 Markov에 대한 직관입니다!

이를 테면 친구와 가위바위보를했는데 계속비겨왔어요 저친구가 가위를 내지 않을까?하는느낌과 오늘 해가 떴는데 내일부터 3일간 날씨가 해-비-해일 확률은 얼마일까? 같은것들이요

 

여태봐온 군집화나 분류 문제들과는 조금 다른 이런 순서를 가진 패턴에 대해서 배울 수 있는거져