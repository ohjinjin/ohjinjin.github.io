---
title: "Naive Bayes_Machine Learning(2)"
categories: 
  - MachineLearning
last_modified_at: 2020-04-08T15:24:00+09:00
toc: true
---

Intro
---
학교 수강과목에서 학습한 내용을 복습하는 용도의 포스트입니다.<br/>

기존에 수강했던 인공지능과목을 통해서나 혼자 공부했던 내용이 있지만 거기에 머신러닝 수업을 들어서 보충하고 싶어서 수강하게 되었습니다.<br/>

gitlab과 putty를 이용하여 교내 서버 호스트에 접속하여 실습하는 내용도 함께 기록하려고 합니다.<br/>

* [원격 실습환경구축 따라하기](https://ohjinjin.github.io/git/gitlab/)<br/>

* [Machine Learning(1) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-1/)<br/>

* [Machine Learning(2) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-2/)<br/>

이번 주제는 Naive Bayes에 대한 theory입니다.<br/>
<br/>
과거 이 모델에 대해 스스로 정리한 적이 있었는데 함께 [여기](https://ohjinjin.github.io/machinelearning/NaiveBayes-titanic/)에 링크를 걸어두겠습니다.<br/>
<br/>

Naive Bayes
---
머신러닝에서는 확률을 0~100%로 표현하기보다는 0~1사이로 많이들 표현하곤합니다.<br/>
우리는 모든 사건의 확률의 합은 1이 된다는 것을 알고 있습니다.<br/>

Naive bayes 모델을 이해하기 위해서는 bayes rule을 선수지식으로 알고 있어야 합니다.<br/>
베이즈정리(Bayes Rule)는 아래와 같습니다.<br/>
e는 event 또는 evidence, H는 Hypothesis를 말합니다.<br/>
P(H|e) = (P(e|H)*P(H))/P(e)<br/>

식을 설명하자면, P(e|H)는 Likelihood입니다. 이게 주어진 상태를 가정하지요, 반대로 P(H|e)는 사후확률, Posterior로, 얼마나 이 가설이 그럼직한가에 대한 값입니다.<br/>
P(H)는 사전확률, Prior라고 부르며 evidence와는 전혀 상관없이 가설 자체의 확률을 말합니다.<br/>
P(e)는 Marginal이라고 부르며, 모든 i에 대해 P(e|Hi)*P(Hi)값의 합을 뜻합니다. 모든 가능한 가설 하에 새로운 사건 e가 일어날 확률인것이죠.<br/>

왜 이 정리가 필요할까요?<br/>
간단합니다. P(H|e)를 바로 구할 수 없기 때문이죠.<br/>
하지만 우변에 있는 모든 값들은 저희가 알아낼 수 있습니다.<br/>

문제를 하나 봅시다.<br/>
두개의 바구니가 있고, 한쪽에는 빨간공 50개, 파란공 50개가 담겨있으며 한쪽에는 빨간공 30개, 파란공 70개가 담겨있습니다.<br/>

1. 바구니를 고른다.<br/>
2. 그 바구니 안에서 공을 꺼낸다.<br/>

이렇게 뽑았을 때 그 공이 빨간공이었는데 첫번째 바구니에서 나온 공일 확률을 구해봅시다.<br/>

빨간공일 사건을 e로두고 첫번째 바구니일 확률을 H라고 합시다.<br/>
그럼 P(H|e)라는 조건부확률을 구해야하는 것이 우리가 해야할 일인데, 바로 구하기 어렵기 때문에 베이지 정리를 이용해서 우회해서 풀어내는 것이죠.<br/>

p(e|H) = 첫번째 바구니에서 꺼냈는데 그공이 빨간색일 확률 = 1/2 (첫번째 바구니의 빨간색 비율이 50/100이니까)<br/>
P(H) = 첫번째 바구니를 선택할 확률 = 1/2<br/>
p(e) = 빨간공일 확률 = p(e|H)*p(H) + p(e|H')*p(H') = 1/2*1/2 + 3/10*1/2 = 2/5<br/>

혹시 p(e|H)를 (저처럼ㅎㅎ) 1/4라고 구한분이 계시다면.. 너무 자연스럽게 p(e|H)*p(H) 즉, 왼쪽 바구니를 선택하고 동시에 빨간공일확률을 구해버렸던 것입니다.<br/>

P(H|e) = (P(e|H)*P(H))/P(e) = (1/2 * 1/2)/(2/5) = 1/4 / 2/5 = 5/8<br/>

3/8이 두번쨰 바구니에서 빨간공을 꺼낼 확률입니다.<br/>

분모의 marginal을 구하기 위해서는 모든경우를 다봐야해서 computation은 integral할 것을 요구합니다.<br/>
그러다보니 분모를 정확한값을 계산하기가 불가능한 경우가 있습니다.<br/>
그럴때 Approximation 기법을 이용해줘야하는데 variational bayes, belief propagation 등이 있습니다.<br/>
너무 지엽적이니 여기에서는 더 다루지 않습니다.<br/>

주요 수식을 다시 한 번 기억합시다.<br/>
P(A|B) = P(A,B)/P(B) = (P(B|A)*P(A))/P(B)<br/>

Bayes Classifier의 구현은 매우 간단해보입니다.<br/>
~~~
if P(B|A)*P(A) > P(B|A')*P(A'):
    x = A사건에 해당
~~~
이게 전부죠.<br/>

하지만 이것만으로 풀 수 없는 경우가 생깁니다.<br/>
예를들어 feature가 두개로 늘어나기만해도 바로 구할수 없어진답니다.<br/>
그래서 사용되는 것이 바로 Naive Bayes 입니다.<br/>

Naive Bayes Classfier의 구현 시 매우 중요한 Assumption이 있습니다. 바로 Feature들이 서로 **독립적**이라는 것입니다.<br/>

독립적이라면 P(A,B,C)=P(A)*P(B)*P(C)가 성립하기 때문입니다.<br/>
이는 feature간에 상호 커플링 등의 관계가 있다면 성립되지 않습니다.<br/>
그래서 P(feature1,feature2|A)P(A) = P(feature1|A)P(feature2|A)P(A)가 성립되어 풀어낼 수 있어집니다.<br/>

하지만 여전히 예측확률값이 0이 나올 수도 있다는 risk가 존재합니다. 그래서 normalization을 적용해 이를 해소하기도 합니다.<br/>
분포를 이용하는 것이지요.<br/>
그 방법론이 바로 Gaussian Naive Bayes 입니다.<br/>
지금까지는 P(X|Class)를 단순히 빈도수에만 기반하여 계산했지만, 특정 분포를 따른다고 가정을 할 수 있습니다.<br/>
분포에 기반하여 결과값을 얼버무리는 것이죠!<br/>

Gaussian Naive Bayes Classifier를 구현할 때에는 Gaussian 분포를 가정합니다.<br/>
(수식 이미지)

(수정중)