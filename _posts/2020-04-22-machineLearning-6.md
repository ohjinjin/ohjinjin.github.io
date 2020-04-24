---
title: "SVD_Machine Learning(6)"
categories: 
  - MachineLearning
last_modified_at: 2020-04-24T19:38:00+09:00
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

원행렬에 A 변환을 적용했을때 어떤 결과벡터가 나오는데, 도대체 그 결과는 어떤방향으로(고유벡터) 몇배늘리거나 줄이거나 했길래(고유값) 나오게 된 것일까?라고 보시면됩니다.<br/>
v1과 v2를 기저로 갖는 공간에서 고유값1 고유값2 배만큼 변환이 적용된 것이지요.<br/>

고유벡터를 어떻게 구하는 방법이 궁금하실 겁니다.<br/>

어떠한 선형변환을 가하는 연산자 역할을 하는 것이 위 식에서 A 입니다.<br/>
고유벡터는 A 행렬을 곱함으로써 변환을 가하더라도 그 결과가 자기 자신 고유벡터로서 다시금 표현이 가능해야합니다.<br/>
그말인 즉슨, 변환 전의 벡터와 A를 적용해서 변환을 가한 후의 벡터가 서로 평행한 관계라는 조건을 갖는 것이 고유벡터가 가질 조건이라는 뜻 입니다.<br/>

평행하기 위한 조건은 또 무엇일까요? [1 1]과 [3 3]은 평행합니다.<br/>
[1 1]과 [-3 -3] 역시 평행합니다. 역방향 벡터더라도 몇배의 실수배를 하던지 간에 절대 접점이 없다면 평행하다 말할 수 있습니다.<br/>

이러한 조건을 만족하는 특수한 벡터가 바로 고유벡터인데, 일반적으로 임의의 정방행렬 nXn인 A 행렬에 대한 고유벡터는 n개입니다.<br/>

