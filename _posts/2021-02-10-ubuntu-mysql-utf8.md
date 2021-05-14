---
layout: post
title: 우분투에서 mysql utf-8 (한글깨짐) 문제 해결하기
date: 2021-02-10
Author: soreal 
tags: [Linux, Ubuntu, Mysql, Infra]
comments: true
toc: true
---




DB에 데이터를 넣을 때 유니코드와 latin 문자 설정으로 인해 한글이 깨질 때가 있다. 

아래는 엑셀(csv, xlxs) 파일을로 DB에 데이터를 한 번에 넣고 싶을 때 사용했던 명령어 이다.


`mysql> LOAD DATA INFILE '/home/ubuntu/shark/db insert site.csv' INTO TABLE shark.site FIELDS TERMINATED BY ','; ` 


인터넷에 많은 해결 방법들이 존재하는데 내가 해결한 방법을 소개한다.


# 1. mysql 설정 확인

````
> mysql  show variables like 'C%';

````

아마도 중간중간 환경 변수에 lain1 이 끼워져 있는 것이 보일 것이다.



# 2. 깔끔하게 완전 삭제 및 재설치

데이터가 없길 바란다. 나는 초기 데이터 설정에서 발견한 문제라서 일단 복잡할 필요없이 깨끗하게 밀어버리기로 결정했다.


````
sudo apt-get remove --purge mysql*
sudo apt-get purge mysql*
sudo apt-get autoremove.
sudo apt-get autoclean.
sudo apt-get remove dbconfig-mysql.
sudo apt-get dist-upgrade.
sudo apt-get install mysql-server.
````


# 3. utf-8 설정


mysql 에서 최초 생성시 설정으로는 `mysql> stauts;` 를 사용하면 아마도 일부는 utf-8로 일부는 latin1으로 설정되어 있을 것이다.

이걸 바꿔줘야 한다.

이를 위해서 MYSQL의 설정 파일을 열어서 utf8로 기본 설정을 변경해 주는 작업을 해야한다.


````
$ vim /etc/mysql/my.cnf
````

해당 파일의 마지막에 다음과 같은 내용을 덧붙여준다.


````
...

[client]
default-character-set=utf8

[mysql]
default-character-set=utf8

[mysqld]
collation-server = utf8_unicode_ci
init-connect='SET NAMES utf8'
character-set-server = utf8

````

vim으로 수정할때 `i` 버튼으로 인서트 모드로 수정하고 `esc`로 빠져나와서 `:wq!`로 저장한다.



# 4. 외부 포트 열어주기.


설정 내용을 저장하기 위해서 mysql을 재시작 하기 전에, 포트 열어 주는 작업도 같이한다.

보통 외부 서버 우분투에서 mysql을 사용하는 경우 외부에서의 접속을 붙이는 것이 보통이기 때문이다.


````
> sudo su
> cd /etc/mysql/mysql.conf.d
> vim mysqld.cnf
````

설정 파일의 위치가 다를 수도 있으니 확인 바란다.

해당 파일에서 `bind-address` 값이 127.0.0.1로 되어있을 텐데 이를 `0.0.0.0`으로 바꿔주고 저장한다.


# 5. mysql 재시작하기

````
$ /etc/init.d/mysql restart
`````

이 명령아가 (나같은 경우엔) 먹을 때가 있고 안먹을 때가 있다. 아마 인내심을 가지고 초기화를 하거나, 제대로 따라왔다면 ok가 뜰것이다.

그러면 이제 mysql을 사용할 준비가 다 되었다.


````
mysql> status;

혹은

mysql> show variables like 'c%';
````

를 쳤을 때 아름답게 모두가 utf-8 로 설정이 되어있으면 해당 과정이 완료 된 것 이다.






