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

객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.

<br>
<br>
<br>
<br>

### 출처

위키북스, 『모던 자바스크립트 Deep Dive』, 이웅모

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
