## 목차

[📗배운 점 ](#📗배운-점)

[🤔궁금한 점](#🤔궁금한-점)

[📌중요한 점](#📌중요한-점)

## 📗배운 점

## 12.1 함수란?

일련의 과정을 문으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것

매개변수 : 함수 내부로 입력을 전달받는 변수

인수 : 입력

반환값 : 출력

함수는 값이며, 여러 개 존재할 수 있으므로 특정 함수를 구별하기 위해 함수 이름을 사용할 수 있음

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/f04af250-f7ad-42fc-9af6-fcc5ea170f53)

## 12.2 함수를 사용하는 이유

함수는 필요할 때 여러번 호출할 수 있기 때문에 코드의 재사용이라는 측면에서 매우 유용

코드의 중복을 억제하고 재사용성을 높이는 함수는 유지보수의 편의성을 높이고 실수를 줄여 코드의 신뢰성을 높임

## 12.3 함수 리터럴

함수 리터럴은 function 키워드, 함수 이름, 매개변수 목록, 함수 몸체로 구성

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/417cbd14-e866-45d6-9e13-54ca06cbaaef)

리터럴은 값을 생성하기 위한 표기법

함수 리터럴도 평가되어 값을 생성하며 이 값은 객체이기 때문에 함수는 객체임

- 일반 객체는 호출할 수 없지만 함수는 호출할 수 있다는 점에서 일반 객체와 다름

## 12.4 함수 정의

함수를 호출하기 이전에 인수를 전달받을 매개변수와 실행할 문들, 그리고 반환할 값을 지정하는 것

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/1543de2a-164e-43b4-a0ad-58a1492b3255)

### 12.4.1 함수 선언문

```javascript
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 참조
// console.dir은 console.log와는 달리 함수 객체의 프로퍼티까지 출력한다.
// 단, Node.js 환경에서는 console.log와 같은 결과가 출력된다.
console.dir(add); // ƒ add(x, y)

// 함수 호출
console.log(add(2, 5)); // 7
```

- 함수 선언문은 함수 리터럴과 형태가 동일

```javascript
// 함수 선언문은 함수 이름을 생략할 수 없다.
function (x, y) {
  return x + y;
}
// SyntaxError: Function statements require a function name
```

- 함수 리터럴은 함수 이름을 생략할 수 있지만 함수 선언문은 함수 이름을 생략할 수 없음

표현식이 아닌 문은 변수에 할당할 수 없음  
함수 선언문도 표현식이 아닌 문이므로 변수에 할당할 수 없음

```javascript
// 함수 선언문은 표현식이 아닌 문이므로 변수에 할당할 수 없다.
// 하지만 함수 선언문이 변수에 할당되는 것처럼 보인다.
var add = function add(x, y) {
  return x + y;
};

// 함수 호출
console.log(add(2, 5)); // 7
```

- 이 예제에서는 함수 선언문이 변수에 할당되는 것처럼 보임
- 함수 선언문은 함수 이름을 생략할 수 없다는 점을 제외하면 함수 리터럴과 형태가 동일
- 함수 이름이 있는 기명 함수 리터럴은 함수 선언문 또는 함수 리터럴 표현식으로 해석될 가능성이 있음

```javascript
// 기명 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석된다.
// 함수 선언문에서는 함수 이름을 생략할 수 없다.
function foo() {
  console.log("foo");
}
foo(); // foo

// 함수 리터럴을 피연산자로 사용하면 함수 선언문이 아니라 함수 리터럴 표현식으로 해석된다.
// 함수 리터럴에서는 함수 이름을 생략할 수 있다.
(function bar() {
  console.log("bar");
});
bar(); // ReferenceError: bar is not defined
```

- 위 예제에서 단독으로 사용된 함수 리터럴(foo)은 함수 선언문으로 해석
- 그룹 연산자 () 내에 있는 함수 리터럴(bar)은 함수 리터럴 표현식으로 해석
- 그룹 연산자의 피연산자는 값으로 평가될 수 있는 표현식이어야 함
- 따라서 표현식이 아닌 문인 함수 선언문은 피연산자로 사용할 수 없음

