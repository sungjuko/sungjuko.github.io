---
layout: post
title: 인텔리제이에서 DB 스키마가 모두 나오지 않는 문제
date: 2020-12-25
Author: soreal
tags: [Intellij]
comments: true
toc : true
---

Intellij DB를 연결했는데 테이블이 보이지 않을 때.

## 문제상황

간단한 현상인데 처음 마주하면 당황스러운 현상.

인텔리제이 자체 데이터베이스 DB를 연결을 제대로 했는데 스키마나 테이블이 안나오는 현상이 발생할 때가 있다.



## 원인

기본 DB datasource 설정 체크가 풀린 상태로 연결 되기 때문.

***

## 해결

DataBase tab -> `Data source properties` 라는 탭 공구모양 달린 아이콘 클릭 -> Schema 탭에 들어감

이후 연결& 표기하길 원하는 테이블이 모두 체크 되어있는지 확인하고 풀려있을 시 모두 체크할 것!


해결완료!


***
- 자체 tags

#우당탕탕트러블슈팅 #깨알팁

