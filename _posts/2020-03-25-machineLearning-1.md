---
title: "Machine Learning(1)"
categories: 
  - MachineLearning
last_modified_at: 2020-03-29T19:03:00+09:00
toc: true
---

Intro
---
학교 수강과목에서 학습한 내용을 복습하는 용도의 포스트입니다.<br/>

기존에 수강했던 인공지능과목을 통해서나 혼자 공부했던 내용이 있지만 거기에 머신러닝 수업을 들어서 보충하고 싶어서 수강하게 되었습니다.<br/>

gitlab과 putty를 이용하여 교내 서버 호스트에 접속하여 실습하는 내용도 함께 기록하려고 합니다.<br/>

[원격 실습환경구축 따라하기](https://ohjinjin.github.io/git/gitlab/)

이번 주제는 theory 개요입니다.<br/>
<br/>

theory 개요
---
* 인공지능과 머신러닝과 딥러닝의 관계 : 인공지능이 머신러닝을 포함하며 머신러닝이 딥러닝을 포함하는 관계<br/>

* 인공지능과 빅데이터의 관계 : 빅데이터 파이프라인의 마지막 단계인 분석(analysis)에서 인공지능 기술이 사용될 수 있습니다. 이는 요리에 비유하여 다시 말하면 빅데이터가 인공지능의 '재료'가 되며, 인공지능은 '레시피' 역할이라할 수 있습니다.<br/>

* 뒤늦게 딥러닝이 각광받게 된 이유 : 과거에는 컴퓨팅 리소스가 부족하여 방대한 양의 데이터를 저장하거나 연산을 수행하기에 어려움이 있었으나 현대에와서 gpu기술의 발달 및 여러 소자들의 저가화 및 범용화를 통해 딥러닝 관련 연구가 활발히 이루어졌습니다. 이 과정에서 backpropagation 등 새로운 이론이 수립되기도 하며 더욱 발전할 수 있었습니다.<br/>

* 컴퓨터의 학습 패러다임은 결국 인간이 세상을 모방한 것이라 할 수 있습니다.<br/>
인공신경망 역시 생물학적 모방을 통해 개발되었지요.<br/>

* 학습 종류는 크게 supervised learning, unsupervised learning, semi-supervised learning, reinforcement learning가 있습니다.<br/>
<br/>

Supervised Learning
---
* supervised learning의 경우 학습을 위해서는 정답레이블이 주어진 데이터가 필요합니다.<br/>

* 보통 classifier의 구현에 많이 사용됩니다.<br/>

* 대표적인 분류모델은 의사결정트리(Decision trees), 인공신경망(Neural Networks), SVM(Support Vector Machine)등이 있습니다.<br/>

Unsupervised Learning
---
* unsupervised learning의 경우 학습데이터에 정답레이블이 주어지지 않습니다.<br/>

* 데이터만 있으면 군집화(clustering)알고리즘을 통해 기계가 스스로 학습 및 패턴을 찾습니다.<br/>

* 대표적인 군집화모델은 Hierarchical clustering과 k-means clustering이 있습니다.<br/>
<br/>

Semi-Supervised Learning
---
* semi-supervised learning은 일부 데이터에만 정답레이블이 존재하는데, 정답이 없는 데이터도 학습에 도움이 될 것이라는 가정을 기반으로하기 때문입니다.<br/>

* semi-supervised learning을 위한 모델들도 있으나 본 강의 커리큘럼에는 포함되지 않습니다.<br/>
<br/>

Reinforcement Learning
---
* reinforcement learning은 기계가 어떠한 행동을 했을 때 보상이 주어지거나 패널티가 주어져 더 나은 방향으로 학습합니다.<br/>
<br/>

Feature
---
Attribute라고도 합니다.<br/>
Feature는 여러가지 data type일 수 있습니다.<br/>
1. categorical(=nominal)
2. string
3. number, real-number

feature를 적절하게 정의하는 것은 중요합니다. 모델의 성능을 좌우하기 때문이지요.<br/>

Feature의 개수(Feature dimension) 설정<br/>
* classification의 경우 label 개수보다는 많은 것이 일반적
* Data 개수보다는 적은 것이 일반적
* 무턱대고 Feature를 늘리면 curse of dimension 우려
* Feature 정의를 생략할 수 있는가? 딥러닝의 경우, feature를 자동으로 각 층에서 인지하게 되므로 feature 정의 과정에 들어가는 노력은 매우 적습니다. 하지만 딥러닝의 경우는 각 feature에 대해 해석을 할 수 없다는 단점을 갖기도 합니다.
<br/>
curse of dimension이란?<br/>
feature가 늘어남에 따라 데이터 조합의 개수 즉 특징 공간은 exponential하게 증가하기 때문에 그만큼 데이터 양도 증가해야하고, 차원에 비해 데이터가 너무 적으면 overfitting이 발생할 우려가 있습니다.<br/>
<br/>

Model
---
method라고도 합니다.<br/>
model은 기계의 실체라고 볼 수 있습니다.<br/>
즉, 모델은 주어진 데이터에 대하여 임의의 task를 수행하기 위한 hypothesis입니다.<br/>

cf) ML로 문제를 해결할 때 데이터 분포를 먼저 눈으로 보고 어느 모델이 적합할지 고르는 과정이 필요하기도 합니다.<br/>

