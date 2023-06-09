## 인터럽트
---
- 인터럽트: CPU가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치나 예외 상황이 발생하여 처리가 필요할 경우에 마이크로 프로세서에게 알려 처리할 수 있도록 하는 것을 말함.
    - 하드웨어 인터럽트: 하드웨어가 발생시키는 인터럽트로, CPU가 아닌 다른 하드웨어 장치가 CPU에 어떤 사실을 알려주거나 CPU 서비스를 요청해야 할 경우에 발생시킴.
        - 외부 인터럽트: 전원 이상 인터럽트, I/O 인터럽트, 타이머 인터럽트 등.
        - 내부 인터럽트: 잘못된 명령이나 잘못된 데이터를 사용할 때 발생함. 프로그램 검사 인터럽트 등.
            - Division by zero, Overflow/Underflow
    - 소프트웨어 인터럽트: 소프트웨어가 발생시키는 인터럽트로, 소프트웨어(사용자 프로그램)가 스스로 인터럽트 라인을 세팅하여 발생시킴.
        - CPU는 매번 명령을 수행하기 전에 인터럽트 라인이 세팅되어 있는지 검사함.
        - 예외 상황, 시스템 콜, SVC
        - SVC(SuperVisor Call): 프로세서 명령어로 수행 시 문제가 생기면 프로세서가 운영체제를 관리 감독하는 프로그램에게 제어권을 넘겨서 해결하는 것을 말함, 시스템 콜을 실행시키기 위한 CPU 명령어

- 인터럽트 핸들러(interrupt handler) 또는 인터럽트 서비스 루틴(Interrupt Service Routine, ISR): 인터럽트 접수에 의해 발생되는 인터럽트에 대응하여 특정 기능을 처리하는 기계어 코드 루틴임. 운영 시스템이나 임베디드에서 장치 드라이버에서 요구하는 일을 처리하는 기능적 코드 집합으로 콜백 루틴 방식으로 처리됨.
- 인터럽트 벡터(interrupt vector): 인터럽트가 발생했을 때, 그 인터럽트를 처리할 수 있는 서비스 루틴들의 주소를 가지고 있는 공간.
- 인터럽트 벡터 테이블: 인터럽트 벡터들을 저장하는 데이터 구조, 인터럽트 서비스 루틴의 시작 주소를 찾는 3가지 방법에서 사용됨.
    - 타이머 인터럽트 서비스 루틴, 입출력 인터럽트 서비스 루틴, 예외 처리 인터럽트 서비스 루틴

- 인터럽트 과정: 요청 → 중단 → 보관 → 인터럽트 처리 → 재개
    - 인터럽트 요청
    - 프로그램 실행 중단: 현재 실행 중이던 Micro Operation까지 수행
    - 현재 실행 중인 프로그램 상태 보관: PCB 저장
    - 인터럽트 원인 판별: 인터럽르르 요청한 장치를 식별하여 원인을 파악함. Interrupt Vector 테이블을 참조하여 호출할 ISR(인터럽트 서비스 루틴) 주소 값을 얻음.
    - ISR(인터럽트 서비스 루틴) 처리: 인터럽트 처리 작업을 수행함. 서비스 루틴 수행 중, 우선 순위가 더 높은 인터럽트가 발생하면 재귀적으로 1~5 과정을 수행함. 인터럽트 서비스 루틴을 실행할 때 인터럽트 플래그(IF)를 0으로 하면 인터럽트 발생을 방지할 수 있음.
    - 상태 복구: 저장해둔 PC(Program Counter)를 다시 복원하여 이전 실행 위치로 복원함.
    - 중단된 프로그램 실행 재개: PCB의 값을 이용하여 이전에 수행 중이던 프로그램을 재개함.

- 인터럽트 우선순위: 여러 장치에서 인터럽트가 동시에 발생하거나 인터럽트 서비스 루틴 수행 중 인터럽트가 발생한 경우 우선순위 판별 필요함. 일반적으로 하드웨어 인터럽트 > 소프트웨어 인터럽트이며, 외부 인터럽트 > 내부 인터럽트의 우선 순위를 가짐.
    1. 전원 이상(Power fail)
    2. 기계 착오(Machine Check)
    3. 외부 신호(External)
    4. 입출력(I/O)
    5. 명령어 잘못
    6. 프로그램 검사(Program Check)
    7. SVC(SuperVisor Call)
- 우선순위 판별 방법
    - 소프트웨어적인 방법(Polling): 인터럽트 요청 플래그를 차례로 비교하여 우선순위가 가장 높은 인터럽트 자원을 찾고, 이에 해당하는 인터럽트 서비스 루틴을 수행, 속도가 빠른 장치에 높은 등급을 부여함.
        - 장점: 우선순위 변경이 쉬움, 회로가 간단하고 융통성이 있으며 별도의 하드웨어가 필요없음.
        - 단점: 많은 인터럽트가 있을 경우 하드웨어적인 방법에 비해서 우선순위 판단 속도가 느림, Polling 주기가 짧으면 server 성능에 부담이 생기며, 주기가 떨어지면 실시간성이 떨어짐.
    - 하드웨어적인 방법(Verctored Interrupt): 인터럽트를 요청할 수 있는 장치와 CPU 사이에 장치번호를 식별할 수 있는 버스를 직/병렬로 연결함. 하드웨어적인 방법은 아래 2가지로 나뉨.
        1. Daisy Chain: 인터럽트가 발생한 모든 장치를 하나의 직렬 회선으로 연결, 우선순위가 높은 장치를 상위에 두고 우선순위 차례대로 배치.
        2. 병렬(Parallel) 우선순위 부여 방식: 인터럽트가 발생하는 모든 장치를 하나의 직렬 회선으로 연결, 각 장치별 우선 순위를 판별하기 위한 Mask register에 bit를 설정함, Mask register 상 우선 순위가 높은 서비스 루틴 수행 중 우선 순위가 낮은 bit를 비활성화할 수 있음, 반대로 우선 순위가 높은 인터럽트는 낮은 인터럽트 수행 중에도 우선 처리됨.
        - 장점: 별도의 소프트웨어가 필요없이 하드웨어로 처리되기에 속도가 빠름.
        - 단점: 소프트웨어적인 방법에 비해 비경제적이며, 회로가 복잡하고 융통성 없음.