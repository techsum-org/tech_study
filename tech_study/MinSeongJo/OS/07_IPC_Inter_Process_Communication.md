# IPC ( Inter Process Communication)

## Table of Contents
* [IPC에 대해](#inter about IPC)


### IPC (InterProcess <U><font color="pink">Communication</font></U>, <U><font color="pink">프로세스</font></U>간 <U><font color="pink">통신</font></U>) 이란?

* 실행 <U><font color="pink">프로세스</font></U> 간에 <U><font color="pink">통신</font></U>을 가능케하는 <U><font color="pink">메커니즘</font></U>
  * <U><font color="pink">프로세스</font></U> 간에 서로 <U><font color="pink">통신</font></U>하는 규칙에 관한 문제
* <U><font color="pink">호스트</font></U>의 기종, <U><font color="pink">운영체제</font></U> 등이 무엇인지 관계없이 일정 규칙으로 <U><font color="pink">통신</font></U>하는 것이 매우 중요함.
  * 통상, 두 <U><font color="pink">프로세스</font></U> 간에 일정 포맷과 순서를 따르는 <U><font color="pink">메세지</font></U>를 주고 받으며 <U><font color="pink">통신</font></U>을 하게 됨.
* 결국, <U><font color="pink">멀티태스킹 운영체제</font></U> 내 또는 <U><font color="pink">네트워크</font></U>화 (Networked) / 분산된 (Distributed) <U><font color="pink">컴퓨터</font></U>들 사이에,
  * 각각 실행되는 <U><font color="pink">프로세스</font></U> 간에 <U><font color="pink">정보</font></U>의 교환을 가능케 하는 기법

### IPC 구현 기법들 구분

* 전통적인 주요 기법 둘
  * 공유 메모리 기법 (Shared Memory)
    * 협력적 프로세스들이 공유 메모리 영역을 통해 데이터 교환
      * 주로, 전역변수, 공유변수, 공유 파일을 통해 통신을 이룸
    * 충돌 가능성은 있으나, 일반적으로 더 빠르고 커널 도움이 거의 필요 없음
      * 즉, 고속 통신이 가능하나, 통신 책임이 응용 프로세스에 있고,
      * 운영체제는 단지 공유 메모리만 제공 함
  * 메세지 전달 기법 (Message Passing)
    * 협력적 프로세스 간에 메세지 교환
    * 충돌하지 않으나, 적은 양의 데이터 교환 위주
    * 통신 책임 및 수단이 운영체제에 의해 제공됨
* 유닉스 초기 IPC 구현 3가지 기법
  * 공유 메모리 (Shared memory)
    * 다중 프로세스들이 가상 메모리 (Virtual Memory)를 공유
    * 협력 프로세스들 간에 공유되는 메모리 영역이 운영체제에 의해 구축 제공됨
  * 세마포어 (Semaphore) : 공유 자료에 대한 접근을 통제하는 일종의 카운터
  * 메시지 큐 (Message Queue)
* 메시지 전달 (Message Passing)에 기반을 둔 기법들
  * 시그널 (Signal)
    * 실시간으로 프로세스에 이벤트 발생을 알리기 위함
  * 세마포어 (Semaphore)
    * 공유 자료에 대한 접근을 통제하는 일종의 카운터
  * 파이프 (Pipe)
    * 2개의 프로세스 입출력을 직렬 연결하여 하나의 공유 페이지를 제공
      * ls | pr (ls 를 수행한 표준출력이 pr의 표준입력으로 전달 됨)
    * 이름 없는 파이프 : 상호 관련 있는 프로세스 간 통신에 사용
    * 이름 있는 파이프 (Named Pipe) : 장치 파일을 통해, 상호 관련 없는 프로세스 간 통신에 사용
  * 소켓 (Socket)
    * 네트워크에 기반ㅇ르 둔 IPC 메커니즘
    * 파이프 개념을 네트워크로 확장시킨 것
  * RPC(Remote procedure Call) : 클라이언트 - 서버 모델을 이용하는 기법
    * 원격지 프로세스 간에 함수의 호출에 기반을 둔 기법
    * 한편, LPC (local procedure Call)는 동일 시스템내에서 호출 기법을 말함
### 통신계층의 관점
* IPC는 트랜스포트 계층(Layer 4) 또는 세션 계층(Layer 5)에서 이루어짐

### IPC의 사용 예시

* **운영체제와 사용자 인터페이스** : 컴퓨터에서 어플리케이션을 실행하거나, 파일을 이동하거나, 시스템 설정을 변경할 때, 대부분의 경우 이러한 동작은 여러 프로세스간의 통신을 필요로 합니다. 예를 들어, 사용자 인터페이스가 사용자의 명령을 받아 해당 명령을 수행하는 다른 프로세스에 전달합니다.
* **웹 서버와 데이터베이스** : 웹 애플리케이션은 보통 웹 서버와 데이터베이스 서버 사이의 IPC를 통해 데이터를 주고 받습니다. 웹 서버는 사용자의 요청을 받아 데이터베이스 서버에 전달하고, 데이터베이스 서버는 요청된 데이터를 웹 서버에 반환합니다.
* **분산 시스템** : IPC는 분산 시스템에서 데이터를 주고받는 데도 사용됩니다. 분산 시스템은 여러 컴퓨터가 네트워크를 통해 연결되어 하나의 시스템처럼 동작하는 컴퓨터 시스템입니다. 각 컴퓨터는 IPC를 통해 데이터를 주고받아 분산 시스템의 전반적인 작업을 조율합니다.
* **멀티코어나 멀티프로세서 시스템** : IPC는 멀티코어나 멀티프로세서 컴퓨터 시스템에서도 중요한 역할을 합니다. 각 코어나 프로세서는 독립적인 프로세스를 실행하고 IPC를 통해 작업을 조율하거나 데이터를 주고받습니다.

### IPC 종류와 특징

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F2641923B5718784D35">
- 위 그림처럼 Process는 완전히 독립된 실행객체입니다. 서로 독립되어 있다는 것은 다른 프로세스의 영향을 받지 않는다는 장점이 있습니다. 그러나 독립되어 있는 만큼 별도의 설비가 없이는 서로간에 통신이 어렵다는 문제가 있게 됩니다. 이를 위해서 커널 영역에서 IPC라는 내부 프로세스간 통신 - Inter Process Communication을 제공하게 되고, 프로세스는 커널이 제공하는 IPC설비를 이용해서 **프로세스 간 통신**을 할 수 있게 됩니다.

#### IPC의 2가지 표준 (System V IPC와 POSIX IPC)

- System V IPC는 오래된 버전이고 POSIX IPC는 비교적 최근에 개발된 표준입니다. System V IPC는 오랜 역사를 가진 만틈 이기종간 코드 호환성을 확실히 보장해 주지만, API가 오래되었으며, 함수명도 명확하지 않습니다. POSIX IPC는 직관적으로 API가 구성되어 있어서 상대적으로 조금 더 사용하기 쉽다고 보여집니다.

#### IPC 설비들
- 현실에서도 필요에 따라 다양한 통신 설비들이 존재하는 것처럼 IPC에도 다양한 설비들이 존재합니다. 각각의 필요에 따라서 적당한 통신 설비들이 준비되어야 하는 것과 마찬가지로 내부 프로세스간 통신에도 그 상황에 맞는 IPC 설비를 선택할 필요가 있게 됩니다.

상황에 맞는 IPC의 선택은, 특히 fork()를 이용해서 만들어진 멀티 프로세스의 프로그램에 있어서 중요합니다. 잘못된 IPC 설비의 선택은 코딩과정을 어렵게 만들거나 프로그램의 작동을 효율적이지 못하게 만들 수 있기 때문입니다.

**<font color="pink">1) PIPE (익명 PIPE, Anonymous PIPE)</font>**

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F247CBC4357187A3411">
- 위 그림은 PIPE의 작동원리를 보여줍니다. 파이프는 두 개의 프로세스를 연결하게 되고, 하나의 프로세스는 데이터를 쓰지만, 다른 하나는 데이터를 읽기만 할 수 있습니다. 한쪽 방향으로만 통신이 가능한 파이프의 특징 때문에 Half-Duplex(반이중) 통신이라고 부르기도 합니다.