Model의 complexity<br/>
1. computational complexity는 낮을수록 좋으며
2. data complexity는 높을수록 좋습니다.
<br/>
<br/>

Parametric, Non-parametric
---
ML은 결국 문제(task)를 해결하는 방법론이라고 할 수 있는데, 파라메트릭이나 논파라메트릭은 해당 태스크를 가장 잘 해결하는 방법을 고민하는 것과 밀접한 관련이 있습니다.<br/>
주어진 데이터의 분포를 보고 파라메트릭 접근을 하거나 논파라메트릭 접근을 하는 것입니다. 특히 비지도학습같은 경우에 이를 따져보는 과정이 더 중요할 수 있지만 꼭 비지도학습에만 국한되는 것이 아니고 레이블이 달려있는 데이터를 다루는 경우(지도학습)에도 적용될 수 있는 이야기인 것이죠.<br/>

파라메트릭, 논파라메트릭 용어에 쓰이는 '파라미터=매개변수'는 모델이 최적화하는 대상(bias, weight 따위)을 말하며 파라메트릭이라는 이름이 붙은 이유는 고정 된 크기의 매개 변수 세트로 데이터를 요약하는 학습 메소드(훈련 예제 수에 관계없이)의 특징을 갖기 때문입니다. 파라 메트릭 모델에서 아무리 많은 데이터를 처리하더라도 필요한 매개 변수 수에 대한 고려를 할 필요가 없습니다.<br/>

반면 논파라메트릭 메소드의 경우에는 모델을 assumption하기에 어려운 상황 즉, 데이터 feature가 많아진다거나 데이터 분포양상에 대한 사전 지식이없고 최적의 모델을 선택하는 것에 대해 너무 걱정하고 싶지 않을 때 사용하면 좋습니다.<br/>

대표적인 파라메트릭 메소드의 경우에는 Logistic Regression, Linear Discriminant Analysis, Perceptron, Naive Bayes, Simple Neural Networks 등이 있고, 대표적인 논파라메트릭 메소드의 경우에는 k-Nearest Neighbors, Decision Trees, Support Vector Machines, Gaussian cluster 등이 있습니다.<br/>

이 부분을 이해할 때 저는 https://machinelearningmastery.com/parametric-and-nonparametric-machine-learning-algorithms/ 이 글을 많이 참고했습니다!<br/>

+ 추가로 다른 분께서 설명해주신 것이 인상적이어서 함께 내용을 실어봅니다.
> ML은 주어진 데이터를 가지고 "문제 해결"을 하는 관점에서 많이 사용되고, 논 파라메틱이나 파라메틱 같은 경우에도 모델의 테스트 관점이 아닌 해결하고자 하는 문제에 대해 현재 가지고 있는 데이터의 형태 혹은 분포를 파악한 후 매개변수로써 원하는 결과를 도출 할 수 있다면 파라메틱적 메소드의 해당하는 모델을 사용하고, 다소 파라미터를 사용하는게 제한적인 데이터 형태 혹은 조건이다라고 하면 논 파라메틱 메소드 형태의 모델을 선택해 모델링을 하는 것이 맞지 않을까 싶습니다.
>  파라메트릭 모델들은 "매개변수"를 활용해 학습이 진행이 되는데, 여기서 각 모델마다 사용하는 매개변수의 크기가 고정되어 있어 훈련 예제 수 와 관계없이 변수의 수가 변하지 않아 파라메트릭이라고 불리는 게 아닐까 싶습니다. 반면 논 파라메트릭 모델 같은 경우 KNN과 Descision Tree 를 예로 KNN은 K의 개수를 어떻게 가져가느냐에 따라 결과가 변하고, Descision Tree 같은 경우에는 어떤 Feature을 처음으로 사용하는지 그리고 트리의 깊이를 어떻게 가져가는지에 따라 결과가 달라져 훈련 예제 수의 따라 영향을 받는 점이 파라메트릭과 다른 특징을 갖기 때문인거 같습니다.<br/>
<br/>