이름이 있는 기명 함수 리터럴은 코드의 문맥에 따라 함수 선언문 또는 함수 리터럴 표현식으로 해석됨

함수 선언문과 함수 리터럴 표현식은 함수 객체를 생성한다는 점에서 동일하지만 호출에 차이가 있음

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/d1f0cff2-b1d1-4a42-8c1c-c45bf869a42e)

- 함수 몸체 외부에서는 함수 이름을 함수를 호출할 수 없음
- foo는 함수 몸체 내부에서만 유효한 식별자인 함수 이름이므로 foo로 함수를 호출할 수 없어야 함
- 위 예제에서는 식별자 foo를 선언한 적도 없고 할당한 적도 없음
- 그럼 무엇인가? → foo는 자바스크립트 엔진이 암묵적으로 생성한 식별자

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/72eb10f6-2208-407c-b1dd-5ac16a05ea40)

- 자바스크립트 엔진은 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체를 할당함

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/4b830486-c745-48ad-ae2d-51b9916a15e7)

- 함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출

### 12.4.2 함수 표현식

자바스크립트의 함수는 일급 객체 → 함수를 값처럼 자유롭게 사용할 수 있음

```javascript
// 함수 표현식
var add = function (x, y) {
  return x + y;
};

console.log(add(2, 5)); // 7
```

- 함수는 일급 객체이므로 함수 리터럴로 생성한 함수 객체를 변수에 할당할 수 있음

```javascript
// 기명 함수 표현식
var add = function foo(x, y) {
  return x + y;
};

// 함수 객체를 가리키는 식별자로 호출
console.log(add(2, 5)); // 7

// 함수 이름으로 호출하면 ReferenceError가 발생한다.
// 함수 이름은 함수 몸체 내부에서만 유효한 식별자다.
console.log(foo(2, 5)); // ReferenceError: foo is not defined
```

- 함수를 호출할 때는 함수 이름이 아니라 함수 객체를 가리키는 식별자를 사용해야 함
- 함수 이름은 함수 몸체 내부에서만 유효한 식별자이므로 함수 이름으로 함수를 호출할 수 없음

### 12.4.3 함수 생성 시점과 함수 호이스팅

```javascript
// 함수 참조
console.dir(add); // ƒ add(x, y)
console.dir(sub); // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x - y;
};
```

- 함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출할 수 있음
- 그러나 함수 표현식으로 정의한 함수는 함수 표현식 이전에 호출할 수 없음
- 이는 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르기 때문
- 이처럼 함수 선언문이 코드의 선두로 끌어 오려진 것처럼 동작하는 자바스크립트 고유의 특징을 **함수 호이스팅**이라 함
  - 변수 호이스팅 : var 키워드로 선언된 변수는 undefined로 초기화
  - 함수 호이스팅 : 함수 선언문을 통해 암묵적으로 생성된 식별자는 함수 객체로 초기화
- 변수 할당문의 값은 할당문이 실행되는 시점, 즉 런타임에 평가되므로 함수 표현식의 함수 리터럴도 할당문이 실행되는 시점에 평가되어 함수 객체가 됨
- 따라서 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생
- 함수 표현식 이전에 함수를 참조하면 undefined로 평가
- 함수 표현식으로 정의한 함수는 반드시 함수 표현식 이후에 참조 또는 호출해야 함

### 12.4.4 Function 생성자 함수

Function 생성자 함수에 매개변수 목록과 함수 몸체를 문자열로 전달하면서 new 연산자와 함께 호출하면 함수 객체를 생성해서 반환

- 생성자 함수 : 객체를 생성하는 함수

```javascript
var add1 = (function () {
  var a = 10;
  return function (x, y) {
    return x + y + a;
  };
})();

console.log(add1(1, 2)); // 13

var add2 = (function () {
  var a = 10;
  return new Function("x", "y", "return x + y + a;");
})();

console.log(add2(1, 2)); // ReferenceError: a is not defined
```

