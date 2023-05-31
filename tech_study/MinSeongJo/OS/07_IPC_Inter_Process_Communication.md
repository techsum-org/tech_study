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

