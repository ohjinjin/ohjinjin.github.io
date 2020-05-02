---
title: "Install Docker Toolbox"
categories: 
  - Server
last_modified_at: 2020-05-02T21:54:00+09:00
toc: true
---

Intro
---
프로젝트를 하다보면 전 보통 센트럴 서버 파트를 맡곤하는데요,<br/> 기존까지는 서브넷 환경을 구축해놓고 서버 클라이언트 패러다임의 통신 따위를 구현해왔었지만, COVID19 사태로 인해 함께 모여서 작업하는게 쉽지가 않다보니 공통된 개발환경을 구축해 배포해 이를 해결하기로 했습니다.<br/>

그나마 익숙한 VB도 있었지만 현업에서도 많이 사용된다는 docker와 CentOS를 이 기회에 사용해보려고 합니다.<br/>
docker 컨테이너에 centOS를 올리고 APM 환경까지 구축해 배포해주는게 1차적인 목표인데요, centOS 설치까지의 과정을 기록하려고 합니다.<br/>

docker는 컨테이너를 기반으로하는 오픈소스 가상화 플랫폼입니다.<br/>
docker는 다양한 프로그램이나 실행환경 등을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포하거나 관리하는 것을 단순하게 해줍니다.<br/>
제 경우처럼 데이터베이스 서버 뿐만 아니라 여러 백엔드 프로그램, 메시지 큐등 어떤 프로그램도 컨테이너로 추상화할 수 있으며 조립PC, AWS, Azure, Google cloud등 어디에서든 실행할 수 있다는 큰 장점을 갖습니다.<br/>

제 PC의 OS는 windows10 pro 미만입니다. ㅠ.ㅠ<br/>
그래서 본 글에서는 docker를 windows10 Home에 설치하는 과정에 대해 기록합니다.<br/>

dockerToolBox로 설치를 하게 되면 virtual Box 기반으로 동작하는 docker를 실행할 수 있습니다.<br/>
Windows 10 pro 사용자는 Docker Desktop for Windows 로 설치하면 되고, BIOS 설정에서 Hyper-V를 enabled로 설정해주면 됩니다.<br/>

도커를 설치 및 실행하기 위해서는 다음의 조건이 되어야 가능합니다.<br/>

windows 버전이 windows7 이상이어야하며, 하드웨어 자원이 가상화를 지원해야합니다.<br/>
가상화를 지원하더라도 enable 하도록 BIOS 설정창 또는 작업관리자의 성능 탭에서 설정을 해주셔야 합니다.<br/>

* docker Toolbox 다운로드 url : [https://github.com/docker/toolbox/releases](https://github.com/docker/toolbox/releases)
여기에서 저는 19.03.1 installer를 다운받았습니다.<br/>

설치를 하셨다면, 도커 iso 등의 설치를 위해 Docker Quickstart Terminal을 실행해주시기 바랍니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture1.JPG" alt=""> {% endraw %}

이렇게 화면이 나온다면 도커가 성공적으로 설치된 것입니다.<br/>
이후의 도커의 모든 명령은 cmd나 powershell이 아닌 이 터미널 화면에서 실행하시면 된다는 점을 기억해주세요!<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture2.JPG" alt=""> {% endraw %}
도커가 잘 설치되었는지 윈도우 powershell에서 확인해보았습니다!<br/>

하지만 처음 사용하시는 경우엔 CL 인터페이스가 다소 불편하실 수 있습니다.<br/>
도커이미지 설치나 컨테이너 실행 등의 작업을 GUI 환경으로도 하실 수 있습니다. 바로 kitematic(alpha) 인데요, 이를 실행해서 CentOS를 설치해보도록 하겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture3.JPG" alt=""> {% endraw %}
centOS 검색 결과에서 첫번째 인덱스의 CREATE 버튼을 클릭해주세요.<br/>

이미지 다운로드가 완료되면 CentOS 이미지의 컨테이너가 자동 생성되며 실행됩니다.<br/>
(이미지 4)

exec를 클릭하여 선택한 컨테이너에 콘솔로 접속합니다.<br/>

<br/>
<br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!
<br/><br/>