Generative, Discriminative
---
이 용어 역시 모델에게 주어진 task를 해결하는 방법론 중 한가지인데, generative 방식은 Joint probability P(x,y)를 학습하는 것이며 discriminative의 경우 conditional probability P(y|x)를 다이렉트로 학습하는 방식입니다.<br/>

보통 joint연산을 이용하게 되면 비교적 다양한 목적들에 사용이 가능하기때문에 generative가 더 powerful하다고 표현들을 하지만 이 모델을 설계하거나 학습하는 것이 쉽지 않으며, generative 방식 역시 classification때는 Bayes rule을 이용해서 P(y|x)를 계산합니다.<br/>
<br/>

No Free Lunch vs Occam's Razor
---
이 용어는 문제해결에 도움이 되는 것은 물론이거니와 현업에서의 소통에서도 흔히 사용될 중요한 상식이라고 볼 수 있습니다.<br/>
No Free Lunch는 모든 것에 최선인 알고리즘은 없다라는 컨셉이며, Occam's Razor는 단순한 모델이 의외로 진리일 수 있다라는 컨셉이라고 까지만 알아두면 될 듯 합니다.<br/>
<br/>

모델의 평가_평가방법
---
평가(Test, Evaluation)란 모델 검증을 위한 작업을 말하며 정성 평가와 정량 평가로 나뉩니다.<br/>

정성평가의 경우 쉽게 말해 눈으로 직접 확인하는 것을 말합니다.<br/>
예를 들어 case를 분석하거나, 특정결과들의 원인을 추론하는 것이죠.<br/>

정량평가의 경우는 '정답(truth ground)와 비교하여 성능을 대수로 표현하고 비교하는 것을 말합니다.<br/>
그렇다보니 객관적인 정량평가를 많이 취급하게 됩니다.<br/>

그 중에서도 많이 사용되는 정량평가 방법들을 몇가지 소개하겠습니다.<br/>
1. Accuracy<br/>
Accuracy = 1 - Error<br/>
에러함수는 1부터 n까지의 실제값과 예측값 사이의 Loss 함수값의 합 * 1/n으로 Loss함수의 값은 정답인경우 0, 오답일 경우 1로 정의됩니다.<br/>

2. Precision, Recall, F1 score<br/>
F1 = 2*1/(1/recall + 1/precision) = 2*(precision*recall)/(precision+recall)<br/>
precision과 recall의 정의가 중요한데요, 이 부분을 이해하기 위해서는 true condition과 prediction condition 테이블상에서의 TP, FP, TN, FN을 확인해야합니다.<br/>

예제문제로 사람 1,2,3,4,5,6이 있는데 2,3,4가 범인이며 범인을 예측하는 모델의 성능을 평가한다고 합시다.<br/>
모델의 예측은 1,2,3이 범인일 것이라 예측했습니다.<br/>

이 경우<br/>
precision = TP/(TP+FP) = 범인이라 예측했는데 진짜 범인인 수 / 모델이 범인이라고 선택한 수 = 2/3
recall = TP/(FN+TP) = 범인이라 예측했는데 진짜 범인인 수 / 진짜 총 범인의 수 = 2/3

가 됩니다.<br/>

헷갈릴수 있지만 사실 간단합니다.<br/>
* 모델의 예측값 => Positive(범인이라고 예측) or Nagative(범인이아니라고 예측)<br/>
* 모델예측값에 대한 채점 => true(딩동댕) or false(땡)<br/>

