---
title: "HMM-Machine Learning(17)"
categories: 
  - MachineLearning
last_modified_at: 2020-07-03T10:24:00+09:00
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

<br/>

HMM 모델에 대해 배워보겠습니다.<br/>

HMM(Hidden Markov Model)
---
뭐가 숨겨졌다는걸까여?
HMM은 군집화 모델이 아닙니다
과거의 경험(sequential pattern)을 토대로 현재의 의사결정을 하는 것이 Markov에 대한 직관입니다!
이를 테면 친구와 가위바위보를했는데 계속비겨왔어요 저친구가 가위를 내지 않을까?하는 느낌과 오늘 해가 떴는데 내일부터 3일간 날씨가 해-비-해일 확률은 얼마일까? 같은것들이요

여태봐온 군집화나 분류 문제들과는 조금 다른 이런 순서를 가진 패턴에 대해서 배울 수 있는거져

열방향은 말그대로 오른쪽에서 왼쪾으로 갑니다.
시간을 거슬러 올라가기때문에여
베타2에 괄호 안에는 3
베타 2에 괄에 1이들어가는경우
초기값 줫던 베타에다가 관측…이자나
우리한테 줫던 시퀀스에서 가장 마지막 이 얼마나 라이클리하냐
다더하는고에요
베타값 자체가 아니라 점수를 얻어야하는거거든
파이화 첫번째관측값에 대한 확률값과 첫번째상태 자체에대한 확률과  다곱해서 더해서 계산해줘여
오른쪽에서 왼쪽으로 오면서 모든 경우에 대해 
뉴럴넷에서도 그랬듯이 종합한 정보일거란거져
hmm에서 알아야할 세가지중ㅇ에서 probability evaluation은 끝났어염

다음은 옵티말 스테이트 시퀀수입니다.
점수를 매기는게 아니라 최적화
forward passing+backtracking
알고 보면 별거없어여
내가 가진 경험과지식에의해(모델파라미터) 계산해보건데 각 노드위에 써잇는게 그러한 확률값
당연히 맨오른쪽에 잇는애들이 시퀀스상 젤 종합적인정보잖아요
제일 그럼직한애를 후보로올려여
그리고 거슬러올라가여

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture200.JPG" alt=""> {% endraw %}

해해비비엿구나하고 결론을 내릴수잇어여
계산을 어케하는지 보겟습니다
큰녀석을 찾아라
두개 중에서 큰놈을 찾아라
S11에 대해서는 그것과 a11을 곱해여
A11은 비가내렷는데 다시 비가올 확률을 곱하는거에여
그다음은 a21
타우라는 표기법이 새로나왓는데여
두번째에서 첫번째노드인 s21에서 이 표기법이 나왓는데
이 길을 표시해놓고 가는거에여
두개 중에서 더 큰녀석이 누구엿는지 유망한애가 누구엿는지를 기억하는 용도입니다.
그럼 이전스텝으로 갈때에는?백트랙킹할 때 쫓아갈 수 있으니까
2라고 써놔여

그럼 나중에는 결국 이 타우값만 보고 쫓아가면되는거야
그렇게 동적프로그래밍..

방금까지 설명했던 과정을 좀더 formal하게 수식으로 표현한거에여

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture201.JPG" alt=""> {% endraw %}

백트랙킹왜쓰냐면 가장유망한 시퀀스 찾아내ㄹ건데 젤 쉽게 하려구 체크해놓는겨
22번슬라이드는 혼자해보기

HMM의 파라메터 에스터메이션은 baum welch 알고리즘인데 본질적으로는 EM 알고리즘에 속합니다.
24페이지 Z 몇번째항아리인지를 가리킴
Q=p로 놓고 시작하네여
알파 앞에서 본 포워드패싱이랑 똑같아여
베타도 마찬가지에여 맨마지막은 1로 두고시작한댔자나염
아래부분 수식보면 알파랑 베타랑 t번째스텝까지 구해서 곱한겨

알파랑 베타는 중복되서 구해지는건없어여
모든 상태를 구한거 다더한거가 분모져
나를기준으로 모든 왼쪽경우가 알파, 오른쪽경우가 베타임니다

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture202.JPG" alt=""> {% endraw %}

24번슬라이드가 e스텝,,,
이제 m스텝에 들어와서 파라메터를 다시 계산해야합니다.


{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture203.JPG" alt=""> {% endraw %}

이 제약조건을 만족하게하려구 라그랑지 메소드 적용해줍니다
이후 전체식을 편미분해서 각 파라메터를 구해줍니다
파이 i는 i번째state가 처음 골라질 확률이었잖아여
파이를 봣으니까 a랑 크게 다를건 없는데
 새로나타난부분이 빨간색부분이에여


{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture204.JPG" alt=""> {% endraw %}

j번짹 관측일때만 고려하겠다라는 말이됩니다.
P()부분을 확률이라고 하기보다 걍 어떤 색공이 뽑힌 횟수라고 해봅시다
Bij는 i번째항아리에서 j번째 색을 관측하는 상황을 말합니다
색별로 카운트를 하기위해서 저 델타함수가 들어간거에여


{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200410ml/capture205.JPG" alt=""> {% endraw %}

(수정중)