- Function 생성자 함수로 생성한 함수는 클로저를 생성하지 않는 등, 함수 선언문이나 함수 표현식으로 생성한 함수와 다르게 동작

### 12.4.5 화살표 함수

funcion 키워드 대신 화살표를 사용해 좀 더 간략한 방법으로 함수를 선언

화살표 함수는 항상 익명 함수로 정의

## 12.5 함수 호출

### 12.5.1 매개변수와 인수

함수를 실행하기 위해 필요한 값을 함수 외부에서 함수 내부로 전달할 필요가 있는 경우, 매개변수(인자)를 통해 인수를 전달

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/cb7a44fc-fb6c-4bc6-9401-a45959eb77ff)

- 인수는 값으로 평가될 수 있는 표현식, 함수를 호출할 때 지정하며 개수와 타입에 제한이 없음
- 매개변수는 함수를 정의할 때 선언, 함수 몸체 내부에서 변수와 동일하게 취급

```javascript
function add(x, y) {
  console.log(x, y); // 2 5
  return x + y;
}

add(2, 5);

// add 함수의 매개변수 x, y는 함수 몸체 내부에서만 참조할 수 있다.
console.log(x, y); // ReferenceError: x is not defined
```

- 매개변수의 스코프는 함수 내부

```javascript
function add(x, y) {
  return x + y;
}

console.log(add(2)); // NaN
```

- 인수가 부족해서 인수가 할당되지 않은 매개변수의 값은 undefined

```javascript
function add(x, y) {
  console.log(arguments);
  // Arguments(3) [2, 5, 10, callee: ƒ, Symbol(Symbol.iterator): ƒ]

  return x + y;
}

add(2, 5, 10);
```

- 매개변수보다 인수가 더 많은 경우 초과된 인수는 무시
- 버려지는 건 아니고 암묵적으로 arguments 객체의 프로퍼티로 보관

### 12.5.2 인수 확인

```javascript
function add(x, y) {
  return x + y;
}

console.log(add(2)); // NaN
console.log(add("a", "b")); // 'ab'
```

- 코드 상으로 어떤 타입의 인수를 전달해야 하는지, 어떤 타입의 값을 반환하는지 명확하지 않음
- 이러한 상황이 발생한 이유
  - 자바스크립트 함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않음
  - 자바스크립트는 동적 타입 언어로 자바스크립트 함수는 매개변수의 타입을 사전에 지정할 수 없음

```javascript
function add(x, y) {
  if (typeof x !== "number" || typeof y !== "number") {
    // 매개변수를 통해 전달된 인수의 타입이 부적절한 경우 에러를 발생시킨다.
    throw new TypeError("인수는 모두 숫자 값이어야 합니다.");
  }

  return x + y;
}

console.log(add(2)); // TypeError: 인수는 모두 숫자 값이어야 합니다.
console.log(add("a", "b")); // TypeError: 인수는 모두 숫자 값이어야 합니다.
```

- 함수 내부에서 적절한 인수가 전달되었는지 확인
- 그래도 부적절한 호출을 사전에 방지할 수 없고 에러는 런타임에 발생하게 됨

arguments 객체를 통해 인수 개수를 확인할 수도 있고 단축 평가를 사용해 매개변수에 기본값을 할당하는 방법도 있음

```javascript
function add(a = 0, b = 0, c = 0) {
  return a + b + c;
}

console.log(add(1, 2, 3)); // 6
console.log(add(1, 2)); // 3
console.log(add(1)); // 1
console.log(add()); // 0
```

- 매개변수 기본값을 사용하면 함수 내에서 수행하던 인수 체크 및 초기화를 간소화할 수 있음
- 매개변수 기본값은 매개변수에 인수를 전달하지 않았을 경우와 undefined를 전달한 경우에만 유효

### 12.5.3 매개변수의 최대 개수

이상적인 함수는 한 가지 일만 해야하며 가급적 작게 만들어야 함

따라서 매개변수는 최대 3개 이상을 넘지 않는 것을 권장  
그 이상의 매개변수가 필요하다면 하나의 매개변수를 선언하고 객체를 인수로 전달하는 것이 유리

