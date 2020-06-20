---
title: "Machine Learning(15)"
categories: 
  - MachineLearning
last_modified_at: 2020-06-20T23:16:00+09:00
toc: true
published : false
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

여기서 사용되는 모든 것 들이 python에서 import해서 사용할 수 있어요

꽃의 무게에 따라서도 종류를 분석할 수 있을 것 같은데 하면 공부를 하는겨, 새로운feature를 발굴을 해내는 것입니다. 도메인 지식이 필요해요.

 

Missing value 다루기

날려버리거나 matrix completion 방법이 있습니다.

구멍을 완벽하게 메꿔준다라고 해서 matrix completion이라고부릅니다.

또는 mean값으로 채우는 것이요

 

Imputation 알고리즘도 missingvalue를 채워넣는 방법입니다.

https://github.com/epsilon-machine/missingpy

 

Missing value들은 채워 넣는 것이 항상 적절한 걸까?

MAR(Missing at Random) : 특정 변수(feature, variable)의 결측치들이 무작위로 발생

MCAR(Missing Completely at Random) : 완전히무작위로 결측치 발생

언제 채워 넣는 것이 좋고 언제 채우면 안되는 것인지에 대한 용어에요. MAR과MCAR 둘다 imputation해도 되는데 MNAR일 때는 하면 안됩니다

MNAR(Missing Not at Random)

 

 

딥러닝 모델 중에서 CNN(Convolutional NeuralNetwork)라는 모델이 있는데 이 모델은 주된 타겟이 바로 이미지입니다. 오늘 배우게되는 Topic Modeling은 바로 텍스트에 많이 사용되는 모델입니다.

토픽모델링을 위한 데이터를 만들어 줬어요. 그 문서를 읽고 사람은“아 이 문서는 OO에 관한 것이네”라고 알 수 있거든요.

그런데 엄청나게 많은 문서가 있다고 하면 언제 다 읽겠어요? 이 것이 motivation이 됩니다. 이를 대신 해주기 위한 모델이 바로Topic Model입니다.

토픽모델도 일종의 클러스터입니다.

클러스터 수가 3개로 설정되느냐 4개로설정되느냐에 따라 결과가 달라졌던 것처럼 토픽모델도 마찬가지 입니다.

그런데 서로 다른 토픽모델이 서로 다르게 카테고리화를 하게 된다 하면 결국 그 끝에는 사람이 선택하게 됩니다. 결정까지도 자동으로 해주는 기술도 나왔습니다.

 

좀더 디테일하게 들어가도록 하겠습니다.

 

LDA에 대해 배울 것입니다.LDA란 것은 이전에 앞서 배웠던 Linear Discriminant Analysis가아니고 Latent Dirichlet Allocation입니다.

2003년에 처음 소개된 기술이지만 그 이전에 근거가 있습니다. 현대 사람들이 가장 많이 사용하는 토픽모델이 바로 LDA입니다.

 

LDA라는 모델의 구조를 표현한 것이 아래 그림입니다.


Bayesian network랑 똑같이 이해해주시면 됩니다.

하지만 베이즈 네트워크에서 보지 못했던 그림이 있어요. 바로 노드의색이 다르다는 것과 네모박스가 있다는 것입니다.

네모박스는 반복을 말합니다.

D라고 써있는데 이는 Document의개수를 말합니다.

네모박스가 반복이라고 이야기했잖아요?

도큐먼트 개수만큼 있어!라는 뜻입니다.

저 세타가 도큐먼트 개수만큼 있는 것입니다.

가령 1번 문서와 2번문서가 있을 때 1번문서를 위한 세타가 있고 2번문서를 위한세타가 또 따로 있는 것입니다.

이 세타라는 애는 문서 d의 topicdistributior입니다.

그래서 문서 1이 정치 이야기 60%,농구 이야기 40%가 있었다하면 문서 1에 대한세타는 6:4 분포로서 표현되게 됩니다.

D 박스 안에 Nd라는박스가 하나 더 들어가네요?

