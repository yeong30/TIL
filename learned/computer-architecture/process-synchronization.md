# 프로세스

동시다발적으로 실행되는 프로세스들은 서로 협력하며 영향을 주고받는데, 이 과정에서 지원의 일관성을 보장해야한다. (쓰레드 포함) 즉 프로세스들을 동기화해야한다.

## 동기화란?

각기 다른 프로세스들은 공동의 목적을 위해 협력해서 수행될 수 있다.
그러나 프로세스를 아무렇게나 실행하면 안되며 올바른 수행을 위해 서로 동기화되어야한다.

**동기화란 사전적으로 수행시기를 맞추는것을 의미한다.** 명확하게는 실행순서제어를 위한 동기화, 상호배제를 위한 동기화 두가지로 구분할 수 있다.
실행순서는 프로세스를 올바른 순서대로 실행하는 것이고, 상호배제는 동시에 접근해서는 안되는 자원에 하나의 프로세스만 접근하도록 하는 것이다.

실행의 문맥을 갖는 모든 대상은 동기화 대상이기때문에 프로세스외에 쓰레드 또한 동기화 대상이다.

## 실행 순서 제어를 위한 동기화

실행 순서 제어를 위한 동기화 예시문제로는 **`reader writer problem`**문제가 있다.
`writer` 프로세스와 `reader` 프로세스가 각각 존재할 때, `reader` 프로세스와 `writer` 프로세스는 아무렇게나 실행되어선 안된다. 두 프로세스 간에 실행의 순서가 있기 때문이다. 예를들어 `reader` 프로세스는 읽을 값이 있을때, 즉 작성된 값이 있다는 조건이 만족할 때 실행이 가능하다.

## 상호 배제를 위한 동기화

상호 배제를 위한 동기화는 공유가 불가능한 자원의 동시 사용을 피하기 위한 동기화를 의미한다.
상호 배제를 위한 동기화 예시문제로는 **Bank account problem**문제와 **Producer & Consumer problem**이 있다.
위 문제는 다음과 같다. 초기값이 0인 전역변수 X에 값을 1씩 더하는 생산자 함수와 1씩 차감하는 소비자 함수가 존재한다. 이 생산자 함수와 소비자 함수를 동시에 100000번 실행하면 그 결과 X는 0이 될 것이라 예상하지만 실제로는 랜덤하게 전혀 다른 값들이 된다. 그 이유는 동시에 접근해서는 안되는 자원 X에 동시에 접근하였기 때문이다. 즉 동기화가 되지 않았기 때문이다.

### 공유자원과 임계값

여러 프로세스나 스레드가 공유하는 자원을 공유자원이라고 하는데 전역변수, 파일, 입출력장치들이 이에 해당한다. 이러한 자원 중, 위 예시처럼 동시에 접근해서는 안되는 자원에 접근하는 코드를 임계 구역이라고 한다. 위 예시로는 X를 읽어들여 1을 더하고, 1을 빼고 다시 저장하는 코드들이 이에 해당하다.
따라서 임계구역은 동시에 두개이상의 프로세스가 실행할 경우 문제가 발생할 수 있다. 임계구역은 한번에 하나의 프로세스만 실행해야한다.

#### 레이스 컨디션

레이스 컨디션은 여러 프로세스나 스레드가 동시에 같은 자원에 접근하거나 조작할 때 발생할 수 있는 문제를 의미한다. 위 예시처럼 동시에 코드가 자원에 접근하는 순서에 따라 예상치 못한 결과가 발생할 경우 레이스 컨디션이 일어났다고 한다.

### 임계구역 문제를 해결하기 위한 원칙

자원의 일관성을 지키고 임계구역 문제를 해결하기 위해서는 세가지 원칙을 충족해야한다.

1. 상호 배제 : 임계구역에 한번에 하나의 프로스세스(스레드)만 진입할 수 있도록 보장하는 원칙
2. 진행 : 임계구역에 진입하려는 프로세스가 없을때, 진입을 원하는 프로세스가 공정하게 접근할 수 있도록 보장
3. 한정대기 : 임계구역 진입을 기다리는 프로세스가 무한히 대기하지 않도록 보장

## 동기화를 위한 기법들

동기화를 위한 기법들은 여러가지 존재한다.

### 뮤텍스

상호 배제를 위한 동기화 도구로서 뮤텍스는 자원을 사용할 때, 한번에 하나의 프로세스(스레드)만 접근할 수 있도록 하는 방법이다.
뮤텍스를 통해 공유 자원에 접근할 때는 반드시 `lock`을 걸어야 하고, 사용이 끝나면 `unlock`을 해제해야한다. 만약 다른 스레드가 같은 자원에 접근하려 할때 `lock`이 걸려있다면 `lock`이 풀릴 때 까지 대기하게 되어 자원의 일관성을 지킬 수 있다.

### 세마포어

세마포어는 뮤텍스와 유사하지만 정해진 수만큼, 다수의 프로세스가 동시에 접근할 수 있게 허용한다.
세마포어는 `wait`연산과 `signal`연산, 그리고 접근가능한 공유자원의 개수를 나타내는 전역변수 S를 사용한다. `wait`연산으로 S의 값을 감소시키고 `signal`연산으로 S의 값을 증가시킨다. S의값이 0일때는 프로세스들은 대기하고 signal으로 자원이 해제되면 대기중인 프로세스가 접근할 수 있다.

세마포어는 상호 배제 외에도 실행 순서제어를 위한 도구로서 사용될 수 있다.

#### Busy Waiting

임계구역에 진입하려는 프로세스가 여러개이고 현재 사용가능한 자원의 개수가 0일때, 프로세스는 사용할 수 있는 자원이 있는지 반복적으로 확인하며 대기하게 된다. 이처럼 프로세스(스레드)가 자원에 접근할 수 있거나 특정 조건이 충족될때까지 CPU를 사용하여 반복적으로 확인하며 대기하는 것을 `Busy Waiting`이라고 한다. `Busy Waiting`는 CPU 자원을 계속해서 소모하며 대기하때문에 CPU사이클을 낭비한다.

`Busy Waiting`을 피하기 위한 대안 사용할 수 있는 자원이 없을 경우 대기상태로 만들고(해당 프로세스의 PCB를 대기 큐에 삽입), 다시 사용할 수 있는 자원이 생겼을 때 대기중인 프로세스를 준비상태(대기 큐에서 PCB를 꺼내 준비큐에 삽입)로 만드는 방법이 있다.

### 모니터

모니터는 프로세스가 자원에 안전하게 접근할 수 있도록 하는 고급 동시성 제어 도구이다. 자원을 안전하게 접근하는 메서드를 모니터 내부에 두고 모니터에는 한번에 하나의 프로세스만 진입할 수 있도록 보장하는 방식이다.