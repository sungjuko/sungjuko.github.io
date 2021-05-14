
## READ_MD 번역 

### 2020-12-23

~한국어 사용자를 위한 LOFTER 번역(Feat.google)~


LOFFER는 LOFTER에서 벗어나는 데 도움이되는 소프트웨어입니다.

GitHub에 게시 할 수있는 Jekyll 블로그입니다. GitHub에 블로그를 배포하기 위해 코드를 작성하거나 명령 줄을 사용할 필요가 없습니다.

이제이 문서를 기본 튜토리얼과 분리했습니다.이 문서는 LOFFER의 기존 기능과 업데이트를 설명하는 데 사용됩니다. 

** 코드 기반이없는 사용자를 위해 작성된 튜토리얼을 보려면 [여기 클릭](https://fromendworld.github.io/LOFFER/document/)**


## 콘텐츠 업데이트

### 2019-07-25 V0.4.0

업데이트 된 콘텐츠 개정 디렉토리가 건너 뛰어 깨지는 문제는 완벽한 해결책은 아니지만 깨지지는 않습니다.

LaTeX 렌더링에 대한 지원이 추가되었습니다. [참조](https://fromendworld.github.io/LOFFER/math-test/)。

top 기능을 높이려면 게시물의 YAML Front Matter에 추가하기 만하면됩니다 (이는 기사 헤드의 정보입니다).

` pinned: true `，이 기사는 올릴 수 있습니다.

LOFFER의 테마 색상을 변경하는 방법도 소개합니다. LOFFER는 오픈 소스 색상 표를 사용합니다. 

[Open Color](https://yeun.github.io/open-color/) 색상 표에서 제공하는 옵션 색상은 다음과 같습니다.：red, pink, grape, violet, indigo, blue, cyan, teal, green, lime, yellow。

LOFFER의 기본 상태는 청록색입니다. 테마 색상을 변경하려면 파일을 열기 만하면됩니다. ` _sass/_variables.scss `，파일의 모든 청록색을 원하는 색상으로 바꿉니다. 예를 들어, 청록색 찾기, 인디고 바꾸기, 모두 바꾸기, commit, 완료!


### 2019-07-20 V0.3.0

새 버전은 디렉토리 기능을 추가합니다. 게시물의 정보 센터에`toc : true`를 추가하면이 블로그 게시물에 디렉토리가 표시됩니다.

이번에는 구성에 대한 수정이 없으므로 [이 방법](https://github.com/KirstieJane/STEMMRoleModels/wiki/Syncing-your-fork-to-the-original-repository-via-the-browser)를 전달할 수 있습니다. 업데이트에 대한 풀 요청을 자신에게 제공하십시오.

카탈로그는 [allejo의 jekyll-toc](https://github.com/allejo/jekyll-toc)를 기반으로합니다.

현재 재판에서 작은 문제를 발견했습니다. 당신의 타이틀 레벨이 루틴에 따라 변하지 않으면 이해하지 못할 것입니다 .

`# 1 단계 표제`

다음은 다음과 같아야합니다

 `## 2 단계 표제`,  
 
 `### 3 단계 표제`

참고 : 현재 디렉토리는 데스크톱 버전에만 표시됩니다.


### 2019-06-30 V0.2.0

새 버전은 스타일을 더욱 최적화하고 GitHub 문제 주석을 기반으로 Gitalk를 지원합니다 (아래 구성 지침 참조).

LOFFER를 이미 포크하고 새 버전으로 업데이트하려면 [이 방법](https://github.com/KirstieJane/STEMMRoleModels/wiki/Syncing-your-fork-to-the-original-repository)을 시도해보세요. -브라우저를 통해 또는 대부분의 구성 설정과 모든 게시물을 유지하는 한 간단히 삭제하고 다시 시작할 수 있습니다.

LOFFER는 컨테이너 일 뿐이며 게시물은 블로그의 핵심입니다.

## 지원기능

Markdown 문서를 사용하여 _post 폴더에 블로그 게시물을 게시합니다. 기존 기능에는 작성자 표시, 게시물 배치, 디렉토리 추가가 포함됩니다.

YAML 예：

    ---
    layout: post
    title: Markdown번역소개
    date: 2013-07-16
    Author: Shengbin 
    tags: [sample, markdown]
    comments: true
    toc: true
    ---

레이블 및 날짜별로 블로그 게시물 아카이브를 봅니다. / tags 및 / archive 페이지를 확인하세요.

블로거의 소셜 미디어를 연결합니다. _config.yml을 입력하십시오.

Disqus 및 Gitalk 댓글 영역을 모두 지원합니다. _config.yml에서 설정하십시오.


## 감사

* [Jekyll](https://github.com/jekyll/jekyll) - 이 사이트의 기본
* [Kiko-now](<https://github.com/aweekj/kiko-now>) - 먼저 테마를 분기 한 다음 중국어로 수정 한 다음 LOFFER가 있습니다.
* [Font Awesome](<https://fontawesome.com/>) - 소셜 네트워크 아이콘은 무료이며 FontAwesome의 오픈 소스 콘텐츠입니다.



## 이 프로젝트를 도와주세요

더 많은 사람들에게 그것을 사용하도록 소개하고, 더 높은 곳을 없애고, 자유롭게 비행하세요!

Issues and Pull Requests에 오신 것을 환영합니다.

STAR PLEASE!!

![img](https://raw.githubusercontent.com/FromEndWorld/LOFFER/master/images/givemefive.png)
