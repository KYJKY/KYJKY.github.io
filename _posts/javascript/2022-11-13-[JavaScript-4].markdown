---
layout: post
title: "[모던JS] 연산자"
date: 2022-11-13 22:11:44 +09:00
excerpt: "모던 자바스크립트 Deep Dive<br>2022-11-13"
javascript: true
categories: javascript
tags: javascript
comments: true
---

# 📌 [모던 자바스크립트 13주 뿌시기] 7. 연산자

---

<figure>
    <a href="/assets/img/JavaScript/2022-11-10/bookcover.png"><img src="/assets/img/JavaScript/2022-11-10/bookcover.png"></a>
    <figcaption style="text-align:center"></figcaption>
</figure>

<br>
<br>

# 7. 연산자

연산자: 하나 이상의 표현식을 대상으로 산술/할당/비교/논리/타입/지수 연산 등을 수행하여 값을 만들어 줌.
피연산자: 연산의 대상이 되는 것. 값으로 평가될 수 있는 표현식.

<br>

### 연산자의 종류

##### 산술 연산자

피연산자를 대상으로 수학적 계산을 수행함.
산술연산이 불가능한 경우, `NaN`을 반환.

**이항 산술 연산자**
2개의 피연산자를 산술 연산하여 값을 만듬.
피연산자의 값을 변경하는 부수 효과가 없다.
ex) 덧셈(+), 뺄셈(-), 곱셈(\*), 나눗셈(/), 나머지(%)

**단항 산술 연산자**
1개의 피연산자를 산술 연산하여 값을 만듬.
피연산자의 값을 변경하는 부수 효과가 일부 존재한다.

```javascript
let x = 1;

x++; // 'x = x + 1'과 같다
x--; // 'x = x - 1'과 같다.
-x; // -1의 값을 가진다.
+x; // 값의 변화가 없다.
```

<br>

++, --의 위치에 따라 의미가 달라진다.
전위 증가/감소연산자: 연산자를 피연산자 앞에 위치하고 먼저 피연산자의 값을 선 증가/감소 후, 다른 연산을 진행.
후위 증가/감소연산자: 연산자를 피연산자 뒤에 위치하고 먼저 다른 연산을 진행한 후, 피연산자의 값을 증가/감소 시킴.

```javascript
let x;

// 전위 연산자
x = 10;
console.log(x++); // 10 출력
console.log(x); // 11 출력

x = 10;
console.log(x--); // 10 출력
console.log(x); // 9 출력

// 후위 연산자
x = 10;
console.log(++x); // 11 출력
console.log(x); // 11 출력

x = 10;
console.log(--x); // 9 출력
console.log(x); // 9 출력
```

**단항 산술 연산자 `+`는 값의 변화도 없고 부수 효과도 없는데 무슨 의미가 있나요?**
`+`는 숫자 타입이 아닌 피연산자 사용할 경우, 숫자 타입으로 변환해준다.
마치, 숫자 타입에 `+ ''`를 사용하여 문자 타입으로 변환하는 것과 같다.

<br>
<br>

##### 할당 연산자

우항에 있는 피연산자의 평가 결과를 좌항에 있는 변수에 할당함.
좌항의 변수에 할당하는 행동이므로 부수 효과가 있음.

```javascript
let x;

x = 10;
x += 5; // 'x = x + 5' 와 같다
console.log(x); // 15

x = 10;
x -= 5; // 'x = x - 5' 와 같다
console.log(x); // 5

x = 10;
x *= 5; // 'x = x *+ 5' 와 같다
console.log(x); // 50

x = 10;
x /= 5; // 'x = x / 5' 와 같다
console.log(x); // 2

x = 10;
x %= 3; // 'x = x % 5' 와 같다
console.log(x); // 1
```

<br>
<br>

##### 비교 연산자

좌항과 우항의 피연산자를 비교하여 그 결과를 불리언 값으로 반환한다.

**동등/일치 비교 연산자**
동등비교(==): 암묵적 타입 변환을 통해 타입을 일치시킨 후 값을 비교하여 같은 경우 true를 반환함.
일치비교(===): 값과 타입이 같은 경우에만 true를 반환함.

```javascript
console.log(5 == "5"); // 동등 비교, true
console.log(5 == 5); // 동등 비교, true

console.log(5 === "5"); // 일치비교, false
console.log(4 === "5"); // 일치비교, false
console.log(5 === 5); // 일치비교, true

// 주의할 것
console.log(NaN === NaN); // false
console.log(0 === -0); // true
```

**대소 관계 비교 연산자**
피연산자의 크기를 비교하여 불리언 값을 반환함.

```javascript
let x, y;

x = 10;
y = 5;
console.log(x > y); // true
console.log(x < y); // false

x = 10;
y = 10;
console.log(x >= y); // true
console.log(x <= y); // true
```

<br>
<br>

##### 삼항 조건 연산자

사용방법

> 조건식 ? 조건식이 true일 때 반환 값 : 조건식이 false일 때 반환 값

```javascript
let x, y;

x = 5;
y = 7;

console.log(x > y ? "x가 더 커요!" : "y가 더 커요!"); // "x가 더 커요!"를 출력한다.
```

삼항 조건 연산자의 표현식은 값으로 평가할 수 있는 표현식인 문이기 때문에 값처럼 사용될 수 있다.

<br>
<br>

##### 논리 연산자

피연산자를 논리 연산한다.

```javascript
let x = true;
let y = false;

// 논리합: 좌우항 하나라도 true > true
console.log(x || x); // true
console.log(x || y); // true
console.log(y || x); // true
console.log(y || y); // false

// 논리곱: 좌우항 둘 다 true > true
console.log(x && x); // true
console.log(x && y); // false
console.log(y && x); // false
console.log(y && y); // false

// 논리 부정
console.log(!x); // false
console.log(!y); // true
```

<br>
<br>

##### 그룹 연산자

소괄호 `(`, `)`로 피연산자를 감싸서 연산의 우선순위를 가장 높게 설정할 수 있다.

```javascript
console.log(5 + 10 * 3); // 35
console.log((5 + 10) * 3); // 45
```

<br>
<br>

##### typeof 연산자

피연산자의 데이터 타입을 문자열로 반환한다.
반환하는 문자열은 아래와 같다.

-   string
-   number
-   boolean
-   undefined
-   symbol
-   object
-   function

**아래는 typeof의 버그이다.**

```javascript
// 자바스크립트 버그 주의
let x = null;
console.log(typeof x); // object. null이 아니다.

// 대체 방안
console.log(x === null); // true
```

<br>
<br>

##### 지수 연산자

좌항을 '밑'으로, 우항을 '지수'로 거듭 제곱하여 숫자를 반환한다. 이는 ES7에서 도입되었고 그 전에는 Math.pow 메서드를 사용하였다.

```javascript
console.log(2 ** 3); // 8
console.log(2 ** (1 / 2)); // 1.4142135623730951
console.log(2, 0); // 1
console.log(2, -2); // 0.25

// Math.pow 메서드 사용
Math.pow(2 ** 3); // 8
Math.pow(2 ** (1 / 2)); // 1.4142135623730951
Math.pow(2, 0); // 1
Math.pow(2, -2); // 0.25
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
