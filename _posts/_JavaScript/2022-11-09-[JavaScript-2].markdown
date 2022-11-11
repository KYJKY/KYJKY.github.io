---
layout: post
title: "[모던JS] 표현식과 문"
date: 2022-11-09 23:35:44 +09:00
excerpt: "모던 자바스크립트 Deep Dive<br>2022-11-09"
cs: true
categories: JavaScript
tags: javascript
comments: true
---

# 📌 [모던 자바스크립트 13주 뿌시기] 5. 표현식과 문

---

<figure>
    <a href="/assets/img/JavaScript/2022-11-10/bookcover.png"><img src="/assets/img/JavaScript/2022-11-10/bookcover.png"></a>
    <figcaption style="text-align:center"></figcaption>
</figure>

<br>
<br>

# 5. 표현식과 문

## 값과 리터럴, 표현식

`값`: 값은 식(표현식)이 평가되어 생성된 결과, 변수에 할당되는 것.
`리터럴`: 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법
`표현식`: 값으로 평가될 수 있는 statement. 표현식이 평가되면 새로운 값을 생성하거나 기존 값을 참조한다.

값은 리터럴로 생성할 수 있다.  
자바스크립트 엔진은 리터럴을 평가하여 값을 생성한다.

#### 예시

```javascript
function sum(a, b){
    return a + b;
}

let myName = "Hi";

let myObj = {
    objName: "obj"
    , objNum: 1
    , objFunc: function(){
        return objNum + objName;
    }
}

let dice = {1,2,3,4,5,6};


// 리터럴 표현식
125;
"문자열";
true;

// 식별자 표현식
dice[2];
myObj.objNum;
myName;

// 함수/메서드 호출 표현식
sum(dice[3], dice[0]);
myObj.objFunc();

```

<br>
<br>

## Statement(문)과 토큰

Statement: 프로그램을 구성하는 기본 단위이자 최소 실행 단위. 프로그램은 문의 집합이다.
토큰: 문법적인 의미를 가지며, 문법적으로 더 이상 나눌 수 없는 코드의 기본 요소 (ex: 키워드, 식별자, 연산자, 리터럴, 세미콜론 ';', 마침표 '.')

<br>
<br>

## 세미콜론과 세미콜론 자동 삽입 기능

세미콜론은 문의 종료를 나타낸다.
문의 종료에는 세미콜론을 붙이지만, 코드 블록의 형태 뒤에는 세미콜론이 오지 않는다.
(자체 종결성을 갖기 때문)

<br>

#### 세미콜론 자동 삽입 기능(ASI: automatic semicolon insertion)

자바스크립트 엔진은 소스코드를 해석하면서 문의 끝이라고 판단될 경우 세미콜론을 자동으로 붙여주는 `세미콜론 자동 삽입 기능`이 암묵적으로 수행된다.

'세미콜론을 붙이는가 vs 붙이지 아니한가' 에 대한 논란은 끝이 없지만 붙이는 쪽이 보편적이다. 가끔 세미콜론이 개발자의 의도대로 동작하지 않는 경우가 있다.

#### 예시

```javascript
function test() {
    return;
    {
    }
    // ASI의 동작 결과: return; {};
    // 개발자의 예측: return {};
}

console.log(test()); // undefined 출력

var test2 = (function () {})(function () {});
// ASI의 동작 결과: var test2 = function () {}(function() {})();
// 개발자의 예측: var test2 = function () {}; (function() {})();
```

<br>
<br>

## 표현식인 문과 표현식이 아닌 문

문은 표현식과 표현식이 아닌 문으로 나뉜다.

표현식인 문: 값으로 평가될 수 있다.
현식이 아닌 문: 값으로 평가될 수 없다.

**표현식은 값으로 평가될 수 있는 문**이기 때문에 변수에 할당할 경우, 표현식인 문은 변수에 할당할 수 있지만 표현식이 아닌 문은 할당할 수 없다.

<br>
<br>
<br>
<br>

### 출처

위키북스, 『모던 자바스크립트 Deep Dive』, 이웅모

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
