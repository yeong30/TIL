# 프로토타입

자바스크립트는 명령형, 함수형, 프로토타입 기반 객체지향을 지원하는 멀티 패러다임 프로그래밍 언어이다. 자바스크립트는 클래스가 아닌 프로토타입을 기반으로 객체지향 모델을 제공한다. (ES6에 클래스가 도입되었지만 기존 프로토 타입 기반 패턴의 문법적 설탕으로 볼 수 있다.)

> 객체지향 프로그래밍 이란?  
> 객체지향 프로그래밍이란 실세계의 사물을 인식하는 철학적 사고를 프로그래밍에 접목한 것으로 프로그램을 명령어, 함수의 집합으로 바라보는 명령형 프로그래밍에서 벗어나 여러개의 독립적 단위인 객체의 집합으로 바라보는 프로그래밍 패러다임이다.
> 여기서 객체는 서로를 구별할 수 있는 속성으로 구성한 복합적인 자료구조이다. 객체는 상태를 나타내는 프로퍼티와 프로퍼티를 조작할 수 있는 동작, 메서드를 하나의 논리적인 단위로 묶은 복합적인 자료구조이다.

### 상속과 프로토타입

상속은 객체지향 프로그래밍의 핵심개념으로 특정 객체의 프로퍼티와 메서드를 다른 객체가 물려받아 그대로 사용할 수 있는 것을 의미한다.
상속을 사용하면 불필요한 중복을 제거할 수 있다.

**자바스크립트는 프로토타입을 기반으로 상속을 구현**한다.
**포르토타입이란 어떤 객체의 상위(부모) 역할을 하는 객체로서 다른 객체에 공유 프로퍼티(메서드)를 제공**한다. 프로토타입을 상속받은 하위(자식) 객체는 상위 객체의 프로퍼티와 메서드를 자신의 프로퍼티처럼 접근할 수 있다.

모든 객체는 [[prototype]] 이라는 내부 슬롯을 가지며 이 값에 자신의 프로토타입을 참조한다. 객체가 생성될 때 해당 객체의 포로토타입이 결정되고 그 참조가 [[ptotoype]]에 저장된다.
예를 들어, 객체리터럴 방식으로 생성한 객체의 프로토타입은 Object.prototype이 되고
생성자함수로 생성된 객체의 프로토타입은 생성자함수의 prototype에 바인딩되어 있는 객체이다. 모든 객체는 하나의 프로토타입을 가지며 프로토타입은 생성자 함수와 연결되어있다.
_(여기서 prototype 속성은 위 [[prototype]]과 관계없는 속성 키 이름이다)_

### 프로토 타입에 접근하기

하위 객체, 즉 자식객체는 자신의 [[prototype]]에 직접 접근할 수 없지만 [객체명].**protoype** 접근자 프로퍼티를 통해 간접적으로 접근할 수 있다. 접근자**proto**에 접근할 때는 함수 getter, setter를 통해 값이 호출되고 할당된다.
(+ 자바스크립트는 원칙적으로 내부슬롯에 접근할 수 있는 방법을 제공하지않으나 일부 내부 슬롯과 메서드만 간접적으로 접근할 수 있는 수단을 제공한다)

Person을 상속받아 James 객체 생성.  
-> James의 프로토타입은 Person.prototype.  
-> Person.prototype의 접근자 프로퍼티. -> James**proto**

###**proto** 접근자 프로퍼티는 상속을 통해 사용된다.

**proto** 으로 프로토타입에 접근함으로서,**proto**가 자체 프로퍼티처럼 느껴지지만 그건 아니며**proto** 는 상위 객체의 prototype의 프로퍼티이다.
즉 [상위객체].protoype.**proto** 이다.

```javascript
function Student() {
  this.job = "student";
}
Student.prototype.sayHello = function () {
  console.log(`Hi, My name is ${this.name}`);
};

const sarah = new Student();

sarah.name = "Sarah";

console.log(sarah.hasOwnProperty("job")); //true
console.log(sarah.hasOwnProperty("sayHello")); //false
console.log(sarah.hasOwnProperty("__proto__")); //false
```

## 프로토타입 체인

이렇게 모든 객체는 프로토타입을 통해 상위 -하위의 계층 구조를 가지게 된다.  
자바스크립트는 객체의 특정 프로퍼티에 접근하려할 때 해당 객체에 찾으려는 프로퍼티가 없을때 [[prototype]] 내부슬롯을 따라 상위 프로토타입에서 프로퍼티를 순차적으로 검색하게 되는데 이를 프로토타입 체인이라고 한다.  
Object.prototype은 모든 객체의 프로토타입 체인 최상위에 존재하며 프로토타입 체인의 종점이라고 불린다. Object.prototype의 [[prototype]] 은 null이다.

- _스코포 체인은 식별자 검색을 위한 매커니즘이라면 프로토타입 체인은 프프로퍼티 검색을 위한 메커니즘_

###**proto** 접근자 프로퍼티를 사용하는 이유

본인의 프로토타입에 접근 할 때**proto** 라는 접근자 프로퍼티를 사용하는 이유는 상호 참조를 방지하기 위해서다.
만약 A.**proto** = B, B.**proto** = A를 할당 시 서로가 자신의 프로토타입이 되는 비정상적인 프로토타입 체인이 형성된다 .따라서 접근자 프로퍼티를 사용하여 체크 후 프로토타입을 교체하도록 구현한 것이다.

