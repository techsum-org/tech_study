# 주제 : Process & Thread

## 목차
- 주제 : Process & Thread
  - [폰노이만 구조 & 하버드 구조](#폰노이만-구조--하버드-구조)
  - [Process란?](#process란-무엇인가)
  - [Process 상태](#process의-상태)
  - [Process의 생성](#process의-생성)
  - [Thread란?](#thread란-무엇인가)
  - [Process & Thread 정리 ](#process--thread-정리)

<br>

---

## 폰노이만 구조 & 하버드 구조
<img width="665" alt="스크린샷 2023-05-18 오후 5 45 55" src="https://github.com/techsum-org/tech_study/assets/81874493/47279e94-fda9-48ff-9057-0878239eae5c">

* 정의 : 폰노이만이 고안한 내장 메모리 순차처리 방식 구조

<br>

* 특징 
  * 현재와 같은 <U>**CPU, 메모리, 프로그램 구조를 갖는 범용 컴퓨터 구조의 확립**</U>
  
  * 폰 노이만 구조는 `내장 메모리 순차 처리 방식` 을 통해 하드웨어는 그대로 두고 소프트웨어(프로그램)만 교체하면 된다
  * <details>
        <summary>폰노이만 구조는 내장 메모리 순차 처리 방식의 구조</summary>
        내장 메모리 순차 처리 방식이란?
        
        이전 컴퓨터는 명령을 수행하기 위해 하드웨어 전선을 매번 바꿔 끼워가며 명령을 입력해야 했다.

        폰 노이만 구조에서는 명령어( +, -, *, / 등)를 담은 소프트웨어가 메모리 안에 내장 되어 있어 필요시 마다 메모리 안의 소프트 웨어와 데이터를 CPU에 전달하여 처리하면 된다.

        처리 과정
        - 메모리로 부터 명령어 가져오기 - fetch
        - 명령어의 의미를 해석 - decode
        - 명령어를 실행 - excute
        - 명령 결과를 저장하는 - store
        
        ⇒ 위의 순서로 처리된다.
    </details>
    <br>
    ⇒  편의성 증가 되었고 다양한 목적으로 사용이 가능하여 범용성이 향상
    
    <br>

* 단점
    
    * 폰노이만 구조의 단점으로는 **병목 현상**이 존재 한다.
    
      * 병목 현상 :  “ 전체 시스템의 성능이나 용량이 하나의 구성요소로 인해 제한을 받는 현상을 의미한다”
        
        <br>

      - 폰노이만 구조에서 CPU에서 빠르게 계산 처를 할 수 있어도 데이터를 불러오는 속도가 느리면 전체적으로 속도가 느려진다는 단점
        
        - ex) 성능이 좋은 CPU를 사용하지만 용량이 작은 메모리를 사용하여 처리하는 데이터를 불러오는데 시간이 오래 걸릴 경우 전체적인 처리 시간은 느려진다 
        
        <br>

        ⇒ 계산 속도가 빨라도 기억장치의 속도 영향을 받음
        
        ⇒ 즉 기억장치의 속도가 전체 시스템의 성능 저하를 야기한다.
<br>

<br>

<br>


<img width="681" alt="스크린샷 2023-05-18 오후 5 46 04" src="https://github.com/techsum-org/tech_study/assets/81874493/2ac1bf60-5d95-4391-afb3-8145cc53b806">

* 정의 : 폰노이만 구조의 병목 현상을 극복하기 위한 컴퓨터 아키텍처중 하나이다.

* 특징
  * 병목 현상이 일어나는 근본적 원인
    
    *  프로그램 메모리와 데이터 메모리가 물리적 구분 없이 하나의 버스를 통해 CPU와 교류가 원인
    
        ⇒ 이로인해 CPU는 명령어와 데이터에 동시 접근 불가능
    
        ⇒ 나열된 명령을 한 번에 하나씩 읽고 쓰게 됨
    
    <br>

  * 프로그램 메모리와 데이터 메모리의 구분
    
        ⇒ 하버드 구조에서는 CPU가 명령어와 데이터를 동시에 사용할 수 있도록 물리적으로 프로그램과 명령어영역을 물리적으로 구분
    
        ⇒ 이를 통해 현재 명령 처리를 끝냄과 동시에 다음 명령을 읽어 들일 수 있기때문에 폰노이만 구조 보다 더 빠른 속도를 낼 수 있다.
    
    <br>

  - 하버드 구조의 단점
    - 이러한 속도를 높히기 위해 보다 많은 전기 회로를 필요로 한다.
    - 두개의 버스와 메모리를 가지게 되어 CPU 코어에 공간을 많이 차지 한다.


---

## Process란 무엇인가

<img width="452" alt="스크린샷 2023-05-18 오후 5 47 15" src="https://github.com/techsum-org/tech_study/assets/81874493/697ae084-8700-4ec6-8b3e-51825ea681a4">

* 정의 : 프로세스란 운영체제로부터 자원을 할당받아 프로그램이 메모리 상으로 올라갔을 때의 상태를 의미한다.

<br>

<img width="685" alt="스크린샷 2023-05-18 오후 5 48 16" src="https://github.com/techsum-org/tech_study/assets/81874493/c57cd31c-579b-487c-9cc4-8e6ce2b001d2">


* 프로세스 구조
  - text(CODE): 컴파일된 소스 코드가 저장되는 영역
  - data: 전역 변수/초기화된 데이터가 저장되는 영역(BSS + Data)
    - BSS: 초기화 되지 않은 전역 변수가 담긴다.
    - DATA: 초기값이 있는 전역 변수가 담긴다.
  - stack: 임시 데이터(함수 호출, 로컬 변수 등)가 저장되는 영역
  - heap: 코드에서 동적으로 생성되는 데이터가 저장되는 영역


<br>

---

## Process의 상태

<img width="715" alt="스크린샷 2023-05-18 오후 5 46 47" src="https://github.com/techsum-org/tech_study/assets/81874493/a5486b81-d154-4be7-b966-b312e31557d2">


* 생성상태 -> 준비상태
    
    미리 정의된 정책에 따라 스케줄러에 의해 호출, 이때 메모리의 이용 가능성과 어떤 장치가 요구되는지를 검사한다.

    <br>

* 준비상태 -> 실행상태
    
    사전에 정의된 알고리즘(FCFS, SJF, SRT, RR등)에 따라 스케줄러에 의해 처리된다. 이 과정을 디스패치라고 한다.

    <br>
    
* 실행상태 -> 준비상태
    
    할당시간의 만료나 우선순위 알고리즘을 택하고 있는 시스템에서 높은 우선순위의 프로세스가 오는 경우 스케줄러에 의해 처리된다.

    <br>
    
* 실행상태 -> 대기상태
    
    READ, WRITE 또는 다른 I/O 요구, 페이지 교환을 요구하는 작업 같은 명령 등에 의하여 일어난다.

    이러한 작업은 상대적으로 오랜 시간이 걸리기 때문에 그동안 CPU를 다른 프로세스에 할당하여 활용하기 위함이다.

    <br>
    
* 대기상태 -> 준비상태
    
    I/O 장치 관리자의 신호에 의해 일어난다.
    페이지 교환의 경우 페이지 인터럽트 핸들러가 메모리에 그 페이지가 있다는 신호를 보내게 되며, 프로세스는 준비 큐에 놓이게 된다.

    <br>
    
* 실행상태 -> 종료상태
    
    프로세스를 성공적으로 끝마친 경우, 혹은 운영체제가 에러 발생을 감지하고 프로세스를 강제로 종료시킨 경우에 스케줄러에 의해 실행된다.

<br>



---



## Process의 생성

Process 생성에는 크게 두가지 방식으로 구분된다

* Directed Process Creation (직접 생성)
  * 운영체제가 Disk에 있는 프로그램을 memory에 올려서 process로 만들고 process image(PCB)를 만든다.
  
  <br>

  * 과정
    1. 새로운 프로세스를 위한 메모리 공간 확보
    2. 확보한 메모리 공간에 새로운 프로세스의 code, data를 Load, call Stack 생성
    3. PCB 초기화
    4. 새로운 프로세스를 준비상태로 전환 (준비큐에 삽입)

    <br>

    ⇒ 일반 OS에서 첫 번째 Process는 이런 과정으로 만든다.

    ⇒ *init process = first process = pid가 1인 프로세스*

<br>

* Cloning ( 복제 )
  - 부모프로세스에서 복제하여 자식 프로세스 생성하는 방법
      - **부모프로세스와 PCB의 상당부분 값이 비슷하다**
  - unix/Linux 에서 fork() 시스템 호출(System call)를 통해 새로운 프로세스를 생성한다.
    
    <br>

    1. 부모 프로세스 PCB에서 text,data,stack 복사
    2. 반드시 필요한 부분만 수정
        
        ⇒ 새로운 프로세스 생성시 fork()를 통해 복제 이후,
        
        ⇒ exec() 시스템 콜을 통해 child의 메모리 공간을 모두 새로 할당
        
        ⇒ code, data, bss 영역을 새로 할당
        
        ⇒ 동적 영역인 heap, stack은 리셋 된다. 
        
    3. new process를 ready state 로 전환 (준비 큐에 넣는다.)

---

## Thread란 무엇인가

<img width="685" alt="스크린샷 2023-05-18 오후 5 48 16" src="https://github.com/techsum-org/tech_study/assets/81874493/c6635e87-89b4-4dc3-bad0-f6285cc022a6">

* 정의 : 스레드는 프로세스 내에서 운영체제로부터 할당받은 자원을 이용하여 작업을 수행하는 단위를 의미한다.
 

* Thread 구조
  * 스레드는 프로세스 내에서 각각 Stack만 할당받고 Code, Data, Heap영역은 공유된다.
  *  한 프로세스 내에서 동작되는 여러 실행의 흐름이며 프로세스내의 주소공간이나 자원(Heap) 등과 같은 프로세스 내에 스레드끼리 공유하면서 실행이 됩니다.
  *   같은 프로세스 안에 있는 여러 스레드들은 같은 힙 공간을 공유하지만 프로세스는 다른 프로세스의 메모리에 직접 접근은 불가능합니다.
  * 각각의 스레드는 별도의 레지스터와 스택을 갖고 있지만 힙 메모리는 서로 읽고 쓸 수 있습니다

---



## Process & Thread 정리

* 폰노이만 구조가 무엇인가요?
  * 답변 : 폰노이만이 고안한 내장 메모리 순차처리 방식 구조로 필요시 마다 메모리 안의 소프트 웨어와 데이터를 CPU에 전달하여 처리 방식을 따르며
    * 편의성 증가 되었고 다양한 목적으로 사용이 가능하여 범용성이 향상되었다는 장점이 존재하며
    * 전체 시스템의 성능이나 용량이 하나의 구성요소로 인해 제한을 받는 병목현상이 있다는 단점이 존재합니다.

<br>

* 하버드 구조가 무엇인가요?
  * 답변 : 폰노이만 구조의 병목현상을 완화하기위해 나온 구조로
    *  CPU가 명령어와 데이터를 동시에 사용할 수 있도록 물리적으로 프로그램과 명령어영역을 물리적으로 구분하여 더 빠르다는 장점이 존재하며
    *  두개의 버스와 메모리를 가지게 되어 CPU 코어에 공간을 많이 차지 한다는 단점이 존재합니다.

<br>

* 프로세스가 무엇인가요?
  * 답변 : 프로세스란 운영체제로부터 자원을 할당받아 프로그램이 메모리 상으로 올라갔을 때의 상태를 의미 합니다.


<br>

* 프로세스의 생성은 어떻게 되나요?
  * 답변 : 프로세스의 생성에는 직접생성 방식과 복제 방식이 존재하며 
    * 직접 생성 방식은 운영체제가 Disk에 있는 프로그램을 memory에 올려서 process로 만드는 방식이며
    * 복제 방식은 부모프로세스에서 복제하여 자식 프로세스 생성하는 방식 입니다.

<br>

* Thread란 무엇인가요?
  * 답변 : Thread란 운영체제로 부터 자원을 할당 받은 자원을 이용하여 프로세스 내의 작업을 수행하는 작업 단위 입니다.

<br>
