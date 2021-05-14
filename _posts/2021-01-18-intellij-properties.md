---
layout: post
title: Intellij에서 properties 파일이 깨질 때
date: 2021-01-18
Author: soreal
tags: [Intellij, 깨알팁]
comments: true
toc : false
pinned : false
---


인텔리제이로 properties 파일을 열었을 때 파일 인코딩이 깨져서 알아볼 수 없을 때가 있다. 한글 깨짐 현상을 해결해 보자.


<!-- more-->

> \BC@#\dajs\23gA\......

대략 다음과 같은 글자들로 알아볼 수 없는 주석이나 내용이 생성되어있을 것이다. 해당 현상은 Encoding이 utf-8로 맞지 않아 생기는 현상이다.


- Setting > Editor > File Encodings 에서 properties가 저장된 경로를 찾아 UTF-8로 변경한다.


일단 항상 UTF-8로 세팅을 다 해놓는 편이 정신건강에 이로운 것 같다. 
