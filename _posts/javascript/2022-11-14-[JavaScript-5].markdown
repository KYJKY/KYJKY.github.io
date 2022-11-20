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
let answer = "A";
let score = 0;

switch (answer) {
    case "A":
    case "a":
        score = 3;
        break;
    case "B":
    case "b":
        score = 1.5;
        break;
    case "C":
    case "c":
        score = 0;
        break;
    default:
        console.log("잘못 입력했습니다.");
}
```

※ 개인적인 생각이지만 `true`, `false`로 나뉘는 조건에 적합한 경우 `if`..`else`문을 활용하고 어떤 특정한 '값'에 대한 상황을 나누는 것에 적합한 경우 `switch`를 활용하는 것이 좋은 것 같다.

<br>
<br>

### 반복문

-   조건식의 평과 결과가 참인 경우 코드 블록을 실행한다.
-   반복 주기마다 조건식을 재평가하여 코드 블록을 실행하며, 거짓이 될 때까지 반복한다.
-   `for`, `while`, `do..while` 등이 있다.

<br>

#### for문

-   조건식 결과가 거짓으로 평가될 때까지 코드 블록을 실행한다.
-   반복 변수는 반복을 의미하는 **iteration**의 `i`를 쓰는 것이 보편적.

##### 예시

```javascript
// 일반적인 for문
for (let i = 0; i < 0; i++) {
    console.log(`${i}번째 반복문 입니다.`);
}

// for문을 무한루프로 활용할 경우
for (;;) {
    // 실행문
}

// 중첩 for문을 활용한 구구단 출력
for (let i = 2; i <= 9; i++) {
    console.log(`----- ${i}단 출력 ----------------`);
    for (let j = 1; j <= 9; j++) {
        console.log(`${i} x ${j} = ${i * j}`);
    }
}
```

<br>

#### while문

-   주어진 조건식의 평가가 참이면 코드를 반복 실행한다.
-   `while`문은 반복 횟수가 불명확할 때 주로 사용된다.
-   조건식의 결과가 boolean이 아닌경우, 강제적 형변환을 통해 참/거짓을 구별한다.

##### 예시

```javascript
// 일반적인 while문
let num = 155212;
let temp = num;
let count = 0;

while (temp > 1) {
    temp /= 10;
    count++;
}
console.log(`${num}은 ${count} 자릿수 입니다.`);

// while문을 무한루프로 활용하는 경우
while (true) {
    // 실행문
}

// 무한루프의 탈출 방법
count = 0;
while (true) {
    console.log(count++);

    if (count > 50) {
        console.log("종료");
        break;
    }
}
```

<br>

#### do...while문

-   기존 `while`과 다른 점은 `do`...`while`은 코드 블록을 먼저 무조건 실행 후 조건식을 평가한다.
-   해당 루프가 무조건 1번은 돌아야하는 상황에 사용한다.

##### 예시

```javascript
let count = 0;

do {
    console.log(count);
    count++;
} while (count < 3);
```

<br>

#### break문

-   break 문은 레이블 문과 반복문, `switch`문의 코드블록을 탈출한다.
-   위에서 언급한 문 외의 경우에서 `break`문을 사용할 경우, 에러가 발생한다.

레이블 문: 식별자가 붙은 문

##### 예시

```javascript
labelTest: {
    console.log("Hi label");
    break labelTest;
    console.log("hello?"); // 중간에 break 때문에 실행되지 않음.
}
```

레이블 문은 중첩된 for문 외부로 탈출할 때 유용하다.

```javascript
outer: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        if (i + j === 3) break outer;
        console.log(`현재 [i, j] = [${i}, ${j}]`);
    }
}
```

위의 예시에서 원래 `break`만 있었더라면 첫 번째 for문의 루프는 계속 돌았겠지만, 레이블 문을 사용하여 루프를 돌지 않는다.

<br>

#### continue문

-   반복문의 코드 블록 실행을 `continue` 문에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. (반복문을 탈출시키는 것은 아님)

##### 예시

```javascript
let string = "Hello World.";
let search = "l";
let count = 0;

// continue를 사용하지 않을 경우
for (let i = 0; i < string.length; i++) {
    // l이면 count++
    if (string[i] === search) {
        count++;
        // ...
        // ...
        // ...
    }
}
console.log(count);

// continue를 사용할 경우
count = 0;
for (let i = 0; i < string.length; i++) {
    // l이면 카운트 증가 X
    if (string[i] !== search) continue;

    count++;
    // ...
    // ...
    // ...
}
console.log(count);
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
