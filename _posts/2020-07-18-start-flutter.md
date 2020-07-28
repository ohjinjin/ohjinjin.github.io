---
title: "start Flutter with visual studio code"
categories: 
  - Flutter
last_modified_at: 2020-07-28T22:48:00+09:00
toc: true
---

아래 링크로 이동하여 Flutter SDK를 설치합니다.<br/>
[https://flutter.dev/docs/get-started/install/windows](https://flutter.dev/docs/get-started/install/windows)

혹은 Flutter의 공식 git repository를 통해 클론해서 사용하셔도 됩니다.<br/>

[https://github.com/flutter/flutter](https://github.com/flutter/flutter)

저는 첫번째 방법으로 설치를 진행하겠습니다. 다운로드 받은 zip파일을 flutter 공식 문서에서 시키는대로 C:\\src\\flutter에 압축해제해줍니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture1.png" alt=""> {% endraw %}

그 다음 flutter_console.bat 파일이 최상단에서 보이실 건데요 관리자 권한으로 실행해주세요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture2.png" alt=""> {% endraw %}


여기까지하셨다면 flutter 콘솔에서  flutter 명령을 실행할 준비가 완료된 상태입니다.<br/>

아래와 같은 화면이 확인되실 겁니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture3.png" alt=""> {% endraw %}


**사용자 환경변수**에 C:\\src\\flutter\\flutter\\bin 과 같은 flutter/bin의 full 경로를 추가해주세요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture4.png" alt=""> {% endraw %}


flutter를 설치를 완료하기 위해 필요한 의존성을 볼 수 있도록 도와주는 flutter doctor를 실행해볼 것입니다.<br/>
windows 콘솔을 열어서 flutter doctor라는 명령여럴 입력해주세요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture5.png" alt=""> {% endraw %}


설치 완료를 위해 어떤 작업이 추가적으로 필요한지를 보여주게 됩니다.
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture6.png" alt=""> {% endraw %}


안드로이드 스튜디오 라이센스가 없다네요 doctor가 시키는대로 해보겠습니다.<br/>

~~~
flutter doctor --android-licenses
~~~

위 명령어를 입력해주세요.<br/>
그리고 y를 입력해주다보면... 아래와 같이 자격을 취득하게 됩니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture7.png" alt=""> {% endraw %}


그 다음 doctor의 소견은 android 스튜디오를 방금 막 설치하고선 최초 실행을 안해줘서 아직 설치가 안되어있다고 뜨는 것 같으니 설치를 마저 진행하고나서 다시 doctor를 실행시켜보겠습니다.<br/>

안드로이드 스튜디오 설치과정이 궁금하신 분들께서는 [여기](https://ohjinjin.github.io/android%20studio/install-androidstudio/)를 눌러주세요.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture8.png" alt=""> {% endraw %}


네 Dart와 Flutter plugin을 android studio에서 설치해봅시다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture9.png" alt=""> {% endraw %}


SDK manager를 통해서 Flutter plugin을 검색해서 설치를 진행하면 Dart가 required라고 함께 설치하라고 뜹니다. 설치해주시면 됩니다.<br/>

플러그인 설치 이후에는 원활한 적용을 위하여 IDE를 재부팅하시길 권장드립니다<br/>

이제 vs code에서 extension을 설치하겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture10.png" alt=""> {% endraw %}
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture11.png" alt=""> {% endraw %}

doctor가 요구하는 것은 다 맞췄는데, 저는 Dart 언어 특성상 가독성...을 조금이라도 높이고자 rainbow brackets라는 플러그인도 함께 설치해주었습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture12.png" alt=""> {% endraw %}

새로운 flutter project, hello world를 작성해보겠습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture13.png" alt=""> {% endraw %}

ctrl\+P를 누르게 되면 검색툴바같은게 뜰 건데요, 아래 문장을 입력해주세요.<br/>

~~~
>flutter
~~~

그 다음 new project를 생성하도록 선택해주시고 바로 이어서 project name을 입력하면 됩니다.<br/>
원하는 저장위치를 선택해주시고 나면 샘플 프로젝트의 main.dart 파일이 열리게 됩니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture14.png" alt=""> {% endraw %}

바로 테스트코드를 빌드해볼거에요<br/>
마찬가지로 ctrl\+P를 눌러 아래 명령어를 입력해주세요<br/>

~~~
>flutter:emu
~~~

이 정도만 입력하더라도 밑에 launch emulator가 뜨네요. 선택해주세요.<br/>
그러면 안드로이드 sdk를 통해 미리 설치해둔 에뮬레이터 목록이 뜨게 됩니다.<br/>

기기를 선택하시면 가상 기기가 뜰 겁니다.<br/>
빌드 해봅시다. F5를 눌러주세요!<br/>

에뮬레이터에서 데모 앱을실행시켜주시면 잘 되는 것을 확인하실 수 있습니다.<br/>

{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200718flutter/capture15.png" alt=""> {% endraw %}

<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>