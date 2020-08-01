---
title: "how to build a container contains Anaconda, Python3 on docker"
categories: 
  - Server
last_modified_at: 2020-08-01T18:23:00+09:00
toc: true
---

본 포스트에서는 Anaconda와 python3가 올라가 있는 도커 이미지를 다운 받고 컨테이너를 생성하여 격리된 개발환경을 구축하는 과정을 기록합니다.<br/>

**도커 이미지를 pull**<br/>
이미 누군가가 친절하게 anaconda와 python3가 올라가 있는 환경을 갖춘 도커 이미지를 올려주었답니다.<br/>

도커 허브에서 검색하면 civis\-jupyter\-python3라는 이름의 이미지를 찾을 수 있습니다.<br/>

저는 이 친구를 pull 받아서 사용하겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture2.png" alt=""> {% endraw %}<br/>

**이미지 확인**
잘 받아졌는지 확인하기 위해서 이미지들을 출력해봅니다.<br/>
이미지 리스트들 중 방금 다운받은 civisan...가 보이지요?<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture3.png" alt=""> {% endraw %}<br/>

**현재 실행중인 도커 프로세스 확인**
도커의 프로세스들을 모두 확인합니다.<br/>
필요없는 컨테이너는 깔끔하게 작업하기 위해 모두 종료하거나 삭제해주시고 진행하시면 좋을 것 같습니다.<br/>
근데 전 공용 서버 pc라서 안껐습니다 ㅎㅎ<br/>

**컨테이너 생성하면서 실행**
pull 받은 civis 이미지를 가지고 docker_for_ohjinjin이라는 이름의 컨테이너를 생성하면서 터미널 배시를 통해 대화할 수 있도록 프로세스를 키면서 실행시키라고.. 도커 명령어를 입력했습니다.<br/>
포트는 9090을 사용할 것입니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture4.png" alt=""> {% endraw %}<br/>

python 버전이나 anaconda 버전 확인 명령어등을 입력하게 되면 이미 잘 설치 되어있는 것으로 확인되실 겁니다.<br/>

저는 바로 테스트를 위해 주피터 노트북을 실행해보려고 합니다.<br/>

**Jupyter notebook 실행**
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture5.png" alt=""> {% endraw %}<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture6.png" alt=""> {% endraw %}<br/>

네 잘됩니다.<br/>
<br/>

**아나콘다 가상환경 생성**

제가 Anaconda와 python3가 올라간 이미지를 pull한 첫 번째 이유는..<br/>

머신러닝 프로젝트를 주로 하게 될 건데, python 언어를 주로 사용할 것이기 때문입니다.<br/>

두 번째 이유는 가상환경을 이용하기 위함인데요,<br/>
도커라는 프로세스 단위로 환경을 격리시켜주는 방법을 적용한 것은 공용서버에서 다른 사용자분들의 환경을 해치지 않기 위함이 목적이었기 때문에,<br/>

ohjinjin 환경 아래에서도 여러 프로젝트를 진행하다보면 프로젝트별로 요구하는 스펙이 다를 거니까 그들 간의 각각 독립된 conda 가상환경을 매번 따로 두기 위함이었습니다.<br/>

따라서 저는 첫 번째 프로젝트를 위한 가상환경을 아나콘다를 이용해 생성해주도록 하겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture7.png" alt=""> {% endraw %}<br/>

ㅎㅎ 여러분께선 conda update 먼저 하고 진행해주세용.<br/>


**가상환경 활성화**
기존에는 base라는 환경에서 실행되고 있었지만 제가 방금 생성한 가상환경을 활성화시켜주겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture8.png" alt=""> {% endraw %}<br/>

활성화가 잘 되었는지 정확하게 확인하기 위해 conda info \-\-env를 입력하면 * 표시가 제가 방금 생성한 가상환경에 붙어있는 것을 알 수 있습니다.<br/>

그럼 활성화된 것입니다.<br/>

**설치 패키지 확인**
이 가상환경에 어떤 패키지들이 설치되었는지 확인하기 위해 conda list를 입력합니다.<br/>

음 네 뭐 거의 아무것도 없네요.<br/>

여기서 머신러닝 프로젝트를 진행하기 위해서는 앞으로 tensorflow라던지 numpy라던지 pands라던지.. pickle.. 뭐 기타 등등의 3rd party library를 설치해줘야하겠지요!<br/>

참고로 tensorflow\-gpu 버전은 그냥 docker말고 nvidia docker로 설치해주셔야합니다!<br/>

**가상환경 커널로 등록**
아직 해당 프로젝트에 대한 소프트웨어 스택이 확정되지 않아 거기까진 진행하지 않았습니다. 다만 앞으로 내가 이 프로젝트를 할 커다란 통은 이 가상환경이 되는 것입니다. 이 프로젝트는 이 안에서만 놀게 될거에요!<br/>

따라서 편의를 위하여 pykernel로 등록해줍니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture9.png" alt=""> {% endraw %}<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200716docker_env/capture10.png" alt=""> {% endraw %}<br/>

짜잔입니당..!<br/>

제가 설정한대로 name이 display 되고 있습니다.<br/>

흠 근데 좀 보기싫길래 나중에 Python(env_project_rna)로 바꿔줬어요 ㅎㅎ<br/>

명령어는 똑같이 입력하되 display name 인수만 "Python(env_project_rna)"로 바꾸시면 커널 이름을 수정하실 수 있습니다.<br/>


<br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>