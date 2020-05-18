---
title: "Building a MySQL server development environment using Docker Toolbox"
categories: 
  - Server
last_modified_at: 2020-05-19T00:11:00+09:00
toc: true
---

Intro
---
먼저 서버 구축을 해봤을 때의 기록을 남겨둔 포스팅의 링크입니다.<br/>
[https://ohjinjin.github.io/server/install-docker/](https://ohjinjin.github.io/server/install-docker/)<br/>

위 링크에서는 오류를 포함하고 있으며 해당 오류에 대해 해결하는 과정을 본 포스트에서 다루니 참고하시기 바랍니다.<br/>

docker에 centOS를 올리고 MySQL 설치까지 어떻게 해보았는데 systemctl 명령어에서 "Failed to get D-Bus connection: Operation not permitted" 오류가 나왔습니다.<br/>

찾아보니 cgroup을 찾지 못하거나 권한 문제로 이용할 수 없어  centOS 이미지부터 다시 올려줘야한다는 것을 알았습니다.<br/>
원인과 해결책에 대한 내용이 실려있는 포스팅의 링크를 [여기](https://this-programmer.com/entry/%EB%8F%84%EC%BB%A4Docker%EB%A1%9C-CentOS-%EC%9D%B4%EB%AF%B8%EC%A7%80-systemctl-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-2-failed-to-get-DBus-connection-Operation-not-permitted)에 걸어놓겠습니다.<br/>

위 포스팅을 참고하여 처음부터 다시 서버 환경을 구축하는 내용에 대해 기록합니다.<br/>


Install centOS
---
기본 제공되는 정식 centOS가 아닌 Dockerfile 이라는 이름의 도커 파일을 직접 만들어줘야 합니다.<br/>
파일의 내용은 아래와 같이 써주세요.<br/>

~~~
FROM centos

ENV container docker

RUN yum -y update; yum clean all
RUN yum -y install systemd; yum clean all; \
(cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

VOLUME ["/sys/fs/cgroup"]
CMD ["/usr/sbin/init"]
~~~

vim 에디터를 이용해 만들어도 좋습니다만 저는 권한 문제로 잘 되지 않아서 windows 환경에서 파일을 생성하고 c/Program Files/Docker Toolbox/에 저장해주었습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture26.JPG" alt=""> {% endraw %}

확장자명 없이 저장하기 위해서는 저장 시 파일명을 큰 따옴표로 감싸주면 됩니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture27.JPG" alt=""> {% endraw %}

도커파일을 생성했다면 아래 명령어로 빌드합니다.<br/>

~~~
docker build --rm -t centos7-systemd .
~~~
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture28.JPG" alt=""> {% endraw %}

빌드가 완료되었으면 아래의 명령어를 입력해 컨테이너로 올립니다.<br/>
~~~
docker run --privileged --name centos_demo -p 80:80 -itd -e container=docker -v /sys/fs/cgroup:/sys/fs/cgroup centos7
-systemd /usr/sbin/init
~~~

이렇게 실행하게되면 대화형쉘이 바로 뜨는 것이아니라 백그라운드에서 centos가 돌게 되므로 docker exec 명령어로 다시 실행해봅니다.<br/>

~~~
docker exec -it centos-demo /bin/bash
~~~

프롬트가 바뀐 것을 확인하실 수 있을 겁니다.<br/>

centOS가 잘 설치되었다면 이어서 바로 MySQL을 설치해보겠습니다.
<br/><br/>


Install MySQL
---
MySQL 설치 과정에 대한 링크를 [여기](https://ohjinjin.github.io/server/install-docker/#install-mysql)에 걸어드리겠습니다.<br/>

MySQL만 봐주시면되는데 위 포스트에서는 어떤 오류를 맞이하게 되거든요, 하지만 그 오류를 해결할 수 있도록 빌드된 dockerfile을 통해 centOS를 올려주었으니 이제 잘 될겁니다!<br/>

~~~
systemctl start mysqld
systemctl enable mysqld
~~~

위 명령어를 입력했을 때 아래와 같이 나와야 정상적으로 실행된 것 입니다!<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture29.JPG" alt=""> {% endraw %}

명령어 mysql을 입력해 mysql을 실행해봅시다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200502docker/capture30.JPG" alt=""> {% endraw %}

프롬트가 바뀌었다면 성공적으로 설치하신 것입니다.<br/>

<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!

<br/><br/>