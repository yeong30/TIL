# Compound Component Pattern

- Compound Component Pattern(합성 컴포넌트)는 자식 컴포넌트들이 부모 컴포넌트 내부에서 상태를 공유하면서 비지니스 로직과 사용자 인터페이스와 관련된 부분을 구분하는 React 패턴이다.
  각각의 역할을 하는 작은 컴포넌트로 조립하여 큰 컴포넌트를 만드는 방식이다.

- 하나의 컴포넌트 안에 수많은 props를 전달하지 않고 서브 컴포넌트에 적절히 분배하여 관심사를 분리할 수 있다는 장점이 있다.

- 합성컴포넌트는 Context API를 사용한 방법과 React.Children.map을 사용한 방법으로 구현이 가능하다.

### 1. React.Children.map활용

- 컴포넌트 최상단 컴포넌트 내부에서 React.cloneElement를 사용하여 자식 컴포넌트를 복제하여 props로 상태와 필요 props를 전달하는 방식.
  내부에서 map을 사용하기 때문에, 자식 컴포넌트를 약속된 형태로 넘겨야 하는 제약이 있다.

### 2. Context API 활용

- 각각의 작은 컴포넌트에서 공통적으로 필요한 상태를 관리하는 Context Provider를 컴포넌트를 최상단에 위치 시킴으로서, 내부의 children들이 공유받도록 하고 그렇지 않은 값은 각각의 자식 컴포넌트가 Props로 받아서 처리하도록 하는 방식.

참조

[[KAKAO 기술블로그] - 합성 컴포넌트로 재사용성 극대화하기](https://fe-developers.kakaoent.com/2022/220731-composition-component/)

[디자인 시스템에 Compound Component Pattern 적용해보기](https://iyu88.github.io//react/2023/03/25/react-compound-component-pattern.html)

[patterns.dev - compound pattern](https://www.patterns.dev/react/compound-pattern)
