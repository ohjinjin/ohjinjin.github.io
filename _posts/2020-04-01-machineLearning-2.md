---
title: "Decision Tree_Machine Learning(2)"
categories: 
  - MachineLearning
last_modified_at: 2020-05-13T18:30:00+09:00
toc: true
---

Intro
---
학교 수강과목에서 학습한 내용을 복습하는 용도의 포스트입니다.<br/>

기존에 수강했던 인공지능과목을 통해서나 혼자 공부했던 내용이 있지만 거기에 머신러닝 수업을 들어서 보충하고 싶어서 수강하게 되었습니다.<br/>

gitlab과 putty를 이용하여 교내 서버 호스트에 접속하여 실습하는 내용도 함께 기록하려고 합니다.<br/>

* [원격 실습환경구축 따라하기](https://ohjinjin.github.io/git/gitlab/)<br/>
* [Machine Learning(1) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-1/)<br/>

* [Machine Learning(3) 포스트 보러가기](https://ohjinjin.github.io/machinelearning/machineLearning-3/)<br/>

이번 주제는 Decision tree에 대한 theory입니다.<br/>
<br/>

Decision tree
---
Tree 하면 나무라는 뜻이죠.<br/>
Deicision tree는 나무의 가지친 모양새를 본따 붙혀진 이름입니다.<br/>

단 거꾸로 되어있지요<br/>
그래서 제일 꼭대기에는 하나의 root node가 존재하게 됩니다.<br/>

각 가지들은 branch 또는 edge라고 부릅니다.<br/>

그리고 가장 끝에 자식이 없는 노드를 leaf node 또는 terminal node 또는 external node라고 부릅니다.<br/>

반대로 자식을 갖는 노드들은 internal node 또는 하나이상의 자식 중 결정을 지어준다해서 decision node라고 합니다.<br/>

어떤 offer에 대해 accept of decline 하는 즉 결정을 내려 분류를 하는 모델이 바로 decision tree입니다.<br/>

그렇다면 좋은 트리의 기준은 무엇일까요?<br/>

모델의 정확도, 트리의 높이 등이 그 기준이 됩니다.<br/>

정확도가 아주 높더라도 트리의 높이가 너무 높다면 처리 속도가 매우느릴것입니다.<br/>

좋은 트리의 조건은 다시 정리하자면, 트리의 높이는 최대한 짧되 leaf node에서 통일된 label의 데이터만 남는 것을 말합니다.<br/>

같은 데이터가 주어졌다해도 어떤 feature를 먼저 고려하는가에 따라 트리의 높이가 달라질 것입니다.<br/>

바로 그 시사점이 decision tree의 핵심입니다.<br/>

트리 생성방법은 root 노드부터 leaf 노드까지 순서로 간다는 것을 베이스로 둬야합니다.<br/>
1. 노드에서 고려할 데이터가 이미 하나의 class에만 속하였거나, 더이상 고려할 feature가 없을 경우에는 leaf node로 여겨 자식노드를 생성하지 않게 됩니다.<br/>

그렇다면 leaf 노드에 레이블이 여러개가 남겨져있다면 어떻게 판단해야할까요?<br/>
여러 방법이 존재할 수 있지만, 다수결로 분류 결과를 뱉게됩니다.<br/>

2. 또한 데이터들을 가장 잘 나눠주는 feature를 먼저 선택하는 것이 유리합니다.<br/>

3. 선택된 feature에 대한 조건 별로 자식노드를 생성합니다.<br/>

4. 각 자식노드에 대해서는 해당 조건을 만족하는 데이터만 고려하여 1부터 반복합니다.<br/>

그렇다면 2번 단계가 중요한데요, 가장 잘 나눠주는 feature를 어떻게 골라낼 수 있을까요?<br>
수학정으로 이를 정의해줘야합니다.<br>
그 전에 앞서서 intuitive하게 접근을 해봅시다.<br/>

두개의 클래스 A, B가 있을 때 feature f가 {a,b}중 하나의 값을 가질 수 있는데, f=a이면 Class는 A가 되고, f=b일 때 Class는 B가 되는 데이터들만 골라낼 수 있다면 f는 매우 훌륭한 feature이지 않겠습니까?<br/>

다시 말해 고려중인 f=v에 대하여 각 자식 노드에 동일 class에 속한 데이터들만 해당된다면 그야말로 완벽한 모델이지 않겠습니까?<br/>

하지만 트리는 항상 leaf 노드에서 완벽하게 나눠진다는 보장이 없다는 특징을 갖습니다.<br/>
optimal한 해를 구하는 것을 장담할 수 없는데 좋은 feature가 무엇인지 찾아내는 것에 대해 어떻게 접근해야 좋을까요?<br/>

1. purity
한 쪽 데이터만 존재할 수록 more pure하다고 표현합니다.<br/>

2. entropy
entropy는 purity의 반대 개념으로 Impurity라고도 부릅니다.<br/>

entropy에 대한 값의 범위는 0~1사이로 나오게되며 수식은 class i일 확률 \* -1 \* class i 일 확률의 log2 값의 합입니다.<br/>
급히 쓰느라 이미지로 수식을 첨부하지 못하고 글로 표현하고 있는 점 양해바랍니다.<br/>

entropy가 크다는 것은 purity하지 못하고 정보가 많다는 뜻이며 chaotic 하다고 표현합니다.<br/>

그렇다면 이 Entropy라는 개념을 tree 생성에 어떻게 적용할까요?<br/>

Information Gain의 개념이 여기서 나옵니다.<br/> IG는 부모노드의 엔트로피 - 자식노드들의 엔트로피 입니다.<br/>

자식노드가 여러개인 경우 가많기 때문에 Weighted Average Entropy of Children을 구하여 IG를 구하게 되는데요, Weighted란 단어가 붙은 의미는 자식노드들의 entropy만을 가지고 수식을 내기에는 각 자식노드들의 instance의 개수가 너무 많이 차이가 나면 성능에 좋지 않은 영향을 끼칠 수 있어 instance개수에 가중을 두고 고려하기 때문입니다.<br/>
무슨말이냐하면 극단적인 예를 들어, pure하나 한두개만 인스턴스가 있을 수도 있는 거잖아요? pure하진 않지만 500여개의 인스턴스중 단 몇개만 빼고는 하나의 class일 수도 있을 거구요!<br/>

그래서 실제 weighted average entropy of children의 수식을 펼쳐보면 각 자식의 entropy값에 instance개수만큼을 곱해주는 것을 확인할 수 있습니다.<br/>

결국 가장 잘 데이터를 나눠주는 feature를 선택하는 방법은 IG가 가장 큰 feature를 선택하는 것입니다.<br/>

그래서 모델의 학습시 초기에 각 feature별로 IG를 전부 계산하고 order에 따라 트리의 결정노드로서 먼저 생성되는 것이지요.<br/>
(최적의 해를 구할 것이라고 보장을 할수는 없지만요.)

Decision Tree 심화
---
위에도 썼지만 Decision Tree는 어떤 가설(IG가 큰쪽이 좋을것이다) 하에 알고리즘이 만들어진 것이지 최적의 해를 구할수 있는 것은 아닙니다.<br/>

이 모델은 현업에서도 많이 사용되는 모델로 이 알고리즘을 확실히 이해하고 넘어가야 합니다.<br/>

여태까지 본 데이터는 categorical feature로 yes-no 두 가지로만 분기가 되었습니다.<br/>
그런데 우리에게 주어진 feature가 만약 real-value라면 어떻게 해야할까요?<br/>

여러 방법이 있지만, 본 수업에서는 bin을 이용합니다.<br/>
bin 방법은 특정 root노드로부터 모종의 분기를 맞이해야하는데 그 value가 0~255까지 있다고 합시다.<br/>
첫번째 자식노드는 [0,32) 구간에 해당하는 경우, 두번째 자식노드는 [32,64) 구간에 해당하는 경우, ... , 여덟번째 자식노드는 [224,255] 구간에 해당하는 경우로 나누는 것입니다.<br/>
참고로 열린구간은 '[ | ]'로, 닫힌 구간은 '( | )'로 표기합니다.<br/>

여기서 잠시 tree 모양에 따른 용어를 알아보겠습니다.<br/>
균형이 잡힌 이진트리는 balanced tree, 높이가 높은 트리의 경우는 deep tree, 옆으로 넓게 퍼진 모양새의 트리는 bushy tree, 한쪽으로만 편향된 트리는 left | right skewed tree라고 부릅니다.<br/>

지금 당장은 이런 용어를 알아두는게 큰 의미가 없다고 생각할 수 있지만, 그래프나 트리 등으로 표현되는 알고리즘이나 모델들은 edge에 화살표 존재 유무도 구분해서 받아들여야합니다!<br/>

다시 Decision Tree로 돌아와서, Decision Tree는 Overfitting 되기가 쉽습니다.<br/>
Decision Tree는 학습하는 순간에 이미 overfitting이 되는가가 이미 정해집니다.<br/>
feature별 IG를 따져 위에서부터 정해져 내려오는데 국부적으로 최적으로 보이는 feature를 먼저 취함으로써 마치 나비효과처럼 첫단추부터 잘못끼우는 셈이 되는 것이죠.<br/>
그러면 이후에는 학습데이터에 과하게 맞추게될 가능성이 높습니다.<br/>
그렇기 때문에 Decision Tree 모델의 복잡성은 트리의 높이와 깊은 연관이 있습니다.<br/>

보통 데이터 마이닝 시 feature 값들을 0~1 사이의 값을 갖도록 normalization을 하는 과정을 거치기도 하는데, Decision Tree에서는 그럴 필요가 없습니다.<br/>
왜냐하면 해봤자 어차피 똑같은 노드형태를 취할 것이기 때문이죠.<br/>

Decision Tree는 구현이나 이해가 비교적 쉬운 모델입니다.<br/>
모델이 뱉어낸 결과도 사람이 보고 직관적으로 이해할 수 있으며 설명이 가능하다는 장점을 갖습니다.[WhiteBox]<br/>
여러 모델들을 배우다보면 이런 모델들이 흔치가 않답니다.<br/>

하지만 쉬운만큼 아주 powerful한 모델은 아닙니다. 그러다보니 아주 조금만 복잡한 문제를 해결하려해도 성능이 훅 떨어진다는 단점이 있습니다.<br/>
예를 들어 비선형 문제의 대표적인 문제인 XOR 문제의 경우에도 Decision boundary를 잘그려내지 못합니다.
<br/>
<br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>
