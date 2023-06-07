## 1. IPC(Inter Process Communication)

- 커널이 제공하는 프로세스 간 데이터를 주고받는 메커니즘
    - 즉, 동시 접근 가능한 공유 메모리가 필요하단 뜻임

## 2. 프로세스 간 통신을 해야하는 경우

- 중요 프로세스의 안정성을 위해
    - 하나의 프로세스에서 공유자원을 동기화하고 여러 스레드가 사용하면 데이터 공유가 쉽지만, 해당 프로세스가 죽어버리면 같은 프로세스의 모든 스레드가 죽어버려 위험한 상황이 올 수도 있음
- 싱글코어만 쓰는 언어에서의 cpu사용율을 높여 성능 최적화가 필요한 경우
    - 파이썬은 job(스레드)이 많이 생성되더라도 운영체제가 하나의 코어를 사용하다보니 최적의 성능을 뽑기 어려움. 따라서 job이 많이 생성되야 하는경우 프로세스를 나눠 처리하는 방식이 효율적일 수 있음

## 3. IPC 구현 방법

### 운영체제에서 지원하는 방식

- 파이프(pipe)
    - 익명의 PIPE를 통해서 동일한 PPID를 가진 프로세스들 간에 단방향 통신을 지원
    - FIFO 구조, 생성된 PIPE에 대하여 Write 또는 Read만 가능
    
    ![Untitled](https://leesuha.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbbd30cf7-1b24-48e8-9782-77cccdb416e0%2FUntitled.png?id=9e3c9b7e-07e5-4c68-8842-9928efd94955&table=block&spaceId=cf3675a0-7c1e-48eb-8acf-e80ee8e7fb54&width=1390&userId=&cache=v2)
    
- 명명된 파이프 (Named Pipes)
    - 이름을 가진 PIPE를 통해서 서로 다른 프로세스들이 PIPE의 이름만 알면 통신이 가능
    - FIFO 구조, 생성된 PIPE에 대하여 Write 또는 Read만 가능
    
    ![Untitled](https://leesuha.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6682a1f6-f428-4975-9e97-49429a6523b1%2FUntitled.png?id=20d1da2b-9404-40e3-9df6-88021c2669a3&table=block&spaceId=cf3675a0-7c1e-48eb-8acf-e80ee8e7fb54&width=1390&userId=&cache=v2)
    
- 메시지 큐 (Message Queues)
    - 메모리를 사용한 PIPE이며, 구조체 기반으로 통신
    - FIFO 구조, msgtype에 따라 다른 구조체를 가져올 수 있음
    
    ![Untitled](https://leesuha.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6dec3bd6-fbcc-421b-af7f-933e41ef8c0d%2FUntitled.png?id=b8511212-f1af-4598-be62-f4cebcb34f8b&table=block&spaceId=cf3675a0-7c1e-48eb-8acf-e80ee8e7fb54&width=1390&userId=&cache=v2)
    
- 공유 메모리(shared memory)
    - 시스템 상의 공유 메모리를 통해 통신
    - 일정한 크기의 메모리를 프로세스간에 공유하는 구조, 공유 메모리는 커널에서 관리
    
    ![Untitled](https://leesuha.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F98a8ddac-2fe8-4d2b-8590-fd41042e861c%2FUntitled.png?id=08e891a9-2c32-4a0e-84ed-6bec0e1343dd&table=block&spaceId=cf3675a0-7c1e-48eb-8acf-e80ee8e7fb54&width=1390&userId=&cache=v2)
    
- 메모리 맵 (Memory Map)
    - 파일을 가상 메모리에 매핑하여 프로세스 간 데이터 공유를 지원
    - 쉽게 말해 메모리 맵은 파일을 메모리처럼 다룰 수 있게 함. 일반적으로 파일을 읽거나 쓰기 위해서는 디스크에서 파일을 읽어 메모리에 복사한 후에 작업을 수행해야 함. 하지만 메모리 맵을 사용하면 파일의 내용을 메모리에 직접 매핑하여 디스크에서 복사하는 오버헤드를 줄일 수 있음.
        - 메모리 맵은 파일을 메모리에 직접 매핑하여 데이터 공유를 지원하고, 디스크에서의 데이터 복사를 최소화하여 효율적인 데이터 공유가 가능
    
    ![Untitled](https://leesuha.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F88862437-a70e-436f-9af7-c1173a9ed467%2FUntitled.png?id=8b9ed8e2-581f-4c55-8611-ea646fa20158&table=block&spaceId=cf3675a0-7c1e-48eb-8acf-e80ee8e7fb54&width=1390&userId=&cache=v2)
    

### 소켓(네트워크)을 사용하는 방식

- 소켓 (Sockets)
    - 네트워크 소켓 통신을 시용한 데이터 공유
    - 네트워크 소켓을 이용하여 Client - Server 구조로 데이터 통신
    
    ![Untitled](https://leesuha.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe4dd583a-f958-4bc6-8a27-4f3c83cbd688%2FUntitled.png?id=8be0f877-8f03-4995-aa2a-89217959802d&table=block&spaceId=cf3675a0-7c1e-48eb-8acf-e80ee8e7fb54&width=1280&userId=&cache=v2)
    

---

| IPC 종류 | 사용 시기 | 공유 매개체 | 통신 단위 | 통신 방향 | 통신 가능 범위 |
| --- | --- | --- | --- | --- | --- |
| 파이프 (Pipes) | 동시 실행되는 프로세스 간에 데이터를 실시간으로 전달해야 할 때 | 메모리 | 바이트 스트림 | 단방향 (한쪽으로) | 단일 호스트 내에서 프로세스 간 통신 |
| 명명된 파이프 (Named Pipes) | 동일한 호스트의 다른 시기에 실행되는 프로세스 간에 데이터를 주고받을 때 | 파일 시스템 | 바이트 스트림 | 양방향 | 단일 호스트 내에서 프로세스 간 통신 |
| 메시지 큐 (Message Queues) | 메시지 기반의 통신이 필요하며, 비동기적인 통신이 가능해야 할 때 | 커널 큐 | 메시지 | 양방향 | 단일 호스트 내에서 프로세스 간 통신 |
| 공유 메모리 (Shared Memory) | 빠른 데이터 공유와 저렴한 통신 비용이 필요할 때 | 메모리 | 변수나 구조체 | 양방향 | 단일 호스트 내에서 프로세스 간 통신 |
| 메모리 맵 (Memory Map) | 대용량 데이터를 공유해야 할 때 | 파일 | 메모리 영역 | 양방향 | 단일 호스트 내에서 프로세스 간 통신 |
| 소켓 (Sockets) | 네트워크를 통한 분산 환경에서 프로세스 간 통신이 필요할 때 | 네트워크 (TCP/IP 또는 UDP) | 패킷 | 양방향 | 다른 호스트 또는 네트워크에 있는 프로세스 간 통신 |