# 목차

[📌중요한 점](#📌중요한-점)

[📗배운 점 ](#📗배운-점)

[🤔궁금한 점](#🤔궁금한-점)

---

<br>

# 📌중요한 점

## 연산자

- 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 하나의 값을 만든다.
  - 피연산자를 연산하여 새로운 값을 만드는 역할
- 연산의 대상 => 피연산자 (값으로 평가될 수 있는 표현식)

## 7.4 삼항 조건 연산자

![7-1 삼항조건연산자](/assets/7-1.jpg)

**삼항 조건 연산자 표현식과 if...else문의 차이는 무엇일까?**

- `삼항 조건 연산자는 표현식으로 값처럼 사용할 수 있지만 if...else문은 표현식이 아닌 문이므로 값으로 사용할 수 없다.`

## 7.5 논리 연산자

- 논리 연산자는 우항과 좌항의 피연산자(부정 논리 연산자의 경우 우항의 피연산자)를 논리 연산한다.
<table>
 <tr>
    <td>논리 연산자</td>
    <td>의미</td>
   <td>부수 효과</td>
  </tr>
  <tr>
    <td>||</td>
    <td>논리합 (OR)</td>
   <td>X</td>
  </tr>
  <tr>
  <td>&&</td>
    <td>논리곱 (AND)</td>
   <td>X</td>
  </tr>
  <tr>
  <td>!</td>
    <td>부정 (NOT)</td>
   <td>X</td>
  </tr>
</table>

### 07-25

```javascript
// 논리합(||) 연산자 => 둘 중 하나 T
true || true; // -> true
true || false; // -> true
false || true; // -> true
false || false; // -> false

// 논리곱(&&) 연산자 => 둘 다 T
true && true; // -> true
true && false; // -> false
false && true; // -> false
false && false; // -> false

// 논리 부정(!) 연산자
!true; // -> false
!false; // -> true
```

### 07-26

```javascript
// 암묵적 타입 변환
!0; // -> true
!"Hello"; // -> false
```

- `논리 부정 연산자(!)는 언제나 불리언 값을 반환`한다. 단, 피연산자가 반드시 불리언 값일 필요는 없고 불리언 값이 아니더라도 암묵적으로 타입이 변환된다.

### 07-27

```javascript
// 단축 평가
"Cat" && "Dog"; // -> 'Dog'
```

- 논리합(||) 또는 논리곱(&&) 연산의 결과도 불리언이 아닐 수도 있다 => 2개의 피연산자 중 어느 한쪽으로 평가.
  <br>

<br>

# 📗배운 점

## 7.3.1 동등/일치 비교 연산자

**일치 비교 연산자(===)에서 NaN을 주의하자 !**

- NaN은 자기 자신과 일치하지 않는 유일한 값.
- 숫자가 NaN인지 조사하려면 빌트인 함수 `Number.isNaN`을 사용한다.

### 07-15

```javascript
// NaN은 자신과 일치하지 않는 유일한 값이다.
NaN === NaN; // -> false
```

### 07-16

```javascript
// Number.isNaN 함수는 지정한 값이 NaN인지 확인하고 그 결과를 불리언 값으로 반환한다.
Number.isNaN(NaN); // -> 숫자 아니니까 true
Number.isNaN(10); // -> 숫자라서 false
Number.isNaN(1 + undefined); // -> true
```

<br>

**숫자 0도 주의하자. 자바스크립트에서 양의 0과 음의 0을 비교하면 true를 반환한다.**

### 07-17

```javascript
// 양의 0과 음의 0의 비교. 일치 비교/동등 비교 모두 결과는 true이다.
0 === -0; // -> true
0 == -0; // -> true
```

<br>

## 7.8 typeof 연산자

- typeof 연산자로 null을 연산해보면 'null'이 아닌 'object'를 반환하므로 주의하자.
- `값이 null 타입인지 확인할 때는 typeof 연산자 말고 일치 연산자(===)를 사용하자 !`
- 선언하지 않은 식별자를 typeof 로 연산하면 ReferenceError가 아닌 undefined를 반환한다.
  - typeof가 단순히 변수의 타입을 확인하는 연산자로서, 변수가 선언되지 않았을 때도 실행될 수 있도록 설계되어 있음

### 07-31

```javascript
typeof ""; // -> "string"
typeof 1; // -> "number"
typeof NaN; // -> "number"
typeof true; // -> "boolean"
typeof undefined; // -> "undefined"
typeof Symbol(); // -> "symbol"
typeof null; // -> "object"
typeof []; // -> "object"
typeof {}; // -> "object"
typeof new Date(); // -> "object"
typeof /test/gi; // -> "object"
typeof function () {}; // -> "function"
```

### 07-32

```javascript
var foo = null;

typeof foo === null; // -> false
foo === null; // -> true
```

### 07-33

```javascript
// undeclared 식별자를 선언한 적이 없다.
typeof undeclared; // -> undefined
```
