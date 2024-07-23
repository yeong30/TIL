자바스크립트 객체

자바스크립트 객체의 종류는 크게 표준 빌트인 객체, 호스트 객체, 사용자 정의 객체로 분류할 수 있다.

## 표준 빌트인 객체란?

표준 빌트인 객체는 ECMAScript 사양에 정의된 객체로 애플리케이션 전역의 공통 기능을 제공한다.
빌트인 객체는 ECMAScript 사양에 포함된 객체이므로 브라우저/Node.js등 실행환경에 관계없이 사용할 수 있다.

## 호스트 객체

호스트 객체는 ECMAScript 사양에 정의되진 않았지만 자바스크립트 실행환경(브라우저 또는 Node.js)에서 추가적으로 제공하는 객체를 말한다. 브라우저의 경우 DOM,BOM, fetch… Node.js는 Node.js 고유의 API를 호스트객체로 제공한다.

## 사용자 정의 객체

사용자 정의 객체는 표준 빌트인, 호스트 객체를 제외한 객체로서 사용자가 직접 정의한 객체이다

## 표준 빌트인 객체

일반적으로 Object, String,Number ,Symbol, Date, Math , RegExp, Array, Map/Set, JSON,Error 등을 포함한 40여개의 표준 빌트인 객체가 존재한다.
Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체로 프로토타입 메서드와 정적메서드를 제공하고 생성자 함수 객체가 아닌 객체는 정적 메서드만 제공한다(ex Math.max..)

### 원시값과 래퍼객체

일반적으로 숫자나 문자를 선언할 경우 Number , String등 생성자 함수를 이용하기 보다 원시값으로 바로 초기화해서 사용한다. 그럼에도 생성자 함수가 존재하는 이유는 무엇일까
바로, 원시값의 래퍼객체로서 원시값도 빌트인 객체의 메서드를 사용할 수 있게해준다.
원시값에 대해 마치 객체처럼 마침표 표기법(.)으로 접근하면 자바스크립트 엔진은 일시적으로 원시값을 암묵적으로 연관된 객체로 변환해주고 변환된 객체로 프로퍼티에 접근하거나 메서드를 호출 후 다시 원시값으로 돌려놓는다.
이렇게 **원시값에 대해 객체처럼 접근할 때 생성되는 임시 객체를 래퍼 객체**라고 하며 표준 빌트인 객체 String, Number, Boolean등의 생성자함수의 프로퍼티와 메서드에 접근할 수 있다.

### 전역 객체

전역 객체는 코드가 실행되기 전 자바스크립트 엔진에 의해 가장 먼저 생성되는 특수한 객체로서 최상위 객체이다.
전역 객체는 자바스크립트 환경에 따라 지칭하는 이름이 모두 다르다.

- 브라우저 환경 -> window
- Node.js 환경 -> global
- 공통
- -> globalThis

#### 전역 객체의 특징

전역객체는 다음과 같은 특징을 갖는다.

1. 개발자가 의도적으로 생성할 수 없다.
2. 전역객체의 프로퍼티를 참조할 때 window(global)을 생략할 수 있다.
3. 모듈환경이 아닌 경우에서의 var 키워드로 선언한 전역변수와 선언하지 않는 변수에 값을 할당하는 암묵적 전역, 그리고 전역함수는 전역객체의 프로퍼티가 된다.
4. 브라우저환경의 모든 자바스크립트 코드는 하나의 전역 객체 window를 공유한다, 여러개의 스크립트로 분리해도 하나의 전역객체를 공유하게 된다.