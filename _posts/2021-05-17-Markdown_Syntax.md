## 마크다운 문법 정리  (Syntax)

### 제목 (header) (H1 ~ H6 : #의 갯수로 지정)

```markdown
H1 크기
# [제목명]

H2 크기 이게 가장 적당함
## [제목명]
```

### 강조 (Emphasis)

```markdown
이텔릭체 : *[문자열]* 또는 _[문자열]_로 사용
볼드 : **[문자열]** 또는 __[문자열]__로 사용
이텔릭체 볼드 : **_[문자열]_**
취소선 : ~~[문자열]~~
밑줄 : <u>[문자열]</u>
```

이텔릭체 : *[문자열]* 또는 _[문자열]_로 사용  
볼드 : **[문자열]** 또는 __[문자열]__로 사용  
이텔릭체 볼드 : **_[문자열]_**  
취소선 : ~~[문자열]~~  
밑줄 : <u>[문자열]</u>  

> 줄 간격을 좁게하려면 shift+enter를 누르면 위 와같이 줄 간격이 붙어[?] 있습니다.

### 목록 (List)

```markdown
1. 번호를 붙일경우
   - 번호를 붙이지 않을 경우#1
   * 번호를 붙이지 않을 경우#2
   + 번호를 붙이지 않을 경우#3
```

  		1. 번호를 붙일경우  
  	   - 번호를 붙이지 않을 경우#1  
  	     * 번호를 붙이지 않을 경우 #2  
  	       + 번호를 붙이지 않을 경우 #3  

### 코드

4개의 공백 또는 하나의 탭으로 들여쓰기를 만나면 변환되기 시작하여 들여쓰지 않은 행을 만날때까지 변환이 계속된다.

### 코드블럭

- Case 1

```markdown
<pre><code>{code}</code><pre>
```

- Case 2

~~~markdown
```
<code>
```
~~~

- Case 3

~~~markdown
``` [Language]
~~~

> Language 부분은 지원하는 코드가 많으니 인터넷으로 참고하여 사용하면 된다.

### 수평선

```markdown
--- (Hyphens)
*** (Asterisks)
___ (UnderScore)
```

___

***

***

### 표

헤더셀을 구분할 때 3개 이상의 - (하이픈) 기호가 필요  
헤더 셀을 구분하면서 : (콜론) 기호로 셀(열/칸) 안에 내용을 정렬이 가능  
가장 좌측과 가장 우측에 있는 |(파이프) 기호는 생략 가능  

```markdown
| 값 | 의미 | 기본값 |
|---|:---:|---:|
| `static` | 유형(기존) 없음 / 배치 불가능 | `static` |
| `relative` | 요소 자신을 기준으로 배치 |  |
| `absolute` | 위치 상 부모(조상) 요소를 기준으로 배치 |  |
| `fixed` | 브라우저 창을 기준으로 배치 |  |

값 | 의미 | 기본값
---|:---:|---:
`static` | 유형(기존) 없음 / 배치 불가능 | `static`
`relative` | 요소 자신을 기준으로 배치 |
`absolute` | 위치 상 부모(조상) 요소를 기준으로 배치 |
`fixed` | 브라우저 창을 기준으로 배치 |
```

| 값         |                  의미                   |   기본값 |
| ---------- | :-------------------------------------: | -------: |
| `static`   |      유형(기존) 없음 / 배치 불가능      | `static` |
| `relative` |        요소 자신을 기준으로 배치        |          |
| `absolute` | 위치 상 부모(조상) 요소를 기준으로 배치 |          |
| `fixed`    |       브라우저 창을 기준으로 배치       |          |

| 값         |                  의미                   |   기본값 |
| ---------- | :-------------------------------------: | -------: |
| `static`   |      유형(기존) 없음 / 배치 불가능      | `static` |
| `relative` |        요소 자신을 기준으로 배치        |          |
| `absolute` | 위치 상 부모(조상) 요소를 기준으로 배치 |          |
| `fixed`    |       브라우저 창을 기준으로 배치       |          |

### 인용문 (BackQuote)

```markdown
> 인용문
>> 중첩된 인용문(Nested BlockQuote)을 생성
>>> 중중첩된 인용문 1
>>> 중중첩된 인용문 ..
```

> 인용문
>
> > 중첩된 인용문(Nested BlockQuote)을 생성
> >
> > > 중중첩된 인용문 1
> > > 중중첩된 인용문 ..

### 원시 HTML 사용이 가능

HTML을 잘 모르므로 마크다운(Markdown) 문법이 익숙해지자 (마크다운에서 지원하지 않는 기능을 사용할 때 유용)

### 줄바꿈

```markdown
가나다
라마바사  <!-- 띄어쓰기(Space) 두번 -->
아자차카타<br>
파하
```

> 줄바꿈을 지원하지 않는 환경의 경우, Space 두번 또는 \<br\>을 활용할 수 있음

### 이미지

여러가지 방식이 있으나 가장 많이 사용할 것 같은 소스만 정리함

```markdown
기존의 웹에서 Markdown으로 삽입할 경우
![test](https://github.com/sungjuko/sungjuko.github.io/blob/main/images/profile_a.jpg?raw=true "테스트")

로컬 경로로 삽입할 경우
![test](images/profile_a.jpg "테스트")
```

![test](https://github.com/sungjuko/sungjuko.github.io/blob/main/images/profile_a.jpg?raw=true "테스트")

![test](images/profile_a.jpg "테스트")

### 링크

```markdown
링크 테스트 입니다. 더 많은 정보를 확인하시려면 [Blog](https://sungjuko.github.io)를 방문해주세요
```

링크 테스트 입니다. 더 많은 정보를 확인하시려면 [Blog](https://sungjuko.github.io)를 방문해주세요.



## 참고

### 특수문자 치환

치환이 필요로 하지 않는경우는 역슬래시(\\\)를 통하여 문자열 그대로 사용하면 된다