```javascript
$.ajax({
  method: "POST",
  url: "/user",
  data: { id: 1, name: "Lee" },
  cache: false,
});
```

- 객체를 인수로 사용하는 경우 프로퍼티 키만 정확히 지정하면 매개변수의 순서를 신경쓰지 않아도 됨
- 주의할 것은 함수 외부에서 함수 내부로 전달한 객체를 함수 내부에서 변경하면 함수 외부의 객체가 변경되는 부수효과가 발생한다는 것

### 12.5.4 반환문

함수는 return 키워드와 표현식(반환값)으로 이뤄진 반환문을 사용해 실행 결과를 함수 외부로 반환할 수 있음

```javascript
function multiply(x, y) {
  return x * y; // 반환문
  // 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시된다.
  console.log("실행되지 않는다.");
}

console.log(multiply(3, 5)); // 15
```

- 반환문은 함수의 실행을 중단하고 함수 몸체를 빠져나감
- 반환문은 return 키워드 뒤에 오는 표현식을 평가해 반환한다

```javascript
function foo() {
  return;
}

console.log(foo()); // undefined
```

- 반환값으로 사용할 표현식을 명시적으로 지정하지 않으면 undefined 반환

```javascript
function foo() {
  // 반환문을 생략하면 암묵적으로 undefined가 반환된다.
}

console.log(foo()); // undefined
```

- 반환문은 생략할 수 있음
- 이때 함수는 함수 몸체 마지막 문까지 실행한 후 암묵적으로 undefined를 반환

return 키워드와 반환값으로 사용할 표현식 사이에 줄바꿈이 있으면 세미콜론이 자동 삽입되어 반환값이 무시됨

## 12.6 참조에 의한 전달과 외부 상태의 변경

매개변수도 함수 몸체 내부에서 변수와 동일하게 취급되므로 매개변수 또한 타입에 따라 값에 의한 전달, 참조에 의한 전달 방식을 그대로 따름

```javascript
// 매개변수 primitive는 원시 값을 전달받고, 매개변수 obj는 객체를 전달받는다.
function changeVal(primitive, obj) {
  primitive += 100;
  obj.name = "Kim";
}

// 외부 상태
var num = 100;
var person = { name: "Lee" };

console.log(num); // 100
console.log(person); // {name: "Lee"}

// 원시 값은 값 자체가 복사되어 전달되고 객체는 참조 값이 복사되어 전달된다.
changeVal(num, person);

// 원시 값은 원본이 훼손되지 않는다.
console.log(num); // 100

// 객체는 원본이 훼손된다.
console.log(person); // {name: "Kim"}
```

- 원시 타입 인수는 값 자체가 복사되어 매개변수에 전달되기 때문에 함수 몸체에서 그 값을 변경해도 원본은 훼손되지 않음
- 객체 타입 인수는 참조 값이 복사되어 매개변수에 전달되기 때문에 함수 몸체에서 참조 값을 통해 객체를 변경할 경우 원본이 훼손

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/25b5a1fe-08ea-46bf-8cf8-06d9604db0fb)

- 이처럼 함수가 외부 상태를 변경하면 상태 변화를 추적하기 어려움
- 문제 해결 방법
  - 객체를 불변 객체로 만들어 사용
    - 객체의 복사본을 새롭게 생성하는 비용은 들지만 객체를 마치 원시 값처럼 변경 불가능한 값으로 동작하게 만드는 것
    - 이를 통해 객체의 상태 변경을 원천 봉쇄
    - 객체의 상태 변경이 필요한 경우 객체의 방어적 복사를 통해 원본 객체를 완전히 복제
    - 즉, 깊은 복사를 통해 새로운 객체를 생성하고 재할당을 통해 교체

## 12.7 다양한 함수의 형태

### 12.7.1 즉시 실행 함수

함수 정의와 동시에 즉시 호출되는 함수

즉시 실행 함수는 단 한번만 호출되며 다시 호출할 수 없음

즉시 실행 함수를 사용하는 이유

