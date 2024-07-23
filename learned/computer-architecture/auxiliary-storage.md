# 보조기억장치

보조기억장치에는 대표적으로 하드디스크, 플래시 메모리등이 속한다.

## 하드디스크

- 자기적인 방식으로 데이터를 저장허는 보조기억장치이다. (자기기억장치의 일종으로도 불림)
- 하드디스크는 여러겹의 플래터(판떼기)와 스핀들, 디스크암, 헤드로 구성된다. **플래터**는 수많은 N극과 S극 자기적인 물질로 덮여있다. 플래터는 많은 용량의 저장을 하기위해 일반적으로 여러겹이고 양면을 모두 사용한다. 이러한 플래터를 스핀들이 회전시켜주는데 회전의 단위가 RPM(분당 회전수)이다.
  스핀들이 회전시켜준 플래터를 읽고 쓸 수 있는 수단을 **헤드** 라고한다. 헤드는 플래터와 아주 미세하게 간격이 있으며 자기물질을 읽는 구성요소이다. 플래터가 여러겹이듯이 헤드도 여러겹으로 플래터면마다 위치해있다
  이러한 헤드를 움직여주는 구성요소를 **디스크암**이라고한다. 일반적으로 모든 헤드가 디스크 암에 부착되어 함께 움직인다 (=여러겹의 헤드가 한번에 움직임)
  플래터에 데이터가 저장되는데, 이때 트랙과 섹터 단위로 데이터가 저장된다.
  트랙은 플래터를 이루고 있는 동심원을 그리는 단위이다.
  섹터는 트랙을 조각으로 나누었을 때 한 조각을 섹터라고 부른다. 하나 이상의 섹터를 묶어 블록이라고 표현하기도 한다.
  또한 여러겹의 플래터 상에서 같은 트랙이 위치한 곳을 모아 연결한 논리적 단위를 실린더라고한다. 연속된 정보는 한 실린더에 저장된다.(헤드는 디스크 암에 부착되어 다같이 움직이는데, 한 실린더에 기록하면 헤드를 움직이지 않아도 세로로 데이터를 읽어낼 수 잇기때문에 연속된 정보는 한 실린더에 저장된다)

### 하드디스크가 저장된 데이터에 접근하는 시간

하드디스크에 저장된 어던 값을 읽거나 쓸때 걸리는 시간은 3가지로 분류할 수 있다.

- 탐색시간(시크타임) : 접근하려는 데이터가 저장된 트랙까지 헤드를 이동시키는 시간
- 회전지역 :원하는 트랙까지 헤더를 위치시켰다면 헤더가 있는곳까지 플래터를 회전하는 시간
- 전송시간 : 하드디스크와 컴퓨터 간에 데이터를 실제로 전송하는 시간

## 플래시 메모리

- 전기적으로 데이터를 읽고 쓰는 반도체 기반 저장 장치
  SSD,SD카드, USB 모두 플래시 메모리 기반의 보조기억장치
  단, 플래시메모리는 범용성이 넓어 보조기억장치에만 속한다고 보기는 어려움

### 플래시 메모리의 종류

플래시 메모리는 NAND플래시 메모리와 NOR플래시 메모리가 있는데 이중 요즘에 대용량 저장장치로 많이 사용되는것은 NAND 플래시메모리이다.

### 플래시 메모리의 구성

셀은 플래시 메모리를 이루는 가장 작은 단위, 플래시 메모리에서 데이터를 저장하는 가장 작은 단위이다. 이 셀이 모여 MB, GB,TB가 된다.
하나의 셀에 1비트를 저장할 수 있는 플래시 메모리 (SLC), 하나에 셀에 2비트를 저장할 수 있는 플래시 메모리(MLC), 3비트(TLC), 4비트(QLC)가 있다. 플래시메모리의 성능, 가격, 수명을 결정한다
같은 플래시 메모리라도 내부 구성에 따라 수명, 가격, 성능이 다르다
같은 16GB USB여도 플래시 메모리 종류에 따라 수명, 가격, 성능이 다르다.

#### SLC

- 한 셀에 1비트를 저장. 한 셀로 두개의 정보 표현이 가능
- 비트의 빠른 입출력이 가능하고 긴 수명을 가진다.(플래시 메모리는 수명이 있다. )
- 단 용량 대비 가격이 높다
- 한집에 한명이사는 구조와 유사.

#### MLC

- 한 셀에 2비트를 저장하여 한 셀로 네 개의 정보 표현이 가능하다(= 대 용량화에 유리하다)
- SLC보다 느린 입출력과 짧은 수명을 가진다
- SLC보다 저렴하다
- 시중에서 많이 사용된다(MLC,TLC,QLC)
- 한 집에 두명이 사는 구조와 유사

#### TLC

- 한 셀에 3비트를 저장하여 한셀로 여덟배의 정보 표현이 가능
- MLC보다 느린 입출력과 짧은 수명
- MLC보다 저렴

### 플래시 메모리 저장단위

앞서 플래시 메모리를 이루는 가장 작은 단위는 셀 이라고 하였다. 이러한 셀들이 모여 페이지가 되고, 페이지들이 모여 블록이 되고, 블록이 모여 플레인, 플레인이 모여 다이가 된다.

### 플래시 메모리의 단위

플래시 메모리의 읽기/쓰기 단위와 삭제 단위는 다르다.
읽기/쓰기는 페이지 단위로 이루어지고 삭제는 블록 단위로 이루어진다.

## 페이지 단위

페이지는 상태를 가질 수 있는데 크게 FRee상태, valid상태, invalid 상태가 있다

- Free 상태 : 어떠한 데이터도 저장하고 있지 않앗 새로운 데이터를 저장할 수 잇는 상태
- valid 사앹 : 이미 유효한 데이터를 저장하고 있는 상태
- invalid상태 : 유효하지않은 데이터(스레기값)을 저장하고 있는 상태

  플래시 메모리는 하드 디스크와 달리 덮어쓰기가 불가능하다. 만약 데이터를 변경하고 싶다면 기존 데이터를 invalid상태로 변환하고 새로운 값을 빈 페이지에 추가한다. 그런데 이렇게 하면 불필요한 invalid 데이터가 많아질 수 있다. 이를 방지하기 위해 가비지컬렉션이 있다. 가비지 컬렉션은 유효한 페이지들만을 새로운 블록으로 복사하고 기존의 블록을 삭제하는기능이다