으로 해석하면 편합니다.<br/>

그래서 이 예제문제의 경우 F1 score=6 입니다.<br/>

3. ROC curve에서의 Area Under the Curve(AUC)값<br/>
(독학하라하셨는데 독학 후 업데이트 예정입니다.)<br/>

4. BLEU metric(score):BiLingual Evaluation Understudy<br/>
BLEU의 경우 자동번역 문장에 대한 평가를 할 때 많이 사용되곤 합니다.<br/>

방법은 간단합니다. 실제 답안(human ability, 사람이 번역)과 자동 번역된 결과인 R로부터 n-gram을 뽑아서 답안에서 몇번 등장했는지 계산하는 것입니다.<br/>
1gram precision에서는 전체토큰을 각각 한덩어리로 쪼개두고 몇 번 등장했는지를 보는 것이며, n gram precision에서는 전체토큰을 각 n덩어리로 1stride를 유지하며 겹치게 묶은 뒤 등장했는지를 보는 것입니다.<br/>

이후 BLEU score는 가중기하평균으로 계산됩니다.<br/>
하지만 실제로 이 평가방법은 객관적이지 못합니다. 의미없이 중복된 토큰이 연속으로 있더라도 등장횟수는 자꾸 각 gram 마다 세어질테니까요. 이럴 경우를 대비하여 clipping precision counts라는 대안이 등장했습니다. 말그대로 clip해버립니다.<br/>

또 다른 문제로는 실제로 문장이 완성되지 않았더라도 성능이 높게 나와버리는 경우가 있습니다. 그래서 brevity penalty가 이를 해소합니다. 문장 전체의 length를 염두해두는 방법이지요.<br/>
<br/>

모델의 평가_평가를 위한 데이터 분배
---
1. train + test<br/>
데이터 분배 시 train-test만으로 쪼개는 것은 권장하지 않습니다.<br/>
예를들어 테스트 결과를 보고 피쳐개수를 늘려볼까? 하는 판단을 할 수 도있기 때문입니다.<br/>
이런 경우는 있어선 안됩니다. 왜냐하면 테스트데이터는 테스트하는 용도로만 써야하기 때문이죠. 최적화 단계에서 테스트 결과로부터 영향을 받아선 안됩니다. 그것 자체가 테스트만을 위한 용도가 아니고 테스트 데이터에 맞춰 트레이닝을 한 셈이니까요.<br/>

2. train + validation + test<br/>
그렇다면 최적화가 잘되었는지는 어떻게 확인하면 좋을까요? 그래서 training data에서 일부를 떼어내어 validation data로 두는 것입니다.<br/>
모델 튜닝을 위한 데이터, 학습에 간접적으로 영향을 주는 데이터가 바로 validation data라고 보시면됩니다.<br/>

3. k-fold cross-validation<br/>
이 방식은 위 두가지보다 객관적입니다.<br/>
전체 훈련데이터를 k등분하여 첫번째 토막을 validation 또는 test 데이터로 사용하고 나머지 k-1개의 토막을 training 용으로 사용하여 성능 측정을 합니다. 그 다음 두번째 토막을 validation 또는 test로 쓰고 나머지 k-1개의 토막을....<br/>
...<br/>
이렇게 k번 반복합니다. 보통 k는 5나 10 등으로 많이 둡니다.<br/>

이 방식의 특징은 바로 independent하다는 점입니다.<br/>
또 다른 응용방법으로는 test data를 일부 떼어두고, 나머지 train data를 k등분해서 한 덩어리를 validation으로 매회 돌아가면서 두는 방식으로 퓨전해서 쓰면 성능이 더 높아진다고합니다.<br/>

ML 공학도로서 모델 성능평가를 보고 좋다 좋지않다 정도는 구분할 수 있어야 합니다.<br/>

모델의 평가_Bias,Variance<br/>
---
모델 평가 시에는 bias와 variance를 고려해야합니다.<br/>
두 용어를 설명하기 전에 비유를 해보자면 불이 나서 불을 끄려할 때 소방호스가 향한 방향은 bias, 소방호스에서 물이 나가는 분사 정도는 variance라고 할 수 있습니다.<br/>