- 전역 스코프에 불필요한 변수를 추가해서 오염시키는 것을 방지하기 위해
- 즉시 실행 함수 내부 안으로 다른 변수들이 접근하는 것을 막을 수 있기 때문에
- 즉시 실행 함수 내에 코드를 모아 두면 홍시 있을 수 있는 변수나 함수 이름의 충돌을 방지

```javascript
// 익명 즉시 실행 함수
(function () {
  var a = 3;
  var b = 5;
  return a * b;
})();
```

- 즉시 실행 함수는 함수 이름이 없는 익명 함수를 사용하는 것이 일반적

```javascript
// 기명 즉시 실행 함수
(function foo() {
  var a = 3;
  var b = 5;
  return a * b;
})();

foo(); // ReferenceError: foo is not defined
```

- 그룹 연산자(...) 내의 기명 함수는 함수 선언문이 아니라 함수 리터럴로 평가
- 함수 이름은 함수 몸체에서만 참조할 수 있는 식별자이므로 즉시 실행 함수를 다시 호출할 수 없음

```javascript
function () { // SyntaxError: Function statements require a function name
  // ...
}();
```

- 함수 정의가 함수 선언문의 형식에 맞지 않기 때문에 에러 발생
- 함수 선언문은 함수 이름을 생략할 수 없음

```javascript
function foo() {
  // ...
}(); // SyntaxError: Unexpected token ')'
```

```javascript
function foo() {}(); // => function foo() {};();
```

- 자바스크립트 엔진이 암묵적으로 수행하는 세미콜론 자동 삽입 기능에 의해 함수 선언문이 끝나는 위치, 즉 함수 코드 블록의 닫는 중괄호 뒤에 ";"이 암묵적으로 추가되기 때문에 에러 발생
- 따라서 함수 선언문 뒤의 ()는 함수 호출 연산자가 아니라 그룹 연산자로 해석되고, 그룹 연산자에 피연산자가 없기 때문에 에러가 발생

```javascript
console.log(typeof function f() {}); // function
console.log(typeof function () {}); // function
```

- 그룹 연산자의 피연산자는 값으로 평가되므로 기명 또는 무명함수를 그룹 연산자로 감싸면 함수 리터럴로 평가되어 함수 객체가 됨
- 즉 그룹 연산자로 함수를 묶은 이유는 먼저 함수 리터럴을 평가해서 함수 객체를 생성하기 위해서

### 12.7.2 재귀 함수

재귀 호출 : 함수가 자기 자신을 호출하는 것

재귀 함수 : 자기 자신을 호출하는 행위, 즉 재귀 호출을 수행하는 함수

```javascript
function countdown(n) {
  for (var i = n; i >= 0; i--) console.log(i);
}

countdown(10);
```

```javascript
function countdown(n) {
  if (n < 0) return;
  console.log(n);
  countdown(n - 1); // 재귀 호출
}

countdown(10);
```

- 이처럼 자기 자신을 호출하는 재귀 함수를 사용하면 반복되는 처리를 반복문 없이 구현할 수 있음

```javascript
// 함수 표현식
var factorial = function foo(n) {
  // 탈출 조건: n이 1 이하일 때 재귀 호출을 멈춘다.
  if (n <= 1) return 1;
  // 함수를 가리키는 식별자로 자기 자신을 재귀 호출
  return n * factorial(n - 1);

  // 함수 이름으로 자기 자신을 재귀 호출할 수도 있다.
  // console.log(factorial === foo); // true
  // return n * foo(n - 1);
};

console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
```

- 함수 표현식으로 정의한 함수 내부에서는 함수 이름은 물론 함수를 가리키는 식별자로도 자기 자신을 재귀 호출할 수 있음
- 함수 외부에서 함수를 호출할 때는 반드시 함수를 가리키는 식별자로 해야 함
- 재귀 함수는 자신을 무한 재귀 호출하기 때문에 이를 멈출 수 있는 탈출 조건을 반드시 만들어야 함
- 탈출 조건이 없으면 함수가 무한 호출되어 스택 오버플로 에러가 발생
- 재귀 함수는 반복문을 사용하는 것보다 재귀 함수를 사용하는 편이 더 직관적으로 이해하기 쉬울때만 한정적으로 사용

