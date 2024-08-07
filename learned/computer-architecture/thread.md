# 스레드

스레드란 프로세스를 구성하는 실행 흐름의 단위이다. 하나의 프로세스에는 한개 이상의 스레드가 존재하며 만약 하나의 프로세스가 여러개의 스레드로 실행된다면, 스레드 갯수만큼 여러개의 실행 흐름이 존재할 수 있으며 결국 프로세스의 각기 다른 부분을, 즉 여러 기능을 동시에 수행할 수 있다. 즉 스레드는 프로세스를 구성하는 실행흐름 단위이기 때문에 스레드가 여러개 있다면 프로세스를 이루고 있는 여러개의 명령어들을 동시에 실행할 수 있다.

예를들어 텍스트 편집기 프로세스를 여러개의 스레드로 실행한다면 하나의 스레드는 자동저장, 하나의 스레드는 입력, 또다른 다른 스레드는 출력을 받는 등 여러가지 기능을 동시에 실행할 수 있다.
이렇게 실행흐름이 여러개인 프로세스를 멀티 스레드 프로세스라고 한다.

## 스레드의 구성요소

스레드는

1. 스레드 ID : 하나의 프로세스 안에서 스레드를 식별할 수 있는 스레드 고유 아이디이다.
2. 프로그램 카운터를 비롯한 레지스터값
3. 스택
   등 실행에 필요한 최소한의 정보로 구성된다.
   각 값들은 해당 영역에서 스레드마다 분리되어 저장된다. (ex: 스택영역에 스레드1의 스택, 스레드2의 스택…이 존재, 코드영역에 스레드1의 프로그램카운터, 스레드2의 프로그램카운터등이 각각 다른 값을 가리키고 있음)

중요한 것은 프로세스를 이루는 스레드들은 프로세스 자원을 공유하며 실행된다는 것이다. 스레드1만의 코드영역, 스레드2만의 힙영역이 존재하는 것이 아닌 하나의 프로세스의 힙영역, 코드영역등에 각각 스레드들이 영역을 구분하여 저장된다.
만약 프로세스가 특정 파일에 접근한다면 모든 스레드들은 그 파일에 접근할 수 있게 된다. 자원을 공유하기 때문이다.

## 멀티 스레드와 멀티 프로세스

동일한 작업을 단일 스레드로 여러개 실행하는 것과 하나의 프로세스내의 멀티스레드로 여러개 실행하는것의 차이점은 무엇일까
가장 큰 차이점은 프로세스끼리는 자원을 공유하지 않지만 스레드끼리는 같은 프로세스끼리 자원을 공유한다는 점이다.
단일 프로세스로 여러개의 프로세스를 실행한다면 동일한 기능을 수행한다고 하여도, 각각의 프로세스는 각자의 메모리영역을 차지하게 된다.(예외 : 쓰기 식 복사)
반면 스레드들은 반드시 식별되어야 할 값들을 제외하고(스택, 레지스터값, 스레드ID등) 프로세스가 가지는 값을 공유한다.

정리하자면, 프로세스끼리는 자원을 공유하지않고 독립적으로 실행되며 스레드는 프로세스의 자원을 공유한다.
이러한 멀티 스레드는 협력과 통신에 유리하지만 프로세스에 장애가 생기면 모든 스레드가 실행되지못하는 단점이 있다.

- IPC: 일반적으로 프로세스 간 자원을 공유하지 않지만 프로세스 간 통신(IPC)이 존재한다. 같은 파일을 읽음으로서 파일을 통한 프로세스 간 통신, 공유 메모리영역을 통한 프로세스 간 통신이 이루어진다.
