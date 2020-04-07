---
title: "How to use R in jupyter notebook"
categories: 
  - MachineLearning
last_modified_at: 2020-04-08T03:25:00+09:00
toc: true
---

R은 통계와 관련하여 자주 쓰이는 프로그래밍 언어입니다.<br/>

R도 Jupyter Notebook 환경에서 사용하면 참 편리하겠죠.<br/>

시계열 분석이라는 과목을 수강하면서 실습하는 모든 내용에 대해 R studio보다는 jupyter notebook 환경으로 코딩을 하고 깃허브에 업로드하려고 합니다.<br/>

R을 jupyter notebook 환경으로 사용하도록 하는 방법에 대해 기록하겠습니다.<br/>

저는 Anaconda 가 설치되어있어 Anaconda navigator로 간편하게 설치해보려고 합니다.<br/>

Anaconda 설치에 대해 궁금하시다면 [여기](https://ohjinjin.github.io/anaconda/anaconda-navigator/)를 눌러주세요.<br/>

1. Anaconda Navigator를 이용하여 새 가상환경 생성하기<br/>
Navigator를 켜셨다면, 아래와 같이 R 프로그래밍을 위한 독립적인 가상환경을 새롭게 만들어줍니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200407r_jupyter/capture1.JPG" alt=""> {% endraw %}

반드시 R에도 체크해주셔야합니다.<br/>

2. 가상환경 활성화 및 Jupyter Notebook<br/> 실행하여 확인하기
가상환경 생성이 완료되었다면 이후에는 방금 생성한 가상환경을 활성화시킬 건데, Jupyter notebook과 함께 open해주시면 됩니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200407r_jupyter/capture2.JPG" alt=""> {% endraw %}

Jupyter notebook이 켜졌다면, R언어용 새 notebook파일을 생성해주세요!
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200407r_jupyter/capture3.JPG" alt=""> {% endraw %}
<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200407r_jupyter/capture4.JPG" alt=""> {% endraw %}

여기까지는 아래 링크를 참고해 작성한 포스트입니다.<br/>
[https://docs.anaconda.com/anaconda/navigator/tutorials/r-lang/](https://docs.anaconda.com/anaconda/navigator/tutorials/r-lang/)<br/>

여기서 설치가 끝난 것이 아닙니다. 각종 R 패키지들의 사용을 위해서는 명령프롬트를 통해 설치해줘야할 것이 몇가지 더있는데요,<br/>
기존에 설치해 사용하셨던 R과 R studio에서는 이상없이 설치되는 패키지가 Anaconda Jupyter notebook 환경에서는 에러가 되는 상황을 맞이하게됩니다.<br/>
그 이유는 jupyter notebook이 r자바경로와 설정되지 않아서라고 합니다.<br/>

콘솔을 켜 R을 입력해 대화형 쉘을 실행시키고 아래 명령어를 입력해주세요.<br/>

> install.packages('devtools')<br/>

저는 국내 seoul 1이라는 CRAN 저장소를 선택했습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200407r_jupyter/capture5.JPG" alt=""> {% endraw %}

그 다음은 IRkernel을 설치합니다.<br/>
이것이 R과 jupyter notebook을 연동시켜줄겁니다.<br/>

> devtools::install_github('IRkernel/IRkernel')<br/>

성공적으로 설치를 했다면 아래 명령어로 설치가 잘 되었는지 확인해주세요.<br/>

> IRkernel::installspec()<br/>

정상적으로 설치가 되었다면 jupyter notebook으로 R을 확인해볼겁니다.<br/>
R 쉘에서 나와 jupyter notebook을 실행시켜주세요.<br/>

그럼 정상적으로 실행이 될겁니다!<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200407r_jupyter/capture6.JPG" alt=""> {% endraw %}