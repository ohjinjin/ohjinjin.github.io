---
title: "Kmeans_Machine Learning(12)"
categories: 
  - MachineLearning
last_modified_at: 2020-06-02T23:05:00+09:00
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

* [Machine Learning(10) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-10/)<br/>

* [Machine Learning(11) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-10/)<br/>

이번 시간에는 Kmeans을 배웁니다.<br/>
<br/>


Semi supervised learning k-means clustering
---
Semi supervised learning은 Unsupervised learing과 supervised learning의 중간이겠지요.<br/>

데이터가 너무 적은 경우 또는 불균형 데이터를 갖는 경우
데이터가 너무 적은 경우에는 어떻게 하는 것이 좋을까요?

첫 번째로. transfer learning(전이학습)을 통해 해결할 수 있어요.<br/>

학습 데이터가 부족한 분야의 모델 구축을 위해 유사한 데이터가 풍부한 분야에서 훈련된 모델을 재사용합니다.<br/>
(ex: pre-trained model의 파라메터로 초기화하는 것 등)

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture144.JPG" alt=""> {% endraw %}

한글\->중국어 데이터가 100개만 있다고 할 때, 걍 100개만가지구 학습시킨것보다 훨씬 나은 성능을 보입니다.<br/>

두 번째로, Distant supervision 가 있습니다.<br/>

약하게 레이블링된 트레이닝셋을 이용합니다.<br/>
훈련데이터는 휴리스틱이나 규칙에 기반하여 자동적으로 레이블되어있는 것이지요.<br/>

데이터 불균형시 또 다른 방법으로는 소개했 듯아 up/down sampling 이 있구요.<br/>

GAN을 이용하여 fake data를 생성하여 robustness를 높이기도 합니다.<br/>

두번째 방법은 loss weight control인데요.<br/>

Cost sensitive learning이란 학습 데이터의 label 비율에 반비례하게 loss 함수에 weight 조절을 함으로써, 비교적 적은 비율의 Label에 해당하는 데이터에 더욱 민감하게 학습하는 것을 말합니다.<br/>

Focal loss 는 학습 데이터 label 비율이 높아서 상대적으로 쉽게 분류가 가능한 Label에 대한 weight를 작게 조절함으로써, Label 비율이 작은 데이터들에 집중하도록 조절하는 것을 말합니다.<br/>

Q. 둘 다 같은 거 아니에요?<br/>
Cost-는 레이블 비율에 의해서만이죠,

focal은 쉽게 분류가 가능한 데이터가 판별이 될거잖아요?<br/>

실제로 모델을 돌려보면요?<br/>
성능 차이가 나는 여러 이유들중에  하나가 레이블 비율이 될수 있는 것 뿐이고요.<br/>
쉽게 분류가 안되는 데이터들에 대해 더 weight를 크게 조절하겠다 라는 것을 말합니다.<br/>

이런 방식은 부스팅에서도 봤었죠.<br/>
<br/>

Semi supervise learning
---
예제는 동그라미와 세모 두가지 클래스에 대해 분류하는 바이너리 분류기입니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture145.JPG" alt=""> {% endraw %}

그림에서 보다시피 레이블이 되어있는 데이터는 꽤 적네요.<br/>

만약 저 decision boundary 즉 빨간선이 없다고 생각해보세요.<br/>

사람이라면 왠지 저 빨간색선으로 나눌 것 같은데? 라는 직관에서 이러한 semi supervised learning이 출발합니다.<br/>

잘 알려진 semi supervised는 세 가지 모델이 있습니다.<br/> 


1. Active learning
2. Self-learning
3. Co-learning

Semi Supervised Learning\- Active learning
---
Active learning은 "아, 나 다른애들은 어떻게든 하겠는데, 얘는 좀 어렵네 이거 알려줘" 라고 머신이 사람에게 물어보는 방식입니다.<br/>

그럼 머신은 사람에게 물어볼 데이터를 어떻게 결정하는 걸까요?<br/>

그에 대한 연구도 ongoing인데
크게 두 가지를 소개하겠습니다.<br/>

* Uncertainty sampling : 하나의 모델을 학습한 다음에 레이블 뿐아니라 confidence가 몇 점인지도 낸다고 가정을 하는거에요.<br/>
젤 작은 confident를 갖는 데이터의 레이블을 물어보게 되는거죠.<br/>
가장 애매한걸 머신이 사람에게 query하는 것이지요.<br/>

* Committee-based sampling : 만약 네 개의 모델을 만들었다고하면 각 unlabeled data에 대해 “야 이거 뭐같애?”하면서 물었는데 2:2가 나오면 그때만 사람에게 query 하는거에요.<br/>
3:1이나오면 자기들끼리결정해버리는 거구요.<br/>
<br/>

Semi Supervised Learning\- Self training
---
레이블이 되어있는 학습데이터(gold dataset)이라고 합시다.<br/>

얘를 supervised 학습으로서 생성한 모델 M을 사용하여 unlabeled instance {x1,x2,x3,…}에 대해 예측한 결과 {y1, y2, y3,…}를 얻을 수 있습니다.<br/>

Confidence가 높은 일부(silver dataset)을 학습용으로 사용하여 모델 M’을 얻습니다.<br/>

위 과정을 우리가 정한 일정조건을 만족할 때까지 반복합니다.<br/>

모델이 낸 결과지만 너무나 confidence가 높아서 이건 학습용으로 써도 괜찮을 것 같아 라는 취지에서 나오는 것이 바로 silver dataset입니다.<br/>

하지만 자칫 잘못하면 모델이 엉뚱한 방향으로 학습될 수 있다는 단점이 있습니다.<br/>
<br/>

Semi Supervise Learning\- Co\-learning
---
Co\-learning은 독립적인 모델들이 각각 self\-learning을 하되, 서로 간에 confidence가 높은 데이터를 물물교환하는 것을 말합니다.<br/>

"이거 내가 보니까 확실하더라! 이거 너도 써" 하고 서로 교환하는거지요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture146.JPG" alt=""> {% endraw %}

Q 최종 모델은 그럼 누구로 결정하게될까요?<br/>

*최종모델을 결정하기 위한 연구들이 이미 존재할꺼야. 사람이 생각할 수 있는 거의 모든 방법은 이미 다 연구되어있다고 봐야 해요. (예: 두 모델을 모두 사용(voting)하거나, 두 모델의 성능 등을 바탕으로 weighted voting 등..)*


클러스터링은 레이블이 없어도 쓸 수 있는 모델입니다.<br/>
하지만 결국 아주 적다하더라도 레이블은 달려있어야 해요.<br/>
클러스터링을 할 때 우리가 원하는 목적의 레이블이 존재해야만 합니다.<br/>

예를 들어 우리의 목적은 하마와 기린을 분류하는 것일 때가 있을 것이고 같은 데이터가 있다하더라도 수컷과 암컷을 분류해야하는 것일 수 도 있었다는것이죠.<br/>

물론 레이블을 쓰지 않고 measure하는 방법도 있긴하지만 결국 그런 메소드들은 정답 없이 성능을 측정했으니, 결국 진짜 성능이라고 보기 어렵겠지요.<br/>

(수정중, K-means 알고리즘 업데이트 예정)
<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!
<br/><br/>