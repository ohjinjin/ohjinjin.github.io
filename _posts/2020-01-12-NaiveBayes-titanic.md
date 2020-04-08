---
title: "Analyzing NaiveBayes model with titanic data of kaggle"
categories: 
  - MachineLearning
last_modified_at: 2020-04-8T15:27:00+09:00
toc: true
---

###### <span style="color:lightslategray"> #DSC활동 #ML</span>

캐글 데이터 타이타닉를 응용하여 EDA(Exploratory Data Analysis)를 포함한 데이터 마이닝부터 모델링까지 정말 잘 되어있는 실습 레퍼런스를 얻게 되었습니다.<br/>
그래서 저는 그 자료에서 적용된 모델링 기법 중 하나였던 Naive Bayes를 사용된 데이터에 맞춰 자세히 뜯어보려고 합니다.<br/>

(출처 : [https://github.com/minsuk-heo/kaggle-titanic/blob/master/titanic-solution.ipynb](https://github.com/minsuk-heo/kaggle-titanic/blob/master/titanic-solution.ipynb))


그 전에 앞서 Naive Bayes에 대하여 간단히 설명하고 정리하고 시작하겠습니다.<br/>


Naive Bayes란?
----------------------------

Naive Bayes는 **조건부 확률**을 채용한 머신러닝 모델입니다. 고로 Naive Bayes모델을 이해하기에는 베이즈 추론에 대한 사전지식이 필요합니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/bayes_expr.JPG" alt=""> {% endraw %}

조건부확률 P(A\|B)는 사건 B가 발생한 경우 A도 발생할 확률을 말하는데, 베이즈 정리는 이 때 P(A\|B)의 추정이 P(A∩B)와 P(B)에 기반을 두어야한다는 것을 말합니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/bayes_expr2.JPG" alt=""> {% endraw %}


이항하여 식을 정리해보면 위와 같은 식이 성립됨을 알 수 있습니다. 이 때 P(A)를 사전확률, P(A\|B)를 사후 확률이라고도 합니다.<br/>

베이즈 정리를 이 쯤 이해했다면 본격적으로 Naive Bayes에 대해서도 알아보도록 합시다.<br/>
우선 Naive 는 '순진하다'라는 뜻을 갖는 단어라고합니다. 이는 Naive Bayes 모델에 입력될 데이터셋의 모든 필드들이 동등하며 또 **독립적**이어야한다는 특성으로부터 착안된 것이 아닐까 개인적으로 생각합니다.<br/>

독립적? 아래와 같은 데이터가 주어지는 경우를 예로 들어 설명해보도록 하겠습니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/NB_ex1.JPG" alt=""> {% endraw %}
<br/>
(출처 : [https://gomguard.tistory.com/69](https://gomguard.tistory.com/69))-설명이 아주 잘 되어있어서 참고하고 이해할 수 있었습니다.

위 데이터의 경우 습도가 비가 올지 안올지에 대하여 사실은 더 중요한 변수일 수 있으나 이런 사실을 무시합니다. 독립적이라고 가정해야하기 때문이죠.<br/>
'만약 오늘 날씨가 좋고, 바람이 많이 불지 않고, 기압은 높은데, 온도가 낮다면 오늘 비가 올 것인가?'를 식으로 바꿔 예측하는 과정을 살펴봅시다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/NB_ex2.JPG" alt=""> {% endraw %}

직관적으로 여기까지는 식을 세울 수 있을 거라 예상합니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/NB_ex3.JPG" alt=""> {% endraw %}

앞서 배운 베이즈 정리에 의거하여 P(비|날씨∩\~바람∩기압∩\~온도)를 치환하는 것까지도 무리 없이 이해가 가시리라 짐작합니다.<br/>
하지만 그 다음은 설명이 조금 더 필요합니다.<br/>

이런 계산이 가능해지는 이유는 바로 나이브 가정 때문입니다.<br/>
나이브 가정이란 확률변수 A, B가 독립일 때 A, B의 결합확률은 주변확률의 곱이라는 것을 말합니다.<br/>

우리는 P(A,B) = P(A)P(B) 라는 것을 중학교 때? 초등학교 때였나요 ㅎㅎ 어쨌든 어린 시절 배워서 잘 알고 있습니다.<br/>

다시 바꿔 말하자면 나이브 가정은 조건이 되는 확률변수 C에 대한 A,B의 결합 조건부 확률이 C에 대한 A, B의 조건부 확률의 곱과 같으면 A와 B가 C에 대해 조건부독립이라고 할 수 있다는 걸 말합니다.<br/>
P(A,B|C) = P(A|C)P(B|C)가 성립한다는 것이죠.<br/>

예를 들어 독립변수 x가 D차원인 경우에는<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/bayes_expr3.JPG" alt=""> {% endraw %}

이며 이 때의 가능도 함수는<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/bayes_expr4.JPG" alt=""> {% endraw %}
가 됩니다.<br/>

그렇기 때문에 P(날씨|비)P(\~바람|비)P(기압|비)P(\~온도|비)P(비)/P(날씨∩\~바람∩기압∩\~온도) 로 식을 바꿔 쓸 수 있답니다.<br/>
분모는 무시하고 풀어서 '구해야 할 것 1'을 해결하네요!<br/>
같은 방법으로 '구해야 할 것 2'도 해결할 수 있습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/NB_ex4.JPG" alt=""> {% endraw %}

'구해야 할 것 1'과 '구해야 할 것 2'를 구했다면 문제에서 설명한 조건 하에 비가 올 확률과 비가 오지 않을 확률을 각각 계산해낼 수 있습니다.<br/>



Naive Bayes의 특징
-----------

위처럼 확률 이론을 기반으로 예측값이 계산되는 Naive Bayes 모델은 간단한 가정을 베이스로하는 설계의 알고리즘이지만, 특정 지도학습에 있어서 매우 효율적으로 훈련이 가능하다고 합니다.<br/>
또한 분류에 필요한 파라미터를 추정하기 위한 트레이닝 데이터의 양이 매우 적더라도 식을 세울 수만 있다면 학습이 가능하다는 장점을 가집니다.<br/>

다만 Naive Bayes 모델을 사용할 경우 모수 추정을 기반으로 한다는 것을 기억해야 합니다.<br/>
무슨 말이냐하면,<br/>
첫째로 클래스의 사전확률은 클래스간 **동일**확률로 가정하여 계산한다는 것을 기억해야합니다.<br/>
둘째로는 훈련용 데이터셋으로부터 클래스의 확률 추정치는 미리 계산해두면 됩니다. 이후에는 대입하여 계산하면 된다고 볼 수 있겠습니다.<br/>
(참고로 특징의 분포에 대한 모수들을 추정하기 위해서는 트레이닝 셋의 특성들을 위한 비 모수 모델이나 분포를 가정 또는 생성해야한다고 합니다.)<br/>

각 특징 분포에 대한 여러 가정들이 Naive Bayes 분류 이벤트를 구분합니다.<br/>
예를 들어 이산적 특성을 가진 특징들을 다루게 될 경우 **다항분포 나이브베이즈 모델** 또는 **베르누이분포 나이브베이즈 모델**이 흔히 사용되고, 연속적인 값을 지닌 데이터를 처리할 경우에는 **가우시안 나이브베이즈 모델**을 사용하곤 합니다.<br/>
전형적으로 각 클래스의 연속적인 값들이 가우스 분포를 따른다고 가정하는 것이라고 하네요.<br/>

(일부러 특징값들을 이산화하여 베르누이분포 모델을 사용하는 경우도 있지만, 이산화 과정에서 의미있는 차별적 정보를 손실하게 될 가능성이 있다고 합니다.)<br/>

실수 특징 x를 포함하는 트레이닝 데이터의 경우 클래스에 따라 데이터를 나눈 뒤, 각 클래스에서 x의 **평균**과 **분산**을 계산합니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/bayes_expr5.JPG" alt=""> {% endraw %}

테스트 시에는 클래스의 값들의 확률분포가 정규분포식을 통하여 각각 M과 S로 매개변수화 되어 계산됩니다.<br/>


이러한 특징을 가진 머신러닝 모델, Naive Bayes를 가지고 이번엔 캐글의 타이타닉 데이터를 응용한 실습 레퍼런스 결과와 함께 분석해보겠습니다.<br/>



캐글 데이터 타이타닉 적용
------------------------

k-NN 포스트에서도 작성했듯이 훈련용 데이터는 892개, 테스트 데이터는 417개였습니다.<br/>
Naive Bayes모델 역시 지도학습 모델로서 활용되었는데요,<br/>
데이터셋의 필드 중에서 저희는 survived를 0 또는 1로 예측하는 모델을 만드는 것입니다.<br/>
k-NN때와 마찬가지로 정답 레이블이 주어진 것이죠.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/finalDataCapture.JPG" alt=""> {% endraw %}

EDA 과정 이후의 데이터 폼 일부분을 캡처한 것 입니다.<br/>
Naive Bayes 모델에 입력될 실질적인 값들이라고 할 수 있지요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/sourceCodeCapture.JPG" alt=""> {% endraw %}

실습 레퍼런스의 원본 코드에서 발췌 캡처하였습니다.<br/>
Naive Bayes 모델의 성능평가 결과로 78.78의 score를 확인할 수 있습니다.<br/>

해당 레퍼런스에서 사용되었던 다른 머신러닝 모델과 비교해서 딱히 성능이 우수하다고 말하긴 어렵겠네요..<br/>
개인적인 의견으로는 연속적인 데이터를 다뤄서 가우시안 나이브 베이즈를 사용하려면 EDA 과정이 참 중요할 듯 합니다.<br/>

이번에도 마찬가지로 실습 데이터를 표로 표현해보았습니다.<br/>
Naive Bayes 특징에서 소개되었 듯 모수추정 기반으로 훈련용 데이터셋으로부터 클래스의 확률 추정치는 미리 계산해줍니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/chartCapture.JPG" alt=""> {% endraw %}

정말로 각 평균과 분산을 계산할 자신은 없어서 blah로 대체하겠습니다ㅎ ㅎ<br/>

그리고 P(survived0)=P(survived1)=0.5로 각 클래스의 동등한 값을 할당해줍니다.<br/>
참고로 사전 확률 분포는 보통 도메인 지식이나 트레이닝 셋에서의 각 클래스의 빈도수에 기반을 두고 정해지기도 한다고 합니다.<br/>

위 문제에 대해서 Naive Bayes 수식에 대입하여 다시 한번 풀이하자면<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200112NaiveBayes/bayes_expr6.JPG" alt=""> {% endraw %}

이렇게 되겠습니다.<br/>



개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/>
