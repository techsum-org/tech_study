# 주제 : 프로세스와 스레드

## Table of Contents
* [프로그램과 프로세스](#프로그램과-프로세스)
* [프로세스의 구조](#프로세스의-구조)
* [프로세스 과정](#프로세스가-되는-과정)
* [멀티프로그래밍과 멀티프로세싱](#멀티프로그래밍과-멀티프로세싱)
* [스레드](#스레드)
* [스레드의 장단점](#스레드를-사용하는-이점)
* [프로세스와 스레드의 차이](#프로세스와-스레드의-차이)
* [멀티스레드 모델](#멀티스레드-모델)

## 프로그램과 프로세스

*  프로그램 (Program)
    - HDD와 SSD와 같은 저장장치에 저장된 명령문의 집합체를 말한다.
    - 애플리케이션이나 앱이라고도 불리운다.
    - 윈도우 운영체제에서는 .exe의 확장명을 가지고 있다.
    > 프로그램은 컴퓨터 관점에서는 저장장치만 사용하는 <font color="red">수동적</font>인 존재

* 프로세스 (Process)
    - 실행 중인 프로그램
    - 저장장치에 저당된 프로그램이 메모리에 올라갔을 때 실행중인 프로그램 즉, 프로세스라고 한다.
    > 프로세스는 메모리도 사용하고, 운영체제의 CPU 스케줄링 알고리즘에 따라서 CPU도 사용하고,
    > 필요에 따라 입럭과 출력도 하기에 <font color="red">능동적</font>인 존재

### 프로세스의 구조
* 코드 영역 (Code Area)
    - 자신을 실행하는 코드가 저장되어 있음
* 데이터 영역 (Data Area)
    - 전역 변수와 Static(정적)변수가 저장되어 있음
* 스택 영역 (Stack Area)
    - 함수 호출 시 매개변수와 돌아갈 주소가 저장됨.
    - 지역변수와 함수 호출 시 필요한 정보들이 저장됨.
* 힙 영역  (Heap Area)
    - 프로그래머(사용자)가 동적으로(런타임 시) 메모리를 할당할 수 있는 메모리 공간
    - C언어에서 `malloc()`과 `free()`을 호출 시 힙 영역에서 자원을 할당/해제 할 수 있음.
        - malloc() : 힙 영역에 메모리 공간 할당
        - free() : 할당된 메모리 공간 해체

### 프로세스가 되는 과정

```C
#include <stdio.h>

void main()
{
    int num1 = 5;
    int num2 = 7;
    int result = num1 + num2;
}
```
위 코드는 C언어로 작성된 두 숫자를 더하는 코드이다.

C언어는 **컴파일 언어**이기 때문에 컴파일을 해야 실행가능하기 때문에 컴파일을 해줘야 함

#### 컴파일 과정
1. test.c
    - 먼저 전처리기를 거쳐 매크로로 정의한 숫자를 치환하고, 필요한 파일을 불러옴
2. test.i
    - 전처리기 된 파일은 확장자명이 i로 바뀜.
    - 컴파일러가 컴파일을 해줌
    - 컴파일을 마치면 고수준 언어인 C언어를 저수준 언어인 어셈블리어로 변환
3. test.s
    - 컴파일러를 거치면 확장자명이 s로 바뀜.
    - 어셈블러가 어셈블리어를 기계어로 변환해줌
    - 그럼 s파일은 0과 1로 구성된 기계어 파일로 구성됨. 
4. test.o
    - 어셈블러를 거치면 확장자명이 o로 바뀜.
    - 기계어로 구성되어 있기 때문에 파일을 텍스트 에디터로 열어보면 글씨가 깨져보임
    - 마지막으로 링커가 링킹을하여 여러가지 라이브러리나 다른 소스코드를 연결함. 
5. test.exe
    - 링커를 거치면 확장자명이 최종적으로 exe로 바뀜.


위 방법을 거쳐 test.exe 파일을 더블 클릭하여 실행하면, 하드디스크에 있는 우리의 test.exe파일이 메모리에 올라가게 되고, 이렇게  **메모리에 올라간 프로그램을 우리는 <font color="yellow"> 프로세스 </font>라고 부른다.**

> 이 프로세스는 이제 운영체제의 의해 관리되어짐.

## 멀티프로그래밍과 멀티프로세싱
### 메모리 관점
* 유니프로그래밍 : 메모리에 오직 하나의 프로세스가 올라온 것을 말함
* 멀티프로그래밍 : 메모리에 여러개의 프로세스가 올라온 것을 말함
### CPU 관점
* 멀티프로세싱 : CPU가 여러개의 프로세스를 처리하는 것을 말함

<br>



### 오늘 날의 운영체제에는 멀티프로그래밍과 멀티프로세싱이 공존한다.
* 메모리에는 여러개의 프로세스가 올라오는 멀티프로그래밍이 있고.
* 시분할 처리로 CPU가 각각의 프로세스를 짧은 시간 동안 교대로 실행하는 멀티프로세싱이 있다.

### 과거에는 메모리가 작아서 멀티프로그래밍이 없었고 유니프로그래밍을 하면서 멀티프로세싱을 하였음
1. 메모리에 프로세스를 올려서 CPU로 처리함
2. 이 프로세스를 저장장치에 저장함.
3. 다른 저장장치에 있는 프로세스를 메모리에 올림
4. CPU로 처리하는 멀티프로세싱 기법을 사용

> 이 때, 메모리에서 저장장치에 올리고 저장장치에서 메모리에 올리는 것을 스와핑(swapping)이라고 함.


### 고아 프로세스와 좀비 프로세스
* 고아 프로세스(orpahn process)는 부모 프로세스가 먼저 종료되어 돌아갈 곳이 없는 프로세스
* 좀비 프로세스(zombi process)는 자식 프로세스가 종료되었는데도 부모 프로세스가 뒤처리를 하지 않아 발생하는 프로세스
* C 언어에서는 exit() 또는 return() 문을 사용해 자식 프로세스의 작업이 끝났음을 부모 프로세스에 알림

## 스레드
### 스레드의 정의
* CPU 스케줄러가 CPU에 전달하는 일 하나
* CPU가 처리하는 작업의 단위는 프로세스로부터 전달받은 스레드
    - 운영체제 입장에서의 작업 단위는 프로세스
    - CPU 입장에서의 작업단위는 스레드
    > <font color="yellow">스레드 Thread : 프로세스의 코드에 정의된 절차에 따라 CPU에 작업 요청을 하는 실행 단위</font>

## 프로세스와 스레드의 차이
* 프로세스끼리는 약하게 연결되어 있는 반면 스레드끼리는 강하게 연결되어 있음

### 프로세스
    * 운영체제로부터 자원을 할당받은 독립적인 실행 단위
    * 메모리에 로드되어 실행되는 프로그램의 인스턴스
    * 각각의 프로세스는 독립된 메모리 공간을 가지고 있으며, 서로 간섭 없이 실행
    * 프로세스 간 통신(IPC)을 위해서는 별도의 메커니즘 필요
### 스레드
    * 프로세스 내에서 실행되는 흐름의 단위
    * 한 프로세스 내에서 동작하며, 프로세스의 자원을 공유함
    * 스레드는 프로세스 내의 코드 실행 경로를 나타내는데, 프로세스의 특정 부분을 병렬적으로 실행할 수 있음
    * 스레드는 프로세스 내의 주소 공간, 파일 핸들, 시스템 레지스터 등을 공유함.
    * 스레드는 프로세스의 메모리에 할당된 스택 영역과 일부 레지스터를 가지고 있음

> 즉, 프로세스는 독립된 실행 단위로 메모리와 자원을 독립적으로 관리하며,
> 스레드는 하나의 프로세스 내에서 동작하는 실행 흐름으로 프로세스의 자원을 공유함

### 스레드를 사용하는 이점
1. 자원 공유 : 스레드는 같은 프로세스 내에서 자원을 공유하기 때문에 데이터 전달 및 처리가 효율적임
2. 응답성 향상 : 스레드는 동시에 실행 될 수 있으므로, 사용자에 대한 응답성이 향상됨.
3. 자원 절약 : 프로세스를 생성하는 것보다 스레드를 생성하는 비용이 적으며, 메모리를 공유하기 때문에 자원도 절약됨.

### 스레드를 주의해야할 점
1. 동기화 : 스레드는 공유 자원을 사용하기 때문에 동시에 접근할 경우 동기화 문제가 발생할 수 있음.
2. 교착 상태 (Deadlock) : 교착 상태란 두개 이상의 스레드가 서로가 점유한 자원을 기다리며 무한히 대기하는 상태를 말함. 예를 들어, 스레드 A가 자원 X를 점유한 상태에서 자원 Y를 기다리고, 스레드 B는 자원 Y를 점유한 상태에서 자원 X를 기다릴 때 교착 상태가 발생함. 이를 방지하기 위해 교착 상태의 발생 조건을 분석하고, 교착 상태를 예방하거나 해결하는 알고리즘을 적용해야함
3. 성능 문제 : 스레드는 동시에 실행 될 수 있지만, 너무 많은 스레드를 생성하면 컨텍스트 스위칭(Context Switching) 오버헤드가 발생하고, 이는 성능 저하로 이어질 수 있음. 또한, 스레드 간의 자원 공유로 인해 동기화 비용이 발생하며, 이로 인해 성능이 저하 될 수 있음
4. 디버깅 및 테스트의 어려움 : 멀티스레드 환경에서 버그를 찾거나 디버깅하는 것은 단일 스레드 환경보다 어려움. 여러 스레드가 동시에 실행되므로 각 스레드의 상태와 상호작용을 추적하고 이해하는 것이 복잡해짐. 또한, 스레드 간의 타이밍 문제로 인해 일관된 테스트가 어려울 수 있음.

## 멀티스레드 모델
### 커널 스레드와 사용자 스레드
* 커널 스레드 : 커널이 직접 생성하고 관리하는 스레드
* 사용자 스레드 : 라이브러리에 의해 구현된 일반적인 스레드

### 사용자 스레드 (1 to N 모델)
* 사용자 프로세스 내에 여러개의 스레드가 커널의 스레드 하나와 연결 (1 to N 모델)
* 라이브러리가 직접 스케줄링을 하고 작업에 필요한 정보를 처리하기 때문에 **<font color="yellow">문맥 교환이 필요없음</font>**
* 커널 스레드가 입출력 작업을 하기 위해 대기 상태에 들어가면 모든 사용자 스레드가 같이 대기하게 됨.
* 한 프로세스의 타임 슬라이스를 여러 스레드가 공유하기 때문에 **<font  color="yellow">여러 개의 CPU를 동시에 사용할 수 없음</font>**

### 커널 스레드 (1 to 1 모델)
* 하나의 사용자 스레드가 하나의 커널 스레드와 연결 (1 to 1 모델)
* **<font color="yellow">독립적으로 스케줄링</font>** 이 되므로 특정 스레드가 대기 상태에 들어가도 다른 스레드는 작업을 계속할 수 있음
* 하나의 스레드가 **<font color="yellow">대기 상태</font>** 에 있어도  **<font color="yellow">다른 스레드는 작업을 계속할 수 있음</font>**
* 커널의 기능을 사용하므로 보안에 강하고 안정적으로 작동
* **<font color="pink">문맥 교환할 때 오버헤드 때문에 느리게 작동</font>** 

### 멀티레벨 스레드 (M to N 모델)
* **<font color="yellow">사용자 스레드</font>** 와 **<font color="yellow">커널 스레드</font>** 를 혼합한 방식 (M to N 모델)
* 커널 스레드가 대기 상태에 들어가면 다른 커널 스레드가 **<font color="yellow">대신 작업</font>** 을 하여 사용자 스레드보다 유연하게 작업을 처리할 수 있음
* **<font color="yellow">커널 스레드를 같이 사용하기 때문에</font>** 여전히 문맥 교환 시 오버헤드가 있어 사용자 스레드반큼 빠르지 않음
* 빠르게 움직여야 하는 스레드는 사용자 스레드로 작동하고, 안정적으로 움직여야 하는 스레드는 커널 스레드로 작동

    <img src="https://velog.velcdn.com/images/minseong1459/post/d2a8ce44-d72c-4947-96a1-242dc8418227/image.png" height="80%" width="80%">

---




