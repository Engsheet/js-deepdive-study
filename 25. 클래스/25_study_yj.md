## 목차

[📗배운 점 ](#📗배운-점)

[🤔궁금한 점](#🤔궁금한-점)

[📌중요한 점](#📌중요한-점)

## 📗배운 점

## 25.2 클래스 정의

클래스는 class 키워드를 사용하여 정의

클래스를 표현식으로 정의할 수 있다는 것은 클래스가 값으로 사용할 수 있는 일급 객체라는 것을 의미

- 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능함
- 변수나 자료구조(객체, 배열 등)에 저장할 수 있음
- 함수의 매개변수에 전달할 수 있음
- 함수의 반환 값으로 사용할 수 있음

```javascript
// 클래스 선언문
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name; // name 프로퍼티는 public하다.
  }

  // 프로토타입 메서드
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }

  // 정적 메서드
  static sayHello() {
    console.log("Hello!");
  }
}

// 인스턴스 생성
const me = new Person("Lee");

// 인스턴스의 프로퍼티 참조
console.log(me.name); // Lee
// 프로토타입 메서드 호출
me.sayHi(); // Hi! My name is Lee
// 정적 메서드 호출
Person.sayHello(); // Hello!
```

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/cd01f44a-764e-4361-8f6d-eb73449d351b)

## 25.3 클래스 호이스팅

클래스는 함수로 평가

클래스 선언문으로 정의한 클래스는 함수 선언문과 같이 소스코드 평가 과정, 즉 런타임 이전에 먼저 평가되어 함수 객체를 생성함

이 때 클래스가 평가되어 생성된 함수 객체는 생성자 함수로서 호출할 수 있는 함수, 즉 constructor.

```javascript
console.log(Person);
// ReferenceError: Cannot access 'Person' before initialization

// 클래스 선언문
class Person {}
```

- 클래스는 클래스 정의 이전에 참조할 수 없음.
- 클래스 선언문은 마치 호이스팅이 발생하지 않는 것처럼 보이나 그렇지 않음

```javascript
const Person = "";

{
  // 호이스팅이 발생하지 않는다면 ''이 출력되어야 한다.
  console.log(Person);
  // ReferenceError: Cannot access 'Person' before initialization

  // 클래스 선언문
  class Person {}
}
```

- 클래스 선언문도 변수 선언, 함수 정의와 마찬가지로 호이스팅이 발생
- 단, 클래스는 let, const 키워드로 선언한 변수처럼 호이스팅
- 클래스 선언문 이전에 일시적 사각지대에 빠지기 때문에 호이스팅이 발생하지 않는 것처럼 동작

## 25.4 인스턴스 생성

```javascript
class Person {}

// 인스턴스 생성
const me = new Person();
console.log(me); // Person {}
```

- 클래스는 인스턴스를 생성하는 것이 유일한 존재 이유이므로 반드시 new 연산자와 함께 호출해야 함

## 25.5 메서드

### 25.5.1 constructor

```javascript
// 클래스는 함수다.
console.log(typeof Person); // function
console.dir(Person);
```

![image](https://github.com/jin62413/js-deepdive-study/assets/71061884/a1f93e47-25bd-4fc5-9924-c8f4fdda0cfa)

- 클래스는 평가되어 함수 객체가 됨
- 모든 함수 객체가 가지고 있는 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor 프로퍼티는 클래스 자신을 가리키고 있음. 이는 클래스가 인스턴스를 생성하는 생성자 함수라는 것을 의미
- 즉, new연산자와 함께 클래스를 호출하면 클래스는 인스턴스로 생성

constructor는 클래스 내에 최대 한 개만 존재할 후 있고 생략 가능, constructor를 생략하면 클래스에 빈 constructor가 암묵적으로 정의

```javascript
class Person {
  constructor() {
    // 고정값으로 인스턴스 초기화
    this.name = "Lee";
    this.address = "Seoul";
  }
}

// 인스턴스 프로퍼티가 추가된다.
const me = new Person();
console.log(me); // Person {name: "Lee", address: "Seoul"}
```

- 인스턴스를 생성할 때 클래스 외부에서 인스턴스 프로퍼티의 초기값을 전달하려면 constructor에 매개변수를 선언하고 인스턴스를 생성할 때 초기값을 전달
- 이때 초기값은 constructor의 매개변수에게 전달

```javascript
class Person {
  constructor(name) {
    this.name = name;

    // 명시적으로 객체를 반환하면 암묵적인 this 반환이 무시된다.
    return {};
  }
}

// constructor에서 명시적으로 반환한 빈 객체가 반환된다.
const me = new Person("Lee");
console.log(me); // {}
```

- 만약 this가 아닌 다른 객체를 명시적으로 반환하면 this, 즉 인스턴스가 반환되지 못하고 return문에 명시한 객체가 반환
- 명시적으로 원시값을 반환하면 원시값 반환은 무시되고 암묵적으로 this가 반환
- 따라서 constructor 내부에서 return 문을 반드시 생략

### 25.5.2 프로토타입 메서드

```javascript
// 생성자 함수
function Person(name) {
  this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHi = function () {
  console.log(`Hi! My name is ${this.name}`);
};

const me = new Person("Lee");
me.sayHi(); // Hi! My name is Lee
```

- 클래스 몸체에서 정의한 메서드는 생성자 함수에 의한 객체 생성 방식과는 다르게 클래스의 prototype 프로퍼티에 메서드르 추가하지 않아도 기분적으로 프로토타입 메서드가 됨

### 25.5.3 정적 메서드

정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있는 메서드

```javascript
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
  }

  // 정적 메서드
  static sayHi() {
    console.log("Hi!");
  }
}
```

- 클래스에서는 메서드에 static 키워드를 붙이면 정적 메서드(클래스 메서드)가 됨

### 25.5.4 정적 메서드와 프로토타입 메서드의 차이

1. 정적 메서드와 프로토타입 베서드는 자신이 속해 있는 프로토타입 체인이 다름
2. 정적 메서드는 클래스로 호출, 프로토타입 메서드는 인스턴스로 호출
3. 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있음

```javascript
class Square {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  // 프로토타입 메서드
  area() {
    return this.width * this.height;
  }
}

const square = new Square(10, 10);
console.log(square.area()); // 100
```

- 정적 메서드는 클래스로 호출해야 하므로 정적 메서드 내부의 this는 인스턴스가 아닌 클래스를 가리킴
- 즉, 프로토타입 메서드와 정적 메서드 내부의 this 바인딩이 다름
- 따라서 메서드 내부에서 인스턴스 프로퍼티를 참조할 필요가 있다면 this를 사용해야 하며, 이러한 경우 프로토타입 메서드로 정의해아 함
- 하지만 메서드 내부에서 인스턴스 프로퍼티를 참조해야 할 필요가 없다면 this를 사용하지 않게 됨

## 25.6 클래스의 인스턴스 생성 과정

1. 인스턴스 생성과 this 바인딩
2. 인스턴스 초기화
3. 인스턴스 반환

## 25.7 프로퍼티

### 25.7.1 인스턴스 프로퍼티

constructoro 내부 토드가 실행되기 이전에 constructor 내부의 this에는 이미 클래스가 암묵적으로 생성한 인스턴스인 빈 개체가 바인딩 되어 있음

### 25.7.2 접근자 프로퍼티

```javascript
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  // fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
  // getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }

  // setter 함수
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(" ");
  }
}

const me = new Person("Ungmo", "Lee");

// 데이터 프로퍼티를 통한 프로퍼티 값의 참조.
console.log(`${me.firstName} ${me.lastName}`); // Ungmo Lee

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
me.fullName = "Heegun Lee";
console.log(me); // {firstName: "Heegun", lastName: "Lee"}

// 접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
console.log(me.fullName); // Heegun Lee

// fullName은 접근자 프로퍼티다.
// 접근자 프로퍼티는 get, set, enumerable, configurable 프로퍼티 어트리뷰트를 갖는다.
console.log(Object.getOwnPropertyDescriptor(Person.prototype, "fullName"));
// {get: ƒ, set: ƒ, enumerable: false, configurable: true}
```

접근자 프로퍼티는 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수, 즉 getter 함수와 setter 함수로 구성

### 25.7.3 클래스 필드 정의 제안

클래스 필드는 클래스 기반 객체지향 언어에서 클래스가 생성할 인스턴스의 프로퍼티를 가리키는 용어

```javascript
class Person {
  // 클래스 필드 정의
  name = "Lee";
}

const me = new Person();
console.log(me); // Person {name: "Lee"}
```

- 클래스 몸체에서 클래스 필드를 정의하는 경우 this에 클래스 필드를 바인딩해서는 안 됨
- this는 클래스의 constructor와 메서드 내에서만 유효

```javascript
class Person {
  // this에 클래스 필드를 바인딩해서는 안된다.
  this.name = ''; // SyntaxError: Unexpected token '.'
}
```

- 클래스 필드를 참조하는 경우 this를 반드시 사용해야 함

```javascript
class Person {
  // 클래스 필드
  name = "Lee";

  constructor() {
    console.log(name); // ReferenceError: name is not defined
  }
}

new Person();
```

- 클래스 필드에 초기값을 할당하지 않으면 undefined를 갖음

```javascript
class Person {
  // 클래스 필드를 초기화하지 않으면 undefined를 갖는다.
  name;
}

const me = new Person();
console.log(me); // Person {name: undefined}
```

- 인스턴스를 생성할 때 외부의 초기값으로 클래스 필드를 초기화해야 할 필요가 있다면 constructor에서 클래스 필드를 초기화해야 함

```javascript
class Person {
  // 클래스 필드에 문자열을 할당
  name = "Lee";

  // 클래스 필드에 함수를 할당
  getName = function () {
    return this.name;
  };
  // 화살표 함수로 정의할 수도 있다.
  // getName = () => this.name;
}

const me = new Person();
console.log(me); // Person {name: "Lee", getName: ƒ}
console.log(me.getName()); // Lee
```

- 클래스 필드에 함수를 할당하는 경우, 이 함수는 프로토타입 메서드가 아닌 인스턴스 메서드가 됨
- 모든 클래스 필드는 인스턴스 프로퍼티가 되기 때문
- 따라서 클래스 필드에 함수를 할당하는 것은 권장하지 않음

### 25.7.4 private 필드 정의 제안

```javascript
class Person {
  // private 필드 정의
  #name = "";

  constructor(name) {
    // private 필드 참조
    this.#name = name;
  }
}

const me = new Person("Lee");

// private 필드 #name은 클래스 외부에서 참조할 수 없다.
console.log(me.#name);
// SyntaxError: Private field '#name' must be declared in an enclosing class
```

- private 필드의 선두에는 #을 붙임
- private 필드를 참조할 때도 #을 붙임

```javascript
class Person {
  constructor(name) {
    // private 필드는 클래스 몸체에서 정의해야 한다.
    this.#name = name;
    // SyntaxError: Private field '#name' must be declared in an enclosing class
  }
}
```

- private 필드는 반드시 클래스 몸체에 정의
- private 필드를 직접 constructor에 정의하면 에러 발생

## 25.8 상속에 의한 클래스 확장

### 25.8.1 클래스 상속과 생성자 함수 상속

상속에 의한 클래스 확장은 기존 클래스를 상속받아 새로운 클래스를 확장하여 정의하는 것

### 25.8.2 extends 키워드

상속을 통해 클래스를 확장하려면 extends 키워드를 사용하여 상속받을 클래스를 정의

```javascript
// 수퍼(베이스/부모)클래스
class Base {}

// 서브(파생/자식)클래스
class Derived extends Base {}
```

- 상속을 통해 확장된 클래스: 서브클래스(파생 클래스, 자식 클래스)
- 서브클래스에 상속된 클래스: 수퍼클래스(베이스 클래스, 부모 클래스)

## 25.8.3 동적 상속

extend키워드는 클래스뿐만 아니라 생성자 함수를 상속받아 클래스를 확장할 수도 있음

단, extends 키워드 앞에는 반드시 클래스가 와야 함

```javascript
function Base1() {}

class Base2 {}

let condition = true;

// 조건에 따라 동적으로 상속 대상을 결정하는 서브클래스
class Derived extends (condition ? Base1 : Base2) {}

const derived = new Derived();
console.log(derived); // Derived {}

console.log(derived instanceof Base1); // true
console.log(derived instanceof Base2); // false
```

- extends 키워드 다음에는 클래스뿐만이 아니라 [[Construct]] 내부 메서드를 갖는 함수 객체로 평가될 수 있는 모든 표현식 사용 가능
- 이를 통해 동적으로 상속받을 대상을 결정할 수 있음

### 25.8.4 서브클래스의 constructor

클래스에서 constructor를 생략하면 클래스에 다음과 같이 비어있는 constructor가 암묵적으로 정의

```javascript
// 수퍼클래스
class Base {}

// 서브클래스
class Derived extends Base {}
```

- 수퍼클래스와 서브클래스 모두 constructor를 생략

```javascript
// 수퍼클래스
class Base {
  constructor() {}
}

// 서브클래스
class Derived extends Base {
  constructor() {
    super();
  }
}

const derived = new Derived();
console.log(derived); // Derived {}
```

- 위 예제와 같이 클래스에는 다음과 같이 암묵적으로 constructor가 정의

### 25.8.5 super 키워드

**super를 호출하면 수퍼클래스의 constructor를 호출**

```javascript
// 수퍼클래스
class Base {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
}

// 서브클래스
class Derived extends Base {
  // 다음과 같이 암묵적으로 constructor가 정의된다.
  // constructor(...args) { super(...args); }
}

const derived = new Derived(1, 2);
console.log(derived); // Derived {a: 1, b: 2}
```

- 수퍼클래스에서 추가한 프로퍼티와 서브클래스에서 추가한 프로퍼티를 갖는 인스턴스를 생성한다면 서브클래스의 constructor를 생략할 수 없음
- 이 때 연산자와 함 께 서브클래스를 호출하면서 전달한 인수 중에서 수퍼클래스의 constructor에 전달할 필요가 있는 인수는 서브클래스의 constructor에서 호출하는 super를 통해 전달

```javascript
// 수퍼클래스
class Base {
  constructor(a, b) {
    // ④
    this.a = a;
    this.b = b;
  }
}

// 서브클래스
class Derived extends Base {
  constructor(a, b, c) {
    // ②
    super(a, b); // ③
    this.c = c;
  }
}

const derived = new Derived(1, 2, 3); // ①
console.log(derived); // Derived {a: 1, b: 2, c: 3}
```

- new 연산자와 함꼐 Derived 클래스를 호출(①)
- 전달한 인수 1, 2, 3은 Derived 클래스의 contructor(②)에 전달
- super 호출(③)
- Base 클래스의 constructor(④)에 일부가 전달

super 호출 시 주의 사항

1. 서브클래스에서 constructor를 생략하지 않는 경우 constructor에서는 반드시 super를 호출해야 함
2. 서브클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없음
3. super는 반드시 서브클래스의 consturctor에서만 호출

**super를 참조하면 수퍼클래스의 메서드 호출**

1. 서브클래스의프로포타입 메서드 내에서 super.sayHi는 수퍼클래스의 프로토타입 메서드 sayHi를 가리킴

```javascript
// 수퍼클래스
class Base {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    return `Hi! ${this.name}`;
  }
}

// 서브클래스
class Derived extends Base {
  sayHi() {
    // super.sayHi는 수퍼클래스의 프로토타입 메서드를 가리킨다.
    return `${super.sayHi()}. how are you doing?`;
  }
}

const derived = new Derived("Lee");
console.log(derived.sayHi()); // Hi! Lee. how are you doing?
```

```javascript
// 수퍼클래스
class Base {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    return `Hi! ${this.name}`;
  }
}

class Derived extends Base {
  sayHi() {
    // __super는 Base.prototype을 가리킨다.
    const __super = Object.getPrototypeOf(Derived.prototype);
    return `${__super.sayHi.call(this)} how are you doing?`;
  }
}
```

- super 참조를 통해 수퍼클래스의 메서드를 참조하려면 super가 수퍼클래스의 메서드가 바인딩 된 객체, 즉 수퍼클래스의 prototype 프로퍼티에 바인딩된 프로토타입을 참조할 수 있어야 함

2. 서브클래스의 정적 메서드 내에서 super.sayHi는 수퍼클래스의 정적 메서드 sayHi를 가리킴

```javascript
// 수퍼클래스
class Base {
  static sayHi() {
    return "Hi!";
  }
}

// 서브클래스
class Derived extends Base {
  static sayHi() {
    // super.sayHi는 수퍼클래스의 정적 메서드를 가리킨다.
    return `${super.sayHi()} how are you doing?`;
  }
}

console.log(Derived.sayHi()); // Hi! how are you doing?
```

### 25.8.6 상속 클래스의 인스턴스 생성 과정

1. 서브클래스의 super 호출

- 서브클래스는 자신이 직접 인스턴스를 생성하지 않고 수퍼클래스에게 인스턴스 생성을 위임
- 서브클래스의 constructor에서 반드시 super를 호출해야 하는 이유

2. 수퍼클래스의 인스턴스 생성과 this 바인딩

```javascript
// 수퍼클래스
class Rectangle {
  constructor(width, height) {
    // 암묵적으로 빈 객체, 즉 인스턴스가 생성되고 this에 바인딩된다.
    console.log(this); // ColorRectangle {}
    // new 연산자와 함께 호출된 함수, 즉 new.target은 ColorRectangle이다.
    console.log(new.target); // ColorRectangle
...
```

- 인스턴스는 new.target이 가리키는 서브클래스가 생성한 것으로 처리

3. 수퍼클래스의 인스턴스 초기화

- 수퍼클래스의 constructor가 실행되어 this에 바인딩 되어있는 인스턴스 초기화

4. 서브클래스 constuctor로의 복귀와 this 바인딩

- super가 반환한 인스턴스가 rhis에 바인딩
- 서브클래스는 별도의 인스턴스를 생성하지 않고 super가 반환한 인스턴스를 this에 바인딩하여 그대로 사용

```javascript
// 서브클래스
class ColorRectangle extends Rectangle {
  constructor(width, height, color) {
    super(width, height);

    // super가 반환한 인스턴스가 this에 바인딩된다.
    console.log(this); // ColorRectangle {width: 2, height: 4}
...
```

- 이처럼 super가 호출되지 않으면 인스턴스가 생성되지 않으며, this 바인딩도 할 수 없음
- 서브클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없는 이유

5. 서브클래스의 인스턴스 초기화

- 서브클래스의 constructor에 기술되어 있는 인스턴스 초기화가 실행

6. 인스턴스 반환

- 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환

## 🤔궁금한 점

## 📌중요한 점
