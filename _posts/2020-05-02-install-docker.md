---
title: "Building a server development environment using Docker Toolbox"
categories: 
  - Server
last_modified_at: 2020-05-11T22:12:00+09:00
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
그래서 본 글에서는 비록 성능은 좋지않다하지만 docker toolbox로 windows10 Home에 설치하고 centOS 이미지를 올린 뒤 그 안에 Nginx와 python, MySQL을 설치한 컨테이너를 생성하는 과정에 대해 기록합니다.<br/>

dockerToolBox로 설치를 하게 되면 virtual Box 기반으로 동작하는 docker를 실행할 수 있습니다.<br/>
Windows 10 pro 사용자는 Docker Desktop for Windows 로 설치하면 되고, BIOS 설정에서 Hyper-V를 enabled로 설정해주면 됩니다.<br/>

도커 이해를 돕기위한 비유)*********************수정예정
도커는 VB, <br/>
이미지는 ova 파일,<br/>
컨테이너는 생성한 머신<br/>

Install DockerToolbox
---
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
도커가 잘 설치되었는지 윈도우 powershell에서도 확인해보았습니다!<br/>

하지만 처음 사용하시는 경우엔 CL 인터페이스가 다소 불편하실 수 있습니다.<br/>
도커이미지 설치나 컨테이너 실행 등의 작업을 GUI 환경으로도 하실 수 있습니다. 바로 kitematic(alpha) 인데요, 이를 실행해서 CentOS를 설치해보도록 하겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture3.JPG" alt=""> {% endraw %}
centOS 검색 결과에서 첫번째 인덱스의 CREATE 버튼을 클릭해주세요.<br/>
자세히 보면 우리가 원하는 환경에 맞춰 이미 만들어 놓은 것도 있을 수 있지만 아주 처음부터 만들어보죠!<br/>

이미지 다운로드가 완료되면 CentOS 이미지의 컨테이너가 자동 생성되며 실행됩니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture4.JPG" alt=""> {% endraw %}

실행이 완료되면, exec를 클릭하여 선택한 컨테이너에 콘솔로 접속합니다.<br/>

아래는 콘솔을 통해 컨테이너를 활성화한 모습입니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture5.JPG" alt=""> {% endraw %}


이 방법도 있지만, CLI 환경에서도 설치하는 방법을 기록해보겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture6.JPG" alt=""> {% endraw %}

~~~
docker search centos
~~~

라는 명령어로 검색을 해봅니다.<br/>

저 중에서 우리는 centos:latest를 이미 설치했으니<br/>

아직 설치가 안된 분들만 아래 명령어로 설치를 진행하시면 됩니다.<br/>
~~~
docker pull centos:latest
~~~

설치가 잘 되었는지 확인해봅시다.<br/>
~~~
docker images
~~~


