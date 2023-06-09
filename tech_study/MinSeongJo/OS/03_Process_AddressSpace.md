# 주제 : 프로세스 주소공간

## Table of Contents

* 프로그램과 프로세스
* 프로그램의 다중 인스턴스
* 프로세스 주소공간
* [요약](#요약)
* [키워드](#키워드)

---

### 프로세스란?
<font color="grey">(앞서 설명했지만 이번 주제에 대한 사전지식)</font>
프로세스의 사전적 정의 $\to$ 프로세스는 컴퓨터에서 **연속적으로 실행** 되고 있는 컴퓨터 프로그램을 말한다.

즉, 프로그램을 실행시키면 ( 메모리에 올라가면 ), 프로세스가 된다

---

### 프로그램의 다중 인스턴스
$\to$ 여러개의 프로그램을 동시에 실행시키면 각각 다른 인스턴스(객체)로 생성되어 메모리에 올라가게 된다.

### 주소 공간의 개념

#### 초기 시스템

초기 컴퓨터는 많으 추상화를 제공하지 않았고
<br>
초기 컴퓨터의 물리 메모리는 아래의 그림과 같았다.

<img src="https://velog.velcdn.com/images%2Fkshired%2Fpost%2F7d99efb3-4e69-47b5-8edd-881421bf9ac5%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-01%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%201.21.03.png">

OS는 메모리에 상주하는 루틴들의 집합이였고, 물리 메모리에 **하나의 실행 중인 프로세스가 존재**하였으며 OS를 제외한 나머지 메모리를 사용했습니다.

특별히 어떠한 가상화를 사용하지 않았음

#### 멀티 프로그래밍과 시분할

시간이 지나고, 사람들은 컴퓨터를 더 효과적으로 공유하기 시작
<br>
**$\to$ 멀티 프로그래밍의 시대가 도래함.** 

여러 프로세스가 실행 준비 상태에 있고, 운영체제는 그것을 전환하며 실행하였음

* CPU는 실제로 1개인데, 여러 개의 프로세스들은 마치 CPU가 여러개인 것과 같은 환상을 가짐
* 그런 환상을 통해, 여러 프로세스가 동시에 실행되는 것 처럼 보이게 함.

> 이러한 시분할을 구현하는 방법 중 하나는 하나의 프로세스를 짧은 시간동안 실행시키는데, 해당 기간동안 프로세스에게 모든 메모리를 접근할 권한을 주는 것이었음.

그 후에,  이 프로세스를 중단하고 중단 시점의 모든 상태를 디스크 종류의 장치에 저장하고 다른 프로세스의 상태를 탑재하여 짧은 시간 동안 실행시킴

#### 위 방법의 문제점
**레지스터 상태를 저장하고 복원하는 것은 빠르지만 메모리 내용 전체를 디스크에 저장하는 것이 느렸다는 것**
$\to$ 이것을 해결하기 위해, **프로세스를 전환할 때 프로세스를 메모리에 그대로 유지하면서 OS가 시분할을 효율적으로 구현할 수 있게 하는 것이 이번 메모리 가상화의 목표**이다.

<img src="https://velog.velcdn.com/images%2Fkshired%2Fpost%2Fcaab6b56-cedb-4870-a8b4-bf2813fb3013%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-01%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%201.30.45.png">

그림에 세 개의 프로세스 A,B,C가 있고 각 프로세스는 512KB의 물리 메모리에서 각자 작은 부분을 할당 받았고, A는 실행 중이며 B,C는 준비 큐에서 실행을 기다리고 있음
<br>
그런데, 이렇게 여러 프로세스들이 한 메모리에 존재하게 되면 서로 데이터를 침범할 수 있는 가능성이 존재함.
그렇기에 **보호 및 보안이 중요한 문제**가 됨

---

### 주소 공간

위와 같은 위험에 대비하기 위해 OS는 사용자에게 사용하기 쉬운 메모리 개념을 만들어야 한다.
이 개념이 주소 공간 (Address Space)이다.

주소 공간은 프로그램의 모든 메모리 상태를 갖고 있음.

코드, 스택, 힙과 같이 프로그램을 실행시키기 위한 모든 상태를 주소공간이 가지고 있다.

## 주소공간 요약
메모리 가상화를 통해 프로세스들에게 전용공간이라는 환상을 프로그램에게 제공할 책임이 있으며, 이 공간에 프로그램의 명령어와 데이터 전부가 저장됨.
하드웨어의 도움을 받아 운영체제는 가상 메모리 주소를 받아 물리 메모리 주소로 변환을 함.

이러한 작업을 통해 운영체제는 각 프로세스들과 운영체제를 보호하며 격리함.

## 프로세스 주소 공간

* 프로세스는 메로리에 올라갈 때 아래와 같은 4개의 메모리 영역을 가지게 된다.
    
    - 코드 영역
        $\to$ 프로세스 코드가 적재되는 영역, 텍스트 영역이라고도 부름
    - 데이터 영역
        $\to$ 프로세스의 전역 변수들과 정적 변수들이 적재되는 영역
    - 힙 영역
        $\to$ 프로세스가 실행 중에 동적 할당받는 영역
    - 스택 영역
        $\to$ 함수가 호출될 때, 지역 변수, 매개변수, 함수의 리턴 값이 등이 저장되는 영역.

    <img src="https://postfiles.pstatic.net/MjAyMzA0MTZfNjUg/MDAxNjgxNjQwODY0NjE1.du3KoSmhx-qqT69DDMn6kTdwOUI-sV8cyvLxlCRB6Ysg.l78XC-cRF9xcdfJEkjb9LzsRV6CJkkoI81BlN2xZgoIg.PNG.tgyuu_/image.png?type=w966">

    **이로 써  CPU 주소 공간과, 프로세스가 메모리 할당을 받을 때 어떤 공간(4개의 영역)을 받게 된다.**
### 프로세스 주소공간 이란
> 프로세스가 실행 중에 <font color="pink">접근할 수 있도록 허용된 주소의 최대 범위</font>로, 아래 그림처럼 나타낼 수 있다.
<img src="https://postfiles.pstatic.net/MjAyMzA0MTZfNjgg/MDAxNjgxNjQxMzA5Mjk0.uA3rb0QLFt1orA9KpKC_0IhXuwWsOqfAaApHvPBVNyYg.qp56bk0DxSZ1bdhulCSreCE7DLMOmkUDosZ1hDSOX0wg.PNG.tgyuu_/image.png?type=w966">

CPU주소 공간은 **직접적인 물리공간**

프로세스 주소 공간은 **프로세스가 실행되는 동안에만 유효**하며, 프로세스가 실행되면 CPU 주소공간에서 가상으로 공간을 가져와서 사용하는 방식이다.

즉, 프로세스 주소 공간은 프로그램이 메모리에 올라가면 CPU 주소 공간에서 메모리를 전부 할당 받아서 가상으로 사용하는 곳이라고 볼 수 있다.

하지만, 이 프로세스 주소 공간과 실행되고 있는 프로세스의 크기는 엄연히 다르다.
프로세스 주소 공간은 이 프로세스가 최대로 가질 수 있는 공간이라는 뜻이고, 프로세스의 크기는 할당된 4개의 영역의 합과 같다.

$$
프로세스\,크기 = 4개\,영역의\,합
$$

**프로세스 주소 공간은 <font color="pink">프로세스 하나가 최대로 활용할 수 있는 공간</font>이다.

하나의 프세스는 최대 4GB까지 사용할 수 있는데, 대부분의 프로세스는 그렇게 많은 용량을 차지 하지 않는다.

> 그럼 만약, 돌아가고 있는 프로세스의 메모리 합이 물리 메모리 공간(RAM 공간) 보다 클 경우에는 어떻게 될까?

> $\to$ 운영체제는 프로세스 실행에 당장 필요한 부분만 물리 메모리에 적재하고, 나머지는 디스크의 특정 공간(스왑 영역)에 저장해두고 필요할 때 RAM에서 안 쓰는 공간과 다시 스왑해서 사용한다.

<img src="https://postfiles.pstatic.net/MjAyMzA0MTZfMjI5/MDAxNjgxNjQzNzY0MjYx._HhCrpqS1GfHC9dCxii10nAj_2UkhF0f6ghj5-X2UFAg.3VNPaVeDrOIGG80-AtAYmXBRIlsxh9e4rT79VrWygjkg.PNG.tgyuu_/image.png?type=w966">

위 그림처럼 프로세스가 보기에는 코드 영역, 데이터 영역, 힙 영역, 스택 영역이 가지런히 정리되어 나란히 분포하는 것 처럼 보이지만

**실제로는 <font color="pink">주소 매핑 테이블</font>을 이용하여 실제 공간에 <font color="blue">각각 분산되어 분포한다.</font>**

<img src="https://postfiles.pstatic.net/MjAyMzA0MTZfMTE5/MDAxNjgxNjQzODE5MjQy.PQWvMSyCLfGHIZ34b8GEHh01Gfr0yChuoey0Xk6VCGUg.fhj7hYdbQ6y8cWifAfXcJHs8jGFSe5fF7QfQilZ96v0g.PNG.tgyuu_/image.png?type=w966">
위 그림처럼 프로세스가 2개가 돌아간다면
위 처럼 돌아간다.

여기서 주의깊게 보아야 할 점은 서로 다른 프로세스라도 **할당 받는 커널 영역**은 같다는 것이다.


## 요약
* 프로세는 메모리에 올라갈 때 코드, 데이터, 힙, 스택의 네 가지 영역으로 나뉜다.
* 코드 영역에는 프로그램의 명령어가 포함된다.
* 데이터 영역에는 프로그램의 전역 및 정적 변수가 포함된다.
* 힙 영역에는 프로그램이 실행 중에 동적으로 할당한 메모리가 포함된다.
* 스택 영역에는 함수 호출에 사용되는 지역 변수와 매개변수가 포함된다.
* 프로세스 주소 공간은 프로세스가 실행 중에 접근할 수 없는 메모리 범위이다.
* 프로세스 주소 공간은 물리 메모리에 할당될 수 있지만 물리 메모리보다 클 수 있다. 이 경우 운영체제는 프로세스 주소공간의 일부만 물리 메모리에 적재하고 나머지는 디스크에 저장한다.
* 프로세스 주소 공간은 주소 매핑 테이블을 사용하여 물리 메모리에 매핑된다.
* 주소 매핑 테이블은 프로세스 주소 공간의 가상 주소와 물리 주소 간의 매핑을 저장하는 데이터 구조이다.
* 운영체제는 주소 매핑 테이블을 사용하여 프로세스가 물리 메모리에 엑세스 할 수 있도록 한다.

## 키워드
* 코드
* 데이터
* 힙
* 스택
* 프로세스 주소 공간
* 물리 메모리
* 주소 매핑 테이블
* 가상 주소
* 물리 주소

$\to$ 이러한 키워드는 프로세스 주소 공간과 그 작동 방식을 이해하는 데 꼭 필요한 키워드들이다.