해당 설명이 적혀있는 곳에 실린 오른쪽 차트의 '결과'축은 예측오류율을 말합니다.<br/>
트레이닝데이터에 대한 성능은 너무나 당연히 계속해서 낮아져야합니다.<br/>
반면 테스트 데이터는 다시 오류율이 높아지게 되는데 이를 바로 overfitting(과적합)이라고 합니다.<br/>

같은 페이지에 왼쪽 그림에서 H는 모델의결과입니다. 다시 말해 모델의 컴플렉서티가 낮은것이죠. 더 자글자글하게 판단경계선을 나눌 수도 있거든요. 하지만 너무 오버하게되면 학습데이터에만 너무 맞춰지다보니 테스트데이터에 대한 성능은 오히려 떨어질수도 있습니다.<br/>

다시 정리하자면 모델 complexity가 너무 높아지면 오히려 overfitting이 될 확률이 커집니다. 참고로 모델의 complexity는 모델의 feature가 많으면 높아지죠.<br/>

몇가지 용어를 추가로 정리합니다.<br/>

Generalization : unseen data에 대해서도 잘 동작하는가? 그렇다면 그 모델은 generalization이 잘되었다고 표현할 수 있습니다.<br/>
Capacity : 모델에 의한 공간을 말합니다.(판단경계선을 말한다 볼수 있지요 자주사용되는 단어는 아니라고합니다)<br/>
Overfitting : 과적합!! 꼭알아야하는 중요한 단어입니다.<br/>

정리하여 variance가 큰 모델은 overfitting, bias가 큰 모델은 underfitting을 의미하니 이 둘은 trade-off 관계라 볼 수 있습니다.<br/>


Algorithm for Train
---
기계의 학습은 결국 파라미터를 최적화시키는 것을 말합니다.<br/>
모델을 설게해서 결국 그 모델이 갖고있는 파라미터들을 데이터에 맞게 최적화하는 작업입니다.<br/>
그렇다면 최적화할 대상(=파라미터)를 찾아야하는데, 이 역할이 바로 목적함수(=target function, objective function)입니다.<br/>
그리고 그 목적함수의 값을 최적(최대 또는 최소)화하는 파라미터값을 찾아야합니다.<br/>

여기에서는 오류함수와 최적화 함수를 모두 간략하게 소개합니다.<br/>

loss function : data instance에 대한 prediction penalty를 정의하는 함수입니다. 즉, 틀렸을 때 어느정도 틀렸는지를 수치로서 표현해주는 역할입니다.
<br/>(ex) square loss, hinge loss, 0/1 loss etc..)<br/>
당연히 낮을수록 좋습니다.<br/>

cost function(obj,target) : loss함수보다 일반화된 개념으로 한 장의 데이터에 대한 것이 아니라 전체 데이터에 대한 loss함수들의 합의 정규화(추후설명) term을 포함합니다.<br/>
(ex) MSE)<br/>
잠시 간단히 설명하자면 정규화 텀을 왜 넣는 것일까요?<br/>
데이터 한개에 대해 틀렸다 맞았다는 loss함수가 표현할 거잖아요??<br/>
하지만 항상은 아니어도 풀어야하는 task에는 그것 외에 고려해야할 다른 사항들이 있기 마련입니다. 도메인 지식이나 통계적 결과를 기반으로 다른 요소를 포함해줘야하는데 그런 텀들을 모두 정규화 텀이라고 합니다. 또 이런 것까지도 다 포함한것을 cost function이라고 합니다.<br/>
물론 이 함수값도 당연히 낮을수록 좋습니다.<br/>

object function : object function은 문제에 따라 최대화해야할 수도 있고 최소화해야할 수도 있습니다. 걍 최적화하려는 모든 종류의 함수이기 때문이죠.<br/>
(ex)MLE) mle는 참고로 최대화해야하는 오브젝트함수중 하나입니다.<br/>
즉 정리하자면<br/>
Loss is a part of cost which is a type of objective..<br/>
입니다.<br/>


많이 사용되는 학습 알고리즘<br/>
* MLE(Maximum Likelihood Estimation)
* MAP(Maximum a Posteriori Estimation)
* EM(Expectation-Maximization)
* Gibbs sampling
* Gradient Descent
* Variational inference
* Laplace approximation
* Genetic algorithm

... etc


(수정중)
<br/>
<br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>