PIPE와 같은 반이중 통신의 경우 하나의 통신선로는 읽기나 쓰기 중 하나만 가능하므로 만약 읽기와 쓰기, 즉 송/수신을 모두 하기 원한다면 두 개의 파이프를 만들어야만 가능해집니다.

PIPE는 매우 간단하게 사용할 수 있다는 장점이 있습니다. 만약 한쪽 프로세스가 단지 읽기만 하고 다른 쪽 프로세스는 단지 쓰기만 하는, 단순한 데이터 흐름을 가진다면 고민 없이 PIPE를 사용하면 됩니다. 단점은 반이중 통신이라는 점으로 만약 프로세스가 읽기와 쓰기 통신 모두를 해야 한다면 PIPE를 두개 만들어야 하는데, 구현이 꽤나 복잡해 질 수 있습니다. 만약 전이중 통신을 고려해야될 상황이라면 PIPE는 좋은 선택이 아니라고 보여집니다.

**<font color="pink">2) Named PIPE(FIFO)</font>**

- 익명 파이프(PIPE)는 통신을 할 프로세스가 명확하게 알 수 있는 경우 사용합니다. 예를 들어 자식과 부모 프로세스간 통신의 경우에 사용할 수 있으며, Named PIPE는 전혀 모르는태의 프로세스들 사이의 통신의 경우 사용합니다. 익명 파이프(PIPE)의 단점으로 같은 PPID(같은 부모 프로세스)를 가지는 프로세스들 사이에서만 통신이 가능하지만, Named PIPE는 그 부분을 해결한, PIPE의 확장이라고 할 수 있을 것입니다. **Named PIPE**는 <font color="green">**부모 프로세스와 무관하게 전혀 다른 모든 프로세스들 사이에서 통신이 가능**</font>한데 그 이유는 프로세스 통신을 위해 이름이 있는 파일을 사용하기 때문입니다. Named PIPE의 생성은 mkfifo를 통해 이뤄지는데, mkfifo가 성공하면 명명된 파일이 생성됩니다.

