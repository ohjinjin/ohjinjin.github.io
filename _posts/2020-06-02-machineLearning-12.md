---
title: "Kmeans & Knn_Machine Learning(12)"
categories: 
  - MachineLearning
last_modified_at: 2020-06-03T16:20:00+09:00
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


k\-means
---
k\-means 알고리즘은 이름에서도 알 수 있듯이 k개의 mean입니다.<br/>
mean이 뜻하는 것은 평균값이죠.<br/>
그 중심을 기준으로 군집화를 하게 됩니다.<br/>

아래 그림을 몇 개의 군집으로 나눠야 잘 나눴다고 할 수 있을까요?<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture147.JPG" alt=""> {% endraw %}

사람들마다 서로 다른 대답을 할 것입니다.<br/>
이것이 바로 unsupervised learning의 맹점이죠.<br/>


Kmeans 알고리즘의 pseudo code는 아래와 같습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture148.JPG" alt=""> {% endraw %}

임의의 k값을 정하고 군집별 초기 중심위치를 선택해야 합니다.<br/>

데이터i와 1번군집중심의거리, 데이터i와 2번군집중심의거리, … 데이터i와 k번군집중심의거리를 계산해서 가장 가까운 군집쪽으로 할당해줍니다.<br/>

거리를 계산할 때 많이 사용하는 것은 유클리드 거리공식(Euclideandistance)입니다.<br/>

데이터별로 군집 할당을 끝냈으면, 각 군집별 중심을 다시 계산합니다.<br/>

데이터가 할당된 군집이 변경되는 경우가 없어질 때까지 반복합니다.<br/>
다른 말로는 중심이 바뀌지 않을 때까지 반복합니다!<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture149.JPG" alt=""> {% endraw %}

그런데 kmeans에 의한 군집화가 엉망으로 되는 경우도 있을 수 있습니다.<br/>

왜일까요?<br/>

바로 초기값이 어떻게 정해지느냐에 따라서 결과가 좌지우지될 수 있다는 것이죠.<br/>
그래서 한 번만 돌려보면 안됩니다.<br/>

초기값을 어떻게 줄지에 대한 연구도 많고 관점에 따라 달라질 수 있는 ‘최적’의 cluster 개수를 정하는 것에 대한 연구도 많습니다.<br/>

Hierarchical clustering 결과를 활용하여 최적의개수를 짐작하는 방법이 있고 rule of thumb나 elbowmethod, Information Criterion Approch 등의 방법도 있습니다.<br/>

Elbow method의 경우 여러 후보 k값들에 대하여, cluster 들의 적절함을 평가하는 것입니다.<br/>

적절함 이란 예를 들어 cluster 중심으로부터의 거리 등을 말합니다.<br/>

결국 elbow method는 여러 후보값들에 대하여 일일이 시행해보고 관찰하는 면에서 일종의 Grid Search 입니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture150.JPG" alt=""> {% endraw %}

팔꿈치라는 이름이 붙은 이유는 k값을 바꿔가면서 데이터 X의 SSE 값을 그래프로 그려주는 함수로 급격하게 기울기가 변하는 곳이 있는데 그 지점이 최적의 k값이며, 전체적인 그래프를 보았을 때 뾰족한게 팔꿈치같다고ㅎㅎ가 이유입니다.<br/>

Information Criterion Approch는 클러스터링모델에 대해 likelihood를 계산하여 활용하는 방법입니다.<br/>

예를 들어 K-means의 경우에는 Gaussian Mixture Model을 활용하여 likelihood를계산합니다.<br/>

K means는 아까 말했듯이 cluster중심 초기위치에 의해 엉터리 결과가 나올 수 l있습니다.<br/>
구형(normal 분포)이 아닌 클러스터를 찾을때는 부적절한 결과가 나올 수 있는 것이죠.<br/>
Cluster 초기값을 어떻게 결정할 지에 대한 연구들도 많이 있습니다.<br/>

k\-means는 Outlier에 취약합니다.<br/>

해결법은 outlier 제거를 위한 전처리를 해주는 것이며, 또 다른 해결법으로는 k\-medoids 알고리즘이 있습니다.<br/> 이 방법은 mean을 계산하지 않고, 데이터 중에서 하나를 중심으로 사용하는 방법입니다.<br/>

Q 표본데이터중에 하나를 중심으로 뽑는데 그게 만약 튄 값일수도 있지 않을까요? outlier를 제거하는 효과가 있다고 말할 수 있을까요???
 

K\-NN
---
k\-nn(nearest neighbor)알고리즘은 군집화를 위한 모델은 아닙니다.<br/>
이전에 kaggle의 유명한 데이터인 titanic dataset과 관련하여 k\-nn을 설명한 링크를 참고하시라고 [여기](https://ohjinjin.github.io/machinelearning/kNN-titanic/)에 걸어두겠습니다.<br/>

k\-NN 알고리즘은 Instance\-basedlearning에 속합니다.<br/>

Instance\-Based Learning의  또다른 말로는 Memory\-basedLearning라고도 부릅니다.<br/>

Instance\-Based Learning이란 학습 데이터로부터 임의의 모델 파라메터를 학습하는 것이 아닌 학습 데이터와 테스트 데이터를 직접 비교하는 것을 말합니다.<br/>
그래서 Nonparametric method의 일종이지요.<br/>

학습 데이터의 label을 사용하므로 supervised learning에 해당합니다.<br/>


k\-NN알고리즘은 “내가본 것중에 그거랑 제일 비슷하네!”를 취지로 하는 모델입니다.<br/>

이 때 k란 몇 번째로 가까운 데이터까지 살펴볼 지를 의미합니다.<br/>
 
(수정중, K-nn 알고리즘 업데이트 예정)
<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!
<br/><br/>