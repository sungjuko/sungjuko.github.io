---
layout: post
title: linux 특정 문자 grep 해서 앞 뒤로 몇 줄 잡아내기
date: 2020-12-25
Author: soreal
tags: [Linux, 깨알팁]
comments: true
toc : false
pinned : false
---

리눅스 로그 편하게 찾아서 보는 법.

리눅스 로그 볼 때 특정 문자가 포함된 줄을 find 한 다음 grep이나 sed로 해당 구간을 보고 앞뒤 몇 줄을 보고 싶을 때 쓰는 방법을 정리해보았다.

<!--more -->


## 리눅스 특정 문자 줄 grep해서 앞 뒤로 몇 줄 꺼내기

명령어 요약

````
$ grep -n '원하는 것 혹은 정규식' [해당 파일]
$ sed '시작행,끝행!d' [해당파일]
````

참조 링크: [리눅스 문자열 매칭 행번호 확인](https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%EB%AC%B8%EC%9E%90%EC%97%B4_%EB%A7%A4%EC%B9%AD_%ED%96%89%EB%B2%88%ED%98%B8_%ED%99%95%EC%9D%B8, "리눅스 문자열 행 번호 확인")

 예시:
````
grep -n '2020-12-22 14:50:' linux-more-resources-9201.log

2375:2020-12-22 14:50:14.042 DEBUG [bootstrap,39739d9,167da,true] 579 --- [syncExecutor-10] c.l.m.test.service.blog.LinuxBlogTest  : temp, ar.getSomething:soreal13, soreal github...
````


## grep 구간 보기

참조 링크: [리눅스 grep 범위 보기](https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_grep_%EB%B2%94%EC%9C%84_%EB%B3%B4%EA%B8%B0)


````
$ sed '2368,2380!d' linux-more-resources-9201.log

2020-12-22 14:50:14.042 DEBUG [bootstrap,39739d9,167da,true] 579 --- [syncExecutor-10] c.l.m.test.service.blog.LinuxBlogTest  : temp, ar.getSomething:soreal13, soreal github...
2020-12-22 14:50:14.042 DEBUG [bootstrap,39739d9,167da,true] 579 --- [syncExecutor-10] c.l.m.test.service.blog.LinuxBlogTest  : temp, ar.getSomething:soreal13, soreal github...
2020-12-22 14:50:14.042 DEBUG [bootstrap,39739d9,167da,true] 579 --- [syncExecutor-10] c.l.m.test.service.blog.LinuxBlogTest  : temp, ar.getSomething:soreal13, soreal github... :
================예시 로그 예시 ======================
2020-12-22 14:50:14.042 DEBUG [bootstrap,39739d9,167da,true] 579 --- [syncExecutor-10] c.l.m.test.service.blog.LinuxBlogTest  : temp, ar.getSomething:soreal13, soreal github...
2020-12-22 14:50:14.042 DEBUG [bootstrap,39739d9,167da,true] 579 --- [syncExecutor-10] c.l.m.test.service.blog.LinuxBlogTest  : temp, ar.getSomething:soreal13, soreal github...
`````


### 결론

grep -n 옵션으로 줄을 찾고 sed로 위아래 대충 범위 줄을 출력시킨다.

> $ grep -n '[찾는문자열]' [파일]  
> 
> $ sed '시작행,끝행!d' [파일]


끝!