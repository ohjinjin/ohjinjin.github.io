---
title: "solutions of Q3 web of SWM 2020 test exam"
categories: 
  - Web
last_modified_at: 2020-03-13T18:44:00+09:00
toc: true
---

소프트웨어마에스트로 11기 지원자들을 대상으로 하는 1차 코딩테스트 D-1입니다.<br/>

이번 코딩테스트에는 구름IDE를 이용하는 것으로 공개되었는데요.<br/>

제공된 모의시험 문제에서 웹 문제인 3번에 대한 솔루션을 기록하려고 합니다.<br/>
단 문제를 유포하지 않는 것이 원칙이므로 문제 해결에 도움이 될 만한 정보들만을 간략하게 기록하려고 합니다.<br/>

우선 3번 문제를 해결하기 위해선 아래와 같은 선수지식이 필요합니다.<br/>
1. 웹 기초
2. HTML DOM 개념
3. javascript ajax fetch-then 문법
4. javascript lambda 문법

웹기초
------
웹 동작을 추상화해서 말하자면 request와 response입니다.<br/>

문제의 핵심 동작만을 설명하자면,<br/>
HTML의 입력형식으로부터 입력된 데이터들을 적절한 자료형을 이용하여 저장하는 등 일련의 처리를 거쳐 주어진 API로 넘겨주면서 request가 이루어집니다.<br/>

이후 API를 거친 후의 response를 받아오고 또 다시 일련의 로직과 처리를 거쳐 HTML DOM을 수정하여 결과값을 프레젠테이션하는 것이라 할 수 있겠네요.<br/>
이 동작을 가능하게 하는 것이 Javascript 코드가 되는 것이라고 볼 수 있습니다.<br/>

위 이벤트의 트리거 역할을 하는 HTML DOM(보통 버튼)의 속성 중 onclick 속성에 해당 동작을 하는 js를 연결시켜주면됩니다.<br/><br/>

HTML DOM 개념
------
HTML은 웹에서 뼈대 또는 내용 역할을 합니다.<br/>
뼈대를 이루는 것은 각종 HTML 태그들이고 각각의 컨텐츠들인데요,<br/>
DOM이란 이들 자체를 말한다고 보면 됩니다.<br/>
쉽게 말해.. HTML 태그들은 통신의 개념까지 갔을 때에는 그 개개의 데이터들이 모두 객체로서 취급될 것이기 때문에 DOM(Document Object Model)이라고 부릅니다.<br/>

js에서 HTML DOM에 접근하기 위한 방법으로는 [여기](https://humahumahuma.tistory.com/122)에 참고 포스팅을 링크로 걸어드리겠습니다.<br/><br/>


javascript ajax fetch-then 문법
------
js는 웹에서 동작을 담당합니다.<br/>
어떤 요청을 하는 것 또한 동작에 해당하겠지요.<br/>
js에서 요청을 보다 매끄럽고 간결하게 하기 위한 문법으로 fetch-then이라는 것을 만들었다고 보면 됩니다.<br/>

fetch(url,[option]) 함수에서 첫번째 인수는 말 그대로 요청하고자하는 url입니다.<br/>
option은 생략가능한 인수인데, SWM 문제3번의 경우에는 API로 요청을 할 때에 HTML 요청헤더를 지정 추가해 그 형식을 맞추기 위해 작성되었다고 보시면 됩니다.<br/>

어쨌든 그렇다면 **요청**을 해줄 함수라는 것을 아시겠지요? 그러면 당연히 조금 기다리면 **응답**을 받을 수 있으리라는 것까지 생각하시면 됩니다.<br/>

그런데 여기서 제가 말한 것처럼 조금 기다려야 받는다는 것이죠! 그걸 기다리는동안 컴퓨터가 블락킹되도록할 수는 없으니 효율적인 처리를 위해 비동기식으로 구현해놓은 것이 바로 then입니다.<br/>

then()의 인수로는 응답을 받은 뒤 실행하고자 하는 내용을 **익명함수**로서 많이 지정해주곤 하지만 SWM의 문제에서 제안한 방식은 lambda식입니다.<br/>

이 원리를 이해하는데에 도움이 된 참고문서를 [여기](https://www.youtube.com/playlist?list=PLuHgQVnccGMA9-1PvblBehoGg7Pu1lg6q)에 링크걸도록 하겠습니다.<br/>
5.0부터 보시면 되겠습니다.<br/><br/>

javascript lambda 문법
------
js 함수는 객체입니다.<br/>
그리고 람다식과 익명함수는 밀접한 연관이 있습니다.<br/>

lamdba 문법에 대해서도 [여기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98)에 참고할 만한 링크를 걸어두겠습니다.<br/><br/>


문제 해결에 도움이 되셨으면 좋겠습니다.<br/>

개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>