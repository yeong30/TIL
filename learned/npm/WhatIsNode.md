## Node.js와 프론트엔드

node.js는 백엔드를 위한 기술이라고 생각하지만 사실 프론트엔드 개발에도 node.js가 필요하다.

node.js를 사용한다면

1. 최신 스펙으로 개발할 수 있다.
   js의 발전 속도에 비해 브라우저환경의 지원속도는 늘 뒤쳐진다. 이럴때, 바벨과 같은 노드로 기술로 만들어진 도구를 통해 적절한 개발 환경을 갖출 수 있다.

2. 빌드 자동화
   코드를 압축하고, 난독화하는 등 개발 이외의 작업을 node를 통해 진행할 수 있다.
3. 개발환경 커스터마이징
   각 프레임워크에서 제공하는 도구(CRA)를 사용하면 쉽게 개발환경을 구축할 수 있지만 때로는 직접 구축할 필요가 있으며 커스터마이징이 필요한 경우가 있다.

## NPM

- node를 설치하면 node pacakge manger인 npm을 사용할 수 있다.
- npm을 이용해 여러 명령어를 실행할 수 있다.
- npm은 어떻게 패키지를 관리할까?

## 외부 라이브러리를 관리하는 방법

1.  cdn 사용
    - 서버 장애가 발생시 라이브러리를 불러오지 못함
2.  직접 다운로드 받아 사용
    - 서버에 장애가 발생하더라도 이미 다운로드 받은 라이브러리는 영향받지않음.
    - 단, 업데이트가 필요할때 수동 업데이트가 필요하며 버전 호환성 확인 필요
3.  NPM으로 의존성 관리
    - npm install 명령어를 통해 라이브러리를 쉽게 추가
    - 유의적 버전으로 버전을 관리

## 유의적 버전

- 패키지 버전을 관리할 때 매우 엄격하게 제한한다면 프로젝트의 버전을 올리는데 어려움을 겪을 수 있다.
- 반면 버전을 너무 느슨하게 풀어놓는다면 오히려 여러 버전별로 코드를 관리해야하는 어려움이 발생할 수 있다.
- 적절한 버전 번호를 관리하기 위한 규칙이 필요한데 이를 유의적버전이라고 한다.
- 그 중 틸드(~)와 캐럿(^)을 이용해 범위를 명시한다.

### 틸드(~)

- 틸드는 마이너 버전이 명시되어 있으면 패치버전을 변경한다.
- 예를들어, ~1.2.3으로 표기되어있다면 1.2.3<= version <1.3.0의 버전을 포함한다.
- 단, ~0인 경우 0.0.0 <= version < 1.0.0 을 의미한다.

### 캐럿(^)

- 캐럿은 정식버전에서 마이너와 패치버전을 변경한다.
- 예를들어, ^1.2.3 으로 표기되어있다면 1.2.3<= version < 2.0.0의 버전을 포함한다.
- 단, ^0인 경우 0.0.0 <= version < 0.1.0 을 의미한다.
