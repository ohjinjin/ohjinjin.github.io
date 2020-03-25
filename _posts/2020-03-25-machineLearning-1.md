---
title: "Machine Learning(1)"
categories: 
  - MachineLearning
last_modified_at: 2020-03-25T15:08:00+09:00
toc: true
---

Intro
---
학교 수강과목에서 학습한 내용을 복습하는 용도의 포스트입니다.<br/>

기존에 수강했던 인공지능과목을 통해서나 혼자 공부했던 내용이 있지만 거기에 머신러닝 수업을 들어서 보충하고 싶어서 수강하게 되었습니다.<br/>

gitlab과 putty를 이용하여 교내 서버 호스트에 접속하여 실습하는 내용도 함께 기록하려고 합니다.<br/>

이번 주제는 theory 개요입니다.<br/>
<br/>

theory 개요
---
* 인공지능과 머신러닝과 딥러닝의 관계 : 인공지능이 머신러닝을 포함하며 머신러닝이 딥러닝을 포함하는 관계<br/>

* 인공지능과 빅데이터의 관계 : 빅데이터 파이프라인의 마지막 단계인 분석(analysis)에서 인공지능 기술이 사용될 수 있습니다. 이는 요리에 비유하여 다시 말하면 빅데이터가 인공지능의 '재료'가 되며, 인공지능은 '레시피' 역할이라할 수 있습니다.<br/>

* 뒤늦게 딥러닝이 각광받게 된 이유 : 과거에는 컴퓨팅 리소스가 부족하여 방대한 양의 데이터를 저장하거나 연산을 수행하기에 어려움이 있었으나 현대에와서 gpu기술의 발달 및 여러 소자들의 저가화 및 범용화를 통해 딥러닝 관련 연구가 활발히 이루어졌습니다. 이 과정에서 backpropagation 등 새로운 이론이 수립되기도 하며 더욱 발전할 수 있었습니다.<br/>

* 컴퓨터의 학습 패러다임은 결국 인간이 세상을 모방한 것이라 할 수 있습니다.<br/>
인공신경망 역시 생물학적 모방을 통해 개발되었지요.<br/>

* 학습 종류는 크게 supervised learning, unsupervised learning, semi-supervised learning, reinforcement learning가 있습니다.<br/>
<br/>

Supervised Learning
---
* supervised learning의 경우 학습을 위해서는 정답레이블이 주어진 데이터가 필요합니다.<br/>

* 보통 classifier의 구현에 많이 사용됩니다.<br/>

* 대표적인 분류모델은 의사결정트리(Decision trees), 인공신경망(Neural Networks), SVM(Support Vector Machine)등이 있습니다.<br/>

Unsupervised Learning
---
* unsupervised learning의 경우 학습데이터에 정답레이블이 주어지지 않습니다.<br/>

* 데이터만 있으면 군집화(clustering)알고리즘을 통해 기계가 스스로 학습 및 패턴을 찾습니다.<br/>

* 대표적인 군집화모델은 Hierarchical clustering과 k-means clustering이 있습니다.<br/>
<br/>

Semi-Supervised Learning
---
* semi-supervised learning은 일부 데이터에만 정답레이블이 존재하는데, 정답이 없는 데이터도 학습에 도움이 될 것이라는 가정을 기반으로하기 때문입니다.<br/>

* semi-supervised learning을 위한 모델들도 있으나 본 강의 커리큘럼에는 포함되지 않습니다.<br/>
<br/>

Reinforcement Learning
---
* reinforcement learning은 기계가 어떠한 행동을 했을 때 보상이 주어지거나 패널티가 주어져 더 나은 방향으로 학습합니다.

<br/>
<br/>
개인이 공부하고 포스팅하는 블로그입니다. 작성한 글 중 오류나 틀린 부분이 있을 경우 과감한 지적 환영합니다!<br/><br/>