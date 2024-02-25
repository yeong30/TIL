# Testing Library Queries

- 쿼리는 페이지에서 요소를 찾기 위해 테스팅 라이브러리가 제공하는 방법이다.
- 쿼리는 유형별로 command , [All], queryType로 구성된다.

---

## command

- get : 요소가 DOM안에 있다고 예측한다.
- query : 요소가 DOM안에 없다고 예측한다.
- find : 요소가 비동기로 생성됨을 예측한다.

## ALL

- exclude :매치되는 요소가 1개 임을 예측한다.
- include : 매치되는 요소가 1개 이상임을 예측한다.

### QueryType

- Role : 역할로서 요소를 찾는다. 일반적으로 가장 선호된다
- AltText : 이미지 요소를 찾을 때 사용한다.
- Text : 디스플레이된 요소를 찾는다.
- 그 외 PlaceholderText , LabelText...등이 존재한다.