하나의 문서를 단어 W들의 모음이라고 보는 것입니다.

 

우리한테 주어진 것은 바로 단어의 나열입니다.

색깔이 없는 상태로 즉 데이터가 아니고 단어의 나열이라는거죠

이러이러한 과정에 의해서 단어들이 쓰여졌을 거야. 라는 가설을 가지고시작하게 됩니다.

그 안에 있는 단어들을 가지고 문서를 생성해나가는 과정으로 바꿔서 보는 것 입니다.

 

Classifiactin clustering planning이라는카테고리로 그림과 같이 나뉘어져있다는 가정하에 토픽분포가 대충 어느정도일거야라고

1번 토픽은 classification,2번 토픽은 clustering, 3번은 planning이라고가정하고

막대 바 길이가 긴 녀석들일수록 비중이 더 많은애들이에요.

이것을 사전지식으로 사람이 주는것입니다.

그 다음

문서마다 세타가 존재한다고 했었죠.

베타 가있는데 vocab liry라고 부르는데 이 단어가 얼마나 나타나는지를보여주게 됩니다.

Pi?는 토픽 자체인데

 

 

 

사전지식으로 주어진 분포를 기반으로 첫번째 도큐먼트에 대한 세타를 샘플링합니다.

스톱 게임하는고

 

베타가 단어에대한 분포라고했는데

토픽이 주황색 planning으로 결정되어있었자나여

그럼 이 단어에서 또 스탑하는거에요

머릿속으로 가설을 세우는거야

각 단어를 쓸 때에는 또 단어 하나하나 쓸때마다 토픽을 먼저 결정짓고

지금은 농구에 대해서 쓸거에요

 

사전지식에 의해서 document1에 대해서 stop했어요

그렇게 가설을 세운거야 이 모델은

Unsupervised learning에의해서 학습되는것이기 때문에

아래와 같은 상태일 것입니다.

Document 분포에 대한 사전지식 없음 상태로요’


z라는애는 스탑해서 결정된 토픽 자체였자나여? 그래서 가리키는 용도다 라는 의미에서 indicator라고 부릅니다.

여태까지의 과정을 거꾸로 해나가는 거에요

학습을 할 때는 한 번에 하는 것이 불가능해서 gibbs sampling이라는것을 통해 파라미터 에스터메이션 및 학습하게 됩니다.

 

토픽모델 대표모델로서 LDA모델을 봤는데 단어들만 잔뜩주어진상태에서토픽들의 분포를 얻어지게해주고

단어에 대한 분포도 얻게해주는 것을 말합니다.

classification이라는 토픽도 사실 사람이 붙인거에요

사실은 첨에 단어들의 나열만 있을 뿐이에여

사람은 첨에 몇 개의 토픽이 있는지만 말해줄 뿐입니다.

단순히 이 수식에 기반해서 워드 디스트리뷰션을 업데이트해나가는 것일 뿐이야.

아 첫번째꺼에서는 supervised가 많이 나오고 뭐가 많이나오는것을 보니 얘는 classification이라고 하면서 레이블을 붙혀주는 것입니다.

한계점이져 결국은 사람이 해석해야한다는 것

 

사전지식을 알파라고 주는 것은 맞는데 걔는 그저 사전지식일 뿐

단어들의 분포를 보여주는건 별개의 문제입니다.

단어들만 주어진상태에서 거꾸로 가는거에여

베이지안 네트워크를 통해 그 과정을 보여준 것이기 때문에 복잡하다고 생각하실 수 있어요

 

 

EM(Expectation Maximization) Algorithm입니다. 직독직해해서 기대값을 최대화해주는 알고리즘입니다.

기계학습의 본질은 임의의 모델의 파라미터를 데이터로부터 학습하는 것입니다.

그렇다면 무엇의 기대치를 최대화하려는 알고리즘일까요?

학습을 하는 방법으로 이 EM 알고리즘을 사용하는 것입니다.

EM 알고리즘은 unsupervisedlearning 모델을 학습하는 것입니다.

 