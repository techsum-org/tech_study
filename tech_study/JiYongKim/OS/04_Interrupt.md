# 주제 : Interrupt

## 목차
- 주제 : Interrupt
  - [Polling 방식이란?](#polling-방식이란)
  - [Interrupt 방식이란?](#interrupt-방식이란)
  - [Interrupt 분류](#인터럽트의-분류)
  - [Interrupt 처리](#인터럽트의-처리)
  - [Interrupt vs Polling](#interrupt-vs-polling)
  - [Interrupt Vector란?](#interrupt-vector란)
  - [Interrupt 정리](#interrupt-정리)

<br>

---

## Polling 방식이란?

* 정의 : 운영체제가 하드웨어 장치의 상태 레지스터를 읽음으로써 <U>명령의 수신 여부를 주기적으로 확인</U>하는 방법이다. 

<br>

* CPU 에서의 Polling 방식
  * CPU 에서의 Polling 방식은 특정 주기를 가지고 그 주기 마다 처리를 하드웨어의 변화를 지속적으로 읽어 들이며 이벤트의 수행 여부를 주기적으로 검사하여 해당 신호를 받았을때 이벤트를 실행하는 방식이다.

<br>

* 네트워크에서의 Polling 방식
  * 네트워크에서의 Polling 방식은 한 프로그램이나 장치에서 다른 프로그램이나 장치들이 어떤 상태에 있는지를 지속적으로 체크하는 전송제어 방식으로서, 대체로 그들이 아직도 접속되어 있는 지와 데이터 전송을 원하는지 등을 확인한다.

<br>

* 웹에서의 Polling 방식
  - 웹에서의 Polling 방식은 클라이언트에서 서버 데이터 변경 사항들을 실시간으로 반영하기 위해 클라이언트가 일정 주기로 서버에게 필요한 데이터를 요청하는 방식
  
<br>

---

## Interrupt 방식이란?

* 정의 : 인터럽트는 란 마이크로프로세서(CPU)가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치에 예외상황이 발생하여 처리가 필요할 경우에 <U>마이크로 프로세서에게 알려 처리하고 다시 실행중인 작업으로 복귀 할 수 있도록 하는 것</U>을 의미한다.
  
<br>

---

## 인터럽트의 분류

- 실행 중인 명령어로 인해 발생하는 인터럽트
    - 프로그램상 문제 때문에 발생하는 인터럽트( 외부 사용자의 메모리 접근, 오버플로나 언더플로)
    - 컴퓨터 작업자가 의도적으로 프로세스를 중단하기 위해 발생시킨 인터럽트
    - 입출력 장치 같은 주변 장치의 조작에 의한 인터럽트
    - 산술 연산 중 발생하는 인터럽트( 어떤수를 0으로 나눔 )
            
    <br>


- 실행 중인 명령어와 무관하게 발생하는 인터럽트
  - 하드디스크 읽기 오류
  - 메모리 불량 등
                
    ⇒ 하드웨어적 오류로 발생하는 인터럽트로 ( 사용자의 키보드 마우스 인터럽트 등이 있다.)

<br>

---

## 인터럽트의 처리
<img width="665" alt="interrupt 처리" src="https://github.com/techsum-org/tech_study/assets/81874493/8df7d331-423c-4a24-8e79-290cb55b84b1">

1. 인터럽트 요청
2. 프로그램 실행 중단
3. 현재 실행 중인 프로그램 상태 보관
   * PCB, PC 저장
4. 인터럽트 원인 판별
    * 인터럽트 요청 장치 실별 -> 인터럽트 원인 파악
    * 인터럽트 벡터 테이블 참조하여 호출할 ISR(인터럽트 서비스 루틴)주소 값을 얻음
5. ISR(인터럽트 서비스 루틴)처리
    * 인터럽트 처리 작업
    * 서비스 루틴 수행중 우선순위가 높은 인터럽트 발생시 재귀적 1~5번 과정 수행
    * 인터럽트 루틴 실행시 IF(인터럽트 플래그)를 0으로 설정시 인터럽트 발생 방지가 가능
6. 상태 복구
    * 상태 복구 명령어 실행시 저장했던 PC를 다시 복원 하여 이전 실행 위치로 복원
7. 중단된 프로그램 실행 재개
    * PCB 값을 이용하여 이전 수행 중이던 프로그램 재개


<br>

---

## Interrupt vs Polling

<br>

||Interrupt|Polling|
|---|---|---|
|키워드|디바이스가 CPU에게 Interrupt 요청|CPU가 디바이스의 상태를 주기적 체크|
|매커니즘|Interrupt는 하드웨어 매커니즘|Polling은 하드웨어 뿐 아니라 통신이나 웹에서도 공통 사용|
|CPU Service|Interrupt Handler가 Device 처리|CPU가 Device 처리|
|발생 조건|Interrupt는 언제나 발생 가능| CPU가 일정 간격으로 Device 체크|



<br>

---


## Interrupt Vector란?
<img width="665" alt="interrupt Vector" src="https://github.com/techsum-org/tech_study/assets/81874493/e1207c57-31a7-444a-aa03-a18ac0aae57e">

* 정의 : 인터럽트 벡터는 인터럽트가 발생했을 때, 그 인터럽트를 처리할 수 있는 서비스 루틴들의 주소를 가지고 있는 공간이다.

<br>

​시스템에는 많은 인터럽트가 존재하고 각 인터럽트는 한번에 한나씩 발생하는 것이 아니라 한순간 여러개가 동시에 발생하기도 한다.
    
>⇒ 이렇게 동시에 발생하는 인터럽트를 하나로 묶어서 처리하는 개념이 인터럽트 벡터 이다.

<br>

* 인터럽트 벡터(Interrupt Vector) : 인터럽트에 대한 ISR의 시작 주소
* 인터럽트 벡터 테이블(Interrupt Vector Table) : 인터럽트 발생시 처리해야 할 루틴의 주소를 보관하고 있는 테이블



<br>

---




## Interrupt 정리

* Polling방식이 무엇인가요?
  * 답변 : 폴링 방식이란 운영체제가 하드웨어 장치의 상태 레지스터를 읽음으로써 명령의 수신 여부를 주기적으로 확인하는 방법 입니다.

<br>

* Interrupt 방식이 무엇인가요?
  * 답변 : 인터럽트는 란 마이크로프로세서(CPU)가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치에 예외상황이 발생하여 처리가 필요할 경우에 마이크로 프로세서에게 알려 처리하고 다시 실행중인 작업으로 복귀 할 수 있도록 하는 것 입니다.

<br>

* Interrupt에는 무엇이 있나요?
  * 답변 : 인터럽트에는 실행중인 명령어로 인한 인터럽트와 명령어와 무관하게 발생하는 인터럽트가 있습니다.
    * 실행중인 명령어로 인해 발생하는 인터럽트로는
      * 외부 사용자의 메모리 접근이나 오버플로우 언더플로우로 인한 인터럽트
      * 사용자가 의도적으로 발생시킨 인터럽트
      * 입출력 장치등의 조작으로 인한 인터럽트
      * 산술 연산 중 0을 0으로 나눌시 발생하는 인터럽트 
        가 존재하며

    * 명령어 실행과 무관하게 발생하는 인터럽트로는
      * 하드디스크 읽기 오류
      * 메모리 불량 오류
        
        등이 존재합니다.

<br>

* Interrupt의 처리과정은 어떻게 되나요?
  * 답변 : 인터럽트 처리 과정으로는
    
    1. 인터럽트 요청이 오면
    2. 프로그램 실행 중단하고
    3. 현재 실행 중인 프로그램 상태를 보관합니다
    4. 인터럽트 원인 판별하여 인터럽트 벡터 테이블을 참조하여 ISR의 주소를 얻고
    5. ISR(인터럽트 서비스 루틴)처리 합니다.
    6. 처리 완료후 상태 복구 명령어를 실행하여 PC를 통해 이전 상태를 복원 합니다.
    7. 복원이 완료되면 이전에 중단된 프로그램 실행 재개합니다.


<br>

* Interrupt Vector가 무엇인가요?
  * 답변 : Interrupt Vector란 ​시스템에는 많은 인터럽트가 존재하고 각 인터럽트는 한번에 한나씩 발생하는 것이 아니라 한순간 여러개가 동시에 발생하기도 하기 때문에 동시 발생하는 인터럽트를 하나로 묶어 처리하는 개념이 인터럽트 벡터입니다.
    
    또한, 인터럽트 벡터는 인터럽트가 발생했을 때, 그 인터럽트를 처리할 수 있는 서비스 루틴들의 주소를 가지고 있는 공간 입니다.
