---
title: "How to rename files using python"
categories: 
  - BigData
last_modified_at: 2020-06-30T00:47:00+09:00
toc: true
---

Intro
---
블로그 관리를 하다보면 이미지들을 연속으로 대량 올리게 될 때가 있습니다.<br/>

그 때 파일이름을 일일이 치는게 귀찮아서 파일 이름을 1~n까지로 수정해주는 코드를 간단히 짰습니다.<br/>

저의 경우에는 ppt 슬라이드를 모두 JPG로 내보낸 뒤 블로그에 연속으로 사진을 올리는 경우가 더러 있었거든요..<br/>


백장이 넘어가는 프레젠테이션의 경우에는 마크다운으로 일일이 이미지 불러들이는 코드 쓰기도 애매해서 제가 편하려고 짠 코드인데

repository를 파기는 너무 간단한 코드라서 블로그에 쓰기 \+ 혹시 저와 같은 분들이 계실 수도 있으니까 ㅎㅎ 기록해두겠습니다.<br/>

파일 이름 변경
---

~~~python
import os
from os import rename

dir_url = 'D:/ohjinjin.github.io/assets/images/20200629ai_exchangerate/'
files = os.listdir(dir_url)

for f in files:
    rename(dir_url + f, dir_url + f.replace('슬라이드',''))

# create md codes for blog
for f in range(1, len(files)+1):
    print('{% raw %} <img src="https://ohjinjin.github.io/assets/images/20200629ai_exchangerate/' + str(f) +'.JPG" alt=""> {% endraw %}<br/>')
~~~

<br/><br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>