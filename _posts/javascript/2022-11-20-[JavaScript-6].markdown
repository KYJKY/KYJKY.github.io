---
layout: post
title: "[모던JS] 타입 변환과 단축평가"
date: 2022-11-20 18:11:44 +09:00
excerpt: "모던 자바스크립트 Deep Dive<br>2022-11-20"
javascript: true
categories: javascript
tags: javascript
comments: true
---

# 📌 [모던 자바스크립트 13주 뿌시기] 9. 타입 변환과 단축평가

---

<figure>
    <a href="/assets/img/JavaScript/2022-11-10/bookcover.png"><img src="/assets/img/JavaScript/2022-11-10/bookcover.png"></a>
    <figcaption style="text-align:center"></figcaption>
</figure>

<br>
<br>

# 9. 타입 변환과 단축평가

### 타입 변환이란?

값은 모두 타입을 가진다. 이 타입은 다른 타입으로 변환될 수 있다.
타입 변환에는 두 가지 방식이 존재한다.

**명시적 타입 변환(타입 캐스팅)**: 개발자가 의도적으로 값의 타입을 변환하는 것.
**암묵적 타입 변환(타입 강제 변환)**: 개발자의 의도와 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되는 것.

##### ※ 주의

-   명시적 타입 변환은 기존 변수 값을 변경하는 것이 아닌, 기존 원시 값을 통해 새로운 원시 값을 생성하는 것.
-   암묵적 타입 변환은 기존 변수 값을 변경하는 것이 아닌, 기존 원시 값을 통해 새로운 원시 값을 생성하여 한 번만 사용하고 버림.

중요한 것은 상황에 따른 쓰임이다. 명시적 타입 변환만 사용하란 법은 없다. 오히려 암묵적 타입 변환이 가독성이 좋은 경우도 있다. ex) `10 + ''`

<br>
<br>

#### 암묵적 타입 변환의 예

##### 문자열 타입으로 변환하는 경우

1. `+` 연산자의 피연산자 중 하나 이상이 문자열인 경우
2. 템플릿 리터럴의 표현식 삽입 부분은 표현식 평가 결과를 문자열 타입으로 변환함.

<br>

##### 숫자 타입으로 변환하는 경우

1. `+` 를 제외한 산술 연산자(`-`, `*`, `/`, `%`)의 피연산자를 대상으로 숫자 타입으로 변환
2. 그러나 피연산자를 숫자 타입으로 변환할 수 없는 경우는 `NaN`
3. 비교 연산자의 피연산자 중 숫자 타입이 아닌 경우
4. 단항 연산자 `+`의 피연산자가 숫자타입이 아닌 경우

<br>

##### 불리언 타입으로 변환하는 경우

1. `if` 문이나 `for` 문과 같은 제어문 or 삼항 조건 연산자의 조건식은 불리언 타입으로 변환된다.

불리언 타입으로 암묵적 타입 변환이 일어날 때, Truthy 값 또는 Falsy 값으로 구분하게 되는데 Falsy로 평가되는 값은 아래와 같다.

`false`, `undefined`, `null`, `0`, `-0`, `NaN`, `''`(빈 문자열)

위의 Falsy의 예 외의 것은 Truthy 값이다.

<br>
<br>

#### 명시적 타입 변환

##### 문자열 타입으로 변환하는 방법

1. String 생성자 함수를 new 연산자 없이 호출함
2. Object.prototype.toString 메서드를 사용함
3. 문자열 연결 연산자를 이용함

```javascript
// 1번 방법
String(1); // '1'
String(true); // 'true'
String(undefined); // 'undefined'

// 2번 방법
let a = 1,
    b = true,
    c = undefined;
a.toString(); // '1'
b.toString(); // 'true'
c.toString(); // 'undefined'

// 3번 방법
1 + ""; // '1'
true + ""; // 'true'
undefined + ""; // 'undefined'
```

<br>

##### 숫자타입으로 변환하는 방법

