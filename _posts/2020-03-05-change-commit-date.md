---
title: "How to change datetime of git commit"
categories: 
  - git
last_modified_at: 2020-03-05T01:01:00+09:00
toc: true
---

깃은 프로젝트의 소스코드의 버전관리를 해주는 목적으로 사용되다보니, 커밋이 진행된 시점을 기억하고 있답니다.<br/>

하지만 커밋 날짜 또한 변경이 가능합니다.<br/>

그래서 1일 1커밋도 조작하여 달성이 가능합니다.ㅎㅎ 물론 그 투자한 시간으로부터 얻은 지혜를 살 수는 없겠지요!<br/>

git rebase를 이용하여 특정 프로젝트의 커밋 일자 변경하는 과정을 기록해보겠습니다.<br/>
간단한 vim 사용법은 알고 계셔야 해서 [여기](https://www.opentutorials.org/course/730/4561)에 참고하실만한 링크를 걸어드리겠습니다.<br/>

git bash창을 열어 아래 명령어를 순차적으로 입력해주세요.<br/>

> git rebase [변경하고자하는 commit의 이전 commit 해시 값] -i<br/>


vi 에디터로 뭔가가 열린 것 같습니다!<br/>
변경하고자하는 커밋의 선택 내용을 edit로 적용하시면 되는데, 저는 내용은 그대로 유지하겠습니다!<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200305changecommitdate/capture1.JPG" alt=""> {% endraw %}<br/>

저장 후 종료해주시고요, 아래 명령어를 입력해주세요.<br/>

> GIT_COMMITER_DATE="[날짜]" git commit \-\-amend \-\-no\-edit \-\-date "[날짜]"<br/>


{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200305changecommitdate/capture2.JPG" alt=""> {% endraw %}<br/>

> git rebase \-\-continue<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200305changecommitdate/capture3.JPG" alt=""> {% endraw %}<br/>

<br/>
변경 내역을 적용할 때 쓰는 명령어인데, 제 캡쳐화면에서처럼 successfully rebased and updated~ 가 뜨는 것이아니라 refuse 당하셨다면..<br/>

> git commit \-\-allow\-empty<br/>

<br/>
위 명령어를 입력하신뒤 다시한번 rebase continue 명령어를 입력해주세요.<br/>

변경된 내용을 github에 강제 푸시해봅시다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200305changecommitdate/capture4.JPG" alt=""> {% endraw %}<br/>

그러면 본인 계정 깃허브 오버뷰에 잔디가 심어져 있을 겁니다!<br/><br/>


개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>