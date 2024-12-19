## 1️⃣ Headers 헤더
* `#`으로 시작하는 텍스트.
* `#`은 하나부터 여섯개까지 가능.
* `#`이 늘어날때마다 제목의 스케일 낮아짐
* H1은 `===`로도 만들 수 있음
* H2는 `---`로도 만들 수 있음

### 사용법
    This is an H1
    ===
    This is an H2
    ---
    # This is an H1
    ## This is an H2
    ### This is an H3
    #### This is an H4
    ##### This is an H5
    ###### This is an H6   

### 실행결과
This is an H1<br>
===
This is an H2<br>
---
# This is an H1; 부(parts)에 사용<br>
## This is an H2; 장(chapters)에 사용<br>
### This is an H3; 페이지 섹션에 사용<br>
#### This is an H4; 하위 섹션에 사용<br>
##### This is an H5; 하위 섹션 아래의 하위 섹션에 사용<br>
###### This is an H6; 문단에 사용<br>

<br>

## 2️⃣ Emphasis 강조
* 기울여 쓰기(italic) : `*` 또는 `_`로 감싼 텍스트.
* 두껍게 쓰기(bold) : `**` 또는 `__`로 감싼 텍스트.
* 취소선 : `~~`로 감싼 텍스트.
* 이탤릭체와 두껍게를 같이 사용할 수 있습니다.
### 사용법
      *This text will be italic*
      _This will also be italic_
      **This text will be bold**
      __This will also be bold__
      ~~This is canceled~~
      *You **can** combine them*

### 실행결과
*This text will be italic*<br>
_This will also be italic_<br>
**This text will be bold**<br>
__This will also be bold__<br>
~~This is canceled~~<br>
*You **can** combine them*<br>

<br>

## 3️⃣ Blockquotes 인용
* `>`으로 시작하는 텍스트.
* `>`는 3개까지 가능
* `1개`는 인용문
* `2개`는 인용문 안에 인용문
* `3개`는 인용문 안에 인용문 안에 인용문

### 사용방법
    As Grace Hopper said:
    > I’ve always been more interested in the future than in the past.    
    > This is a first blockquote.
    > > This is a second blockquote.
    > > > This is a third blockquote.

### 실행결과
As Grace Hopper said:
> I’ve always been more interested in the future than in the past.
> This is a first blockquote.
> > This is a second blockquote.
> > > This is a third blockquote.

<br>

## 4️⃣ Lists 목록
### 4️⃣.1️⃣ Unordered lists 순서가 없는 목록
* `*`, `+`, `-` 를 이용해서 순서가 없는 목록을 만들 수 있음
* 들여쓰기를 하면 모양이 바뀜

### 4️⃣.2️⃣ Ordered lists 순서가 있는 목록
* 숫자를 기입하면 순서가 있는 목록이 됨
* 들여쓰기를 하면 모양이 바뀜

### 사용방법
    * Item 1
    * Item 2
      * Item 1
      * Item 2
        * Item 1
        * Item 2
     1. Item 1
     2. Item 2
     3. Item 3
       1. Item 1
       2. Item 2
       3. Item 3
         1. Item 1
         2. Item 2
         3. Item 3

### 실행결과
* Item 1
* Item 2
    * Item 1
    * Item 2
      * Item 1
      * Item 2
1. Item 1
2. Item 2
3. Item 3
    1. Item 1
    2. Item 2
    3. Item 3
       1. Item 1
       2. Item 2
       3. Item 3

<br>