1. Number 생성자 함수를 new 연산자 없이 호출함
2. parseInt, parseFloat 함수를 사용함 (문자열 대상)
3. `+` 단항 산술 연산자 사용
4. `*` 산술 연산자 사용

```javascript
// 1번 방법
Number("1"); // 1
Number(true); // 1
Number("123.45"); // 123.45

// 2번 방법
parseInt("1"); // 1
parseInt(true); // 1
parseFloat("123.45"); // 123.45

// 3번 방법
+"1"; // 1
+true; // 1
+"123.45"; // 123.45

// 4번 방법
"1" * 5; // 5
true * 3; // 3
"123.45" * 1; // 123.45
```

<br>

##### 불리언타입으로 변환하는 방법

1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
2. ! 부정 논리 연산자를 두 번 사용하는 방법

```javascript
// 1번 방법
Boolean("1"); // true
Boolean(""); // false
Boolean("false"); // true
Boolean(0); // false
Boolean(1); // true
Boolean(NaN); // false
Boolean(undefined); // false
Boolean(null); // false

// 2번 방법
!!"1"; // true
!!""; // false
!!"false"; // true
!!0; // false
!!1; // true
!!NaN; // false
!!undefined; // false
!!null; // false
```

<br>
<br>

### 단축 평가

**단축평가**: 논리곱 `&&`, 논리합 `||` 연산자가 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환하는 것. 단축 평가는 표현식을 평가하는 도중에 평가결과가 확정된 경우, 나머지 평가 과정을 생략함.

<br>

##### 정리

1. 논리합의 경우, 첫 번째 값이 Thuthy 값일 때 두 번째 피연산자의 평가를 생략한다.
   `true` || `anything` == `true`
2. 그러나 Falsy일 경우, 두 번째 피연산자의 값이 평가된다.
   `false` || `anything` == `anything`
3. 논리곱의 경우, 첫 번째 값이 Falsy 값일 때 두 번째 피연산자의 평가를 생략한다.
   `false` && `anything` == `false`
4. 그러나 Falsy일 경우, 두 번째 피연산자의 값이 평가된다.
   `true` && `anything` == `anything`

<br>
<br>

#### 옵셔널 체이닝 연산자

-   연산자 `?.` 는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 아니라면 우항의 프로퍼티 참조를 이어간다.
-   ES11(ECMAScript2020)에 도입되었다.

##### 옵셔널 체이닝 연산자 사용 예시

```javascript
// 1. 옵셔널 체이닝 연산자 사용 전 null 평가 방법
let val = null;
let result = val && val.value; // null

// 2. 옵셔널 체이닝 연산자 사용
val = null;
result = val?.value;
```

1번과 2번은 비슷한 예제로 보일 수 있으나, 아래와 같은 차이가 있다.

-   1번은 피연산자가 `false`로 평가되는 Falsy값을 반환한다. 그러므로 `0`이나 `''`(빈 문자열)이 포함될 수 있다.
-   2번 옵셔널 체이닝 연산자는 오직 null과 undefined만 검사한다.

<br>
<br>

#### null 병합 연산자

-   연산자 `??` 는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 아니라면 좌항의 피연산자를 반환한다.
-   ES11(ECMAScript2020)에 도입되었다.

##### null 병합 연산자 사용 예시

```javascript
// 1. null 병합 연산자 사용 전 null 평가 방법
let val = "";
let result = val || "hello"; // 'hello'

// 2. null 병합 연산자 연산자 사용
val = null;
result = val ?? "hello"; // 'hello'
```

옵셔널 체이닝 연산자와 마찬가지로 1번과 2번 예제의 차이가 있다.

-   1번은 피연산자가 `false`로 평가되는 Falsy값을 반환한다. 그러므로 `0`이나 `''`(빈 문자열)이 포함될 수 있다.
-   2번 null 병합 연산자는 오직 null과 undefined만 검사한다.

<br>
<br>
<br>
<br>

### 출처

위키북스, 『모던 자바스크립트 Deep Dive』, 이웅모

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
