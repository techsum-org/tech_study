# 주제 : PCB & Context Switching

## 목차
- 주제 : PCB & Context Switching
  - [PCB란 무엇인가](#pcbprocess-control-block란-무엇인가)
  - [PCB의 구조](#pcb-구조)
  - [TCB](#tcb)
  - [PCB 관리](#pcb-관리)
  - [Context Switching이란](#context-switching이란)
  - [Context Switching 과정](#context-switching-과정)
  - [Context Switching overhead](#context-switching-overhead)
  - [PCB & Context Switching 정리](#pcb--context-switching-정리)

<br>

---

## PCB(Process Control Block)란 무엇인가?

<img width="675" alt="pcb" src="https://github.com/techsum-org/tech_study/assets/81874493/518e8e6a-9572-4151-b1ff-df8be1e28e08">


* 정의 : OS가 Process를 제어하기 위해 프로세스의 상태 정보를 저장해놓은 구조체이다.

<br>

* PCB의 특징
  * PCB는 운영체제가 <U>**프로세스의 상태 관리**</U>에 사용된다.
  
  <br>

  * PCB는 <U>**Context Switching에 필요한 프로세스 정보들의 제공**</U>한다.
  
  <br>

  * <U>**Process 생성시 PCB 또한 함께 만들어지며 Process의 실행이 끝나면 함께 폐기**</U>된다.

  <br>
  
  * PCB는 프로세스의 중요한 정보를 포함하고 있기 때문에, 일반 사용자가 접근하지 못하도록 <U>**보호된 메모리 영역에 저장**</U>된다.
    * 일부 운영 체제에서 PCB는 커널 스택의 처음에 위치한다. 
      
      (이 메모리 영역은 편리하면서도 보호를 받는 위치이기 때문)






<br>

---


## PCB 구조

<img width="675" alt="pcb 구조" src="https://github.com/techsum-org/tech_study/assets/81874493/e6c52f1e-1f72-43ee-b812-a34f66fd46c4">

<br>

* (1) Process ID : 프로세스를 구분하는 ID

<br>

* (2) Process State :'준비', '일시중단' 등 프로세스가 CPU에 대한 소유권을 얻은 이후의 State를 저장

<br>

* (3) Program Counter : 프로세스의 다음 Instruction 의 주소를 저장하는 카운터. CPU는 이 값을 통해 Process의 다음 명령을 수행한다.

<br>

* (4) Register : Accumulator, CPU Register, General Register 등을 포함한다.
누산기, 베이스, 레지스터 및 범용 레지스터를 포함하는 CPU 레지스터에 있는 정보

  <details>
    <summary>CPU 레지스터 종류</summary>

  - CPU 내부 일반적 구성 레지스터 종류
      - 메모리 주소 레지스터 (MAR, Memory Address Register)
          
          ⇒ CPU가 메모리의 일부에 데이터를 저장하거나 데이터를 읽을 때 필요한 메모리 위치의 주소를 MAR에 저장한다.
          
          <br>
          
      - 메모리 버퍼 레지스터 (MBR, Memory Buffer Register)
          
          ⇒ 메모리를 읽거나 메모리에 쓰려는 데이터 또는 명령을 저장하는데 사용
          
          ⇒ MBR에 배치된 명령은 명령어 레지스터(IR) 로 전송
          
          ⇒ MBR에 배치된 데이터는 누산 레지스터 (AC) 또는 I/O레지스터로 전송
          
      
          <br>
          
      - I/O 주소 레지스터 (I/O Address Register)
          
          ⇒ I/O 주소 레지스터는 특정 I/O 입출력 장치의 주소를 지정하는데 사용
          
      
          <br>
          
      - I/O 버퍼 레지스터 (I/O Buffer Register)
          
          ⇒ I/O 버퍼 레지스터는 특정 I/O 모듈과 프로세서 간에 데이터 교환하는데 사용
          
          <br>
          
      - 프로그램 카운터 (PC, Program Counter)
          
          ⇒프로그램 카운터는 명령어 포인터(IP, Instruction Pointer) 레지스터 라고도 한다.
          
          - CPU가 수행해야 할 메모리 주소를 담고있는 레지스터
          - CPU는 매번 프로그램 카운터가 가리키는 메모리 위치의 명령을 처리하게 된다.
          - 컴퓨터의 동작이 CPU에 의해서만 이루어지는 것이 아니다. ex 입출력
              1. 메모리에는 사용자 프로그램들과 운영체제가 같이 올라가 수행된다.
              2. CPU는 프로그램 카운터가 가리키는 메모리의 위치의 프로그램을 수행한다.
              - 프로그램 카운터가 메모리 주소 중 운영체제가 존재하는 부분을 가리키고 있다면 현재 운영체제의 코드를 수행중이며 이 경우를 ⇒ 커널모드
              - 반대의 경우 사용자모드라 한다.
          
          <br>
          
      - 명령어 레지스터(IR, Instruction Register)
          
          ⇒ 주 기억장치에서 수행할 명령을 가져오면 명령어 레지스터에 저장된다.
          
          ⇒ 제어장치는 이 레지스터의 지시를 받아 컴퓨터의 해당 구성요소로 신호를 전송하고 명령을 해석하여 실행한다.
          
          <br>

      - 누산기 레지스터(AC, Accumulator Register)
          
          ⇒ 누산기 레지스터는 ALU 내부에 위치하며, ALU의 산술 및 논리 연산 중에 사용된다.
          
          ⇒ 이 레지스터는 시스템에 사용될 초기 데이터, 중간 결과 및 최종 동작 결과를 보관하고 최종결과는 MBR을 통해 주기억장치로 전송된다.
          
          <br>
          
      
      ⇒ 이외에도 많은 레지스터가 존재한다.

  </details>

<br>

* (5) CPU Scheduling Information : 우선 순위, 최종 실행시간, CPU 점유시간 등이 포함된다.

<br>

* (6) Memory Information : 해당 프로세스 주소공간(lower bound ~ upper bound) 정보를 저장.

<br>

* (7) Process Information :페이지 테이블, 스케줄링 큐 포인터, 소유자, 부모 등

<br>

* (8) Device I/O Status :프로세스에 할당된 입출력 장치 목록 등

<br>

* (9) Pointer : 부모/자식 프로세스에 대한 포인터, 자원에 대한 포인터 등

<br>

* (10) Open File List : 프로세스를 위해 열려있는 파일의 리스트

<br>

---

## TCB

<img width="675" alt="TCB" src="https://github.com/techsum-org/tech_study/assets/81874493/8c80db23-447a-4341-b3fa-385b49be8554">

* TCB는 thread 별로 존재하는 자료구조이며 PC값과 register set, 그리고 PCB를 가리키는 Pointer를 가진다.

* thread에 관한 data만 있으면 되므로 TCB는 PCB보다 적은 데이터를  가진다. 


<br>

---

## PCB 관리


* 운영체제는 빠르게 PCB 에 접근하기 위해서 프로세스 테이블을 사용해 각 프로세스의 PCB 를 관리하고 PCB 는 연결 리스트 방식으로 관리된다. 

* 프로세스가 생성, 삭제될 때 PCB 의 삽입 삭제가 용이하다.



<br>

---

## Context Switching이란

* 정의 : 현재 프로세스사가 작업중인 CPU에서 인터럽트나 시스템콜이 발생하여 다른 작업을 수행해야할 때,

  <U> **‘현재 프로세스의 상태 정보를 저장하고 작업해야할 다른 프로세스의 상태 정보를 받아오는 것’** </U>을 의미한다.

<br>



- 문맥(Context)은 프로세스의 상태 정보를 의미하며
- 문맥 교환은 CPU가 현재 작업중인 상태에서 다른 작업을 진행하기 위해
    
    ⇒ 이전의 프로세스의 상태를 PCB를 통해 보관하고
    
    ⇒ 다른 프로세스의 정보를 PCB에서 읽어 레지스터에 적재하는 과정

  <br>    

  즉 **CPU 내 재배치 레지스터에 다음에 실행할 프로세스 정보들로 교체를 하고 다음 프로세스를 진행한다.**
  * 재배치 레지스터(relocation register) : 프로세스의 물리적 메모리 시작 주소를 가진다.

<br>
<br>

**문맥 교환이 필요한 이유**

Computer가 매번 하나의 Task만 처리할 수 있다면?

* 해당 Task가 끝날때까지 다음 Task는 기다릴 수 밖에 없다.
  또한 반응속도가 매우 느리고 사용하기 불편하다.

<br>

그렇다면 다양한 사람들이 동시에 사용하는 것처럼 하기 위해선?

* Computer multitasking을 통해 빠른 반응속도로 응답할 수 있다.
  * 빠른 속도로 Task를 바꿔 가며 실행하기 때문에 사람의 눈으론 실시간처럼 보이게 되는 장점이 있다.
  * CPU가 Task를 바꿔 가며 실행하기 위해 Context Switching이 필요하다.


<br>
<br>

**문맥 교환의 장단점**

  - 장점 : 문맥 교환을 통해 멀티 태스킹이 가능하다
      
      ( 멀티 태스킹 : 다수의 작업(혹은 프로세스, 이하 태스크)이 중앙 처리 장치(이하 CPU)와 같은 공용자원을 나누어 사용하는 것)
      
      <br>

  - 단점 : 문맥 교환중에는 다른 작업을 할 수 없다. ( = overhead 라고 한다)
      
      ⇒ 다중 프로그래밍 정도가 높아짐에 따라 스레싱 현상이 일어날 수 있다.
      
      > 스레싱 현상이란??
      >* 정의 : 프로세스가 집중적으로 사용하는 페이지들의 집합이 메모리에 한꺼번에 적재되지 못하여 <U>**페이지 부재율(page fault)가 많이 발생하게 되고 CPU 이용율이 급격히 떨어지는 현상**</U>


<br>
<br>


**문맥 교환이 일어나는 시점**

- 멀티 태스킹
    
    ⇒ 멀티 태스킹 환경에서 프로세스 전환 과정에서 문맥 교환이 일어난다.
    
- 인터럽트 처리
    
    ⇒ 인터럽트가 발생할 때 문맥 교환이 발생한다.
    
- 사용자 및 커널 모드 전환
    
    ⇒ 운영체제에서 사용자-커널 모드 사이 전환이 필요할때 문맥 교환이 발생한다.

<br>

<br>

---


## Context Switching 과정

<img width="675" alt="Context Switching 과정" src="https://github.com/techsum-org/tech_study/assets/81874493/3589757a-33a5-49cc-9b36-9ee1d86e49d5">

1. 현재 실행 중인 process의 상태정보를 PCB에 저장( PCB0 )

2. 실행하려는 process의 정보를 해당 PCB( PCB1 )에서 불러와서 register에 탑재

3. 실행할 process(여기서는 P1)를 실행합니다.

4. P1 실행 중에 interrupt / system call이 생기면 우선순위에 맞추어 현재 P1의 상태를 PCB에 저장하고 다음 실행 대상을 지정

5. 정해진 대상의 PCB에서 불러와 실행

<br>

---

##  Context Switching overhead


>Context Switching 때 해당 CPU는 아무런 일을 하지 못한다. 따라서 컨텍스트 스위칭이 잦아지면 오히려 오버헤드가 발생해 효율(성능)이 떨어진다.

<br>

| |실행루틴|오버헤드|
|---|---|---|
|1|현제 프로세스||
|2|Interrupt 처리 루틴|현재 상태를 PCB에 저장|
|3|프로세스 스케쥴러|	다음 실행 프로세스를 준비 Queue 에서 선택|
|4|Dispatch|다음 Process의 PCB값 복구|
|5|다음 프로세스|

<br>

* cache miss overhead

  * cache에는 현재 실행 중인 process의 data가 들어간다
  
    ⇒ 근데 context switching이 발생하면 이제 cache에 있는 data가 필요없어지기 때문에 cache를 비운다
  
  <br>

  * 그렇게 cache를 비우면 process가 바뀐 후 초반에는 cache miss가 계속 발생

  <br>

  * 그럼 메모리 참조가 발생하게 되고 이는 overhead가 된다.

  <br>

  * 하지만 같은 프로세스의 thread 간에 context switch가 발생하면 cache를 비우지 않아도 된다
    
    ⇒ 공유하는 데이터가 있기 때문에 cache가 쓸모있어지고, cache miss 발생 횟수도 감소하게 됩니다.
  
    >그렇다면 context switch가 thread 단위에서도 일어나며 thread에 관한 정보는  TCB에 저장된다.

<br>
<br>

* 오버헤드 해결 방안
  * Context Switch 자주 발생하지 않도록 다중프로그래밍의 정도를 낮춤
  * 스택중심의 장비에서는 Stack 포인터 레지스터를 변경하여 프로세스간 문맥교환 수행
  * Light Weight Process인 스레드를 이용하여 Context Switch 부하를 최소화시킴

<br>

---
## PCB & Context Switching 정리


* PCB란 무엇인가요
  * 답변 : OS가 Process를 제어하기 위해 프로세스의 상태 정보를 저장해놓은 구조체 입니다.

<br>

* PCB의 역할은 무엇인가요
  * 답변 : PCB는
    
    * PCB는 운영체제가 프로세스의 상태 관리에 사용되며
    * PCB는 Context Switching에 필요한 프로세스 정보들의 제공하는데
    
      필요합니다.

<br>

* PCB의 구조는 어떻게 되나요
  * 답변 : PCB의 구조로는


    * 프로세스를 구분하는 Process ID 
    * 프로세스가 CPU에 대한 소유권을 얻은 이후의 State를 저장하는 Process State
    * 프로세스의 다음 Instruction 의 주소를 저장하는 Program Counter 
    * Accumulator, CPU Register, General Register 등을 포함하는 Register
    * 우선 순위, 최종 실행시간, CPU 점유시간 등이 포함되는 CPU Scheduling Information
    * 해당 프로세스 주소공간 정보를 포함하는 Memory Information
    * 페이지 테이블등을 포함하는 Process Information 
    * 프로세스에 할당된 입출력 장치 목록 등을 포함하는 Device I/O Status
    * 부모/자식 프로세스에 대한 포인터, 자원에 대한 포인터 등을 포함하는 Pointer
    * 프로세스를 위해 열려있는 파일의 리스트인 Open File List

    
      등이 존재합니다.

<br>

* PCB는 어떻게 관리되나요
  * 답변 : OS는 PCB에 빠르게 접근하기 위해 프로세스 테이블을 이용하여 각각의 PCB를 관리하며 PCB는 연결 리스트 방식으로 관리 됩니다.


<br>

* TCB란 무엇인가요
  * 답변 : TCB란 Thread Control Block으로 thread 별로 존재하는 자료구조이며 PC값과 register set, 그리고 PCB를 가리키는 Pointer를 가집니다.



<br>

Context Switching이란 무엇인가요
  * 답변 : Context Switching 이란 CPU가 하나의 처리만 하지 않고 여러 작업을 번갈아 가며 진행하기 위해 현재 프로세스의 상태 정보를 저장하고 다른 작업의 프로세스 상태 정보를 받아오는 것을 의미합니다.


<br>

* Context Switching의 장단점은 어떻게 되나요
  * 답변 : Context Switching 장단점으로는

    * 문맥 교환을 통해 멀티 태스킹이 가능하다는 장점을 가지고 있으며
    * 문맥 교환중에는 다른 작업을 할 수 없어 다중 프로그래밍 정도가 높아짐에 따라 스레싱 현상이 일어날 수 있다는 단점을 가지고 있습니다.

  
<br>

* Context Switching의 overhead란 무엇인가요
  * 답변 : Context Switching의 overhead는

    * Context Switching 때 해당 CPU는 아무런 일을 하지 못하기 때문에 Context Switching이 잦아지면 효율(성능)이 떨어지며
    * context switching으로 인해 cache를 비우기 때문에 cache miss가 빈번하게 발생하여 효율성이 떨어진다

    는 overhead를 가지고 있습니다.

<br>

* Context Switching의 overhead의 해결책은 무엇이 있을까요
  * 답변 : Context Switching의 overhead의 해결책으로는
    * Context Switch 자주 발생하지 않도록 다중프로그래밍의 정도를 낮추는 방법과
    * Light Weight Process인 스레드를 이용하여 Context Switch 부하를 최소화 시키는

    방법이 존재합니다.

<br>