단점으로는, Named PIPE도 PIPE의 또 다른 단점인 읽기/쓰기가 동시에 가능하지 않으며, read-only, write-only만 가능합니다. 하지만 통신선로가 파일로 존재하므로 하나를 읽기 전용으로 열고 다른 하나를 쓰기 전용으로 열어서 이러한 read/write문제를 해결할 수 있습니다. 호스트 영역의 서버 클라이언트 간에 전이중 통신을 위해서는 결국 PIPE와 같이 두개의 FIFO파일이 필요하게 됩니다.

**<font color="pink">3) Message Queue</font>**

- Queue(큐)는 선입선출의 자료구조를 가지는 통신설비로 커널에서 관리합니다. 입출력 방식으로 보자면 위의 Named PIPE와 동일하다고 볼 수 잇을 것입니다. Named PIPE와 다른 점이라면 Named PIPE가 데이터의 흐름이라면 메시지 큐는 <font color="green">**메모리 공간**</font>이라는 점입니다. 파이프가 아닌, 어디에서나 물건을 꺼낼 수 있는 컨테이너 벨트라고 보면 될 것입니다.

메시지 큐의 장점은 컨테이너 벨트가 가지는 장점을 그대로 가지게 됩니다. 컨테이너 벨트에 올라올 물건에 라벨을 붙이면 동시에 다양한 물건을 다룰 수 있는 것과 같이, **메시지 큐에 슬 데이터에 번호를 붙임**으로써 여러 개의 프로세스가 동시에 데이터를 쉽게 다룰 수 있습니다.

**<font color="pink">4) Shared Memory(공유메모리)</font>**

- Memory Map도 Shared Memory(공유메모리)공간과 마찬가지로 메모리를 공유한다는 측면에 있어서는 서로 비슷한 측면이 있습니다. 차이점은 Memory Map의 경우 <font color="green">**열린파일을 메모리에 맵핑시켜서, 공유**</font>한다는 점일 것입니다. 파일은 시스템의 전역적인(모두 공유할 수 있는) 자원이므로 서로 다른 프로세스들끼리 데이터를 공유하는데 문제가 없을 것임을 예상할 수 있습니다.

**<font color="pink">6) Socket</font>**

- Socket은 프로세스와 시스템의 기초적인 부분이며, 프로세스 들 사이의 통신을 가능하게 합니다. sys/socket.h>라는 헤더를 이용하여 사용할 수 있으며, 같은 도메인에서의 경우에서 연결 될 수 있습니다. 소켓을 사용하기 위해서는 생성해주고, 이름을 지정해주어야 합니다. 또한 domain과 type, Protocol을 지정해 주어야 합니다. 서버 단에서는 bind, listen, accept를 해주어 소켓 연결을 위한 준비를 해주어야 하고, 클라이언트 단에서는 connect를 통해 서버에 요청하며, 연결이 수립 된 이후에는 Socket을 send함으로써 데이터를 주고 받게 됩니다. 연결이 끝난 후에는 반드시 Socket을 close()해주어야 하며, Socket과 관련해서는 이후 네트워크 부분에서 자세히 다루도록 하겠습니다.

**<font color="pink">7) Semaphore</font>**

- Semaphore는 Named PIPE, PIPE, Message Queue와 같은 다른 IPC설비들이 대부분 프로세스간 메시지 전송을 목적으로 하는데 반해, Semaphore는 프로세스 간 데이터를 동기화 하고 보호하는데 그 목적을 두게 됩니다. 프로세스간 메시지 전송을 하거나, 혹은 Shared Memory를 통해서 특정 데이터를 공유하게 될 경우 발생하는 문제가 공유된 자원에 여러개의 프로세스가 동시에 접근하면 안되며, 단지 한번에 하나의 프로세스만 접근 가능하도록 만들어줘야 할 것이며, 이 때 사용되는 것이 Semaphore입니다.

