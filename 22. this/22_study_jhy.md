# 목차

[📗배운 점](#📗배운-점)

[📌중요한 점](#📌중요한-점)

[🤔궁금한 점](#🤔궁금한-점)

## 📗배운 점

### 22.1 THIS 키워드

### This

- 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다.
- this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.
- 자바스크립트 엔진에 의해 암묵적으로 생성
- 코드 어디서든 참조 가능

단, this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.

> this 바인딩
>
> - 식별자와 값을 연결하는 과정

- 자바스크립트의 this 는 함수가 호출되는 방식에 따라 this에 바인딩될 값, 즉 this 바인딩이 동적으로 결정된다.

### 22.2 함수 호출 방식과 this 바인딩

this 바인딩

- 함수 호출 방식
- 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.

1. 일반함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출

#### 22.2.1 일반 함수 호출

기본적으로 this에는 전역 객체가 바인딩
![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/392be1e2-c3c2-48ad-9c73-03a55431b7a7)

콜백함수가 일반 함수로 호출되도 this에 전역객체가 바인딩된다.
![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/0ce08fc6-0277-4cd6-8270-ff9e969368b0)

일반 함수로 호출된 모든 함수(중첩함수, 콜백 함수 포함)내부의 this에는 전역 객체가 바인딩 된다.

#### 22.2.2 메서드 호출

메서드 내부의 this에는 메서드를 호출한 객체, 즉 메서드를 호출할때 메서드 이름 앞의 마침표(.) 연산자 앞에 기술한 객체가 바인딩 된다.
![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/7cab2344-b7f1-484f-b2e0-d27466b0ff51)

#### 22.2.3 생성자 함수 호출

생성자 함수 내부의 this에는 생성자 함수가 미래에 생성할 인스턴스가 바인딩된다.
![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/fc6f1a23-8d93-4691-bbf5-2e2bc1e4c5dd)

#### 22.2.4 Function.prototype.apply/call/bind 메서드에 의한 간접 호출

![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/a9736225-2dac-471e-90e2-e9aa51bee694)
apply와 call 메서드의 본질적인 기능은 함수를 호출하는 것이다.
함수에 인수를 전달하지 않는다.

![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/330df71c-cd9a-457a-a427-126cfb8162bf)
인수를 배열로 묶어 전달한다.
![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/5a76fe23-c097-4046-81a2-09f16ecf7276)

![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/a451640b-25f4-4bb6-b7a4-b778eb4bf535)

#### 함수 호출 방식에 따하 this 바인딩 동적으로 결정

![image](https://github.com/chowonn/js-deepdive-study/assets/101866872/8e02219c-f4a6-40b0-9a31-e512c91acc8b)