{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture7.JPG" alt=""> {% endraw %}

이미지가 확인되지요.<br/>


CentOS 컨테이너 실행
----
우리는 "centOS를 이용할 것이며, yum을 이용해서 os 업데이트를 하고, yum을 이용해서 Nginx를 설치하고, python을 설치하고, MySQL을 설치한다" 라는 내용의 스크립트를 Dockerfile라는 파일명으로 사용해야 합니다.<br/>

그러니 centOS 이미지위에  실행해봅시다. <br/>interactive하게, 의사 TTY를 할당함으로서 터미널 입력을 위한 옵션으로 -i, -t를 설정하며 -p 옵션으로 포트를 외부에 노출할 때 바인딩할 기본 IP 주소를 설정해 centOS 컨테이너를 실행하겠습니다.<br/>

도커 프로세스 종료 시 컨테이너가 자동으로 제거되도록 -rm 옵션도 설정 가능하지만, 저는 오늘 주어진 시간 안에 환경 구축을 다하고 도커파일을 팀원에게 배포할 자신이 없으므로 해당 옵션은 빼고 진행합니다.<br/>

또한 터미널 bash를 실행하라고 centos에게 말해줍니다.<br/>

~~~
docker run -i -t -p 8080:80 --name WiseStudyServer centos /bin/bash
~~~

centos 이미지의 /bin/bash를 container로 실행시키며 그 컨테이너에 WiseStudyServer라는 이름을 지어줬습니다. 그리고 루프백의 8080번 포트를 container의 80번 포트로 연결하도록 설정했습니다.<br/>
이 연결되고 연결되고하는것은 도커가 자동으로 해주는데 굳이 포트 지정한거에요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture8.JPG" alt=""> {% endraw %}

prompt 위치가 바뀐 것이 확인되시죠?<br/>
컨테이너 생성 진짜 빠릅니다.<br/>
버박하고 비교가 안되요..그저 갓<br/>

참고로 컨테이너에서 빠져나올 때는 bash창에 exit를 입력하면 됩니다.<br/>
만들어둔 컨테이너를 시작 및 종료 할 때에는 docker start와 stop명령어를 이용하면되고, 재실행할 때에는 exec 명령어를 이용하면 최초 실행시와 동일한 container id로 접속되는 것을 확인할 수 있습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture10.JPG" alt=""> {% endraw %}

OS를 확인해보면 현재 centOS임이 확인됩니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture9.JPG" alt=""> {% endraw %}


Install Python3
----
파이선 3버전을 먼저 설치해보려합니다.<br/>

centOS의 패키지관리자로는 yum을 사용합니다.<br/>
패키지 관리자는 패키지의 설치 및 삭제 등의 관리를 실행하는 프로세스로서 패키지 설치를 위해서는 패키지가 저장된 위치가 있어야 합니다.<br/>
패키지가 저장된 레포지토리를 관리하는 것은 RPM(Redhat Package Manager)가 하지요.<br/>

참고로 패키지 설치 시 RPM raw파일을 받아서 직접 설치할 수도 있지만 다운로드나 압축해제, 인스톨, 환경변수 셋업까지 자동화해주는 yum을 사용하는 것이 훨씬 편합니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture11.JPG" alt=""> {% endraw %}

아래 명령어를 통해 파이선3을 설치합니다.<br/>

~~~
yum install -y python36u python36u-libs python36u-devel python36u-setuptools
~~~

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture12.JPG" alt=""> {% endraw %}

파이선이 잘 설치되었는지 확인을 해주세요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture13.JPG" alt=""> {% endraw %}

라이브러리들을 편하게 설치하기 위해서 pip도 설치해줍니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture14.JPG" alt=""> {% endraw %}

지금 보면 centOS에서 기본으로 사용하는 python2버전이 있어서 에러가 날 우려가 있기때문에 alias를 잡아보려합니다.<br/>

python3은 /usr/bin/python3에 설치되어 있어요.<br/>

vim으로 /home/.bashrc을 열어 아래와같이 python3의 경로를 추가해줍니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture15.JPG" alt=""> {% endraw %}

.bashrc 파일을 저장하고 source 명령으로 업로드한 내용을 적용합니다.<br/>
다시 python 버전을 확인하면 잘 적용되어 나오네요!<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture16.JPG" alt=""> {% endraw %}

혹시나 python 2를 사용하는 명령들이 영향받진 않았는지 확인을 위해 yum명령을 해봅니다.<br/>

~~~
yum
~~~

에러가 아니라 명령들의 리스트가 나오면 이상없는 것입니다.<br/>

파이선은 잘 설치했네요!<br/>
<br/>


Install Nginx
---
yum 저장소에는 nginx가 없어서 외부저장소를 추가해줘야합니다.<br/>
vi 에디터로 /etc/yum.repo.d/nginx.repo를 열어 아래내용을 추가해주세요.<br/>
~~~
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
~~~

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture17.JPG" alt=""> {% endraw %}

저장하고 나온 뒤에 yum을 통해 nginx 설치를 진행하시면 됩니다.<br/>

~~~
yum --showduplicates list nginx
~~~

위 명령어로 설치 가능한 nginx 버전을 확인합니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture18.JPG" alt=""> {% endraw %}

이 중 저는 스테이블 1.18을 설치하겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture19.JPG" alt=""> {% endraw %}

설치가 완료되었으면 버전 확인해주세요!<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture20.JPG" alt=""> {% endraw %}

Nginx도 설치 완료입니다.<br/>


Install MySQL
---
아래 명령어를 입력하여 yum repository package를 다운로드합니다.<br/>

> wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture21.JPG" alt=""> {% endraw %}

그 다음은 패키지를 설치해줍니다.<br/>
> yum localinstall mysql80-community-release-el7-3.noarch.rpm

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture22.JPG" alt=""> {% endraw %}

아래 명령어를 입력해 MySQL yum repository를 활성화합니다.<br/>

~~~
yum repolist enabled | grep "mysql.*-community.*"
~~~

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture23.JPG" alt=""> {% endraw %}

이제 아래 명령어를 사용해 MySQL을 설치합니다.<br/>

~~~
yum install mysql-community-server mysql mysql-libs mysql-devel mysql-server
~~~

혹시 mariadb와의 충돌이 난다면 아래 명령어를 통해 설치되어있는 maria db 패키지를 모두 출력한 후 모두 제거하고 다시 MySQL을 설치하면 됩니다.<br/>
~~~
yum list installed mariadb\*
~~~

저는 mysql-devel 부분에서 계속 오류가 나서 패키지 하나씩 끊어서 설치했습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture24.JPG" alt=""> {% endraw %}

~~~
systemctl start mysqld
~~~
 
~~~
systemctl enable mysqld
~~~

여기까지 했을 때 프롬트가 mysql로 바뀌었다면 설치가 완료된 것입니다.<br/>

하지만 저는 "Failed to get D-Bus connection: Operation not permitted" 오류가 나오네요.<br/>

찾아보니 centOS 이미지부터 다시 올려줘야한다는 것을 알았습니다.<br/>
원인과 해결책에 대한 내용이 실려있는 포스팅의 링크를 [여기](https://this-programmer.com/entry/%EB%8F%84%EC%BB%A4Docker%EB%A1%9C-CentOS-%EC%9D%B4%EB%AF%B8%EC%A7%80-systemctl-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-2-failed-to-get-DBus-connection-Operation-not-permitted)에 걸어놓겠습니다.<br/>

(수정중)

<br/>
<br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!
<br/><br/>