보통 A의 고유벡터를 구할 때는 A에 A의 전치행렬을 곱하고 특성방정식으로 람다(고유값)를 구하고, 그에 대응하는 고유벡터를 구하게 됩니다.<br/>
자세한 예제가 잘 나와있는 블로그 포스팅 링크를 [여기](https://twlab.tistory.com/47)에 걸어드리겠습니다.<br/>

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

EigenValue Decomposition
---
고유값 분해를 배워봅시다.<br/>
NxN 크기의 정방행렬 A에 대하여, 3개의 행렬(및 벡터)의 내적(PDP를 말함)으로 나타낼 수 있습니다.<br/>
**AX=람다x**라는 식과 **A=PDP의역행렬**라는 식은 똑같은 말을 하는 식입니다.<br/>
그 이유는 아래 그림에 나타내었습니다.<br/>
아래 그림에서 X를 P라고 이해하시면 편합니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture32.JPG" alt=""> {% endraw %}

다시 한 번 변환하는 단계를 이해해봅시다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture33.JPG" alt=""> {% endraw %}
이러한 변환을 어떤 기저 v1과 어떤 또다른 기저 v2로 각각 몇배씩 늘리고 줄임으로써 가져온 변환이라할때, 저 그림처럼 찾을 수 있다는거에요.<br/>
고개를 돌려서 찾아야겠죠!<br/>
<br/>
<br/>

SVD(Singular Value Decomposition)
---
다시 고유벡터와 고유값을 살펴보면, 정방행렬일 때로 가정하여 설명한다는 것을 알 수 있습니다.<br/>

그렇다면 정방행렬이 아닌데 분해할 수 없을까?에 대한 일반화된 분해법이 SVD(Singular Value Decomposition)입니다.<br/>

MxN 행렬 A(변환해주는 연산자 역할)에 대해 3개의 행렬 내적으로 나타낼 수 있습니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture34.JPG" alt=""> {% endraw %}

시그마는 일부만 대각성분이 람다로 채워져있고 나머진 0으로만 이루어진 행또는 열을 가지게 되는 행렬입니다.<br/>

SVD의 개념을 이해해봅시다.<br/>
어떤 임의의 차원의 값을 새로운 차원으로 바꿀 수 있는 거에요!!<br/>
단 컴파스 그린 것 처럼 같은 양의 것으로만 바꾸는 거지요.<br/>
원래 있던 차원을 없애고 새로운 차원이 생겼다고 받아들여봅시다.<br/>

eigenvalue decomposition에서는 A를 바로 분해했는데, SVD는 다른 애를 이용해서 정방행렬로 바꿔준 다음에 eigenvalue decomposition해주게 됩니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture37.JPG" alt=""> {% endraw %}
U는 고유벡터들을 이어붙인 행렬이었잖아요??<br/>
참고로 고유값 구하는 방법은 아래 **특성방정식**을 풀어 람다에 대해 정리해 풀어낼 수 있습니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture35.JPG" alt=""> {% endraw %}
그리고 이에 대응하는 고유벡터들도 구할 수 있죠.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture40.JPG" alt=""> {% endraw %}
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture41.JPG" alt=""> {% endraw %}
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture42.JPG" alt=""> {% endraw %}
흥미로운것은 AtA하고 AAt 결과를 보면 람다값이 동일하다는 점입니다.<br/>
이것이 아까 말한 차원을 높였다해도 양은 그대로 라는 말입니다.<br/>
2차원 공간 상에서의 양과 4차원 공간 상의 양이 같은것이죠.<br/>

다시 SVD를 정리해봅시다.<br/>
Eigenvalue Decomposition을 적용하기 위해 mxn 직사각 행렬을 정사각행렬을 만들때 A^tA를 통해서 그리고 AA^t를 통해서 분해해줘야해요.<br/>
전자(A^tA)는 nxn으로, 후자(AA^t)는 mxm으로 변환해준것이라고 보시면 됩니다.<br/>
전자는 낮은차원으로의 변환을 2번한거고, 후자는 높은차원으로의 변환을 2번한겁니다.<br/>
전자는 U에 해당하고 후자는 V에 해당하는 겁니다.<br/>
이제 가운데 X부분만 설명이 남았는데요, 왜 람다를 쓰긴쓰는데 굳이 루트를 씌울까요?<br/>

첫번째 디컴포지션과 두번째 디컴포지션의 양은 일치했다는 것을 우리가 알게 되었었죠.<br/>
근데 곱하잖아요? 행렬말고 실수 개념으로 비유해 보자면 마치 k*k=k^2이니 원래값을 확인하기 위해 루트를 씌워주는거라고 보시면 편합니다!<br/>

지금까지 설명한 것들을 그림과 함께 다시 정리해봅시다!<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture38.JPG" alt=""> {% endraw %}

SVD의 종류는 방금 배운 FullSVD 보다는 축약된 버전인 reduced SVD가 많이 활용됩니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture36.JPG" alt=""> {% endraw %}


작은값에 대한 값만 남게 된다고 보시면 됩니다.<br/>
저기 다시 정리해보기로 했던 2x1짜리 A에 대한 SVD 예제에서도 보면 람다가 한개밖에 없다는거 확인 되시죠? 1차원이든(A^tA) 2차원이든(AA^t)지요!<br/>
설사 다른 직사각행렬이 더 길다해도 작은애에 맞춰버리겠단거에요!<br/>
애초에 mxn이라는 디멘젼 정보를 가지고 있기때문에 이게 가능한 겁니다.<br/>

그래서 첫번째 reduced SVD인 thin svd는 0인 성분들 다 무시하는 것이며, 두번째 reduced SVD인 compact svd는 계산하고 보니 rank가 부족했던 경우가 있을 수 있어서 그런 추가적으로 확인된 0 성분들을 마저 빼고 계산한 다음에 마지막에는 0이었기 때문에 뺐던 것들을 추가만 하면되는 것입니다.<br/>
결과는 똑같을 거라는 전제를 두고서요.<br/>

세번째 reduced SVD인 truncated svd는 원본행렬 A의 랭크가 r이었는데 그보다도 더 작은 개수 t만큼 줄여버리는겁니다.<br/>
그냥 0이 아니어도 우선 날려버리는거죠. 메모리는 많이 절약되겠죠?<br/>
그렇지만 원래 0이 아니었는데도 없앴으니 이전의 값은 알 수 가 없겠죠? 다시 원래 차원대로 맞추기위해 0이었다고 가정하고 마지막에 메꿔넣어줍니다. 엥?! 싶으시지 않나요?<br/>

그럼 완전히 다른값이 나오는데 이걸 왜? 어따 써먹지? 싶으실거에요!<br/>
일부러 해상도를 떨어뜨리려고 하는 등 압축을 목적으로 사용한답니다.<br/>

하지만 만약 끄트머리 성분들이 만약 핵심적이었다면 치명적일 겁니다.<br/>
그렇지만 열중에 아홉 이상의 경우 좌상단에 있는 애들이 주성분이기 때문에 저희가 잘라내는 아래쪽의 성분들은 없애더라도 크게 문제가 되지 않습니다.<br/>
우하단에 위치할수록 그림의 디테일을 표현하는 애들이 나오게 됩니다.<br/>


만약 제 얼굴이 있는 원본 사진이 있었는데, truncated svd로 압축을 시켰다고 가정합시다.<br/>
truncated svd를 적용함으로써 아래쪽 성분 조금 없앴다해도 "(해상도가 낮긴한데) 이건 오진선의 얼굴 사진이군!" 하고 알아볼 수 있습니다.<br/>
심지어 조금 과하게 없애도 "누군가의 얼굴을 찍은 사진같군!"라고 판단할 수 있을 수준일거에요.<br/>

그런데 만약 왼쪽 위 부분의 성분을 없앤다면? "이게 무슨 사진이지?"가 될 수 있어요!<br/>
<br/>
<br/>

PCA(Principal Component Analysis)
---
한국어로는 **주성분 분석**이라고 합니다.<br/>
데이터의 분포에 대한 주성분을 찾는 것입니다.<br/>
여태 공부했던것처럼 핵심 '축'을 찾는거에요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture39.JPG" alt=""> {% endraw %}

조금 더 고급지게 표현하자면, 데이터의 패턴을 잘 표현해주는 최적의 feature, 또는 성분만의 조합을 찾는 것입니다.<br/>

그래서 PCA는 featur selection 혹은 feature dimension reduction을 위해 사용되곤 합니다.<br/>

PCA 구하는 방법을 살펴봅시다.<br/>
1. 데이터들의 평균(중심)으로 원점을 가정<br/>
2. 데이터들에 대한 공분산행렬, 고유값, 고유벡터 구함<br/>
3. 고유벡터 기반(관점=축=여기선 pca를 말함)으로 데이터를 보면, 가장 큰 분산을 가지게 됨<br/>

공분산(covariance)이란 무엇일까요?<br/>
얼마나 너희 성분들끼리 **동시에** 늘거나 줄어드니? 에 대한 것을 수치화 시킨게 공분산입니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture43.JPG" alt=""> {% endraw %}

서로 다른 feature들의 값에서 각각 mean을 빼면 그거는 분산이잖아요?<br/>
(위 그림에 나와있는 수식 중 y에 바를 씌운게 mean값이에요.)<br/>

그래서 공분산은 두 변량이 각 평균으로부터 변화하는 방향 및 양에 대한 기대값이 됩니다.<br/>

feature가 m개있으면 각 pair를 보기 위해 mxm의 행렬로 나오는게 공분산행렬입니다.<br/>
즉, 서로 연관이 있는 feature pair들을 파악할 수 있게 됩니다.<br/>
feature pair는 다른말로 correlation이라고 합니다.<br/>

이에 대한 고유값과 고유벡터를 얻는 것은 결국 correlation이 존재하는 feature들에 대해 기저를 확보하는 작업이라고 이해할 수 있습니다.<br/>

고유벡터를 기저라고 가정하고 데이터를 보게 되면, correlation이 컸던 feature pair들의 관점(축)으로 보게 되므로 당연하게 분산이 커지는 것 입니다.<br/>

핵심은 원점 옮기기와 공분산행렬 구하기, 그리고 그 행렬을 이용해 eigenvalue와 eigenvector를 구하는 것입니다.<br/> 당연히 공분산행렬이 mxm정방행렬이니까 고유벡터는 m개로 나오겠죠?<br/>

예시를 봅시다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture44.JPG" alt=""> {% endraw %}
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture45.JPG" alt=""> {% endraw %}

첫번째꺼가 두번째꺼보다 낫잖아요?<br/>
예제에서는 한놈만 PCA로 가정하겠어! 하고 1번 축을 선택합니다.<br/>

그 고른 pca를 원 데이터(feature vector)에 곱해줍니다.<br/>

그다음은 고른축으로 각 feature vector들을 사영 시킵니다.(수선의발을 내립니다.)<br/>

그 결과 성분들을 다 구하면 됩니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture46.JPG" alt=""> {% endraw %}

PCA의 주된 활용도는 압축이며, 분산이 작은 것을 중요하게 여기는 데이터/어플리케이션에는 적합하지 않고, 데이터들의 분산이 직교하지 않는 경우에도 적합하지 않습니다.<br/>

위 예제의 경우에는 2차원이다 보니 사람의 직관으로도 PCA를 찾는 것이 가능하지만, feature dimension이 큰 경우에는 어렵겠지요.<br/>

PCA와 유관한 알고리즘으로 Independent Component Analysis 라는 것이 있습니다만 커리에서 이에대한 설명은 생략합니다.<br/>


LDA(Liner Discriminant Analysis)
---
머신러닝하는 사람들 사이에서 LDA라고 하면 목적이 전혀 다른 유명한 알고리즘이 있어서 혼선이 있을 수 있으니까 주의해주세요. ㅎㅎ<br/>
한국말로는 선형판별분석이라하며, fisher라는 사람이 만들어서 fisher's algoritm이라고 부르는 사람들도 있습니다.<br/>

여기서부터는 클래스!라는 말을 씁니다.<br/>
클래스 두개가 있다고 가정을하고 판별을합니다.<br/>
원본에서의 우리의 feature dimension은 x,y축이라고 합시다.<br/>

특정 관점에서 두 클래스가 겹쳐보인다면 좋은 관점이라 할 수 없습니다.<br/>


(수정중)