## 5️⃣ Backslash Escapes 백슬래쉬 이스케이프
* 특수문자를 표현할 때, 표시될 문자 앞에 `\`를 넣고 특수문자를 쓰면 됨
* 주의할 점은 앞과 뒤에가 형식이 똑같이 백슬래쉬 뒤에 특수문자임 `감싸는 형태가 아님`
* 백슬래쉬는 아래의 특수문자를 표현할 수 있음
* \ backslash, \ backtick, * asterisk, _ underscore, {} curly braces, [] square brackets,
() parentheses, # hash mark, + plus sign, - minus sign (hyphen), . dot, ! exclamation mark

### 사용방법
    \*literal asterisks\*
    \#hash mark\#
    \[squre brackets\]

### 실행결과
\*literal asterisks\*<br>
\#hash mark\#<br>
\[squre brackets\]<br>


<br>

## 6️⃣ Links (Anchor) 링크
## 6️⃣.1️⃣ External Links 외부 링크
    인라인 링크: [링크](http://example.com "링크 제목")
    url 링크: <example.com>, <example@example.com>; 꺽쇠 괄호 없어도 자동으로 링크를 사용

### 사용방법
    [Google](http://www.google.com "구글")
    [Naver](http://www.naver.com "네이버")
    [Github](http://www.github.com "깃허브")
    구글 www.google.com; 꺽쇠없음
    네이버 <www.naver.com>; 꺽쇠있음
    My mail <jinkyukim.dev@gmail.com>

### 실행결과
[Google](http://www.google.com "구글")<br>
[Naver](http://www.naver.com "네이버")<br>
[Github](http://www.github.com "깃허브")<br>
구글 www.google.com <br>
네이버 <www.naver.com> <br>
My mail <jinkyukim.dev@gmail.com><br>

## 6️⃣.2️⃣ Internal Links 내부 링크
    [보여지는 내용](#이동할 헤드(제목))
    괄호 안의 링크를 쓸 때는 띄어쓰기는 -로 연결, 영어는 모두 소문자로 작성

### 사용방법
    [1. Headers 헤더](#1-headers-헤더)
    [2. Emphasis 강조](#2-emphasis-강조)
    [3. Blockquotes 인용](#3-blockquotes-인용)

### 실행결과
[1. Headers 헤더](#1-headers-헤더)<br>
[2. Emphasis 강조](#2-emphasis-강조)<br>
[3. Blockquotes 인용](#3-blockquotes-인용)<br>

<br>

## 7️⃣ Fenced Code Blocks 코드 블럭
* 간단한 인라인 코드는 텍스트를 앞뒤로 \`기호로 감싸면 됨
* \`\`\` 혹은 ~~~ 코드
* 첫 줄과 마지막 줄에 Back quote ( \` ) 또는 물결( ~ ) 3개 삽입
* 코드가 여러 줄인 경우, 줄 앞에 공백 네 칸을 추가하면 됨
* \`\`\` 옆에 언어를 지정해주면 syntax color가 적용됨

### 사용방법
    ```
    This is code blocks.
    ```
    ~~~
    This is code blocks.
    ~~~
        4 spaces
    ```javascript
    function test() {
     console.log("look ma’, no spaces");
    }
    ```
### 실행결과
```
This is code blocks.
```
~~~
This is code blocks.
~~~
    4 spaces
```javascript
function test() {
 console.log("look ma’, no spaces");
}
```
<br>

## 8️⃣ Task Lisk 체크 리스트
* 줄 앞에 `- [x]`를 써서 완료된 리스트 표시
* 줄 앞에 `- [ ]`를 써서 미완료된 리스트 표시
* 체크 안에서 강조 외에 여러 기능을 사용할 수 있음

### 사용방법
    - [x] this is a complete item
    - [ ] this is an incomplete item
    - [x] @mentions, #refs, [links](),
    **formatting**, and <del>tags</del>
    supported
    - [x] list syntax required (any
    unordered or ordered list
    supported)

### 실행결과
- [x] this is a complete item
- [ ] this is an incomplete item
- [x] @mentions, #refs, [links](),
**formatting**, and <del>tags</del>
supported
- [x] list syntax required (any
unordered or ordered list
supported)

<br>

## 9️⃣ Horizontal Rules 수평선
* \- 또는 * 또는 _ 을 3개 이상 작성
* 단, -을 사용할 경우 header로 인식할 수 있으니 이 전 라인은 비워둬야 함

### 사용방법
    * * *
    ***
    *****
    - - -
    -------------------

### 실행결과
* * *
***
*****
- - -
-------------------

<br>

## 1️⃣0️⃣ Emoji 이모티콘
* 마크다운을 이용해 이모티콘을 표현가능
* 깃허브도 적용가능
* 더 많은 리스트는 아래의 사이트로 방문
* www.emoji-cheat-sheet.com

### 사용벙법
    GitHub supports emoji!
    :+1: :sparkles: :camel: :tada:
    :rocket: :metal: :octocat:

### 실행결과
GitHub supports emoji!
:+1: :sparkles: :camel: :tada:
:rocket: :metal: :octocat:

<br>

## 1️⃣1️⃣ Table 테이블
* 헤더와 셀을 구분할 때 3개 이상의 `-`(hyphen/dash) 기호가 필요
* 헤더 셀을 구분하면서 :(Colons) 기호로 셀(열/칸) 안에 내용을 정렬할 수 있음
* 가장 좌측과 가장 우측에 있는 |(vertical bar) 기호는 생략 가능

### 사용방법
    테이블 생성

    헤더1|헤더2|헤더3|헤더4
    ---|---|---|---
    셀1|셀2|셀3|셀4
    셀5|셀6|셀7|셀8
    셀9|셀10|셀11|셀12

    테이블 정렬

    헤더1|헤더2|헤더3
    :---|:---:|---:
    Left|Center|Right
    1|2|3
    4|5|6
    7|8|9

### 실행결과
테이블 생성

헤더1|헤더2|헤더3|헤더4
---|---|---|---
셀1|셀2|셀3|셀4
셀5|셀6|셀7|셀8
셀9|셀10|셀11|셀12

테이블 정렬

헤더1|헤더2|헤더3
:---|:---:|---:
Left|Center|Right
1|2|3
4|5|6
7|8|9

<br>

## 1️⃣2️⃣ Line Breaks 줄바꿈
* `<br>`를 활용해서 줄바꿈을 할 수 있음

### 사용방법
    비켜봐 봐, 비켜 핑계는 <br>
    우린 본질 속에 진주가 될래  <br>
    꿈의 난이도 좀 더 난 높일게 <br>
    고통, 시련 다듬어 내가 될게 <br>
    I'm just 이제 조금 알겠어 <br>
    I shine 왜 날 힘들게 울게만 둔 건지 <br>
    Hold me closer broken myself, yeah <br>
    La-la-la, la-la-la-la <br>
    끝까지 가볼래 포기는 안 할래 난 <br>
    La-la-la, la-la-la-la <br>    
    쓰러져도 일어나 <br>
    We go, we high, go now, oh-oh <br>
    La-la-la, la-la-la-la <br>
    Girls never die 절대 never cry <br>

### 실행결과
비켜봐 봐, 비켜 핑계는 <br>
우린 본질 속에 진주가 될래 <br>
꿈의 난이도 좀 더 난 높일게 <br>
고통, 시련 다듬어 내가 될게 <br>
I'm just 이제 조금 알겠어 <br>
I shine 왜 날 힘들게 울게만 둔 건지 <br>
Hold me closer broken myself, yeah <br>
La-la-la, la-la-la-la <br>
끝까지 가볼래 포기는 안 할래 난 <br>
La-la-la, la-la-la-la <br>
쓰러져도 일어나 <br>
We go, we high, go now, oh-oh <br>
La-la-la, la-la-la-la <br>
Girls never die 절대 never cry <br>

<br>

## 1️⃣3️⃣ Images 이미지
* <img>로 변환됨
* 링크와 비슷하지만 앞에 `!`가 붙음
* 인라인 이미지 \![alt text](/test.png\)
* 링크 이미지 \![alt text](image_URL\)
* 이미지의 사이즈를 변경하기 위해서는 `<img width="OOOpx" height="OOOpx"></img>`와 같이 표현

### 사용방법
    ![alt 토심이랑 토뭉이](/img/Toshim_and_Tohmong.PNG)
    ![alt 토심](/img/Toshim.PNG)
    ![alt 토심이랑 토뭉이2](/img/Toshim_and_Tohmong2.PNG)

    
### 실행결과
![alt 토심이랑 토뭉이](/Git/Markdown/img/Toshim_and_Tohmong.PNG)
![alt 토심](/Git/Markdown/img/Toshim.PNG)
![alt 토심이랑 토뭉이2](/Git/Markdown/img/Toshim_and_Tohmong2.PNG)

<br>

## 1️⃣4️⃣ Reference 참고 링크
* [Matering Markdown](https://guides.github.com/features/mastering-markdown/)
* [마크다운 위키백과](https://ko.wikipedia.org/wiki/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4)
* [존 그루버의 웹사이트](https://daringfireball.net/projects/markdown/)

