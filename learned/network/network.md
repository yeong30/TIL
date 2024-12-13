## 컴퓨터 네트워크란?

컴퓨터 네트워크란 여러 개의 장치가 마치 그물(net)처럼 연결되어 정보를 주고 받을 수 있는 통신망.
통신망은 노드와 간선으로 이루어진 그래프 형태이다.

하나의 네트워크는 범위에 따라 여러개의 네트워크로 이루어 질 수 있고,이렇게 각기 다른 네트워크는 네트워크를 이룬다. (=여러 네트워크가 그물처럼 연결되어~~)이와 관련된 용어로 `인터넷`이 있다.

### 인터넷이란?

네트워크의 네트워크.
네트워크 안에 장치들은 히나의 네트워크 안에서 정보를 주고 받을 수 있꼬 네트워크 간에도 정보를 주고 받을 수 있다.

## 네트워크를 알아야 하는 이유?

대부분의 프로그램에는 네트워크가 활용되머, 프로그램을 만드는 개발자는 필수적으로 이해해야한다.

## 네트워크의 기본 구조

네트워크의 기본 구조는 그래프 형태이다.<br>
그리고 그래프란 노드(edge)와 간선(link)으로 이루어진 자료구조이다.

네트워크의 각 장치(컴퓨터, 네트워크 장비)들은 노드, 그리고 이를 연결하는 유무선은 간선인 것이다.<br>
주로 가장자리에는 우리가 사용하는 컴퓨터와 같은 기기, 중간에는 이 기기들을 연결해주는 장비들이 위치한다.

그리고,가장자리에 위치한 노드는 `호스트`, 중간노드에 위치한 노드들은 `네트워크 장비`, 그리고 노드들을 연결해주는 유무선의 연결매체는 `통신 매체`, 노드들끼리 주고받는 정보는 `메시지` 라고한다.

### 호스트

네트워크상에서 주고받는 메시지를 최초 생성하거나 최종 수신받는 대상. 일반적으로 가장자리에 위치한다.

그리고 이러한 호스트는 역할에 따라 클라이언트와 서버로 구분된다.<br>
클라이언트는 요청을 보내는 호스트, 서버는 요청에 대한 응답을 하는 호스트이다.

### 네트워크 장비

호스트간 주고받는 정보가 거치는 중간 노드로서, 정보가 수신지까지 안정적이고 안전하게 전송되도록 돕는 대상.<br>
이더넷 허브, 스위치, 라우터, 공유기등이 해당한다.

### 호스트와 네트워크의 역할?

각 장비들과 호스트를 나눈것은 역할에 따라 나눈것일 뿐 완전히 배타적인 개념은 아니다.<br>
하나의 컴퓨터는 호스트가 될 수 있고 동시에 네트워크 장비로서 사용될 수 있다.
또한 하나의 컴퓨터가 서버가 될 수 있고 클라이언트가 될 수 있다.

### 통신 매체

각 노드들을 연결하는 간선을 의미한다.

### 메시지

통신 매체로 연결된 노드들이 주고받는 정보이다.<br>
다양한 형태의 메시지(ex 웹 페이지, 파일, 메일등)이 존재한다.