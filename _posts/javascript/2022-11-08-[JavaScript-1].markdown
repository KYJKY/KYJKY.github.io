---
layout: post
title: "[모던JS] 변수"
date: 2022-11-08 23:35:44 +09:00
excerpt: "모던 자바스크립트 Deep Dive<br>2022-11-08"
javascript: true
categories: javascript
tags: javascript
comments: true
---

# 📌 [모던 자바스크립트 13주 뿌시기] 4. 변수

---

<figure>
    <a href="/assets/img/JavaScript/2022-11-10/bookcover.png"><img src="/assets/img/JavaScript/2022-11-10/bookcover.png"></a>
    <figcaption style="text-align:center"></figcaption>
</figure>

<br>
<br>

# 4. 변수

### 컴퓨터는 어떻게 연산을 수행하는가? 그리고 변수란 무엇인가?

> 아래 식을 컴퓨터는 어떻게 연산하는가?
> 10 + 20

_"컴퓨터는 CPU를 사용하여 연산하고, 메모리를 사용하여 데이터를 기억한다."_

`메모리(memory)`는 `메모리 셀(memory cell)`의 집합체이다. 이는 하나 당 1byte이다.  
각 셀은 고유의 `메모리 주소(memory address)`를 갖는다.

위의 10 + 20의 연산에서 10과 20은 각각 메모리 상의 임의의 위치에 저장된다.  
CPU는 저장된 10과 20을 읽어들여 연산한다.

연산 결과 30이라는 값이 메모리에 저장된다.  
만약 30이라는 값을 재사용하기 위해서는 저장된 메모리 주소를 직접 접근해야한다.  
그러나, 메모리 주소를 통한 접근 방법은 위험요소가 크다.

변수는 이러한 위험을 피하기 위해 만들어진 메커니즘이다.

**변수: 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그것을 식별하기 위해 붙인 이름.**

변수는 메모리 공간의 주소로 치환된다. 이는 개발자가 메모리 주소를 통한 접근을 대체하면서 안전하게 값에 접근할 수 있도록 한다.

```javascript
// 여러 변수 선언 방법

let name = "김연중";
let age = 26;
let book = { title: "Javascript", cost: 20000 };
let books = [
    { title: "Javascript", cost: 20000 },
    { title: "C#", cost: 30000 },
];

let myName = name;
```

할당: 변수에 값을 저장하는 것. ex) age 변수에 26이라는 값을 할당했다.  
참조: 변수에 저장된 값을 읽어들이는 것. ex) myName 변수에 name 변수를 참조하였다.

<br>
<br>

### 식별자

> 식별자란?  
> 어떤 값을 구별해서 식별할 수 있는 고유한 이름. 즉, 변수이름 = 식별자
> 식별자는 값이 아닌 메모리 주소를 기억한다.

변수와 식별자의 차이?  
식별자는 '변수 이름'으로서의 역할 뿐만이 아닌, 함수, 클래스 등의 구별하여 식별할 수 있는 것을 통칭한다.

<br>
<br>

### 변수 선언

> 변수 선언?
> 변수를 생성하는 것.
> 값을 저장하기 위한 공간의 확보하고 변수 이름과 확보된 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 것.

**변수는 반드시 선언 후 사용할 수 있다.**

변수 선언은 2단계에 거쳐 수행된다.

1. 선언 단계: 변수 이름을 등록해서 JS엔진에게 변수의 존재를 알린다.
2. 초기화 단계: 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined를 할당하여 초기화한다.

만약 선언하지 않은 식별자에 접근하면 ReferenceError(참조에러)가 발생한다.

<br>
<br>

### 변수 선언의 실행 시점과 변수 호이스팅

```javascript
console.log(score); // undefined

var score;
```

<br>

> 위 코드에서 참조에러가 호출되는 것이 아닌 undefined가 출력되는 이유?
> 변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점(런타임)이 아닌, 그 이전 단계에 실행되기 때문이다.
> 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트의 고유 특징을 **변수 호이스팅**이라 한다.

<br>
<br>

### 값의 할당, 그리고 재할당

```javascript
// 변수 선언과 값의 할당
var now; // 변수 선언, undefined
now = "아침"; // 값의 할당, "아침"

// 변수 선언 + 값의 할당을 한 문장으로
var phone = "아이폰";

// 값의 재할당
now = "점심";

const pi = 3.141592;
//pi = 3.14;  // 에러. const 키워드로 선언된 변수는 재할당 할 수 없다.
```

※ 변수 선언은 런타임 이전에 실행되지만, 값의 할당은 런타임에 실행된다.

참고로, 위 코드에서 now에는 undefined와 "아침"이라는 값이 총 두 번 할당된다.  
이는 한 메모리 공간을 공유하는 것이 아니라, 새로운 메모리 공간을 확보하여 할당하는 것이다.

마지막 행에서 now는 재할당 되었지만, pi는 재할당할 수 없다.  
**재할당이 불가능한 것은 변수가 아닌 상수이다.**

now가 "점심"으로 재할당될 때, "아침" 값은 어떻게 되는가?
"아침" 값은 어떤 변수도 값으로 가지고 있지 않기 때문에 불필요한 값으로 분류된다.  
그리고 가비지 콜렉터에 의해 메모리에서 자동 해제된다. 이 시점은 예측불가능하다.

<br>
<br>

### 식별자 네이밍 규칙

꼭 지켜야하는 규칙

-   식별자는 특수문자를 제외한 문자, 숫자, 언더스코어(\_), 달러($) 가능
-   식별자는 숫자로 시작해서는 안된다.
-   예약어(for, if 등 javascript 내에 사용되는 단어)은 식별자로 사용할 수 없다.

강제는 아니지만 지키면 좋은 것

-   변수를 선언할 때, 쉼표로 여러 변수를 한 번에 선언하는 것은 가독성에 안좋다.
-   식별자는 알파벳을 권장한다.
-   변수 이름은 변수의 존재 목적에 맞게 작명하는 것이 좋다. 이는 코드 가독성을 높힌다.
-   주석이 필요 없는 변수명을 만들려고 노력하자.

네이밍 컨벤션의 예

```javascript
// 카멜 케이스 - 보편적인 변수와 함수명에 쓰인다.
var firstMyName;

// 스네이크 케이스
var first_my_name;

// 파스칼 케이스 - 보편적인 생성자 함수, 클래스의 이름에 쓰인다.
var FirstMyName;

// 헝가리안 케이스
var strFirstMyName;
var numberMyAge;
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
