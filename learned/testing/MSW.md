# Mock Service Worker(MSW)

- 브라우저 및 Node용 API모킹 라이브러리로 , 네트워크 요청을 가로채어 모의 응답을 대신 반환할 수 있다.

- service worker를 사용하여, 애플리케이션과 서버 사이에서 요청을 가로채어 응답을 생성할 수 있다.

- 핸들러, 서버 생성한 뒤, 서버가 계속해서 요청을 리스닝하도록 설정하여 네트워크 요청을 가로채는 방식이다.

- 간단한 앱에서는 Jest mocking을 사용할 수 있지만 더 복잡한 앱에서는 MSW로 더 다양한 도구를 이용할 수 있다.

### hanlder

- handler는 인터셉트할 요청과 처리 방식을 설명하는 함수이다.
- 서버에서 정의한 라우트 핸들러와 유사한 역할을 하며 유사하게 작동한다.
- handler는 각각 Request namespace, url, method, Response resolver로 구성된다.

```
Request namespace: 요청 핸들러의 타입으로 https와 graphql이 표준으로 제공된다.
method: request의 method 타입
url : 앱에서 외부로 나가는 요청이 향하는 곳. 즉 가로챌 request  url
Response resolver : 가로챈 요청을 어떻게 처리할 지를 제어하는 기능이다.
```

---

### MSW 설정

1. 서버를 생성한다
2. 생성된 서버 객체로 setupServer 메서드를 실행한다.
3. 테스팅 라이브러리와 함께 사용할 경우, 테스트 중 서버가 구동되도록 설정한다.

참고

[MSW Introduction](https://mswjs.io/docs/)
