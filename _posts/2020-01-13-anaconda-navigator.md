---
title: "How to install 3rd party librarys on ANACONDA"
categories: 
  - Anaconda
last_modified_at: 2020-01-13T12:00:00+09:00
toc: true
---

아나콘다(Anaconda)
----------------------------

아나콘다는 수학 또는 과학 분야에서 사용되는 여러 패키지 관리와 디플로이를 단순화할 목적으로 만들어진 Python과 R 프로그래밍 언어의 오픈 소스 배포판입니다.<br/>

가상 환경 생성
아나콘다 설치 시 함께 설치된 아나콘다 네비게이터(Anaconda Navigator)를 켭니다.<br/>

순서대로 <br/>
**Environments \> base(root)의 화살표 버튼 클릭 \> Open Terminal**<br/>
를 실행합니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200113anacondaNavigator/capture1.jpg" alt=""> {% endraw %}

가상환경이란 하나의 독립적인 통이라고 볼 수 있습니다.<br/>
그리고 아나콘다는 base(root)라는 기본 가상환경을 가지고 있습니다.<br/>
(캡처화면에서 확인되듯이 자주 사용되는 모듈 및 패키지는 이 base(root)라는 통 안에 미리 설치되어 있습니다.)<br/>
Tensorflow등 추가적으로 모듈을 설치해야할 경우 마찬가지로 이 통에 설치를 할 수 도 있지만, 설치 중 라이브러리 버전 오류 등이 발생하거나 엉키게 되면 아주 골치가 아파집니다.<br/>
그런 문제를 예방하기 위한 목적으로 프로젝트별로 각기 다른 가상환경을 새로 하나 만드는 겁니다.<br/>

조금 전에 켰던 터미널창으로 돌아와서 가상환경을 새롭게 생성해봅시다.<br/>

>conda update conda<br/>
콘다를 업데이트<br/>
>conda create \-n 가상환경이름<br/>
[가상환경이름]이라는 이름의 가상환경을 생성<br/>
>conda info \-\-envs<br/>
가상환경 목록 조회를 통해 잘 생성되었는지 확인<br/>
>activate 가상환경이름<br/>
해당 가상환경을 활성화<br/>

여기까지 하게되면 쉘 왼쪽 이름이 base에서 활성화한 가상환경으로 변경되었음을 확인할 수 있습니다.<br/>

참고로 가상환경을 비활성화하는 명령어는 아래와 같습니다.<br/>
>deactivate<br/>

<br/><br/>
또한 가상환경을 삭제하는 명령어는 아래와 같습니다.<br/>
>conda remove \-\-name [가상환경명] \-\-all<br/>

anaconda navigator를 보시게 되면 조금 전 생성한 가상환경도 리스트업되어있음을 확인할 수 있습니다.<br/>

새로운 모듈을 새 통안에 설치하기 위해서는 가상환경을 **활성화**한 상태에서 설치하면 됩니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200113anacondaNavigator/capture2.JPG" alt=""> {% endraw %}

Tensorflow 설치
----------------------------
이 포스트에서는 third party library 중 텐서플로우를 설치하는 과정을 보이도록 하겠습니다.<br/>

cmd 쉘에서 모듈을 설치할 경우에는 pip를 사용했지만 아나콘다에서는 conda를 이용하는 것이 훨씬 좋다고 합니다.<br/>

>conda install tensorflow<br/>
tensorflow를 설치<br/>

설치가 완료되었다면 잘 설치되었는지 콘다 리스트를 조회해 확인합니다.<br/>
>conda list<br/>
이 명령어를 입력하면 해당 가상환경 안에 설치된 패키지를 조회해줍니다.<br/>

아래와 같은 코드의 python 파일을 작성해 다시 한 번 패키지가 잘 설치되었는지 확인해줍니다.<br/>
>import tensorflow as tf<br/>
>a=tf.zeros(2,1)<br/>
>b=tf.ones_like(a)<br/>
>print(a)<br/>
>print(b)<br/>

그러기 위해서는 해당 가상환경 안쪽에 jupyter notebook도 설치해줘야하는데요, 계속해서 주피터 노트북을 사용하는거라고하면 편의상 글로벌 가상환경에 만드는 것도 나쁘지 않을 것 같습니다.<br/>
하지만 저는 새로 생성한 가상환경을 활성화시켜둔 상태에서 설치하도록 하겠습니다.<br/>

>conda install jupyter notebook<br/>
>jupyter notebook<br/>

주피터 노트북을 실행시켜줍니다.<br/>
브라우저가 실행되면서 주피터 노트북 tree가 보인다면 new \> python3를 선택하여 위 소스코드를 작성한 뒤 Run을 눌러 작동여부를 확인해주면 됩니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200113anacondaNavigator/capture3.JPG" alt=""> {% endraw %}

이렇게 결과가 나온다면 아나콘다의 가상환경을 이용한 제3라이브러리모듈, 텐서플로우 설치가 완료된 것 입니다.<br/>


개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/>