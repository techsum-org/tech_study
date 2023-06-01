# CPU Scheduling 

---
## Table of Contents
* [CPU 스케줄링에 대해](#about the CPU Scheduling)
* [CPU 스케줄링의 종류](#cpu-스케줄링의-종류)
* [FCFS에 대하여](#first-come-first-served-fcfs)
* [SJF에 대하여](#sortest-job-first-sjf)
* [우선순위 큐](#priority)
* [라운드로빈](#round-robinrr)
* [다중큐](#multi-level-queue-mlq)
* [다중 피드백 큐](#mulit-level-feedback-queue-mlfq)

---
## <font color="yellow">프로세스 상태</font>
<img src="https://velog.velcdn.com/images%2Fwhwkd11010%2Fpost%2Fec40d7df-d665-41da-89c8-b975652c1688%2F%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%83%81%ED%83%9C.png">

* **new** : 프로세스가 생성 중인 상태 (커널공간에 PCB가 만들어진 상태)
* **Ready** : 프로세스가 CPU를 얻으려고 대기중인 상태 (CPU를 제외한 필요한 자원들을 모두 얻은 상태)
* **Running** : 프로세스가 CPU를 할당 받아 명령어를 수행중인 상태
* **Blocked** : 프로세스가 CPU를 할당 받아도 당장 실행할 수 없는 상태 (현재 프로세스가 I/O 작업 등을 처리 중인 상태를 의미)
* **terminated** : 프로세스의 실행 종료 (프로세스 실행이 완료되고 할당된 CPU를 반납, Kernel 내의 PCB는 남아있음)
* **suspended** : 프로세스의 중지 상태 (메모리를 강제로 뺏긴 상태로 특정한 이유로 프로세스 수행이 정지된 상태를 의미한다. 외부에서 다시 재개시키지 않는 이상 활성화될 수 없음.)

### CPU 스케줄링의 종류

**1) FCFS**

**2) SJF**

**3) Priority**

**4) Round-Robin**

**5) Multi-Level Queue**

**6) Multi-Level Feedback Queue**

### First Come First Served (FCFS)

### Sortest Job First (SJF)

### Priority

### Round-Robin(RR)

### Multi-Level Queue (MLQ)

### Mulit-Level Feedback Queue (MLFQ)


