---
layout: post
title: PyCharm에서 pandas가 import 안될 때
date: 2020-12-26
Author: soreal
tags: [Pycharm, Pandas]
comments: true
toc : false
pinned : false
---


PyCharm 에서 판다스가 import 안되는 문제가 일어날 때가 있다.

import pandas 라고 아무리 쳐도 에러가 뜨는 현상이다.


<!-- more -->


## 문제상황 & 원인 


import pandas 가 안됨.

config에서 판다스 library를 못 받았기 때문.


## 해결 방법

1. Preferences 들어감

2. 프로젝트: [프로젝트명] 들어감

3. Python 인터프리터 잘 경로 설정되어있는지 확인

4. 그리고 패키지 명에 판다스 있는지 확인

5. 없으면  + 키 눌러서 pandas 검색 후 다운.


해결!



감사합니다.

