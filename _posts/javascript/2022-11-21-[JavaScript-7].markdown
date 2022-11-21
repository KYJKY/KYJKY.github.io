---
layout: post
title: "[모던JS] 객체 리터럴"
date: 2022-11-21 01:07:44 +09:00
excerpt: "모던 자바스크립트 Deep Dive<br>2022-11-21"
javascript: true
categories: javascript
tags: javascript
comments: true
---

# 📌 [모던 자바스크립트 13주 뿌시기] 10. 객체 리터럴

---

<figure>
    <a href="/assets/img/JavaScript/2022-11-10/bookcover.png"><img src="/assets/img/JavaScript/2022-11-10/bookcover.png"></a>
    <figcaption style="text-align:center"></figcaption>
</figure>

<br>
<br>

# 10. 객체 리터럴

### 객체란?

-   다양한 타입의 값을 하나의 단위로 구성한 복합적인 자료구조
-   원시 값은 변경 불가능하지만, 객체 타입의 값은 변경 가능
-   객체는 0개 이상의 프로퍼티(key, value)로 구성된 집합

<br>

프로퍼티란? 객체의 상태를 나타내는 값

##### 프로퍼티의 value가 될 수 있는 것

1. 모든 원시 값
2. 함수(JS의 함수는 일급 객체) >> `메서드`라고 함

메서드란? 프로퍼티(상태 데이터)를 참고하고 조작할 수 있는 동작

<br>
<br>

### 객체 리터럴에 의한 객체 생성

JS에서 객체 생성 방법 종류

1. 객체 리터럴
2. Object 생성자 함수
3. 생성자 함수
4. Object.create 메서드
5. 클래스(ES6)

<br>

위 생성 방법 중 가장 일반적이고 간단한 방법은 **객체 리터럴** 사용 방법

```javascript
// 객체 리터럴을 통한 객체 생성
let product = {
    id: 251,
    name: "에어컨",
    price: 50000,
    saleProduct: function (discountNum) {
        this.price *= discountNum / 100;
    },
};

// 빈 객체 생성
let empty = {};
console.log(typeof empty); // object
```

객체 리터럴의 중괄호는 코드 블록을 의미하지 않는다. 값으로 평가되는 표현식이므로 세미콜론을 붙여줘야 한다.

<br>
<br>

### 프로퍼티

객체는 프로퍼티의 집합이며, 프로퍼티는 **키**와 **값**으로 구성된다.

-   키는 값에 접근할 수 있는 이름으로서 식별자의 역할을 한다.
-   키는 문자열이나 심벌 값으로 사용할 수 있다.
-   문자열이나 심벌 값 외의 값을 사용할 경우, 암묵적 타입 변환을 통해 문자열이 된다.
-   보편적으로 문자열을 사용하는데, 식별자 네이밍 규칙을 따르지 않는 경우에는 따옴표로 묶어야한다.
-   문자열 혹은 문자열로 평가할 수 있는 표현식을 사용하여 키를 동적으로 생성할 수 있다. 이 때, 키로 사용할 표현식을 대괄호로 묶어야 한다.
-   빈 문자열도 프로퍼티 키로 사용할 수 있지만, 권장하지 않는다.
-   예약어를 프로퍼티 키로 사용해도 되지만, 예상치 못한 에러가 발생할 수 있으므로 권장하지 않는다.
-   이미 선언한 키를 중복선언할 경우, 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다.

```javascript
// 네이밍 규칙 예시
let student = {
    id: 17,
    name: "Tom", // 네이밍 규칙 준수
    "nick-name": "cat", // 네이밍 규칙 어김
};

// 동적 생성 예시
let product = {};
let key = "name";

product[key] = "computer";

// 암묵적 타입 변환 예시
let foo = {
    0: 1,
    1: 2,
    3: 3,
};

// 중복 프로퍼티 예시
let temp = {
    name: "hi",
    name: "hello",
};
console.log(temp);
```

<br>
<br>

### 메서드

자바스크립트의 함수는 일급 객체이기 때문에 프로퍼티 값으로 사용할 수 있다. 이 함수를 일반함수와 구분하기 위해 **메서드**라고 부른다.

