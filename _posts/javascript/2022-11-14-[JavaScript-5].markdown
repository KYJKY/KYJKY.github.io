---
layout: post
title: "[모던JS] 제어문"
date: 2022-11-13 22:11:44 +09:00
excerpt: "모던 자바스크립트 Deep Dive<br>2022-11-14"
javascript: true
categories: javascript
tags: javascript
comments: true
---

# 📌 [모던 자바스크립트 13주 뿌시기] 8. 제어문

---

<figure>
    <a href="/assets/img/JavaScript/2022-11-10/bookcover.png"><img src="/assets/img/JavaScript/2022-11-10/bookcover.png"></a>
    <figcaption style="text-align:center"></figcaption>
</figure>

<br>
<br>

# 8. 제어문

제어문의 사용 용도

-   조건에 따라 코드 불록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용.
-   보편적으로 흐르는 코드의 방향(위에서 아래로 순차적인)을 벗어나는 실행 흐름 제어를 위해 사용.

<br>

### 블록문

-   0개 이상의 문을 중괄호로 묶은 것. (코드블록, 블록)
-   단독으로 사용 가능하나, 일반적으로 제어문이나 함수를 정의할 때 사용함.
-   블록문 끝에는 세미콜론(;)을 붙이지 않는다.

#### 블록문의 예시

```javascript
// 블록문의 예시
{
    var age = 26;
}

var isTrue = true;

if (isTrue) {
    console.log("true");
}

function sum(a, b) {
    return a + b;
}
```

<br>
<br>

### 조건문

-   주어진 조건식의 평과 결과에 따라 코드 블록의 실행을 결정함. (조건식: boolean값)
-   `if` ... `else` 문과 `switch` 문이 있음

#### if ... else

`if` 문의 조건식 평가 결과에 따라 실행하는 코드 블록이 결정된다.
조건식 평가 결과가 `true`일 경우, `if`문의 블록이 실행되고 `false`일 경우 `else`문의 블록이 실행된다.
`else if`와 `else`는 옵션이므로 필수적으로 작성해야 하는 코드는 아니다.

##### 예시

```javascript
// 일반적인 if 문
let num = 1;

if (num > 0)
    // 블록문이 하나인 경우, 중괄호 생략 가능
    console.log("num은 양수입니다.");

// if ... else 문
if (num > 0) {
    console.log("num은 양수입니다.");
} else {
    console.log("num은 0이거나 음수입니다.");
}

// if...else if 문
if (num > 0) {
    console.log("num은 양수입니다.");
} else if (num == 0) {
    console.log("num은 0입니다.");
} else {
    console.log("num은 음수입니다.");
}

// 삼항 조건 연산자로 치환
num % 2 ? "홀수" : "짝수";

// 삼항 조건 연산자를 통해 if...else if 문과 같이 사용할 수 있지만,
// 가독성이 안 좋다.
num ? (num > 2 ? "홀수" : "짝수") : "0";
```

<br>

#### switch 문

-   주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 `case`문으로 이동한다.
-   `case` 문은 표현식의 결과 `case`를 지정하고 콜론으로 마친다. 그 뒤에 실행할 문을 위치한다.
-   표현식의 결과가 `case`에 없다면, `default`로 이동시킨다.
-   `if` 문과 다르게 논리적 참/거짓보다 여러 상황에 따른 실행문을 결정할 때 사용한다.
-   각 case문마다 `break`문을 사용하여 해당 케이스 실행문을 마치면 블록에서 탈출할 수 있다.
-   `break`를 사용하지 않을 경우, 다음 case문의 실행문까지 실행하게 된다.

##### 예시

```javascript
let phone = "031";

switch (phone) {
    case "031":
        console.log("경기도");
        break;
    case "032":
        console.log("인천");
        break;
    case "033":
        console.log("강원도");
        break;
    case "041":
        console.log("충남");
        break;
    case "042":
        console.log("대전");
        break;
    case "043":
        console.log("충북");
        break;
    case "044":
        console.log("세종");
        break;
    case "051":
        console.log("부산");
        break;
    default:
        // default 문에서는 break 문을 생략하는 것이 일반적이다.
        console.log("그 외");
}
```

<br>

##### 플스루를 활용한 예시

```javascript

```

<br>
<br>
<br>
<br>

### 출처

위키북스, 『모던 자바스크립트 Deep Dive』, 이웅모

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