**proto** 는 es6에서 지원되지만**proto** 를 직접사용하는 것은 권장하지 않는다. 일부 객체는 프로토타입을 참조하지않는 경우가 있기때문에**proto** 를 사용할 수 없을 수 있다.
**proto** 대신 Object.getPrototypeOf(대상객체) / Object.setPrototypeOf를 사용할 수 있다.

### 함수 객체의 prototype 프로퍼티

함수 객체는 일반객체와 달리 prototype 프로퍼티를 갖게되는데 이는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다. 즉 해당 함수로 생성될 객체의 포로토타입을 가리키며 생성자 함수로 작동할 수 없는 화살표 함수, 축약표현 메서드는는 prototype 프로퍼티가 존재하지 않는다.
함수 객체의 prototype 프로퍼티는 함수가 평가,정의 되어 함수 객체를 생성하는 시점에 생성된다.
또한 이렇게 생성된 prototype 객체의 프로토타입은 언제나 Object.prototype이다.

모든 프로토타입은 contructor 프로퍼티를 갖는데 이 contructor프로퍼티는 자신을 참고하고 있는 생성자 함수를 가리킨다. 결국 해당 프로토타입을 상속받은 모든 객체도 contructor 프로퍼티를 갖게되므로, 생성자 함수로 생성된 모든 객체의 contrucotr가 있으며 그 contructor는 생성자 함수를 가리키게 된다

참고
객체리터럴로 생성한 객체도 Object 생성자 함수와 연결된다. 실제로 내부도 객체리터럴이 Object 생성자 함수를 사용하는 것은 아니고 모든 프토로타입과 생성자 함수는 쌍으로 존재해야하므로, 객체 리터럴로 선언한 객체도 가상적인 생성자 함수가 필요하기 때문에 그냥 그렇게 쓴다…

### 프로토타입 체인

자바스크립트는 객체의 프로퍼티에 접근하고자 할때 해당 객체에 찾으려는 프로퍼티가 없을 때, [[prototype]] 내부슬롯 참조를 따라 자신의 부모 역할을 하는 프로토타입에서 다시 프로퍼티를 순차적으로 검색한다. 이를 프로토타입 체인이라고 한다.
스코프체인이 식별자 검색을 위한 메커니즘이라면 프로토타입 체인은 프로퍼티 검색을 위한 메커니즘이다.

프로토 타입의 종점은 언제나 Object.prototype이다. Object.prototype은 null을 반환하며 프로토타입 최상단에서도 검색할 수 없는 경우 undefined를 반환한다.

### 오버라이딩과 프로퍼티 셰도잉

프로토타입이 소유한 프로퍼티와 동일한 이름의 프로퍼티를 인스턴트(생성된 자식 객체)에 추가하면 프로포타입 프로퍼티가 덮어씌워지진 않고 인스턴스의 프로퍼티로 추가된다. 즉 오버라이딩 된다. 이렇게 상속관계에 의해 프로퍼티가 가려지는 현상을 프로퍼티 셰도잉이라고 한다.

### 프로토타입 교체

객체의 프로토타입을 교체하는것도 가능하다. 생성자 함수의 prototype을 변경하거나 **protot** 접근자 프로퍼티를 통해 교체할 수 있다.  
단, 생성자 함수의 prototype을 변경하는 것은 미래의 생성될 인스턴스의 프로토타입을 교체하는 것이고**proto** 접근자 프로퍼티를 이용하는 것은 이미 생성된 객체의 프로토타입을 교체하는것이다.(기존 프로토타입과 연결이 끊어짐)

### instanceof 연산자

instanceof 연산자는 이항 연산자로서 좌변에 객체, 우변에 생성자 함수를 피연산자로 사용한다. 만약 우변의 생성자 함수의 prototype에 바인딩된 객체가 좌변 객체의 프로토타입 체인상에 존재하면 true, 없다면 false를 반환한다.

### 정적 프로퍼티와 메서드

정적 프로퍼티와 메서드는 생성자함수로 인스턴스트를 생성하지 않아도 접근가능한 함수 자체의 프로퍼티와 메서드를 말한다.
정적 프로퍼티/메서드는 프로토타입 체인상에 존재하지 않기때문에 인스턴스로 접근이 불가능하다.
생성자 함수의 메서드는 정적 메서드, 생성자 함수의 prototype 속성의 메서드는 프로토타입 체인 상 메서드가 된다

### 프로토타입 열거

객체의 모든 프로퍼티를 열거하고 싶다면 for…in 문을 사용한다.
주의할 것은 for…in의 열거대상은 순회 대상 객체 자체의 프로퍼티 뿐만 아니라 상속받은 프로퍼티까지 열거하여 순회한다. 즉 객체의 프로토타입 체인 상 존재하는 모든 프로퍼티 중 [[Enumerable]]가 false인 프로퍼티를 제외하고 모든 프로퍼티를 순회하며 열거 한다.

만약 순회하고 싶지않은 프로퍼티는 프로퍼티의 어트리뷰트 [[Enumerable]]를 false로 설정한다. (toString과 가은 속성은 이미 [[Enumerable]] 이 false이기때문에 열거되지않는다)  
또한 상속받은 프로퍼티가 아닌 객체 고유의 프로퍼티만 순회하려면 Object.ptototype.hasOwnProperty를 활용하거나 Object.keys등을 사용한다.
