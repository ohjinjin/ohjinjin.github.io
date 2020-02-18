---
title: "APMSETUP MySQL encoding Korean "
categories: 
  - database
last_modified_at: 2020-02-18T15:40:00+09:00
toc: true
---

저는 apmsetup을 통해 MySQL 서버와 아파치 서버를 관리하고 있습니다.<br/>

DB에 한글 데이터를 저장하고 나면 phpMyAdmin에서 확인해볼때 ???로 나타나더군요.<br/>

table이나 database 세팅을 해주면 될거라고 생각했는데 그대로더라구요.<br/>

구글링해보고 이 한글 깨짐 현상을 해결하는 과정을 기록합니다.<br/>

MySQL 설정 파일인 my.ini라는 파일에서 수정을 해주는 것인데요,<br/>

본래 이 파일의 위치는 2010버전의 apmsetup7을 다운받으신 경우엔 C:\\APM_Setup\\Server\\MySQL5\\data 였을겁니다.<br/>

하지만 복사해서 옮겨붙여넣어주실건데요,
**C:\\APM_Setup\\Server\\MySQL5**에 my.ini 파일을 복사, 붙여넣기 해주시면됩니다.<br/>

그 다음,<br/>

**my.ini**라는 파일 내 [client] 부분에 아래 내용을 추가해줍니다.<br/>
>default\-character\-set=utf8<br/>

<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200218encoding/capture1.JPG" alt=""> {% endraw %}

그 다음 역시**my.ini**라는 파일에서 이번엔 [mysqld] 부분에 아래 내용을 추가해줍니다.<br/>
>init_connect = SET collation_connection = utf_general_ci<br/>
>init_connect = SET NAMES utf8<br/>
>character\-set\-server = utf8<br/>
>collation\-server = utf8_general_ci<br/>

<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200218encoding/capture2.JPG" alt=""> {% endraw %}

그 다음도 마찬가지로 **my.ini**라는 파일에서 이번엔 [mysqldump] 부분에 아래 내용을 추가해줍니다.<br/>
>default\-character\-set = utf8<br/>

<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200218encoding/capture3.JPG" alt=""> {% endraw %}

설정을 변경하였으니 정상적으로 적용될 수 있도록 아파치와 MySQL을 껐다가 다시 켜고, 이미 저장을 하면서 데이터가 손상되었을 수 있으니 데이터 자체를 아예 삭제하고 새롭게 추가해 확인해보겠습니다.<br/>
새롭게 DB 또는 table을 만들어줄 때에도 마찬가지로 collation 설정을 utf8_general_ci로 설정하시기를 권장합니다!<br/>

이제 한글이 깨지지 않고 잘 나타나는 것을 확인하실 수 있을 겁니다.<br/>
{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200218encoding/capture4.JPG" alt=""> {% endraw %}

혹시나 미리 만들어뒀던 데이터베이스나 테이블 등 삭제하고 다시 생성하기가 난감한 상황이라면, 아래와 같은 질의어를 통해 기존 내용을 수정할 수도 있다고 합니다.<br/>

> ALTER DATABASE 데이타베이스_이름 CHARACTER SET utf8 COLLATE utf8_general_ci;<br/>
> ALTER TABLE 테이블_이름 CHARACTER SET utf8 COLLATE utf8_general_ci;<br/>

<br/>
<br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>