```javascript
let square = {
    width: 50,
    height: 10
    getArea: function() {
        return this.width * this.height;
    }
}
```

<br>
<br>

### 프로퍼티 접근

프로퍼티에 접근하기 위한 두 가지 방법

-   마침표 표기법: 마침표 프로퍼티 접근 연산자 `.`를 사용한다.
-   대괄호 표기법: 대괄호 프로퍼티 접근연산자 `[]`를 사용한다.

<br>

##### 표기법 예시

```javascript
let student = {
    name: 'kyj',
    'first-name': 'kim'
    1: 123
    2: 'hi'
};

let key = "name";

console.log(student.name);
console.log(student["name"]); // 반드시 따옴표로 감싼 문자열이여야 한다.
console.log(student[key]);
console.log(student['last-name']);
console.log(student[1]);    // 예외적으로 키가 숫자인 경우 따옴표를 생략할 수 있다.
console.log(student['1']);

console.log(student.'first-name');  // Uncaught SyntaxError: Unexpected string
console.log(student.first-name);  // NaN/ReferenceError
```

※ 키가 식별자 네이밍 규칙을 준수하지 않는 이름인 경우 무조건 **대괄호 표기법**을 사용할 것.

<br>
<br>

### 프로퍼티 값 갱신

프로퍼티에 값을 재할당하면 값이 갱신된다.

```javascript
let student = {
    name: "kyj",
};

student.name = "abc";

console.log(student);
```

<br>
<br>

### 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당할 경우, 동적으로 생성되어 추가된다.

```javascript
let student = {
    name: "kyj",
};

student.id = 112;

console.log(student);
```

<br>
<br>

### 프로퍼티 삭제

`delete` 연산자를 통해 프로퍼티를 삭제할 수 있다.
이 경우, `delete`의 피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다.
삭제하고자 하는 키가 존재하지 않는 경우, 무시되고 에러가 발생하지 않는다.

```javascript
let student = {
    id: 10,
    name: "kyj",
};

delete student.id;
delete student.home;

console.log(student);
```

<br>
<br>

### 객체 리터럴의 확장 기능

##### 프로퍼티 축약 표현

-   프로퍼티 값은 변수에 할당된 값, 즉 식별자 표현식일 수 있다.
-   프로퍼티 값으로 변수를 사용하는 경우, 변수 이름과 키가 동일 이름일 때 키를 생략할 수 있다. 생략한다면 변수명이 키로 자동생성된다.

```javascript
// 식별자 표현식으로 생성
let x = "xxx",
    y = "yyy";

let obj = {
    x: x,
    y: y,
};

console.log(obj);

// 프로퍼티 값으로 변수를 사용, 키 생략
let obj2 = {
    x,
    y,
};

console.log(obj2);
```

<br>

##### 계산된 프로퍼티 이름

계산된 프로퍼티: 문자열 타입 변환이 가능한 값으로 평가되는 표현식을 사용하여 프로퍼티 키를 동적으로 생성 가능(대신 표현식을 대괄호로 묶어야함`[]`)

```javascript
// ES5 > 객체 리터럴 외부에서 동적 생성
let prefix = "prop";
let i = 0;

let obj = {};

obj[prefix + "-" + ++i] = i;
obj[prefix + "-" + ++i] = i;
obj[prefix + "-" + ++i] = i;

console.log(obj);

// ES6 > 객체 리터럴 내부에서도 키를 동적 생성 가능
let prefix = "prop";
let i = 0;

let obj = {
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i,
};

console.log(obj);
```

<br>

##### 메서드 축약 표현

`function` 키워드를 생략하여 메서드를 정의할 수 있지만, 이는 프로퍼티에 할당한 함수와 다르게 동작한다.

```javascript
// ES5
let obj = {
    name: "kim",
    sayHi: function () {
        console.log("Hi! " + this.name);
    },
};

obj.sayHi();

// ES6 > function 키워드를 생략할 수 있다.
let obj = {
    name: "kim",
    sayHi() {
        console.log("Hi! " + this.name);
    },
};
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
