---
layout: post
title: git cannot identify version of git executable 문제
date: 2020-12-26
Author: soreal
tags: [Mac, Git, Intellij]
comments: true
toc : false
pinned : false
---


MacOS에서 intellij 콘솔 git cannot identify version of git executable: no response 오류가 뜰 때 해결하는 방법.


<!-- more -->

## 문제 상황 & 원인

`git cannot identify version of git executable: no response` 라는 오류가 뜰 때 IDLE이 깃 경로를 못잡아줘서 생기는 문제다.

아마도 MacOS 업데이트를 하거나 뭔가 작업을 하다가 꼬여서 생긴 문제로 추정된다.

## 해결 방법


1. cmd 에서 `which git` 커맨드로 git 경로를 확인한다

````
Last login: Tue Dec  1 16:06:50 on ttys000
➜  ~ git --version
git version 2.23.0
➜  ~ which git
/usr/local/bin/git
````

2. Intellij 에서 Preference -> Version Control -> Git -> Path to Git executable 주소 확인

주소가 아마 맞지 않을 것이다 주소 변경해주면 해결!





