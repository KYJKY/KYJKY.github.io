---
layout: post
title: "[모던JS] 데이터 타입"
date: 2022-11-11 22:42:44 +09:00
excerpt: "모던 자바스크립트 Deep Dive<br>2022-11-11"
javascript: true
categories: javascript
tags: javascript
comments: true
---

# 📌 [모던 자바스크립트 13주 뿌시기] 6. 데이터 타입

---

<figure>
    <a href="/assets/img/JavaScript/2022-11-10/bookcover.png"><img src="/assets/img/JavaScript/2022-11-10/bookcover.png"></a>
    <figcaption style="text-align:center"></figcaption>
</figure>

<br>
<br>

# 6. 데이터 타입

데이터 타입: 값의 종류(형태).

`데이터 타입`은 **원시 타입(Primitive type)** 과 **객체 타입(Object type)** 으로 나눌 수 있다.

<br>

#### 원시 타입

-   숫자(number): 숫자의 모든 경우에 속한다. 정수와 실수 구분이 없다.
-   문자열(string): 문자열
-   불리언(boolean): 논리적 참과 거짓(true, false)
-   undefined: 변수가 선언될 때 암묵적으로 할당되는 값
-   null: 값이 없다는 것을 의도적으로 명시할 때 사용하는 값
-   심벌(symbol): ES6에서 추가됨

#### 객체 타입

-   객체
-   함수
-   배열 ... 등

<br>
<br>

##### 숫자 타입

자바스크립트의 숫자 타입은 **배정밀도 64비트 부동소수점 형식**을 따른다.
즉, 모든 수를 실수로 처리한다.

숫자 타입은 모든 수를 배정밀도 64비트 부동소수점 형식의 2진수로 저장되기 때문에, 어떤 형태의 수를 참조하여도 10진수로 해석된다.

```javascript
var binary = 0b01000001;
var octal = 0o101;
var hex = 0x41;

console.log(binary); // 65
console.log(octal); // 65
console.log(hex); // 65

console.log(binary === octal); // true
console.log(octal === hex); // true

console.log(1 === 1.0); // true
console.log(5 / 2); // 2.5
```

숫자 타입에는 아래와 같은 특별한 값도 표현할 수 있다.

-   Infinity: 양의 무한대
-   -Infinity: 음의 무한대
-   NaN: 산술 연산 불가(not a number)

```javascript
console.log(10 / Infinity); // 0
console.log(10 / -Infinity); // -0

console.log(Infinity / -Infinity); // NaN
console.log(1 - Infinity); // -Infinity

console.log(Infinity - Infinity); // NaN
console.log(Infinity / -35); // -Infinity

console.log(1 / 0); // Infinity
```

<br>
<br>

##### 문자열 타입

문자열은 0개 이상의 **16비트 유니코드 문자(UTF-16)의 집합**으로, 전 세계 대부분의 문자를 표현할 수 있다.

```javascript
// 문자열 타입의 표기법
var myText;

myText = "Hello"; // 작은 따옴표
myText = "Hi"; // 큰 따옴표
myText = `ES6 backtick`; // 백틱(ES6)

myText = '작은 따옴표로 표기한 경우, 내부의 "큰따옴표"는 문자열로 인식됨.';
myText = "큰 따옴표로 표기한 경우, 내부의 '큰따옴표'는 문자열로 인식됨.";

// 템플릿 리터럴
var variable = "hello";
var testTemplate = `<div>
    <h1>${variable}, 나는 템플릿 리터럴이야</h1>
</div>`; // ${}를 사용하여 표현식을 삽입할 수 있다.

// hi
```

자바스크립트의 문자열은 원시 타입이므로 **변경이 불가능한 값**이다.
개행이나 탭, 큰 따옴표나 작은 따옴표를 표현하기 위해서는 **이스케이프 시퀀스**를 사용하여 표현하여야 한다.

그러나, 템플릿 리터럴을 사용한다면 이스케이프 시퀀스를 사용하지 않고 표현할 수 있다.
또한 표현식을 삽입하여 가독성 좋게 문자열을 조합할 수 있다.

<br>
<br>

##### 불리언 타입

논리적 참, 거짓을 나타내는 `true`와 `false`로 구성된다.

<br>
<br>

##### undefined 타입

`undefined` 타입은 `undefined`이 유일하다.
변수를 선언하면 자바스크립트 엔진은 자동으로 `undefined` 값으로 초기화한다.

`undefined`는 의도치 않은 미할당 변수임을 식별하는 용도로 쓰이는 것을 권장한다.
때문에 개발자가 일부러 빈 값으로 두고 싶을 때는 `undefined`를 사용하는 것이 아니라 `null`을 사용하는 것이 바람직하다.

<br>
<br>

##### null 타입

`null` 타입은 `null`이 유일하다.
`null`은 변수에 값이 없다는 것을 의도적으로 명시하기 위한 용도로 사용한다.

`null`은 유효한 값이 아닐 경우 반환하는 용도로도 사용된다.
ex) `document.querySelector`는 조건에 부합하는 HTML 요소를 검색하지 못한 경우, 에러 대신 `null`를 반환한다.

<br>
<br>

##### 심벌 타입

심벌은 **변경 불가능한 원시 타입의 값**이다.  
다른 값과 중복되지 않은 유일한 값이기 때문에 이름 충돌 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용한다.
심벌은 Symbol 함수를 호출하여 생성한다.

<br>
<br>

### 데이터 타입이 왜 필요한가?

##### 1. 데이터 타입에 의해 메모리 공간의 확보와 참조

값 > 메모리에 저장 공간이 필요함 > 값을 효율적으로 저장하기 위해서는 대략적인 용량을 결정해야 한다.
즉, 타입에 맞는 효율적인 용량을 정하여 메모리 공간을 확보하기 위함.

또한 참조할 때도 동일하다.
값을 참조함 > 한 번에 얼마나 데이터를 읽어 들여야 할지에 대해 결정해야 한다.
어디까지 값을 읽어들이냐에 따라 데이터가 다르기 때문이다.

<br>

##### 2. 데이터 타입에 의한 값의 해석

메모리에 저장된 값은 여러 형태로 해석될 수 있다.
데이터 타입에 따라 값의 해석이 다르기 때문에 데이터 타입을 통해 개발자가 해석되길 원하는 값의 형태로 해석해줄 수 있다.

<br>
<br>

### 동적 타이핑

정적 타입 언어: 변수를 선언할 때 변수에 할당할 수 있는 데이터 타입을 사전에 선언해야 하는 언어. 선언한 데이터 타입에 맞는 값만 할당 가능.
동적 타입 언어: 변수를 선언할 때 변수에 데이터 타입을 사전에 선언할 필요가 없는 언어. 어떠한 타입의 값을 자유롭게 할당 가능.

typeof 연산자를 통하여 변수의 데이터 타입을 조사할 수 있다.

```javascript
let value = "test";
console.log(typeof value); // string
```

정적 타입 언어는 변수를 선언할 때 타입이 결정되고, 동적 타입 언어는 **할당에 의해 타입이 결정(추론)**되기 때문에 타입이 동적으로 변할 수 있다.
이러한 특성을 **동적 타이핑**이라 한다.

<br>
<br>
<br>
<br>

### 출처

위키북스, 『모던 자바스크립트 Deep Dive』, 이웅모

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