### 12.7.3 중첩 함수

중첩 함수 : 함수 내부에 정의된 함수

외부 함수 : 중첩 함수를 포함한 함수

중첩 함수는 외부 함수 내부에서만 호출 가능

일반적으로 중첩 함수는 자신을 포함하는 외부 함수를 돕는 헬퍼 함수 역할

```javascript
function outer() {
  var x = 1;

  // 중첩 함수
  function inner() {
    var y = 2;
    // 외부 함수의 변수를 참조할 수 있다.
    console.log(x + y); // 3
  }

  inner();
}

outer();
```

### 12.7.4 콜백 함수

콜백 함수 : 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수

고차 함수 : 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수

```javascript
// 외부에서 전달받은 f를 n만큼 반복 호출한다.
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i); // i를 전달하면서 f를 호출
  }
}

var logAll = function (i) {
  console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) {
  if (i % 2) console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1 3
```

- 위 repeat 함수는 경우에 따라 변경되는 일을 함수 f로 추상화했고 이를 외부에서 전달 받음
  - 내부 로직에 강력히 의존하지 않고 외부에서 로직의 일부분을 함수로 전달받아 수행

고차 함수는 매개변수를 통해 전달받은 콜백 함수의 호출 시점을 결정해서 호출

콜백 함수는 고차 함수에 의해 호출  
이때 고차 함수는 필요에 따라 콜백 함수에 인수를 전달할 수 있음

```javascript
// 익명 함수 리터럴을 콜백 함수로 고차 함수에 전달한다.
// 익명 함수 리터럴은 repeat 함수를 호출할 때마다 평가되어 함수 객체를 생성한다.
repeat(5, function (i) {
  if (i % 2) console.log(i);
}); // 1 3
```

- 콜백 함수를 다른 곳에서도 호출할 필요가 있거나, 콜백 함수를 전달받는 함수가 자주 호출된다면 함수 외부에서 콜백 함수를 정의한 후 함수 참조를 고차 함수에 전달하는 편이 효율적

### 12.7.5 순수 함수와 비순수 함수

순수 함수 : 어떤 외부 상태에 의존하지도 않고 변경하지도 않는, 즉 부수 효과가 없는 함수

비순수 함수 : 외부 상태에 의존하거나 외부 상태를 변경하는, 즉 부수 효과가 있는 함수

```javascript
var count = 0; // 현재 카운트를 나타내는 상태

// 순수 함수 increase는 동일한 인수가 전달되면 언제나 동일한 값을 반환한다.
function increase(n) {
  return ++n;
}

// 순수 함수가 반환한 결과값을 변수에 재할당해서 상태를 변경
count = increase(count);
console.log(count); // 1

count = increase(count);
console.log(count); // 2
```

- 순수 함수는 오직 매개변수를 통해 함수 내부로 전달된 인수에게만 의존해 값을 생성하고 반환
- 순수 함수는 일반적으로 최소 하나 이상의 인수를 전달 받음
- 순수 함수는 인수를 변경하지 않는 것이 기본
- 함수의 외부 상태를 변경하지 않음

```javascript
var count = 0; // 현재 카운트를 나타내는 상태: increase 함수에 의해 변화한다.

// 비순수 함수
function increase() {
  return ++count; // 외부 상태에 의존하며 외부 상태를 변경한다.
}

// 비순수 함수는 외부 상태(count)를 변경하므로 상태 변화를 추적하기 어려워진다.
increase();
console.log(count); // 1

increase();
console.log(count); // 2
```

- 인수를 전달받지 않고 함수 내부에서 외부 상태를 직접 참조하면 외부 상태에 의존하게 되어 반환 값이 변할 수 있고, 외부 상태도 변경할 수 있으므로 비순수 함수
- 함수가 외부 상태를 변경하면 상태 변화를 추적하기 어려워짐
- 따라서 함수 외부 상태의 변경을 지양하는 순수 함수를 사용하는 것이 좋음

## 🤔궁금한 점

## 📌중요한 점
