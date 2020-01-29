---
title: "How to rename virtual environment on ANACONDA"
categories: 
  - Anaconda
last_modified_at: 2020-01-29T20:00:00+09:00
toc: true
---

흔히 있는 일은 아닐 수 있지만 가상환경의 이름을 변경하고자할 때가 있을 겁니다.<br/>
<br/>
하지만 conda env와 관련하여 rename이라는 명령어는 없습니다.<br/>

그래서 새로운 이름의 env를 생성하면서 기존에 존재하는 가상환경을 복사해줘야합니다.<br/>
아래 명령어를 따라해주시면 됩니다.<br/>
> conda create --name [new env name] --clone [old env name]<br/>
>conda remove --name [old env name] --all<br/>

<br/>
바꾸려는 가상환경의 새 이름으로 생성하면서 기존에 존재하던 가상환경을 복사하는 것 입니다.<br/>
이후 기존에 존재하던 가상환경은 삭제해주면 됩니다.<br/><br/>

개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>